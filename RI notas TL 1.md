```
REDES LAN Y SEGURIDAD EN SWITCHES (Capa 2 OSI / Acceso al Medio)
├── 1. Fundamentos de Capa 2 y Conmutación
│   ├── 1.1. Trama Ethernet (IEEE 802.3)
│   ├── 1.2. Dirección MAC y Protocolo ARP
│   ├── 1.3. Funcionamiento del Switch y Tabla de Direcciones MAC
│   └── 1.4. Dominios de Colisión y de Broadcast
├── 2. Segmentación de Redes y Extensión Lógica
│   ├── 2.1. VLANs (Virtual LANs) y Puertos de Acceso
│   └── 2.2. Enlaces Troncales (Trunks) y Etiquetado IEEE 802.1Q
├── 3. Redundancia Lógica y Control de Bucles
│   ├── 3.1. Spanning Tree Protocol (STP / IEEE 802.1D)
│   ├── 3.2. Roles de Puertos y Selección de Root Bridge
│   └── 3.3. Estados de Puertos y Optimizaciones (PortFast)
├── 4. Agregación de Enlaces (EtherChannel / LACP)
│   └── 4.1. Protocolo LACP (IEEE 802.3ad / 802.1ax)
└── 5. Gestión del Dispositivo y Seguridad
    ├── 5.1. Modos de Administración (Consola, Telnet y SSH)
    └── 5.2. Seguridad de Puertos (Port Security)
```

---

### 1. Fundamentos de Capa 2 y Conmutación

#### 1.1. Trama Ethernet (IEEE 802.3)

- **Definición:** Es la unidad fundamental de datos (PDU) de la Capa de Enlace de Datos (Capa 2 del modelo OSI o capa de acceso al medio en TCP/IP). Define la estructura estandarizada para encapsular paquetes IP e intercambiar información a nivel físico/enlace.
- **Estructura y Campos:**
    - **Preámbulo y Delimitador de Inicio (SFD):** 8 bytes iniciales de sincronización.
    - **MAC de Destino:** Dirección física del receptor (ubicada al principio para acelerar la conmutación en el switch).
    - **MAC de Origen:** Dirección física del emisor.
    - **Longitud / Tipo:** Si el valor decimal es mayor a 1500 indica **Tipo** (Ethernet II); si es menor o igual a 1500 representa **Longitud** (IEEE 802.3).
    - **Datos (Payload):** Entre 46 y 1500 bytes. La Unidad Máxima de Transferencia (**MTU**) es de 1500 bytes (alcanzando 1518 bytes con cabecera). El tamaño mínimo de trama es de 64 bytes para garantizar la detección de colisiones en el medio.
    - **FCS / CRC:** Secuencia de Verificación de Trama mediante Redundancia Cíclica.
- **Ejemplo:** Al enviar un paquete ICMP (`ping`), el paquete IP se encapsula con el valor Ethertype `0x0800` en el campo Tipo y se envía con una carga útil dentro del rango permitido (46 a 1500 bytes).

#### 1.2. Dirección MAC y Protocolo ARP

- **Definición de Dirección MAC:** Identificador físico unívoco de 48 bits (6 bytes) grabado en la placa de red, representado en 12 dígitos hexadecimales. Se compone de 24 bits de **OUI** (identificador del fabricante) y 24 bits asignados individualmente por la fábrica al dispositivo.
- **Definición de Protocolo ARP (Address Resolution Protocol):** Mecanismo de Capa 2/3 encargado de traducir o resolver una dirección IP de destino a su correspondiente dirección MAC dentro de la red local.
- **Ejemplo:** Cuando la `PC 101` necesita comunicarse con la IP `192.168.1.102` pero desconoce su MAC, emite una solicitud **ARP Broadcast** (`¿Quién tiene la IP 192.168.1.102?`). El destino responde mediante **ARP Unicast** (`Yo soy 192.168.1.102 y mi MAC es 0001.43AA.BBCC`). Esta relación se guarda localmente en la tabla ARP, la cual se consulta con el comando `arp -a`.

#### 1.3. Funcionamiento del Switch y Tabla de Direcciones MAC

- **Definición:** El switch es el dispositivo central de Capa 2 que conmuta, almacena y reenvía tramas procesando la dirección MAC de destino.
- **Mecanismo de Aprendizaje y Reenvío:**
    1. **Inicio:** Al encenderse, el switch tiene su tabla dinámica de direcciones MAC totalmente vacía y opera inundando las tramas de forma similar a un hub.
    2. **Aprendizaje:** Al recibir una trama por un puerto, el switch examina y registra la **MAC de origen** asociada a dicho puerto de entrada.
    3. **Inundación (Flooding):** Si la **MAC de destino** no figura en su tabla, reenvía la trama por todas las bocas excepto por la que ingresó.
    4. **Conmutación Unicast:** Una vez registrada la MAC de destino, conmuta las tramas futuras directamente hacia el puerto específico.
