## que es MPLS y que no lo es
### ¿Qué es MPLS?

**MPLS** (_Multiprotocol Label Switching_ o Conmutación de Etiquetas Multiprotocolo) es una tecnología de transporte de datos de **Capa 2.5** que optimiza y acelera el reenvío de tráfico en las redes de los proveedores de servicios (_carriers_).

En lugar de evaluar la dirección IP de destino en cada salto y consultar tablas de ruteo complejas, MPLS le asigna una **etiqueta de longitud fija** a los paquetes al ingresar a la red y conmuta el tráfico en el núcleo (_core_) basándose únicamente en dicha etiqueta.

### ¿Qué NO es MPLS?
- **NO es un protocolo de Capa 2 ni de Capa 3 pura:** Se sitúa en la **Capa 2.5**, ya que la etiqueta se inserta entre el encabezado de Capa 2 (como Ethernet) y la cabecera de Capa 3 (como IP).
- **NO reemplaza a IP ni a los protocolos de ruteo:** En el plano de control, MPLS depende de protocolos de ruteo IP (como OSPF o RIP) para conocer la topología de la red y generar las tablas a partir de las cuales se asignan las etiquetas.
- **NO realiza búsquedas de coincidencia más larga (_longest match_) en el núcleo:** Mientras que un _router_ IP tradicional debe comparar la dirección de destino contra miles de entradas en tablas de ruteo, un conmutador MPLS de _core_ realiza una búsqueda exacta de una sola etiqueta de tamaño fijo en su tabla de etiquetas, haciendo el proceso mucho más rápido.
- **NO es un protocolo visible para el usuario final:** Toda la marcación y conmutación de etiquetas ocurre de forma transparente dentro del _backbone_ del proveedor de servicios; los clientes o usuarios finales siguen enviando y recibiendo paquetes IP estándar.
### Características y Funcionamiento Clave
- **Estructura de la etiqueta (4 bytes / 32 bits):**
    - **20 bits:** Valor de la etiqueta.
    - **3 bits:** Campos experimentales (utilizados para prioridad y Calidad de Servicio / QoS).
    - **1 bit:** Indicador del fondo de la pila (_stacking_ de etiquetas).
    - **8 bits:** Tiempo de vida (_TTL_ - _Time to Live_).
- **Clase de Equivalencia de Reenvío (FEC - _Forwarding Equivalent Class_):** Es un conjunto de paquetes que comparten el mismo destino y los mismos requerimientos de servicio, por lo que son tratados de la misma manera y reciben la misma etiqueta en el ingreso.
- **Protocolo de Distribución de Etiquetas (LDP - _Label Distribution Protocol_):** Protocolo que opera en el plano de control para intercambiar la información de etiquetas entre los _routers_ de la red.
- **Diferenciación de _Routers_ (LSR - _Label Switching Router_):**
    - **Edge LSR (Frontera / Borde):** Es el _router_ que conecta con el cliente. Evalúa el paquete IP entrante, lo asocia a una FEC, inserta la etiqueta al ingresar a la red MPLS y la retira al salir.
    - **Core LSR (Núcleo):** Conmuta los paquetes basándose exclusivamente en la etiqueta, cambiando la etiqueta de entrada por una de salida (_label swapping_) sin inspeccionar la cabecera IP.
- **Gestión del TTL:** El valor del campo TTL de la cabecera IP se copia al campo TTL de la etiqueta MPLS al ingresar a la red para mantener el control de bucles y decrementar los saltos correctamente.
- **Aplicaciones Principales:** Permite la creación de **redes privadas virtuales (VPNs)** de sitio a sitio (conectividad _any-to-any_ / todos con todos), la implementación de calidad de servicio (QoS) y el transporte de tráfico _unicast_ y _multicast_.

## Que es lo que provee MPLS
**MPLS** (_Multiprotocol Label Switching_) es una tecnología de transporte de datos de nivel 2.5 ampliamente utilizada por los proveedores de servicios (_carriers_). Provee los siguientes servicios y capacidades principales:

