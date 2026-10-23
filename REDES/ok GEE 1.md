# UTN FRBA
## Departamento de Sistemas
**MATERIA:** Redes de Información  
**NIVEL:** Cuarto  
**AÑO:** 2024  

# GUÍA DE EJERCICIOS DE ESCRITORIO Nº1
## Unidades Didácticas 1 a 5

---

## 1. UNIDAD N° 1: Arquitectura de las redes de datos

### 1.1. Clasificación de las redes: LAN, MAN, WAN y GAN.
==🟡1.1.1. En base a la información pública en Internet identifique redes LAN, MAN y WAN que se emplean para e-governement y otros servicios ciudadanos o de gestión, en nuestro país.==  
Rta.:

En el contexto de la infraestructura de telecomunicaciones descrita en tus fuentes, las redes **LAN, MAN y WAN** se aplican de la siguiente manera para sostener los servicios de **e-government (gobierno electrónico)**, gestión pública y atención al ciudadano en el país:

Redes de Área Local (LAN - Local Area Network)
- **Función y alcance:** Son redes de ámbito privado ubicadas en distancias cortas (edificios de oficinas públicas, municipios, facultades u hospitales) que operan a altas velocidades de transmisión.
- **Aplicación en gestión y e-government:**
    - Conectan las computadoras y servidores internos de cada repartición gubernamental mediante estándares cableados (Ethernet) o inalámbricos (WiFi).
    - Implementan **VLANs (LANs Virtuales)** para segmentar el tráfico interno por áreas de trabajo o niveles de seguridad (por ejemplo, separando la red de administración de la red pública abierta a los ciudadanos).
    - Cuentan con políticas de **firewalls** y autenticación de usuarios para proteger la información interna frente a accesos no autorizados.

Redes de Área Metropolitana (MAN - Metropolitan Area Network)
- **Función y alcance:** Redes que abarcan el ámbito de una ciudad o municipio.
- **Aplicación en gestión y e-government:**
    - Se utilizan para la **interconexión de edificios públicos urbanos** (por ejemplo, conectar un Palacio Municipal con sus distintas secretarías o delegaciones dentro de una misma ciudad) mediante enlaces dedicados de fibra óptica o inalámbricos de banda ancha (como **WMAN / WiMAX 802.16**).

Redes de Área Extendida (WAN - Wide Area Network)
- **Función y alcance:** Conectan redes geográficamente distantes a nivel provincial o nacional.
- **Aplicación en e-government y servicios nacionales:**
    - **Infraestructura troncal (ARSAT):** A nivel nacional se destaca la infraestructura administrada por la empresa estatal **ARSAT**, la cual gestiona el nodo central del **Plan Nacional de Fibra Óptica** e integra un **Data Center con categoría Tier 3 en Benavídez** que alberga y resguarda servidores de datos para organismos del Estado.
    - **Interconexión segura (VPNs):** Para interconectar dependencias gubernamentales en distintas provincias de forma económica y segura, se emplean **VPNs (Redes Privadas Virtuales)** sobre enlaces de Internet pública, asegurando confidencialidad, autenticidad e integridad mediante cifrado de extremo a extremo.

Soporte para la Gobernanza Digital y Trámites Ciudadanos
- **Servicios e IP fijas:** Las plataformas de **gobernanza digital** (como la emisión remota de actas o apostillado de documentos) requieren direcciones **IP públicas fijas** contratadas por los organismos gubernamentales o universitarios para que los servidores DNS puedan asociar de forma estable el dominio con los servicios web ciudadanos.
- **Firma Digital:** Para garantizar la validez legal de los trámites ciudadanos sin requerir firma holográfica, la infraestructura se apoya en esquemas de **firma digital** respaldados por autoridades certificantes, los cuales garantizan **autenticidad, integridad y no repudio** en la documentación pública.
- **Marcos Regulatorios:** El uso del espectro electromagnético y los dominios nacionales en estos servicios están regulados por entidades públicas como **ENACOM** y **NIC Argentina**.

1.1.2. Obtenga información sobre las tecnologías subyacentes en las redes de servicios del Gobierno Nacional, de la Pcia Buenos Aires o del GCBA.
RTA.:
Estación Terrena Benavídez es el principal nodo tecnológico y centro de operaciones espaciales y de telecomunicaciones de la compañía estatal ARSAT, ubicado en la localidad de Benavídez, Provincia de Buenos Aires. Este complejo estratégico concentra gran parte de la infraestructura crítica de datos, interconexión satelital y provisión de servicios de telecomunicaciones mayoristas del Estado nacional.
- **Infraestructura de Datos y Cloud:** Alberga uno de los Data Centers más seguros y avanzados del país (Centro Nacional de Datos), diseñado bajo normas internacionales Tier III, que provee alojamiento de servidores, servicios de nube y almacenamiento para organismos públicos y planes federales de conectividad.
- **Red de Telecomunicaciones y Telefonía:** Funciona como nodo concentrador de la Red Federal de Fibra Óptica (REFEFO), permitiendo articular el tráfico de datos de banda ancha y telefonía IP hacia distintas regiones del país mediante enlaces troncales de alta capacidad.
- **Operaciones Satelitales y Enlaces MAN/WAN:** Integra las antenas de control y seguimiento de satélites geoestacionarios (como el ARSAT-1 y ARSAT-2), operando como pasarela (gateway) central entre las redes terrestres de fibra óptica y los segmentos espaciales de telecomunicaciones.

==🟡1.1.3. Empleando Google Maps localice el conjunto de nodos de redes LAN y MAN que proporcionan servicios de infraestructura de datos y telefonía de algún organismo estatal o privado.==
RTA.:
Edificio Telecom (Paseo Colon) funciona como uno de los centros neurálgicos corporativos y de gestión de redes de telecomunicaciones del operador privado Telecom Argentina.
- Alberga oficinas de ingeniería y control de redes encargadas de administrar la conectividad de datos fija y móvil.
- Coordina la integración de servicios de telefonía corporativa y residencial a gran escala.    
- Actúa como punto de enlace administrativo para la interconexión con nodos de conmutación de la red metropolitana (MAN).

Telecom Empresas es una instalación orientada específicamente al soporte técnico, arquitectura de redes corporativas y provisión de soluciones de infraestructura digital para el sector corporativo y gubernamental.
- Gestiona redes privadas virtuales (VPN), enlaces de fibra óptica dedicados y servicios de centros de datos (datacenter).    
- Ofrece soluciones avanzadas de telefonía IP, centralitas virtuales y gestión unificada de comunicaciones para empresas.

Telecom - Golf - Operaciones corresponde a un nodo operativo y técnico vinculado al control y despliegue de infraestructura de telecomunicaciones.
- Concentra equipos técnicos dedicados al mantenimiento y supervisión de plantas externas e internas de red.
- Facilita la coordinación de cuadrillas y sistemas de monitoreo de fallas en los enlaces de acceso y transporte de datos.

Telecom Argentina S.A. representa las oficinas principales de gestión corporativa y atención estratégica del operador.
- Desde este centro se definen los planes de expansión de la red de acceso y la evolución tecnológica hacia redes de alta velocidad.

Central Retiro Telecom es una central telefónica y nodo histórico de conmutación de red fija.
- Alberga equipos tradicionales y de nueva generación (NGN) para el enrutamiento de tráfico de voz y datos.
- Funciona como un nodo de distribución crítico dentro de la red metropolitana (MAN) para la terminación de abonados y enlaces troncales.

Estación Terrena Benavídez es el nodo tecnológico clave de la empresa estatal **ARSAT**, encargada de la infraestructura crítica de conectividad y satelital del Estado argentino.
- Aloja el Centro Nacional de Datos (Data Center Tier III), que provee infraestructura de nube y almacenamiento seguro para organismos públicos.    
- Interconecta la Red Federal de Fibra Óptica (REFEFO) con pasarelas satelitales para llevar servicios de telefonía y datos a zonas alejadas del país.