- **Ejemplo:** La `PC A` (MAC `...11`) en el puerto 1 envía a la `PC B` (MAC `...F3`) en el puerto 2. El switch guarda en su tabla que la MAC `...11` está en el puerto 1. Al responder la `PC B`, el switch asocia la MAC `...F3` al puerto 2 y, en adelante, conmuta el tráfico exclusivamente entre los puertos 1 y 2.

#### 1.4. Dominios de Colisión y de Broadcast

- **Dominio de Colisión:**
    - **Definición:** Área de red donde existe posibilidad de que dos o más tramas colisionen al transmitirse en simultáneo.
    - **Comportamiento:** Un **hub** concentra a todos sus puertos en un único dominio de colisión en modo Half-Duplex. Un **switch** aisla cada puerto como un **dominio de colisión independiente** en modo Full-Duplex (eliminando las colisiones si hay un solo dispositivo por puerto).
- **Dominio de Broadcast:**
    - **Definición:** Conjunto de puertos o dispositivos que reciben tramas dirigidas a la dirección de difusión general (`FF:FF:FF:FF:FF:FF`).
    - **Comportamiento:** El switch **no filtra** los mensajes de broadcast por defecto; toda trama de difusión se replica por todas sus bocas. Únicamente los **routers** o la creación de VLANs dividen los dominios de broadcast.

---

### 2. Segmentación de Redes y Extensión Lógica

#### 2.1. VLANs (Virtual LANs) y Puertos de Acceso

- **Definición de VLAN:** Red local virtual construida lógicamente sobre una infraestructura física. Funciona como "partir el switch con un hacha", separando dominios de broadcast y aislando eléctricamente el tráfico entre grupos de usuarios para mejorar la seguridad y la eficiencia de la red.
- **Definición de Puerto de Acceso:** Modo de puerto en el switch configurado para pertenecer a una sola VLAN y conectarse a un dispositivo final (PC, impresora).
- **Ejemplo de Configuración:**
    - Creación de VLAN: `vlan 10` seguido de `name logistica`.
    - Asignación de puerto: `interface fastethernet 0/1`, `switchport mode access` y `switchport access vlan 10`.
    - _Resultado:_ Una PC en la VLAN 10 (Logística) pierde conectividad a nivel de Capa 2 con una PC en la VLAN 20 (Marketing), aunque estén conectadas físicamente al mismo switch.

#### 2.2. Enlaces Troncales (Trunks) y Etiquetado IEEE 802.1Q

- **Definición de Enlace Troncal:** Enlace físico punto a punto entre switches que transporta el tráfico de múltiples VLANs concurrentes a través del mismo cable.
- **Definición de IEEE 802.1Q:** Protocolo estándar de etiquetado que modifica la trama Ethernet agregando un campo (**tag**) de 4 bytes. Incluye el identificador de protocolo (`0x8100`) y el ID de la VLAN correspondiente.
- **VLAN Nativa:** Es la VLAN asignada por defecto (usualmente VLAN 1) cuyo tráfico atraviesa el enlace troncal **sin etiquetar** (como trama Ethernet 802.3 estándar).
- **Ejemplo:**
    - Configuración del troncal: `interface giga 4/1` e ingresar `switchport mode trunk`.
    - Al enviar una trama desde la VLAN 10 (representada en hexadecimal como `A`), el switch le adosa la etiqueta 802.1Q con ID `0x000A` antes de transmitirla por el enlace troncal hacia otro switch.

---

### 3. Redundancia Lógica y Control de Bucles

#### 3.1. Spanning Tree Protocol (STP / IEEE 802.1D)

- **Definición:** Protocolo de Capa 2 diseñado para evitar bucles de red o tormentas de difusión cuando existen enlaces físicos redundantes entre switches, creando una topología lógica en forma de árbol.
- **Bridge ID (BID):** Identificador único de cada switch formado por la combinación de la **Prioridad del Bridge** (por defecto `32768`) y la **Dirección MAC** del equipo.
- **BPDUs (Bridge Protocol Data Units):** Tramas de control que intercambian los switches para anunciar sus BIDs, calcular costos de enlace y construir el árbol de expansión.

#### 3.2. Roles de Puertos y Selección de Root Bridge

- **Proceso de Elección del Root Bridge (Switch Raíz):**
    1. Al encenderse, todos los switches transmiten BPDUs declarándose el switch raíz.
    2. Tras comparar BIDs, aquel con el **BID más bajo** (menor prioridad o, en su defecto, menor dirección MAC) es seleccionado como **Root Bridge**.
- **Roles de los Puertos:**
    - **Puerto Raíz (Root Port):** Puerto del switch no-raíz que posee el menor costo acumulado para llegar al Root Bridge.
    - **Puerto Designado (Designated Port):** Puerto activo que reenvía datos. Todos los puertos activos del Root Bridge son designados.
    - **Puerto Bloqueado / No Designado (Blocked Port):** Puerto deshabilitado lógicamente para romper el bucle físico.