- **Conmutación ágil basada en etiquetas (_Label Switching_):** Reemplaza la búsqueda iterativa en tablas de ruteo IP (_longest match_) por una búsqueda de coincidencia exacta sobre una **etiqueta de longitud fija de 4 bytes (32 bits)**.
- **Reducción de la carga de procesamiento en el núcleo (_Core_):** Los routers del núcleo (_Core LSR_) conmutan el tráfico analizando y reemplazando únicamente la etiqueta (_label swapping_) sin inspeccionar la cabecera IP del datagrama. La evaluación de la cabecera IP y el etiquetado inicial se delegan a los routers de frontera (_Edge LSR_).
- **Soporte para Redes Privadas Virtuales (VPNs):** Permite a los proveedores conectar múltiples oficinas o sucursales de un cliente sobre una infraestructura pública compartida, garantizando aislamiento lógico y permitiendo conectividad _"todos con todos"_ (_any-to-any_ / _full mesh_).
- **Soporte de Calidad de Servicio (QoS):** Permite clasificar y priorizar distintos tipos de tráfico definiendo Clases de Equivalencia de Reenvío (FEC - _Forwarding Equivalent Class_) y utilizando los bits experimentales/prioridad de la etiqueta.
- **Soporte Multiprotocolo:** Está diseñado para transportar sobre el mismo _backbone_ diversos protocolos de Capa 3 (como IPv4 e IPv6), así como otros tipos de tráfico no IP.
- **Encaminamiento Unicast y Multicast:** Soporta tanto el enrutamiento de tráfico punto a punto (_unicast_) como el tráfico punto a multipunto (_multicast_).

## en MPLS de que se trata el ruteo IP
En la arquitectura de **MPLS** (_Multiprotocol Label Switching_), el ruteo IP se analiza diferenciando cómo funciona el **ruteo IP tradicional** de la **conmutación por etiquetas**, y separando el **plano de control** del **plano de datos**.

### 1. Ruteo IP Tradicional vs. Conmutación en MPLS

- **Ruteo IP tradicional (Capa 3):** Cada router que recibe un datagrama debe inspeccionar la cabecera IP, leer la dirección de destino y comparar ese valor con miles de entradas en su tabla de ruteo local para encontrar la **coincidencia más larga** (_longest match_ o _longest prefix match_). Este proceso se repite independientemente en cada salto.
- **Conmutación en MPLS (Capa 2.5):** Reemplaza la búsqueda compleja en la tabla IP por una búsqueda de **coincidencia exacta sobre una etiqueta de longitud fija** (4 bytes / 32 bits) insertada entre la cabecera de Capa 2 y Capa 3.

### 2. El Rol del Ruteo IP en el Plano de Control

En una red MPLS, el ruteo IP no se elimina; por el contrario, **sirve como la base del plano de control**:

1. **Descubrimiento de rutas (IGP):** Los protocolos de ruteo IP tradicionales (como OSPF, RIP o BGP) corren en el plano de control para descubrir la topología de la red y armar la tabla de ruteo IP.
2. **Asignación y distribución de etiquetas (LDP):** Una vez descubiertas las redes de destino (agrupadas en clases de equivalencia de reenvío o **FEC** - _Forwarding Equivalent Class_), el protocolo **LDP** (_Label Distribution Protocol_) asigna a cada red una etiqueta con significado local y la intercambia con los routers vecinos.

### 3. Funcionamiento en el Plano de Datos

Durante la transmisión real del paquete, los routers desempeñan funciones según su ubicación en el dominio MPLS:

- **Edge LSR (Router de Frontera / Borde):**
    - Recibe el paquete IP tradicional enviado por el cliente.
    - Revisa la dirección IP de destino, determina a qué FEC pertenece y busca en su tabla la etiqueta correspondiente.
    - Inserta la etiqueta MPLS (_push_) y reenvía el paquete etiquetado al núcleo.
- **Core LSR (Router del Núcleo):**
    - Recibe un paquete que ya viene etiquetado.
    - **No lee la cabecera IP ni consulta tablas de ruteo IP**.
    - Consulta su tabla de conmutación de etiquetas, realiza la coincidencia exacta del valor entrante, reemplaza la etiqueta por la de salida (_label swapping_) y conmuta el paquete al siguiente salto.
- **Salida del dominio MPLS:** El router de borde de egreso remueve la etiqueta (_pop_) y entrega el datagrama IP nativo al destino final.

### 4. Beneficios para el Proveedor de Servicios