1.1.4. Busque redes MAN y WAN propietaria de alguna empresa privada. Describa brevemente las tecnologías involucradas. Considere, entre otras fuentes, los dominios de Internet que se pueden consultar en [nic.ar](https://nic.ar/nic-argentina.xhtml).

RTA.:
  
Las redes de área metropolitana (**MAN**) y de área amplia (**WAN**) corporativas son infraestructuras críticas que permiten a las empresas conectar sus sucursales, centros de datos y oficinas centrales de forma segura y eficiente.
Tomando como referencia a los principales operadores de telecomunicaciones del mercado argentino — cuyos nombres de dominio y servicios se pueden verificar en **NIC Argentina** bajo marcas como _telecom.com.ar_, _movistar.com.ar_ o _claro.com.ar_— a continuación se describen estas redes y sus tecnologías subyacentes.

Infraestructura y Cobertura: Redes MAN y WAN Privadas:
Las grandes empresas de telecomunicaciones operan **redes WAN troncales** (de alcance nacional e internacional) y **redes MAN** (desplegadas en el ámbito urbano de las principales ciudades).
- **Red MAN (Metropolitan Area Network):** Interconecta edificios gubernamentales, sedes bancarias, universidades y antenas celulares dentro de una misma ciudad o área metropolitana mediante anillos de fibra óptica de alta redundancia.
- **Red WAN (Wide Area Network):** Extiende esa conectividad a lo largo de todo el país y el exterior, uniendo las distintas MAN provinciales mediante enlaces troncales terrestres (fibra óptica oscura o iluminada) y enlaces satelitales o subacuáticos.

##### Tecnologías Involucradas

###### A. Multiprotocol Label Switching (IP/MPLS)
Es la tecnología clásica y fundamental de transporte para las Redes Privadas Virtuales (VPN-MPLS) que comercializan operadores como Telecom, Movistar y Claro para el sector corporativo.
- **Funcionamiento:** En lugar de enrutar cada paquete analizando su dirección IP completa salto por salto, MPLS añade una "etiqueta" corta al paquete en el ingreso de la red. Los routers intermedios conmutan el tráfico basándose únicamente en esa etiqueta, lo que acelera drásticamente el reenvío.
- **Calidad de Servicio (QoS):** Permite priorizar el tráfico crítico (como telefonía IP/VoIP o videoconferencias) por encima del tráfico de datos genérico, garantizando anchos de banda simétricos y baja latencia.

###### B. Redes definidas por software para WAN (SD-WAN)
Actualmente, las operadoras complementan o reemplazan las arquitecturas MPLS tradicionales con **SD-WAN**, una tecnología que desacopla el hardware de red del plano de control.
- **Funcionamiento:** Utiliza un controlador centralizado basado en la nube para gestionar de manera inteligente múltiples enlaces de acceso (fibras dedicadas, conexiones 4G/5G corporativas o internet comercial).
- **Ventajas:** Permite rutear de forma dinámica las aplicaciones empresariales por el camino más eficiente en tiempo real, simplifica la administración centralizada de políticas de seguridad y reduce costos operativos frente a los enlaces dedicados tradicionales.

###### C. Ethernet Carrier-Grade (EoMPLS / VPLS)
Tecnología utilizada en las redes MAN para ofrecer servicios de capa 2 (nivel de enlace) transparente entre sucursales distantes de una misma compañía.
- **Funcionamiento:** Permite que dos o más oficinas remotas se comporten como si estuvieran conectadas al mismo switch físico local (LAN extendida), facilitando la configuración de redes corporativas sin que la empresa deba administrar enrutadores complejos en cada locación.

==🟡1.1.5. Identifique otros casos de redes MAN, WAN y GAN en otras zonas del país. Analice las arquitecturas, topologías y tecnologías utilizadas. Por ejemplo: [Conicet](http://www.conicet.gov.ar), [Telecom](http://www.telecom.com.ar/), [Telefónica](http://www.telefonica.com.ar/).== 

RTA.:
##### 1. Arquitectura y Topologías (Redes MAN y WAN / Redes Académicas)
- **Integración a la Red WAN Nacional (InTeLl/MPLS e Innovat):** El CONICET no opera de manera aislada, sino que articula sus centros regionales (como el CCT CONICET-La Plata, CCT Córdoba, CCT Rosario, CCT Patagonia Confluencia, entre otros) apoyándose en la infraestructura de alta velocidad de **Innovat** y conectándose de forma directa al backbone nacional de fibra óptica de **Mylife / Refefo** o a la red académica nacional provista por **InnovaRed**.
- **Topología en Estrella e Híbrida:** A nivel nacional, la WAN adopta una topología híbrida mallada con nodos concentradores en las principales capitales de provincia (Buenos Aires, Córdoba, Rosario, La Plata, Mendoza, Bariloche). Cada Centro Científico Tecnológico (CCT) funciona como un nodo principal que centraliza las conexiones LAN de los institutos dependientes de su zona mediante una red de área metropolitana (MAN) o enlaces dedicados de capa 2/3.

##### 2. Tecnologías Involucradas
- **Enrutamiento IP/MPLS y VPN Académicas:** Se emplean túneles virtuales privados sobre infraestructura de telecomunicaciones dedicada para garantizar el intercambio masivo de datos de investigación (como simulaciones científicas, procesamiento de imágenes astronómicas y genómica).
- **Conectividad Inalámbrica y Redes Globales (GAN / Eduroam):** A nivel de campus e institutos (LAN/WLAN), implementan estándares de alta densidad Wi-Fi integrados a la federación internacional de movilidad **Eduroam**, permitiendo que investigadores y becarios se conecten de manera transparente a redes académicas globales en cualquier parte del mundo.

Telecom Argentina S.A. representa uno de los operadores de telecomunicaciones privadas más grandes del país, cuya infraestructura abarca redes MAN urbanas, una extensa WAN nacional y conectividad internacional (GAN).

##### 1. Arquitectura y Topologías (Redes MAN, WAN y GAN)
- **Red de Núcleo (Core Backbone / WAN):** Posee una topología mallada redundante de fibra óptica terrestre de alta capacidad que recorre las principales rutas del país, uniendo las regiones norte, centro y sur, y conectando nodos de interconexión de tráfico (IXP).
- **Redes MAN (Metropolitan Area Networks):** En ciudades densamente pobladas como Buenos Aires, Córdoba, Rosario y Mendoza, implementa anillos de fibra óptica metropolitana basados en tecnología SDH/DWDM para asegurar redundancia ante cortes físicos.
- **Infraestructura Global (GAN):** A través de cables submarinos internacionales (como los sistemas de los que participa en el Atlántico) y enlaces satelitales, interconecta su red nacional con los grandes centros de datos globales e Internet internacional.

##### 2. Tecnologías Involucradas
- **DWDM (Dense Wavelength Division Multiplexing):** Permite multiplexar múltiples señales ópticas en una sola fibra utilizando diferentes longitudes de onda, logrando transportar Terabits por segundo a lo largo de su red WAN troncal.
- **IP/MPLS y Segment Routing:** Tecnologías de transporte de capa 3 que optimizan la ingeniería de tráfico, permitiendo la conmutación eficiente de paquetes para servicios corporativos (VPN IP), telefonía móvil (LTE/5G) y banda ancha fija (FTTH).   
- **GPON / XGS-PON:** Utilizadas en las redes de acceso de última milla (LAN/MAN residencial y corporativa) para llevar fibra directa al hogar o empresa con altas tasas de transferencia simétrica.
#### Telefónica de Argentina (Movistar)
##### 1. Arquitectura y Topologías (Redes MAN y WAN)
- **Backbone Nacional (WAN):** Telefónica opera una red troncal de transporte IP de altísima capacidad estructurada mediante anillos ópticos interprovinciales que conectan los centros de conmutación regional (_Centrales de Tránsito_).
- **Redes de Acceso Metropolitano (MAN):** Su arquitectura urbana se compone de nodos de distribución óptica (AN/OLT) estratégicamente ubicados en centrales telefónicas históricas que se han transformado en nodos de nueva generación (NGN). La topología combina anillos ópticos de transporte con distribuciones en estrella hacia los abonados.

##### 2. Tecnologías Involucradas
- **Carrier Ethernet y Metro-Ethernet (MEF):** Utilizada en las redes MAN para ofrecer servicios corporativos de capa 2 transparentes, permitiendo la interconexión de sucursales bancarias y empresariales con garantías estrictas de SLA (Acuerdos de Nivel de Servicio).
- **IP/MPLS sobre DWDM:** Arquitectura convergente donde el plano de transporte óptico (DWDM) soporta las capas de encaminamiento IP/MPLS, permitiendo la coexistencia de tráfico de voz móvil (VoLTE), telefonía fija IP y datos corporativos de alta criticidad.


==🟡1.1.6. ¿Qué alternativas sobre WAN públicas han surgido para remplazar las WAN propietarias y proveerles una adecuada seguridad de la información? Identifique las arquitecturas, topologías y tecnologías involucradas en dichas alternativas.==  

RTA.:

Para reemplazar las costosas y rígidas WAN propietarias tradicionales (como los circuitos dedicados MPLS) utilizando redes públicas (Internet, conexiones de banda ancha, LTE/5G) sin sacrificar la seguridad, la industria ha adoptado arquitecturas y paradigmas modernos.

A continuación se detallan las principales alternativas surgidas, junto con sus arquitecturas, topologías y tecnologías subyacentes:
###### 1. Principales Alternativas Tecnológicas
- **SD-WAN (Software-Defined Wide Area Network):** Es la base de conectividad moderna. Desacopla el hardware de red del plano de control, permitiendo utilizar múltiples enlaces públicos de bajo costo de manera inteligente y dinámica.
- **SASE (Secure Access Service Edge):** Unifica la red SD-WAN con funciones de seguridad avanzadas entregadas nativamente desde la nube (Cloud-native). Resuelve el problema de la seguridad en la WAN pública integrando la protección directamente en el borde de servicio.
- **SSE (Security Service Edge):** Subconjunto de SASE enfocado exclusivamente en la capa de seguridad basada en la nube (ideal para organizaciones que ya cuentan con SD-WAN pero necesitan robustecer sus políticas de acceso y protección).

###### 2. Arquitecturas Involucradas
- **Arquitectura de Superposición (Overlay Architecture):** Se construye una red lógica virtual (_overlay_) sobre la infraestructura física de transporte público (_underlay_). Los paquetes se encapsulan de forma transparente para viajar de manera segura a través de Internet.
- **Borde de Servicio Distribuido (Cloud-Native PoPs):** A diferencia de las WAN tradicionales (donde todo el tráfico corporativo debía pasar obligatoriamente por un centro de datos centralizado para ser inspeccionado), SASE/SD-WAN distribuyen puntos de presencia (_Points of Presence - PoPs_) globales en la nube. Esto permite aplicar inspección de seguridad cerca del usuario o de la sucursal, optimizando la latencia hacia aplicaciones SaaS y la nube pública.
- **Modelo Zero Trust (Confianza Cero):** La arquitectura abandona la idea del "perímetro seguro de red". Ningún usuario, dispositivo o sucursal es confiable por defecto, por lo que cada conexión y flujo de datos debe ser autenticado y autorizado de forma continua.

###### 3. Topologías de Red
- **Topología Híbrida y Multi-transporte:** Combina enlaces de Internet de fibra comercial, conexiones de banda ancha fija y accesos inalámbricos (4G/5G) en una misma sucursal.
- **Malla Dinámica (Dynamic Mesh):** Las sucursales pueden establecer comunicación directa de manera segura entre sí a través de Internet (creando túneles bajo demanda) sin necesidad de retransmitir el tráfico obligatoriamente a través de una sede central o nodo concentrador físico.
- **Centralización de Gestión (Control Plane Centralizado):** Las políticas de seguridad y enrutamiento se definen desde una consola central en la nube y se distribuyen automáticamente (_Zero-Touch Provisioning_) a todos los dispositivos de borde (_Edge_) de la red.

###### 4. Tecnologías y Protocolos Clave de Seguridad
- **Cifrado IPsec y TLS:** Creación de túneles virtuales cifrados de extremo a extremo para proteger los datos en tránsito sobre la red pública de Internet.
- **ZTNA (Zero Trust Network Access):** Reemplaza a las tradicionales y vulnerables VPNs de acceso remoto, otorgando acceso granular exclusivamente a aplicaciones específicas según la identidad del usuario y el contexto del dispositivo, en lugar de otorgar acceso a toda la red.
- **FWaaS (Firewall-as-a-Service):** Cortafuegos de nueva generación alojados en la nube que aplican políticas consistentes de filtrado de tráfico e inspección de paquetes (Deep Packet Inspection) sin importar dónde se encuentre el usuario.
- **SWG y CASB (Secure Web Gateway & Cloud Access Security Broker):** Tecnologías integradas para monitorear, bloquear amenazas web y garantizar el cumplimiento normativo en el uso de aplicaciones en la nube y servicios SaaS.



### 1.2. Redes orientadas y no orientadas a conexión.
==🟡1.2.1. Realice una representación gráfica esquemática de un sistema orientado a la conexión y otro para el caso sin conexión.==  
RTA.:
```txt
================================================================================
SISTEMA ORIENTADO A LA CONEXIÓN (TCP)      SISTEMA SIN CONEXIÓN (UDP)
================================================================================
Cliente TCP              Servidor TCP     Emisor UDP             Receptor UDP
    │                         │               │                         │
    ├─ 1. SYN (Seq = x) ─────>│               ├─ Datagrama 1 ──────────>│
    │<─ 2. SYN-ACK ───────────┤               ├─ Datagrama 2 ──────────>│
    ├─ 3. ACK ───────────────>│               ├─ Datagrama 3 (PÉRDIDA) ─X  (Sin retransmisión)
    │                         │               ├─ Datagrama 4 ──────────>│
    │ [Sesión Establecida]    │               │                         │
    ├─ Datos (Seq, Payload) ─>│               └─ (Sin Handshake, Sin ACK, Sin Estado)
    │<─ ACK (AckNum) ─────────┤
    │                         │
    ├─ FIN ──────────────────>│
    │<─ ACK ──────────────────┤
    │<─ FIN ───────────────-──┤
    ├─ ACK ──────────────────>│
    │ [Sesión Liberada]       │
===================================================================================
```
##### 1. Sistema Orientado a la Conexión (TCP)
En TCP, la comunicación exige establecer previamente una sesión lógica lógica entre ambos extremos antes de enviar datos:
- **Fase 1: Establecimiento (_3-Way Handshake_):**
    1. **SYN:** El cliente envía una solicitud de sincronización con un número de secuencia inicial (\(x\)).
    2. **SYN-ACK:** El servidor responde confirmando la recepción del SYN (\(Ack = x+1\)) y enviando su propia sincronización (\(Seq = y\)).
    3. **ACK:** El cliente confirma el mensaje del servidor (\(Ack = y+1\)), quedando la sesión oficialmente abierta en modo _full-duplex_.
- **Fase 2: Transferencia Confiable de Datos:**
    - Cada segmento transporta datos e identifica su posición mediante **números de secuencia**.
    - El receptor responde con acuses de recibo (**ACK**). Si un paquete se pierde o el temporizador expira, se ejecuta la **retransmisión automática**.
    - Se aplica **control de flujo** mediante ventana deslizante para no saturar al receptor.
- **Fase 3: Cierre de Conexión (4 Vías):**
    - Para finalizar la sesión, ambos extremos intercambian señales **FIN** (_Finish_) y sus correspondientes **ACK** de forma independiente para liberar los recursos.

##### 2. Sistema Sin Conexión (UDP)
En UDP, la comunicación es directa, liviana y sin conservación de estado (_stateless_):
- **Sin Handshake ni Inicio:** El emisor envía los datagramas inmediatamente a la red sin verificar previamente si el receptor está activo o en condiciones de recibirlos.
- **Sin ACKs ni Retransmisiones:** No existen mensajes de acuse de recibo. Si un datagrama se pierde en la red debido a congestión o fallos, el protocolo de transporte lo ignora y no lo retransmite.
- **Sin Cierre Formal:** Al no existir una sesión o canal lógico abierto, no hay intercambio de banderas de finalización.
- **Mínimo Overhead:** La cabecera fija es de solo **8 bytes** (frente a los 20 bytes mínimos de TCP), lo que reduce drásticamente la latencia y el procesamiento de red.


==🟡1.2.2. Analice las ventajas y las desventajas de las redes orientadas a la conexión.==

RTA.:

En las redes de comunicación, los protocolos y servicios **orientados a la conexión** (cuyo máximo exponente en la capa de transporte es **TCP**, y en capas de red/enlace los **circuitos virtuales**) exigen establecer una sesión lógica previa entre emisor y receptor antes de transmitir datos reales, manteniendo el estado de la comunicación y liberándola al finalizar.

##### 🟢 Ventajas

1. **Garantía de Fiabilidad y Entrega Completa:**
    - Al requerir confirmación explícita (**ACK**) para cada segmento o bloque de datos enviado, el sistema detecta pérdidas o errores por temporizador (_timeout_) y **retransmite automáticamente** los paquetes perdidos hasta asegurar una copia fiel de la información.
2. **Reorganización y Entrega Ordenada:**
    - Asigna números de secuencia a cada trama o segmento, lo que permite al receptor **reensamblar los datos en el orden exacto de origen**, solucionando la llegada desordenada producida por rutas IP heterogéneas.
3. **Control de Flujo:**
    - Utiliza mecanismos de **ventana deslizante** (_sliding window_) para adaptar la tasa de transferencia a la capacidad de procesamiento y almacenamiento en búfer del receptor, evitando la saturación del equipo destino.
4. **Control y Adaptación ante la Congestión:**
    - Realiza un seguimiento del estado de la red (_stateful_) y reduce automáticamente el tamaño de la ventana de envío cuando detecta caídas o demoras excesivas en los acuses de recibo.
5. **Verificación Previa del Estado del Receptor:**
    - Mediante el intercambio inicial de señales (_3-way handshake_: SYN, SYN-ACK, ACK), se verifica que el destinatario esté activo, disponible y listo para procesar la información antes de transmitir la carga útil.


##### 🔴 Desventajas

1. **Mayor Retardo e Ineficiencia Inicial (Latencia):**
    - El requerimiento de completar el saludo de tres vías (_handshake_) antes de enviar datos, sumado al proceso formal de desconexión de cuatro vías (FIN, ACK), introduce una demora fija de establecimiento y liberación que desacelera las comunicaciones cortas.
2. **Alta Sobrecarga de Red y Procesamiento (_Overhead_):**
    - Las cabeceras de control son considerablemente más voluminosas (por ejemplo, mínimo **20 bytes** en TCP frente a 8 bytes en UDP). Además, el constante intercambio de mensajes de confirmación (ACKs) y la gestión de temporizadores consumen mayor ancho de banda y capacidad de CPU en los equipos.
3. **Inadecuado para Aplicaciones en Tiempo Real:**
    - En transmisiones de audio o video en vivo (VoIP, streaming interactivo, juegos en línea), las pausas generadas por la retransmisión de un paquete perdido provocan congelamientos o descalces temporales. En estos escenarios es preferible descartar una pequeña pérdida imperceptible a sufrir latencia acumulada.
4. **Mantenimiento de Estado y Consumo de Recursos:**
    - Al ser un sistema con estado (_stateful_), los nodos de extremo deben mantener registros activos de secuencias, puertos efímeros y buffers en memoria para cada conexión simultánea, limitando el número total de clientes concurrentes si no se escalan los recursos.

==🟡1.2.3. Analice las ventajas y las desventajas de las redes sin conexión.==  
RTA.:
Las **redes y servicios sin conexión** (también conocidos como modo **datagrama**, representados por **UDP** en la capa de transporte e **IP** en la capa de red) se caracterizan porque cada paquete o datagrama contiene toda la información necesaria de direccionamiento para viajar de manera independiente hacia el destino, sin requerir el establecimiento previo de un canal o sesión lógica entre los extremos.

##### 🟢 Ventajas
1. **Baja latencia y rapidez de transmisión:**
    - Al no requerir un intercambio inicial de señales (_handshake_ o saludo de tres vías) ni una fase de cierre de sesión, la transmisión de datos comienza de manera inmediata, eliminando el retardo inicial de establecimiento de conexión.
2. **Menor sobrecarga de red (_Overhead_ reducido):**
    - Las cabeceras de control son considerablemente más pequeñas (por ejemplo, la cabecera fija de UDP ocupa únicamente **8 bytes**, frente a los 20 bytes mínimos de TCP). Esto reduce el consumo de ancho de banda y optimiza el procesamiento en los equipos de red.
3. **Soporte para comunicaciones de difusión y multidifusión (_Broadcast_ y _Multicast_):**
    - A diferencia de los servicios orientados a la conexión (que son estrictamente de punto a punto), los servicios sin conexión permiten enviar información de un punto a múltiples destinatarios (_un punto a varios puntos_) simultáneamente.
4. **Operación sin estado (_Stateless_):**
    - Los nodos y dispositivos intermediarios de la red no necesitan conservar registros del estado de la comunicación ni gestionar ventanas de seguimiento para cada cliente, lo que simplifica la infraestructura y facilita una alta capacidad de escalabilidad.
5. **Apropiado para tráfico en tiempo real y transmisiones en ráfaga:**  
    - En aplicaciones sensibles al tiempo (como voz sobre IP, videoconferencias, streaming en vivo, videojuegos o consultas rápidas de DNS/DHCP), **un mensaje incompleto pero entregado a tiempo es más valioso que un mensaje completo entregado con retraso**.

##### 🔴 Desventajas
1. **Falta de garantía de entrega e irconfiabilidad:**
    
    - No existe mecanismo de acuse de recibo (**ACK**) ni de retransmisión automática en este nivel. Si un datagrama se pierde en el camino debido a congestión o fallos en el enlace, simplemente se descarta.
2. **Entrega desordenada de paquetes:**
    
    - Como cada paquete se enruta de forma independiente, pueden tomar rutas totalmente distintas dentro de la red y **llegar desordenados al destinatario**.
3. **Ausencia de control de flujo y de congestión:**
    
    - El emisor no ajusta automáticamente la tasa de transferencia en función de la capacidad de procesamiento del receptor ni ante la saturación de los buffers en la red, lo que puede provocar pérdidas masivas de paquetes si la red está congestionada.
4. **Mayor complejidad de desarrollo en la capa de aplicación:**
    
    - Toda la responsabilidad de verificar la integridad, ordenar los datos o gestionar posibles retransmisiones (si la aplicación lo requiere) recae exclusivamente sobre la propia **aplicación**, incrementando la carga del programador.

### 1.3. Clasificación de los protocolos de comunicaciones.
1.3.1. Utilice diagramas de estado, secuencia o actividad para representar los 3 sistemas con sondeo y selección. Seleccione la variable más representativa en cada caso y utilice el diagrama más apropiado:  
   * 1.3.1.1. Sondeo selectivo y de grupo.  
   * 1.3.1.2. Sondeo con parada y espera.  
   * 1.3.1.3. ARQ continuo (ventanas deslizantes).  
1.3.2. Mediante los modelos de sistemas más aptos describa cada uno de los tres sistemas sin sondeo: Xon/Xoff, RTS/CTS y TDMA.  
1.3.3. Realice un diagrama del funcionamiento de un sistema con manejo de prioridad (emplee seudocódigo, UML u otra representación sistémica NO ambigua).  
1.3.4. ¿Qué criterios se emplean en los protocolos de comunicaciones de datos cuando los canales tienen baja tasa de error? ¿cuáles, en los casos de alta tasa de error?  

> *Nota: GEE Nro 1 versión 1.71.docx (1-24)*

---

### 1.4. Topología de redes LAN y WAN.
1.4.1. Grafique las topologías de las redes LAN y WAN analizadas en el ejercicio 1.1.  
1.4.2. Realice un análisis comparativo de topologías LAN y las tecnologías que podrían emplear en cada segmento. Haga un análisis de las subredes WAN que identifica.

> **Figura de referencia (Stallings, 2016):** Esquema de red que incluye Internet, Router con firewall, PSTN, Distribution router, IP telephony server, Centralized servers, Edge router, Ethernet switch, Wi-Fi access point, y Physically-attached devices.  
> *Fuente: Stallings, William. Foundations of Modern Networking: SDN, NFV, QoE, IoT, and Cloud. Pearson Education. 2016*

1.4.3. Identifique en el mercado, en organizaciones gubernamentales o en ONG, diferentes topologías de redes WAN. Grafique la localización de los nodos mediante un visualizador de mapas de uso libre (Google Maps, gvSIG, etc).

---

## 2. UNIDAD $N^{\circ}$ 2: Redes de área local - LAN

| EJERCICIOS NECESARIOS | PARA TRABAJOS DE LABORATORIOS |
| :--- | :--- |
| **2.1.3.** | Configuración |
| **2.3.6. a 2.3.14.** | Configuración |
| **2.2.1. - 2.2.2** | Análisis |
| **2.3.15. / 2.3.18.** | Análisis |
| **2.4.8.** | Análisis |

### 2.1. Componentes y características técnicas de las redes LAN.
2.1.1. Detallar la asignación de contactos en una tarjeta de red y en un switch. Graficar el funcionamiento semiduplex y full duplex.  
2.1.2. Detallar las causas por las cuales puede ser descartada una trama en una placa FastEthernet.  
2.1.3. En los esquemas de red que se muestran a continuación, indicar cuántos dominios de colisiones y de broadcast se tienen. Justifique cada respuesta.  
   * **2.1.3.1.** (Esquema de Switch y Hub conectado a un puerto).  
   * **2.1.3.2.** (Esquema de Packet Tracer con Cloud, Linksys Wireless Router, Switches 2950, Hubs y PCs).  
     * 2.1.3.2.1. Si todos los dispositivos de la LAN trabajan en half dúplex.  
     * 2.1.3.2.2. Si todos los dispositivos de la LAN trabajan en full dúplex, con excepción de los conectados al HUB.  
   * **2.1.3.3.** (Esquema jerárquico de red con Capa Núcleo, Capa Distribución, Capa Acceso / IDFs / MDF, y Router de Borde conectado a Internet).  

---

### 2.2. Normas del IEEE relacionadas con las redes LAN.
2.2.1. Se ha efectuado el análisis de una trama Ethernet mediante un analizador de protocolos, obteniéndose al comienzo de la trama los siguientes 28 caracteres hexadecimales: `00 60 08 08 BB 07 00 A0 24 4B 15 7D 08 00`. Indicar: Tipo de Trama Ethernet, Tipo de direccionamiento, direcciones MAC, Tipo de protocolo que transporta.  
2.2.2. Idem ejercicio anterior, para la trama: `FF FF FF FF FF FF 00 A0 C9 D4 4F FD 08 06`.  

---

### 2.3. Protocolos y topologías lógicas y físicas de las redes LAN.
2.3.1. Describa el funcionamiento del algoritmo exponencial binario empleado por el protocolo IEEE 802.3. ¿Qué ventajas presenta, comparado con un simple proceso aleatorio de acceso al bus?  
2.3.2. Calcular el tiempo mínimo de transmisión de las tramas de mayor y menor longitud que se pueden enviar en las redes LAN Ethernet. Suponer entre tramas un tiempo de acceso de 9,6 microsegundos. Efectuar los cálculos suponiendo redes de 100 Mbps y 1 Gbps.  
2.3.3. ¿Qué pasaría en CSMA/CD si, luego de ocurrida una colisión, las estaciones esperaran un tiempo fijo igual para todas?  
2.3.4. Explique el protocolo CSMA/CD, cuando se produce una colisión, como se resuelve la misma con el algoritmo exponencial binario, suponiendo que $n=2$ (contador de colisiones), indicar la probabilidad que se produzca nuevamente una colisión.  
2.3.5. Sea P el tiempo de propagación, de un extremo al otro de una red Ethernet, ¿Cuál es el tiempo máximo que deberá transcurrir para que las estaciones se aseguren de que no ocurrió una colisión? ¿Qué relación guarda éste tiempo con el tamaño mínimo de trama permitido por la norma? ¿Qué pasa si un emisor transmite una trama de tamaño menor al mínimo especificado?  
2.3.6. ¿Qué actividades caracterizan a un protocolo de Control de Enlace de datos?  
2.3.7. ¿Qué rol cumplen los switches en redes Ethernet, de Layer 2 y de Layer 3 y cómo intervienen ante el problema de las colisiones, en las conmutaciones de capa 2 y de capa 3?  
2.3.8. Grafique un escenario de red con topologías sin colisiones y otro con colisiones, con al menos 3 dominios de colisión.  
2.3.9. Grafique un escenario de comunicaciones basadas en colisión, con al menos 3 dispositivos de red, 2 servidores y 12 equipos terminales PC. Determine los dominios de colisión y de broadcast.  
2.3.10. Modifique el escenario anterior para optimizar el ancho de banda dedicado en el / los segmentos más comprometidos con switch. Compare los dominios de colisión y de broadcast con el escenario anterior.  
2.3.11. Transforme el escenario anterior a otro con ancho de banda dedicado y jerarquizado por capas de acceso, de distribución y núcleo. Compare los dominios de colisión y de broadcast con el escenario anterior. Indique los puertos a los cuales le configuraría seguridad de puerto.  
2.3.12. Organice el escenario anterior con 2 VLANs. Indique los puertos que configuraría como de acceso y cuáles, troncales.  
2.3.13. En el escenario del ejercicio 2.1.3.3., indique los puertos que configuraría como de acceso y cuáles, troncales.  
2.3.14. Dado el siguiente esquema indicar cómo funciona el protocolo STP, marcando cuál es el switch raíz y los puertos designado, raíz y bloqueado (Switch A con MAC `00 0a 00 23 ab 15` y Switch B con MAC `00 0b 00 23 ab 15`).  
2.3.15. Grafique cómo modifica la trama 802.3 el protocolo IEEE 802.1Q.  
2.3.16. Para la imagen que muestra la captura de una trama 802.1q, analice: Campo Tipo, Prioridad, Id VLAN, Campo Tipo de la trama Ethernet II enviada por `00:19:d1:70:6e:38`.  
2.3.17. La imagen muestra la captura de una trama 802.1q, analice: Campo Tipo, Prioridad, Id VLAN, Campo Tipo de la trama Ethernet II enviada por `00:19:d1:70:6e:38`.  
2.3.18. ¿Qué permite el protocolo IEEE 802.1D?. Describa la topología básica que se forma.  

---

### 2.4. Tramas: Ethernet e IEEE 802.3.
2.4.1. Detalle la estructura de la trama Ethernet DIX v2 y de la trama IEEE 802.3. Indicar las diferencias.  
2.4.2. ¿Cómo es el tratamiento de errores en el protocolo Ethernet?  
2.4.3. Dado el siguiente conjunto de bits a transmitir `10110101101` y teniendo como polinomio generador $G(x) = x^{4} + x + 1$, aplicar el método para control de errores CRC, determinando la información a transmitir.  
2.4.4. Dibuje los formatos de las tramas IEEE y Ethernet, explicando el significado de cada campo. Explique el mecanismo que se utiliza en un switch para bloquear la entrada de tramas.  
2.4.5. Detallar la trama que se emplea en las redes Ethernet que operan a 1 Gbps.  
2.4.6. ¿Qué tipo de codificaciones se emplean en redes 10 Gigabits Ethernet? Explicar la función de las mismas.  
2.4.7. ¿Qué tipo de medios se utilizan para implementar las redes 10 Gigabits Ethernet?  
2.4.8. Considerando las capturas mostradas en las siguientes imágenes, ¿qué tipo de trama es y qué tipo de datagrama encapsula? (Se incluyen capturas de tramas y campos en hexadecimal para análisis).  
2.4.9. ¿Qué función cumplen "Carrier extensión" y "packet bursting" en redes Gigabits Ethernet?  
2.4.10. ¿Qué código se emplea en las redes Gigabits Ethernet que operan con Fibra óptica?  
2.4.11. ¿Cómo funciona y para qué se emplean las redes "Power over Ethernet"?  

---

### 2.5. Sistema de acceso al medio basado en el "paso de testigo" (Token). Token Ring (paso de testigo en anillo). Norma IEEE 802.5.
2.5.1. Resumir, mediante una tabla comparativa, las similitudes y diferencias entre el modelo de acceso al medio basado en el "paso de testigo" (IEEE 802.5) y el de "acceso aleatorio" (IEEE 802.3).  
2.5.2. Detallar los datos que emplea la trama en las redes IEEE 802.5 y destacar para que proceso se emplea cada uno de ellos.  
2.5.3. Especificar los servicios que presta cada una de las capas / subcapas a la inmediata superior, incluidos aquellos que se prestan a la capa de Red.  

---

## 3. UNIDAD N° 3: Implementación de redes LAN mediante el empleo de cableado estructurado.

> *EJERCICIOS RECOMENDADOS PARA TRABAJOS DE LABORATORIOS: 3.1.2. (Configuración)*

### 3.1. Norma de cableado estructurado EIA/TIA 568.
3.1.1. De acuerdo a la norma de la EIA/TIA 568, indique gráficamente mediante un mapa de cableado cómo quedaría el estado de las conexiones según el Código de Colores del Cableado Estructurado, entre ambos extremos, para el caso de cables derechos y cables cruzados (T568A y T568B).  
3.1.2. Indique ¿qué tipo de cables? se utilizan para conectar los siguientes equipos: Hub a hub, PC a hub, router a switch, PC a router, Switch a switch, router a router, PC a switch, Router a hub, PC a PC, hub a switch.  
3.1.3. Las normas europeas ISO/IEC 11801 y las normas americanas ANSI/TIA/EIA, conforman las normas para cableados estructurados, y reglamentan hoy los sistemas de cableados, donde la europea incluye todas las normas americanas. Describa sintéticamente el alcance de cada una de las siguientes normas:  
   * ANSI/EIA/TIA 568 (A) B1.  
   * ANSI/EIA/TIA 568 (A) B2.  
   * ANSI/EIA/TIA 568 B3.  
   * ANSI/EIA/TIA 606.  
   * ANSI/EIA/TIA 569.  
   * ANSI/EIA/TIA 526-7.  
   * ANSI/EIA/TIA 526-14 A.  
   * ANSI/EIA/TIA 607.  
   * ANSI/EIA/TIA 758.  
3.1.4. Realice un cuadro comparativo de las características y especificaciones técnicas de las siguientes Clases y Categorías de Cableado:  
   * Clase D - Categoría 5.  
   * Clase D - Categoría 5E.  
   * Clase E - Categoría 6.  
   * Clase F - Categoría 7.  
3.1.5. Señale en un Mapa de Cableado el estado de las conexiones según el Código de Colores del Cableado Estructurado y la función que cumple cada hilo en un cable cruzado (Pares 1 a 4, Blanco/Naranja, Naranja, Blanco/Verde, Azul, Blanco/Azul, Verde, Blanco/Marrón, Marrón, Blindaje o Tierra).  

---

### 3.2. Mediciones efectuadas al cableado estructurado efectuado con cable UTP: NEXT, Atenuación, Ruido, Wiremap, Longitud, Resistencia, etc.
3.2.1. Analice la documentación de certificación de una red de cableado estructurado e identifique las situaciones que satisfacen el estándar y las que no lo hacen. Para las defectuosas, explique la causa e indique una posible solución.  

---

### 3.3. Cableado de Oficina. Cableado Horizontal. Cableado del Backbone. Arreglo de la sala de red y cableado de acceso a la red. Administración del cableado estructurado.
Usted se encuentra realizando una revisión técnica de una red instalada (el caso de estudio le será dado en clase). La misma dispone de un switch para el cual el fabricante ha especificado las siguientes reglas topológicas para la implementación de redes LAN:
* **Reglas para conexión semiduplex a 100 Mbps:**  
  * Distancia máxima del cable UTP: 100 m.  
  * Distancia máxima de 412 m para la conexión con FO entre dos switches o una estación y un switch.  
  * Alcance máximo de la red de 325 m para topología con un único repetidor (Ejemplo: 225 m de FO desde un repetidor al switch y 100 m de UTP desde este a una estación).  
* **Reglas para conexión duplex a 100 Mbps:**  
  * Distancia máxima del cable UTP: 100 m.  
  * Distancia máxima de 2000 m para la conexión con FO entre dos switches o una estación y un switch.  

**Se solicita:**  
Rediseñar la topología de red e indicar los elementos necesarios para su implementación de una red WAN organizacional, suponiendo que se dispone de 3 edificios de 6 plantas, 2 redes LAN por piso, cada una de 150 hosts. La distancia entre pisos es de 4 m y cada piso tiene un largo de 150 m y un ancho de 50 m. La montante se encuentra aproximadamente en la mitad del piso. En todos los casos se deben reutilizar las placas de red semi dúplex o planificar los costos de su reemplazo. Se consideraran dos alternativas:
* **Alternativa 1:** Para la implementación de la red se utilizaran en los pisos cable UTP categoría 6, y switches apilables (24 ports por cada uno, pila de hasta 7 equipos) de 100/1000 Mbps. El cableado vertical se efectuara con FO a un Switch 1/10 Gbps, ubicado en planta baja (cableado colapsado). El diseño debe contar con una redundancia del 20% y extensibilidad a 3 edificios similares que se integrarán en el futuro.  
* **Alternativa 2:** Para la implementación de la red se utilizaran en los pisos cable UTP categoría 5e, y switches de 12 ports de 100 Mbps operando semiduplex, cuya regla de conexión se indicó precedentemente. El cableado vertical se efectuara con FO a un Switch ubicado en planta baja (cableado colapsado). El diseño debe contar con una redundancia del 20% y extensibilidad a 3 edificios similares que se integrarán en el futuro.  

---

### 3.4. Calculo del costo y materiales necesarios para realizar el cableado estructurado en un "edificio inteligente".
3.4.1. Se desea construir una red LAN que tiene 500 puestos, calcule el costo de implementarla con redes Ethernet de 100, 1.000 Mbps y 10 Gbps. Se empleará cableado estructurado categoría 6 y switches compatibles.  

---

## 4. UNIDAD N° 4: Redes LAN inalámbricas.

> *EJERCICIOS RECOMENDADOS PARA TRABAJOS DE LABORATORIOS:*  
> *4.1.1. (Configuración)*  
> *4.3.1, 4.3.2, 4.3.3, 4.3.4, 4.3.5. (Configuración)*

### 4.1. Métodos inalámbricos de transmisión de datos. Modulación por pseudoruido. Espectro disperso SSS. Modulación por salto de frecuencia.
4.1.1. Realice un análisis comparativo del/de los método/s de transmisión empleado/s por los Access Point Wifi Cisco LYNKSYS, modelos Wrt54g y WAP300N.  

### 4.2. Métodos de control de acceso.
4.2.1. Mediante la definición de factores de comparación y un estudio detallado, realice un informe sobre los métodos de control de acceso IEEE 802.11g vs IEEE 802.3.  

### 4.3. Protocolos de redes LAN inalámbricas.
4.3.1. Mediante diagramas de sistemas (UML u otro) grafique el funcionamiento de cada uno de los protocolos de LAN inalámbricas (IEEE 802.2 e IEEE 802.11) utilizados por el Access Point que será empleado en el TLab respectivo.  
4.3.2. Dado el Caso de Estudio (esquema con Office, Router, NAT, Access point con IP `172.16.1.1`, enlace inalámbrico punto a punto de 10 kms hacia ISP con IPs `172.16.0.1` y `172.16.0.2`, DHCP en rango `10.0.0.2-254`), resuelva los interrogantes divididos en:  
   * **4.3.2.1. Ejercicio 1: Capa 1 - La capa de acceso al medio** (Preguntas de diagnóstico de abajo hacia arriba ante fallo de correo en notebook).  
   * **4.3.2.2. Ejercicio 2: Capa 2 - La capa IP** (Resolución de problemas de primer salto y DHCP).  
   * **4.3.2.3. Ejercicio 3: Capa 3 + La capa de transporte y superiores** (Análisis de saltos en red `10.0.0.0/8` conectada a Internet vía servidor NAT `192.168.0.2`).  
   * **4.3.2.4. Ejercicio 4:** Configuración de red con cinco dispositivos inalámbricos (Client 1, Client 2, Hub, Repeater 1a, Repeater 1b, Router) y resolución de pruebas de conectividad (ping).  
4.3.3. Señale las diferencias de velocidades que se pueden esperar "a priori" entre una red cableada e interconectada con SWITCH FastEthernet y otra configurada mediante un access point que soporta la norma IEEE 802.11g. Realice un gráfico del rendimiento teórico esperado, en ambos casos, en función de la cantidad de equipos conectados, indicando el "umbral" a partir del cual una red es mejor que la otra.  
4.3.4. Realice el mismo análisis que el del apartado anterior, entre una red cableada e interconectada con SWITCH Giga Ethernet y otra configurada mediante un access point que soporta la norma IEEE 802.11n. Amplíe el gráfico anterior.  
4.3.5. Implemente en el simulador los escenarios analizados y resueltos en los casos 4.3.2.  

---

## 5. UNIDAD N° 5: Protocolo TCP/IP.

> *EJERCICIOS RECOMENDADOS PARA TRABAJOS DE LABORATORIOS:*  
> *5.1.1 (Análisis), 5.2.1 (Análisis), 5.3.1, 5.3.2, 5.3.5 a 5.3.8 (Análisis), 5.4.16.1 a 5.4.16.3, 5.4.17.1, 5.4.17.2 (Análisis), 5.4.1 a 5.4.15 (Configuración), 5.5.1 a 5.5.6 (Análisis), 5.6.1 a 5.6.5 (Análisis), 5.7.1 a 5.7.9 (Configuración), 5.8.1 a 5.8.8 (Configuración), 5.9.1 a 5.9.6 (Análisis), 5.11.1 a 5.11.5 (Análisis).*

### 5.1. Arquitectura del TCP/IP.
5.1.1. Mediante diagramas de capas grafique comparativamente la arquitectura TCP/IP con respecto al modelo OSI. Haga referencia a cada RFC involucrado.  

### 5.2. Aplicaciones TCP/IP: FTP, TELNET, DNS, PING, TFTP, SNMP, SMTP, etc.
5.2.1. Modele mediante un enfoque sistémico el funcionamiento de los protocolos HTTP, FTP, TELNET, DNS, TFTP, SNMP, SMTP.  

### 5.3. El segmento TCP. El datagrama UDP.
5.3.1. Verifique en cada caso los servicios que cumplen TCP, mediante una tabla comparativa, en base a las RFC respectivas, considerando establecimiento de conexión, conexión lógica, transferencia de datos, ordenamiento y reensamble, fiabilidad, reconocimientos y retransmisiones, control de errores, control de flujo, multiplexación, conexión Full Duplex, cierre de conexión, y cierre de conexión en el Rx (subapartados 5.3.1.1 a 5.3.1.12).  
5.3.2. Idem el apartado anterior, para UDP.  
5.3.3. Modele mediante diagramas de sistemas (UML y otros) cada servicio prestado por TCP.  
5.3.4. Idem el apartado anterior, para UDP.  
5.3.5. Identifique en cada caso uno de los servicios que cumplen TCP, los datos que proporciona el encabezado del protocolo respectivo, en base a su PDU. Grafique mediante un diagrama de clases la perspectiva estática y un diagrama de objetos la perspectiva dinámica.  
5.3.6. Idem el apartado anterior, para UDP.  
5.3.7. Considerando las capturas mostradas en las imágenes, analice los campos del encabezado de capa 4 (puerto de origen, puerto de destino, número de secuencia, acuse de recibo, longitud del encabezado, banderas, tamaño de ventana, suma de comprobación).  
5.3.8. Idem anterior para capturas adicionales de TCP y DNS/UDP.  
5.3.9. Observe la imagen de un analizador de protocolos (Ethereal) y responda sobre información intercambiada en TCP (tramas 1, 2 y 3) y sobre la dirección IP `145.254.160.237` (clase, tipo pública/privada, identificación y estaciones reales para máscaras `/18` y `/10`).  

---

### 5.4. El nivel internet. Protocolos IP, funcionamiento y encaminamiento. Clases de direcciones IP.
5.4.1. Su red utiliza la dirección IP `172.30.0.0/16`. Inicialmente existen 25 subredes. Con un mínimo de 1000 hosts por subred. Se proyecta un crecimiento de un total de 55 subredes. ¿Qué máscara de subred se deberá utilizar?  
5.4.2. Usted planea la migración de 100 computadoras de red propietario a TCP/IP con conectividad a Internet. Su ISP le asignó la IP `192.168.16.0/24`. Se requieren 10 Subredes con 10 hosts cada una. ¿Qué máscara usar?  
5.4.3. Una red está dividida en 8 subredes de una clase B. ¿Que máscara de subred si se pretende tener 2500 hosts por subred?  
5.4.4. ¿Cuáles de las siguientes subredes no pertenece a la misma red si se ha utilizado la mascara `255.255.224.0`? (A. `172.16.66.24`, B. `172.16.65.33`, C. `172.16.64.42`, D. `172.16.63.51`).  
5.4.5. ¿Cuáles de los siguientes son direccionamientos válidos clase B (binarios)?  
5.4.6. Se tiene una IP `172.17.111.0` máscara `255.255.254.0`. ¿Cuántas subredes y hosts válidos por subred?  
5.4.7. Se tiene una IP `192.100.100.128` máscara `255.255.255.254`. Seleccionar la opción correcta entre a, b, c, d.  
5.4.8. Asignación de IP para cuatro subredes con la red `10.1.1.0` (crecimiento de una red por año en 4 años). Seleccionar máscara óptima.  
5.4.9. A partir de la IP `172.18.71.2/21`, ¿cuál es la dirección de subred y de broadcast?  
5.4.10. Red clase B dividida en 20 subredes (+ 30 futuras) para 800 hosts por subred. ¿Qué máscara?  
5.4.11. Red clase B dividida en 20 subredes (+ 4 futuras) para 2000 hosts por subred. ¿Qué máscara?  
5.4.12. A partir de la IP `192.168.85.129/26`, ¿cuál es la dirección de subred y de broadcast?  
5.4.13. Red clase C `192.168.1.0/30` dividida en subredes. ¿Cuántas subredes y hosts tendrá cada una?  
5.4.14. IP `156.233.42.56` con máscara de subred de 7 bits. ¿Cuántos host y subredes son posibles?  
5.4.15. Red clase B dividida en subredes para obtener 500 hosts por subred. ¿Qué máscara usar?  
5.4.16. Análisis de campos del encabezado IP (Versión, HLEN, servicio/congestión, longitud total, identificación, banderas, desplazamiento, TTL, protocolo, comprobación, IP origen, IP destino) en capturas 5.4.16.1 a 5.4.16.4.  
5.4.17. Preguntas sobre captura de analizador de tramas (longitud de cabecera valor 5 y 20 octetos; análisis de la IP destino `62.14.4.64` para máscaras `/8` y `/14`).  

---

### 5.5. ARP y RARP.
5.5.1. Suponga que una computadora C recibe una solicitud ARP de A buscando a B, y C tiene la asignación de $IP_B$ a $MAC_B$. ¿C debe contestar? Explíquelo.  
5.5.2. ¿Cómo puede utilizar ARP una estación al iniciarse para descubrir si otra máquina la está personificando? Desventajas.  
5.5.3. Explique cómo el envío de tramas hacia direcciones no existentes en una red Ethernet remota genera tráfico broadcast excesivo.  
5.5.4. ¿ARP debe actualizar la memoria intermedia si ya existe un registro antiguo para cierta IP? ¿Por qué?  
5.5.5. ¿En qué casos especiales un host conectado a una red Ethernet no necesita utilizar ARP?  
5.5.6. Compare RARP con ARP (similitudes y diferencias).  
5.5.7. ¿Cuánto más grandes serán las tramas Ethernet cuando se añade el nombre de la máquina además de la IP al RARP?  
5.5.8. Agregar un segundo servidor RARP aumenta la confiabilidad. ¿Tiene sentido agregar un tercero? ¿Por qué?  

---

### 5.6. Protocolo de control de red ICMP.
5.6.1. Analice todos los tipos de mensajes ICMP y grafique un ejemplo de aplicación para cada uno.  
5.6.2. ¿Un router debe dar mayor prioridad a los mensajes ICMP que al tráfico normal? ¿Por qué?  
5.6.3. No existe mensaje ICMP para informar origen que los errores de transmisión provocan datagramas corrompidos. Explique por qué.  
5.6.4. ¿Bajo qué circunstancias sería útil dicho mensaje?  
5.6.5. ¿Los mensajes ICMP de error deberían contener un timestamp? ¿Por qué?  
5.6.6. ¿En qué consiste la vulnerabilidad del uso de ICMP en el "ataque ICMP"?  

---

### 5.7. Enrutamiento en redes IP. Sistemas autónomos.
5.7.1. Dada la topología (Medrano - Campus con switches y hubs), ¿cómo puede conocer cada router hacia dónde conmutar paquetes a redes no directamente conectadas?  
5.7.2. ¿Qué hace un router con el valor TTL en un encabezado IP?  
5.7.3. Máquina con 2 conexiones físicas y 2 IPs ($I_1, I_2$). ¿Es posible que reciba un datagrama para $I_2$ sobre la red con dirección $I_1$? Explíquelo.  
5.7.4. ¿Es posible direccionar un datagrama a una IP de un router? ¿Tiene sentido?  
5.7.5. ¿Qué mensajes ICMP genera un router?  
5.7.6. ¿Cómo determina un router núcleo original de Internet si un vecino está "up" o "down"? (Consultar RFC 823).  
5.7.7. Si trabaja en una empresa grande con más de un sistema autónomo, explique el intercambio de enrutamiento mediante gráfico y descripción lógica.  
5.7.8. Ventaja y desventaja mayor de dividir en varios sistemas autónomos una corporación multinacional.  
5.7.9. Análisis comparativo de protocolos de enrutamiento: EGP, BGP, RIP, IGRP, EIGRP y OSPF.  

---

### 5.8. Direccionamiento IPv4 con VLSM.
5.8.1. ¿A qué subredes pertenecen: `192.168.10.104/27`, `192.168.10.144/28`, `192.168.12.242/26`, `122.122.239.12/19`?  
5.8.2. Dada la red `192.168.0.0/24`, desarrolle esquema VLSM para: Profesores (20 hosts), Estudiantes (80 hosts), Invitados (20 hosts), y 3 enlaces entre routers (2 hosts c/u).  
5.8.3. Dada la red `192.168.12.0/24`, esquema VLSM para: Marketing (60 hosts), Ventas (80 hosts), Administrativos (20 hosts), y 4 enlaces de 2 hosts.  
5.8.4. Dada la red `172.25.0.0/16`, dividir en: 2 subredes de 1000 hosts, 1 de 2000 hosts, 1 de 5 hosts, 1 de 60 hosts, 1 de 70 hosts, y 15 enlaces de 2 hosts.  
5.8.5. ¿Cuántos hosts pueden haber en las redes más pequeñas para las parejas de IPs: `199.188.133.222` y `199.188.133.202`; `166.177.188.199` y `166.177.209.127`?  
5.8.6. Red `172.16.0.0` requiere: 500 subredes de 200 hosts, 1020 subredes de 100 hosts y 20 enlaces. Indicar máscaras, primera/última red de 100 hosts, de 200 hosts y de enlaces.  
5.8.7. Instituto con red segmentada en 3 subredes (Administración 10 hosts, Departamentos 40 hosts, Alumnos 300 hosts), CPD con 6 servidores (uno con doble tarjeta de red para balanceo). Alumnos y CPD separados por Firewall. Segmentar red `192.168.0.0` basándose en el esquema proporcionado.  
5.8.8. Repetir división para `172.25.0.0/16` considerando análisis de eficiencia de capacidad potencial de red base.  

---

### 5.9. La nueva versión de IP, IPv6. Ventajas de IPv6 respecto de IPv4.
5.9.1. IPv6 no tiene suma de verificación de encabezado. Ventajas y desventajas.  
5.9.2. Análisis numérico del espacio de direcciones de IPv6 comparado con IPv4.  
5.9.3. Construya un esquema de direccionamiento IPv6 para una organización. ¿Seleccionaría asignación jerárquica? ¿Por qué?  
5.9.4. Tamaños para campos ID de proveedores, suscriptores y subredes en IPv6.  
5.9.5. Repase encabezados de autenticación y seguridad de IPv6. ¿Por qué se proponen dos encabezados?  
5.9.6. Semejanzas y diferencias entre IPv6 e IPv4 respecto a autenticación y seguridad.  

---

### 5.10. Transmisión de voz sobre IP - VoIP.
5.10.1. Realice cálculos para red VoIP con parámetros:  
   * **Caso 1:** Códec G.729 (8 Kbps), carga útil 20 bytes, protocolo MP, UDP, CRTP (cabecera 2 bytes). Calcular TTP (bits), PPS (pps), TTD (bps).  
   * **Caso 2:** Repetir Caso 1 con G.729 con 3 tramas por paquete y RTP sin compresión.  
   * **Caso 3:** Calcular Caso 2 sobre Ethernet.  
   * **Caso 4:** Calcular Caso 3 transportado con etiqueta MPLS.  
   * **Caso 5:** Calcular Caso 3 transportado en ATM modo bridge con FCS.  
5.10.2. Verificar cálculos usando calculadora VoIP específica (ej. idris.com.ar o bandcalc.com).  

---

### 5.11. El protocolo DHCP.
5.11.1. Según el estándar, ¿cómo pueden acordar cliente y servidor la duración de arrendamiento sin relojes sincronizados?  
5.11.2. ¿Cómo especifica DHCP renovación y reasignación de temporizadores? ¿Servidor debe establecer siempre uno sin el otro?  
5.11.3. ¿Puede DHCP garantizar que un cliente no es engañado? ¿Por qué?  
5.11.4. DHCP especifica preparación para manejar al menos 312 octetos de opciones. ¿Cómo se obtiene el número 312?  
5.11.5. ¿Puede una computadora que utiliza DHCP obtener una dirección IP operando un servidor? ¿Cómo accede al servidor?  

---

## 6. NOTA Y BIBLIOGRAFÍA

### 6.1 a 6.4. Consideraciones generales de la Cátedra
* Orientación de la guía para la resolución de problemas de ingeniería en exámenes parciales o finales.  
* Desarrollo de ejercicios tipo en clases teóricas y experimentales (laboratorios).  

### Bibliografía y otras fuentes
1. Douglas E. Comer, *Redes Globales de Información con Internet y TCP/IP*, PRENTICE HALL, 3ª Edición.  
2. Ford, ML - Lew H. Kim - Spanier, S. Stevenson, T., *Tecnologías de Interconectividad de Redes*, CISCO PRESS - PRENTICE HALL, 1998.  
3. L. de la Cruz et al., *Redes, sistemas y servicios de comunicación. Problemas resueltos*, EDICIONES UPC, 2002.  
4. Purificación Sáiz Agustín et al., *Redes y Servicios de Telecomunicación. Ejercicios Resueltos*, 2010.  
5. José Alberto Hernández Gutiérrez et al., *REDES DE COMUNICACIONES I - EJERCICIOS RESUELTOS*, UAM, 2011.  
6. Eduard Lara, *INTERNET - UD3 - Direccionamiento IP*, UPC, 2010.  
7. Alberto Escudero Pascual, *Resolución de problemas*, TRICALCAR, 2007.  
8. Materiales del proyecto TRICALCAR, www.wilac.net/tricalcar/.  
9. Rubén Fusario y docentes de la Cátedra Redes de Información, apuntes y ejercicios resueltos, FRBA - UTN, 2011.  
10. Cisco Systems Inc, notas técnicas.  
11. IDRIS - Laurent S.A., artículos técnicos recomendados.  
12. Stallings, William. *Foundations of Modern Networking: SDN, NFV, QoE, IoT, and Cloud*, Pearson Education, 2016.