- **Ejemplo:** Para forzar a que el switch de distribución se elija como raíz sin depender de su dirección MAC, se ejecuta: `spanning-tree vlan 1 root primary` (o se ajusta manualmente su prioridad a un valor menor).

#### 3.3. Estados de Puertos y Optimizaciones (PortFast)

- **Estados de Transición en STP:**
    
    1. **Bloqueo (Blocking):** Recibe BPDUs pero descarta datos y no aprende MACs (evita bucles al encender el switch).
    2. **Escucha (Listening):** Procesa BPDUs para verificar rutas hacia la raíz durante 15 segundos.
    3. **Aprendizaje (Learning):** Registra direcciones MAC en su tabla sin reenviar tramas de datos durante 15 segundos.
    4. **Envío (Forwarding):** Estado operativo que envía y recibe datos normalmente.
    5. **Desactivado (Disabled):** Puerto administrativamente apagado.
    
    - _Tiempo total de convergencia:_ 30 segundos (15s escucha + 15s aprendizaje).
- **Optimización PortFast:**
    - **Definición:** Característica que permite a un puerto de acceso conectado a una estación final (PC) saltearse los estados de escucha y aprendizaje, pasando inmediatamente al estado de **Envío (Forwarding)**.
    - **Comando:** `spanning-tree portfast`.

---

### 4. Agregación de Enlaces (EtherChannel / LACP)

#### 4.1. Protocolo LACP (IEEE 802.3ad / 802.1ax)

- **Definición:** Protocolo de agregación de enlaces que permite agrupar físicamente hasta 8 enlaces individuales entre switches para que funcionen lógicamente como una única interfaz de mayor ancho de banda (Port-Channel).
- **Beneficios:**
    - Proporciona tolerancia a fallos: si un cable físico se corta, el tráfico continúa por los demás sin interrumpir la sesión.
    - Evita que el protocolo Spanning Tree bloquee enlaces paralelos redundantes, al tratarlos como un solo enlace lógico.
- **Ejemplo de Configuración:**
    
    ```
    interface range giga 0/1 - 1
    switchport mode trunk
    channel-protocol lacp
    channel-group 1 mode active
    ```
    
    Al verificar la topología con `show spanning-tree`, las interfaces individuales `g0/1` y `g1/1` dejan de figurar por separado y se muestran consolidadas bajo la interfaz lógica `Po1` (Port-Channel 1) con un costo de enlace reducido.

---

### 5. Gestión del Dispositivo y Seguridad

#### 5.1. Modos de Administración (Consola, Telnet y SSH)

- **Acceso Local por Consola:** Conexión directa mediante puerto serie/RS-232 y cable celeste (rollover) desde una PC terminal. Es el método obligatorio para realizar la primera configuración del switch cuando sale de fábrica.
- **Acceso Remoto In-Band (Telnet vs. SSH):**
    - Para permitir gestión remota, se le asigna una IP a la SVI (Switch Virtual Interface): `interface vlan 1`, `ip address 192.168.1.251 255.255.255.0` y `no shutdown`.
    - **Telnet:** Transmite credenciales y comandos en texto claro sin cifrar (inseguro).
    - **SSH (Secure Shell):** Cifra todo el tráfico mediante claves asimétricas RSA.
- **Ejemplo de Configuración SSH (Versión 2):**
    
    ```
    ip domain-name tl1.com
    crypto key generate rsa (tamaño: 1024 o 4096)
    ip ssh version 2
    username redes privilege 15 secret Cisco
    line vty 0 4
     transport input ssh
     login local
    ```
    
    Permite conectarse cifradamente desde aplicaciones como PuTTY indicando el usuario `redes` y la IP de administración `192.168.1.251`.

#### 5.2. Seguridad de Puertos (Port Security)

- **Definición:** Característica de Capa 2 que vincula de manera estática o dinámica las direcciones MAC autorizadas a un puerto del switch, denegando el acceso a cualquier dispositivo no registrado.
- **Modos de Violación (`violation`):**
    - **Shutdown:** Apaga y deshabilita la interfaz automáticamente (`err-disabled`) al detectar una MAC no autorizada.
    - **Protect / Restrict:** Descartan las tramas de la MAC no autorizada y, en el caso de _restrict_, generan registros en el log/SNMP sin apagar el puerto.
- **Ejemplo de Configuración:**
    
    ```
    interface fastethernet 0/1
    switchport mode access
    switchport port-security
    switchport port-security maximum 1
    switchport port-security mac-address 0001.43AA.BBCC
    switchport port-security violation shutdown
    ```
    
    Si alguien desconecta la PC autorizada (`0001.43AA.BBCC`) para conectar su propia computadora, el switch detecta el cambio de dirección MAC y cambia inmediatamente el estado del puerto a `shutdown`.

---

💡 ¿Te gustaría que elaboremos una guía de comandos rápidos o un diagrama de flujo para resolver problemas comunes en laboratorios de Packet Tracer?