- **Reducción de la carga de procesamiento en el Core:** Los routers centrales (_Core LSR_) no necesitan almacenar ni consultar tablas de ruteo IP globales con cientos de miles de prefijos; solo conmuta etiquetas.
- **Gestión de tráfico y servicios agregados:** Facilita la creación de **Redes Privadas Virtuales (VPNs)** entre sucursales y la aplicación de **Calidad de Servicio (QoS)** al agrupar y priorizar flujos de datos específicos dentro de distintas FECs.

## En MPLS da la arquitectura y en plano de control
### 1. Arquitectura General de MPLS

La arquitectura de **MPLS** (_Multiprotocol Label Switching_) se sitúa funcionalmente en la **Capa 2.5** del modelo OSI, ya que inserta su cabecera entre la capa de enlace de datos (Capa 2, como Ethernet) y la capa de red (Capa 3, como IP).

En lugar de realizar en cada salto una búsqueda compleja en la tabla de ruteo IP basada en el prefijo de mayor coincidencia (_longest match_), MPLS conmuta el tráfico en el núcleo (_core_) de la red realizando una búsqueda de coincidencia exacta sobre una **etiqueta de tamaño fijo**.

#### Componentes de la Arquitectura (LSR)

La red se compone de routers conmutadores de etiquetas (**LSR** - _Label Switching Router_), diferenciados según su función y ubicación:

- **Edge LSR (LSR de Borde o Frontera):** Se ubica en la interfaz entre el mundo IP tradicional (del cliente) y el dominio MPLS del proveedor. Evalúa los datagramas IP entrantes, determina a qué clase de equivalencia pertenecen, les inserta (_push_) la etiqueta correspondiente y los reenvía hacia el núcleo. En el extremo de salida del dominio MPLS, remueve la etiqueta (_pop_) y entrega el datagrama IP nativo al destino.
- **Core LSR (LSR del Núcleo):** Opera exclusivamente dentro del dominio MPLS procesando paquetes etiquetados. Lee la etiqueta entrante, busca la coincidencia exacta en su tabla de conmutación de etiquetas, reemplaza el encabezado por la etiqueta de salida (_label swapping_) y reenvía el paquete al siguiente salto sin inspeccionar la cabecera IP.

#### Estructura de la Etiqueta MPLS

La etiqueta MPLS es un encabezado de **4 bytes (32 bits)** compuesto por cuatro campos:

1. **Etiqueta (_Label_ - 20 bits):** Valor numérico que identifica la FEC o el destino con significado puramente local entre routers vecinos.
2. **Campos Experimentales (_Exp_ - 3 bits):** Utilizados para definir prioridades y aplicar Calidad de Servicio (QoS).
3. **Indicador de Fondo de Pila (_Bottom of Stack_ - 1 bit):** Indica si se trata de la última etiqueta de la pila, permitiendo anidar múltiples etiquetas en un mismo paquete.
4. **Tiempo de Vida (_TTL_ - 8 bits):** Mapea el valor del campo TTL de la cabecera IP al ingresar para controlar bucles de reenvío dentro del dominio MPLS.

#### Clase de Equivalencia de Reenvío (FEC)

Una **FEC** (_Forwarding Equivalent Class_) es un grupo de paquetes que comparten el mismo destino y los mismos requerimientos de servicio, por lo que son tratados de idéntica manera sobre un mismo camino y reciben la misma etiqueta en el nodo de ingreso.

### 2. El Plano de Control en MPLS

La arquitectura de un router MPLS divide sus operaciones entre el **Plano de Control** (gestión y tareas administrativas) y el **Plano de Datos** (operación ejecutiva y conmutación de paquetes).

El **Plano de Control** ejecuta las siguientes funciones clave:

1. **Descubrimiento de Rutas mediante IGP:**
    - Corren aplicaciones de ruteo IP tradicionales (como OSPF, RIP o BGP) que intercambian mensajes con los routers vecinos para descubrir la topología de la red, aprender las rutas de destino y construir la tabla de ruteo IP (_Routing Information Base_ - RIB).
2. **Asignación Local de Etiquetas:**
    - En función de los prefijos y rutas de destino aprendidas por el protocolo de ruteo IP, un proceso local del plano de control asigna a cada red o FEC un valor de etiqueta con alcance y significado estrictamente local.
3. **Distribución de Etiquetas mediante LDP (_Label Distribution Protocol_):**
    - Se ejecuta el protocolo **LDP** (o protocolos de señalización equivalentes), el cual se encarga de comunicar e intercambiar dinámicamente con los routers vecinos las etiquetas que cada nodo asignó localmente a las distintas FECs.
