Para resolver las problemáticas de costos, disponibilidad, riesgo por redimensionamiento y lentitud en la carga de imágenes de **Rekomendashi**, la solución arquitectónica requiere evolucionar de un esquema de escala vertical con servidor único a una **arquitectura distribuida con escalabilidad horizontal, desacoplamiento de la persistencia y distribución de contenido estático**.

---

### 1. Diagnóstico y Estrategia de Solución

|Problemática Actual|Causa Raíz|Solución Arquitectónica|
|:--|:--|:--|
|**Costo elevado en la nube** (1 servidor de 4 cores / 16GB RAM)|Escala vertical exclusiva (_scale-up_).|**Escalabilidad Horizontal (_scale-out_):** Migrar a múltiples nodos más pequeños y económicos (ej. 6 máquinas de 1 core / 4GB) detrás de un balanceador de carga.|
|**Downtime y riesgo por reescalado + BD en el mismo servidor**|Acoplamiento físico de la aplicación y la base de datos en un único servidor.|**Desacoplamiento de la Base de Datos:** Separar la BD del servidor de aplicaciones a un servidor/servicio gestionado independiente.|
|**Caídas del servidor (Memory Leak / Punto Único de Falla)**|Inexistencia de redundancia (_Single Point of Failure_).|**Tolerancia a Fallos y Redundancia:** Varias instancias del backend. Si un nodo cae, el balanceador redirige el tráfico a los nodos sanos mediante _health checks_.|
|**Tiempos de carga lentos por fotos de sushi**|Servidor de aplicaciones sirviendo contenido estático pesado (archivos/imágenes).|**Object Storage + CDN:** Almacenar imágenes en un almacenamiento de objetos y servirlas a través de una Red de Distribución de Contenidos (CDN).|

---

### 2. Propuesta de Arquitectura Componente por Componente

#### A. Capa de Entrega de Contenido Estático (CDN + Object Storage)

- **Object Storage (ej. Amazon S3 / Blob Storage):** Las imágenes de sushi de alta calidad se almacenan de forma independiente al código de la aplicación. Esto evita guardar archivos en el _file system_ local de las instancias de aplicación, lo cual sería inviable al escalar horizontalmente.
- **CDN (Content Delivery Network - ej. Cloudflare / CloudFront):** Se ubica geográficamente cerca de los usuarios para cachear y distribuir las imágenes de sushi.
    - _Beneficio:_ Libera al 100% a los servidores de aplicaciones del consumo de ancho de banda y procesamiento de archivos estáticos, mejorando drásticamente el tiempo de carga percibido por los usuarios.

#### B. Capa de Balanceo de Carga y Entrada (HTTP Load Balancer)

- **Balanceador de Carga HTTP (ej. NGINX / HAProxy / Cloud Load Balancer):** Actúa como el único punto de entrada (_reverse proxy_) para las peticiones de los usuarios.
- **Distribución de Tráfico:** Utiliza algoritmos como _Round Robin_ o _Least Connections_ para repartir la carga equitativamente entre las 6 instancias.
- **Salud del Sistema (_Health Checks_):** Monitorea constantemente los nodos. Si una instancia cae (por ejemplo, debido al _memory leak_ investigado), el balanceador la detecta y desvía el tráfico a las instancias sanas de inmediato.

#### C. Capa de Aplicación Backend (Instancias Clúster)

- **Múltiples Nodos Livianos:** Se despliegan 6 instancias independientes de 1 core y 4GB de RAM.
- **Sin Estado (_Stateless_):** Los nodos de aplicación no guardan estado ni sesiones en memoria local ni archivos en su disco. Las autenticaciones se manejan mediante _tokens_ (JWT) o almacenamiento de sesiones compartido.
- **Autoescalado / Despliegue sin Downtime:** Permite agregar o quitar nodos dinámicamente o aplicar actualizaciones sin apagar el sistema (_Zero Downtime_).

#### D. Capa de Persistencia (Base de Datos Desacoplada)

- **Base de Datos Independiente:** La base de datos relacional se remueve del servidor de aplicaciones y se mueve a su propio servidor dedicado o servicio administrado.
- **Respaldos y Redundancia:** Al estar aislada, se pueden realizar respaldos programados (backups/snapshots) y réplicas sin necesidad de apagar la aplicación ni generar caídas del servicio.

---

### 3. Diagrama de la Arquitectura Propuesta

```
                                [ USUARIOS / CLIENTES ]
                                           │
                    ┌──────────────────────┴──────────────────────┐
                    │                                             │
      (Solicitud de Imágenes / Assets)             (Peticiones Dinámicas API / Web)
                    │                                             │
                    ▼                                             ▼
        ┌──────────────────────┐                     ┌──────────────────────────┐
        │  CDN (Edge Network)  │                     │  Balanceador de Carga    │
        │ (ej. Cloudflare/S3)  │                     │      HTTP (NGINX/ALB)    │
        └───────────┬──────────┘                     └────────────┬─────────────┘
                    │                                             │
                    │ (Origen de Imágenes)                        ├─────────────────┬─────────────────┐
                    ▼                                             │                 │                 │
        ┌──────────────────────┐                                  ▼                 ▼                 ▼
        │    Object Storage    │                           ┌────────────┐    ┌────────────┐    ┌────────────┐
        │   (ej. Amazon S3)    │                           │ Instancia 1│    │ Instancia 2│ ...│ Instancia 6│
        └──────────────────────┘                           │ (1 Core/4G)│    │ (1 Core/4G)│    │ (1 Core/4G)│
                                                           └─────┬──────┘    └─────┬──────┘    └─────┬──────┘
                                                                 │                 │                 │
                                                                 └─────────────────┼─────────────────┘
                                                                                   │
                                                                                   ▼
                                                                  ┌─────────────────────────────────┐
                                                                  │  Base de Datos Desacoplada      │
                                                                  │ (Servidor Dedicado / Mantenido) │
                                                                  └─────────────────────────────────┘
```

---

### 4. Impacto en los Atributos de Calidad

- **Costo y Eficiencia de Recursos:** Reducción sustancial del costo de infraestructura pasando de una máquina pesada sobredimensionada a un clúster de máquinas livianas optimizadas, liberando recursos de cómputo al externalizar las imágenes a un Object Storage + CDN.
- **Disponibilidad y Tolerancia a Fallos:** La caída de una instancia individual (por ejemplo, por un error de memoria) no tumba el sistema. El balanceador desvía el tráfico automáticamente y se elimina el _Single Point of Failure_ en la aplicación.
- **Mantenibilidad y Despliegue sin Downtime:** Se pueden realizar copias de seguridad de la base de datos y desplegar actualizaciones de código de manera progresiva (ej. _Blue-Green_ o _Canary Deployment_) sin interrumpir la operación del cliente.
- **Performance y Usabilidad:** La carga de imágenes de sushi se vuelve casi instantánea al servirse desde nodos de borde geográficamente cercanos (CDN).

¿Te gustaría profundizar en la configuración del balanceador de carga, la estrategia de manejo de sesiones para los nodos o el esquema de réplicas de la base de datos?