4. **Alimentación al Plano de Datos:**
    - Toda la información administrativa recopilada y coordinada en el plano de control (rutas aprendidas por el IGP y equivalencias de etiquetas distribuidas por LDP) se procesa y se escribe directamente en el **plano de datos** para generar la tabla de conmutación de etiquetas (LIB/LFIB) y la tabla de reenvío que utilizan los paquetes en tránsito.
## en MPLS detallar los dispositivos LSRs
En la arquitectura **MPLS** (_Multiprotocol Label Switching_), un **LSR** (**Label Switching Router** o _Router Conmutador de Etiquetas_) es todo dispositivo o router de red equipado con la capacidad de conmutar paquetes analizando únicamente etiquetas de longitud fija (4 bytes) insertadas en la cabecera, en lugar de realizar búsquedas iterativas de la dirección IP de destino (_longest match_).

Los LSRs se clasifican en **dos tipos principales** según su ubicación y función dentro del dominio MPLS:
### 1. Tipos de LSRs en la Red

#### **A. Edge LSR (o LER – _Label Edge Router_ / Router de Frontera o Borde)**

Se ubica en la interfaz o límite entre la red IP nativa (del cliente o de accesos externos) y el dominio MPLS del proveedor:

- **Ingreso al dominio (_Ingress LSR_):**
    1. Recibe el datagrama IP tradicional del cliente.
    2. Evalúa la dirección IP de destino y asocia el paquete a una **FEC** (_Forwarding Equivalent Class_).
    3. Inserta/empuja una etiqueta MPLS (**operación _Push_**) entre la cabecera de Capa 2 (ej. Ethernet) y Capa 3 (IP).
    4. Envía el paquete etiquetado hacia el núcleo (_Core_) de la red MPLS.
- **Egreso del dominio (_Egress LSR_):**
    1. Recibe el paquete etiquetado proveniente de los routers del núcleo.
    2. Retira/remueve la etiqueta MPLS (**operación _Pop_**).
    3. Revisa la dirección IP del datagrama original y lo entrega a la red IP de destino.

> _Nota:_ El **Edge LSR** es el dispositivo con mayor sobrecarga de procesamiento, ya que es el único que debe analizar direcciones IP, gestionar tablas de ruteo complejas y mapear el tráfico a etiquetas.

#### **B. Core LSR (_LSR del Núcleo_)**

Se ubica exclusivamente en el interior o _backbone_ del dominio MPLS:

- **Operación de Conmutación (_Label Swapping_):** No examina la cabecera IP ni conoce las redes IP finales de los clientes. Simplemente recibe un paquete con una etiqueta de entrada, consulta su tabla local de etiquetas, reemplaza ese valor por una etiqueta de salida (**operación _Swap_**) y reenvía el paquete al siguiente salto.
- **Mayor Rendimiento y Rapidez:** Al realizar búsquedas de coincidencia exacta sobre valores enteros de tamaño fijo (20 bits), procesa y conmuta paquetes a velocidades muy elevadas.
### 2. Funcionamiento de los LSRs por Planos

Dentro de un LSR, las operaciones se dividen en dos niveles:

- **Plano de Control (_Control Plane_):**
    - **Descubrimiento de rutas:** Corre protocolos de enrutamiento IP (IGP como OSPF o RIP) para aprender la topología de la red y armar la tabla de ruteo IP.
    - **Distribución de etiquetas:** Ejecuta el protocolo **LDP** (_Label Distribution Protocol_), mediante el cual cada LSR asigna etiquetas con significado local a cada red o FEC y se las informa a sus LSRs vecinos.
- **Plano de Datos / Operativo (_Data Plane_):**
    - Contiene las tablas de conmutación de etiquetas (LIB/LFIB) escritas por el plano de control.
    - Ejecuta la conmutación física de los paquetes entrantes procesando únicamente los encabezados MPLS.

### 3. Manejo del Tiempo de Vida (TTL) en los LSRs

Para evitar que paquetes en bucle circulen indefinidamente en la red MPLS, los LSRs sincronizan el campo TTL entre IP y MPLS:

1. Al ingresar a la red, el **Edge LSR** lee el TTL de la cabecera IP, lo decrementa en 1 y copia ese valor al campo TTL de la etiqueta MPLS.
2. Los **Core LSRs** conmutan el paquete etiquetado decrementando en 1 el campo TTL de la etiqueta MPLS en cada salto (sin modificar ni inspeccionar el TTL IP).
3. Al salir del dominio, el **Egress LSR** copia el valor del TTL de la etiqueta de vuelta al encabezado IP, manteniendo la consistencia de saltos de extremo a extremo.

## en MPLS da sus fundamentar: de que se trata la etiqueta y como es
### Fundamentos de MPLS

**MPLS** (_Multiprotocol Label Switching_) surge para solucionar las limitaciones de rendimiento del ruteo IP tradicional en el núcleo (_core_) de las redes de los proveedores de servicios.

- **El problema del ruteo IP tradicional:** En cada salto de la red, un router tradicional debe inspeccionar la cabecera IP de cada datagrama, consultar su tabla de ruteo global (que puede contener cientos de miles de prefijos) y realizar una búsqueda de la **coincidencia más larga** (_longest prefix match_). Este proceso de búsqueda iterativa consume una capacidad de procesamiento considerable.
- **La solución de MPLS:** Introduce una arquitectura de **Capa 2.5** que opera entre la capa de enlace (Capa 2, como Ethernet) y la capa de red (Capa 3, como IP). En lugar de evaluar la dirección IP de destino en cada nodo, el router de borde (_Edge LSR_) asocia el paquete a una **Clase de Equivalencia de Reenvío** (**FEC** - _Forwarding Equivalent Class_) y le adosa una **etiqueta de longitud fija**.
- **Ventaja operativa:** Los routers internos (_Core LSR_) conmutan el tráfico realizando una búsqueda de **coincidencia exacta** sobre la etiqueta y reemplazándola (_label swapping_), sin necesidad de inspeccionar el encabezado IP ni consultar tablas de ruteo IP complejas.

### ¿De qué se trata la etiqueta en MPLS?

La etiqueta es un encabezado o identificador de control de **4 bytes (32 bits)** que se inserta (_push_) en el router de ingreso de la red entre la cabecera de Capa 2 y la cabecera de Capa 3.

Su propósito principal es identificar el destino y la FEC a la que pertenece un flujo de paquetes. Estas etiquetas tienen **significado puramente local** entre dos routers vecinos y son intercambiadas en el plano de control mediante protocolos de distribución como **LDP** (_Label Distribution Protocol_).

### Estructura y campos de la etiqueta (32 bits / 4 bytes)

El encabezado de la etiqueta MPLS contiene los siguientes campos:

```
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                Etiqueta / Label (20 bits)     | Exp (3)|S| TTL|
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

1. **Etiqueta (_Label_ - 20 bits):** Es el valor numérico usado por la tabla de conmutación de etiquetas para determinar la coincidencia exacta y definir la interfaz y etiqueta de salida.
2. **Campos Experimentales (_Exp / Traffic Class_ - 3 bits):** Se utilizan para marcar prioridades y aplicar políticas de **Calidad de Servicio (QoS)** sobre el tráfico.
3. **Fondo de la Pila (_Bottom of Stack / S-bit_ - 1 bit):** Indica si se trata de la última etiqueta de la celda o pila. Si vale `1`, indica que debajo está la cabecera IP; si vale `0`, indica que hay otra etiqueta anidada debajo (lo que permite apilar etiquetas para servicios como VPNs MPLS).
4. **Tiempo de Vida (_TTL / Time to Live_ - 8 bits):** Copia el valor del campo TTL de la cabecera IP al ingresar al dominio MPLS. En cada salto dentro del _core_, los routers decrementan este TTL para prevenir bucles de reenvío indeseados dentro de la red.

## en MPLS da sus fundamentar: formato de la etiquetas MPLS, explicar operación TTL, como se logra la arquitectura MPLS VPN
### 1. Formato de la Etiqueta MPLS

En la arquitectura **MPLS** (_Multiprotocol Label Switching_), la etiqueta se inserta (_push_) en la frontera de la red entre la cabecera de Capa 2 (como Ethernet) y la cabecera de Capa 3 (IP), ubicándose conceptualmente en la **Capa 2.5**.

La etiqueta tiene una longitud fija de **4 bytes (32 bits)** y está dividida en cuatro campos:

```
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                Etiqueta / Label (20 bits)     | Exp (3)|S| TTL|
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

- **Etiqueta (_Label_ - 20 bits):** Es el valor numérico (cadena de 20 bits) que identifica la **FEC** (_Forwarding Equivalent Class_) o destino del flujo para realizar la conmutación de coincidencia exacta. Tiene significado puramente local entre conmutadores vecinos.
- **Campos Experimentales (_Exp_ - 3 bits):** Se utilizan para definir clases de tráfico y prioridades, permitiendo aplicar políticas de **Calidad de Servicio (QoS)** sobre el flujo.
- **Indicador de Fondo de Pila (_Bottom of Stack / Bit-S_ - 1 bit):** Indica si la etiqueta es la última de la pila. Toma el valor `1` si es la última etiqueta antes del paquete IP, o `0` si existen más etiquetas anidadas debajo.
- **Tiempo de Vida (_TTL / Time to Live_ - 8 bits):** Campo de 8 bits que mapea y sincroniza la función de control de tiempo de vida del paquete IP dentro de la red MPLS.
### 2. Explicación de la Operación del TTL en MPLS

Para mantener el control de bucles de reenvío (_routing loops_) dentro del dominio MPLS, el protocolo sincroniza y armoniza el campo TTL del paquete IP con el campo TTL de la etiqueta MPLS:

1. **Ingreso a la red (_Ingress Edge LSR_):** Cuando un datagrama IP entra al dominio MPLS, el router de borde evalúa el paquete, decrementa en 1 el campo TTL del encabezado IP y **copia ese valor** al campo TTL de la etiqueta MPLS recién insertada.
2. **Conmutación en el Núcleo (_Core LSRs_):** Los routers centrales (_Core LSRs_) conmutan los paquetes leyendo únicamente la etiqueta sin inspeccionar ni modificar la cabecera IP oculta. En cada salto del _core_, el router decrementa en 1 exclusivamente el campo TTL de la etiqueta MPLS. Si el TTL de la etiqueta llega a cero, el paquete es descartado.
3. **Egreso de la red (_Egress Edge LSR_):** Al salir de la red MPLS, el router de borde remueve la etiqueta (_pop_) y **copia de regreso el valor del TTL de la etiqueta** al campo TTL de la cabecera IP original. De esta forma, los saltos realizados dentro de la red MPLS quedan correctamente contabilizados en el paquete IP.

_(Nota: Si el administrador deshabilita la propagación del TTL, los saltos internos quedan ocultos y la red MPLS entera se percibe como un único salto desde la perspectiva del usuario en herramientas como traceroute)_.

### 3. Cómo se logra la Arquitectura MPLS VPN

La arquitectura de **Redes Privadas Virtuales sobre MPLS** (MPLS VPN) permite a los proveedores de telecomunicaciones interconectar múltiples sucursales de diferentes clientes sobre una misma infraestructura pública compartida, garantizando aislamiento lógico y conectividad _"todos con todos"_ (_any-to-any_ / _full mesh_).

Esta arquitectura se logra mediante tres pilares principales:

- **Anidamiento de Etiquetas (_Label Stacking_):** Se utiliza una pila de etiquetas aprovechando el bit **S** (_Bottom of Stack_) para colocar múltiples etiquetas en un mismo paquete:
    - **Etiqueta Externa (_Transport Label_):** Es procesada por los routers centrales (_Core LSRs_) para guiar el paquete a través del _backbone_ del proveedor hasta el router de egreso adecuado.
    - **Etiqueta Interna (_VPN Label_):** Es conservada durante el trayecto y procesada por el router de borde de egreso (_Egress LSR_) para identificar a qué cliente o VPN específica pertenece el paquete y entregarlo a la interfaz privada correspondiente.
- **Aislamiento Lógico por Cliente:** El router de borde gestiona etiquetas diferentes para cada cliente (por ejemplo, una etiqueta para el Cliente A y otra para el Cliente B). De esta forma, el Cliente A no puede ver ni comunicarse con el Cliente B a través del _backbone_ de la red.
- **Independencia y Solapamiento de Direcciones:** Cada cliente percibe la red como si fuera una infraestructura privada dedicada para sus sitios. Esto permite que diferentes clientes utilicen internamente los mismos rangos de direcciones IP privadas sin que se generen conflictos en el núcleo del proveedor.
