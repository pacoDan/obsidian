## formato de celda ATM
Una **celda ATM** (_Asynchronous Transfer Mode_) es la unidad fundamental de datos (PDU) en redes ATM. A diferencia de otros protocolos que utilizan tramas de tamaño variable, ATM emplea celdas de **longitud fija de 53 bytes**.
### 1. Estructura General de la Celda ATM

La celda de 53 bytes se divide en dos componentes principales:

- **Cabecera (_Header_):** 5 bytes (40 bits). Contiene la información de control, direccionamiento del circuito virtual, prioridad y la secuencia de detección de errores de la propia cabecera.
- **Carga Útil (_Payload_ / Datos):** 48 bytes (384 bits). Transporta la información de usuario enviada desde las capas superiores de adaptación (AAL).

### 2. Variantes de Cabecera: UNI vs. NNI

Existen dos formatos para los 5 bytes de cabecera según el tipo de interfaz en el que transita la celda:

1. **UNI (_User-to-Network Interface_):** Interfaz entre el equipo del usuario y el conmutador o nodo de acceso ATM de la red.
2. **NNI (_Network-to-Network Interface_):** Interfaz de conexión exclusiva entre nodos/switches internos del proveedor. En NNI desaparece el campo GFC y sus 4 bits se reasignan para ampliar el campo VPI.
### 3. Campos de la Cabecera ATM (5 Bytes / 40 Bits)

#### Esquema gráfico de los campos:

```
Interfaz UNI (Usuario - Red):
+----------------+----------------+-----------------+---------------+---------------+---------------+
| GFC (4 bits)   | VPI (8 bits)   | VCI (16 bits)   | PT (3 bits)   | CLP (1 bit)   | HEC (8 bits)  |
+----------------+----------------+-----------------+---------------+---------------+---------------+

Interfaz NNI (Red - Red):
+---------------------------------+-----------------+---------------+---------------+---------------+
| VPI (12 bits)                   | VCI (16 bits)   | PT (3 bits)   | CLP (1 bit)   | HEC (8 bits)  |
+---------------------------------+-----------------+---------------+---------------+---------------+
```

#### Descripción de cada campo:

- **GFC (_Generic Flow Control_ / Control Genérico de Flujo - 4 bits):**
    
    - Presente únicamente en la interfaz **UNI**.
    - Se utiliza en la periferia para regular el flujo de acceso del usuario y evitar sobrecargas en la entrada de la red.
- **VPI (_Virtual Path Identifier_ / Identificador de Camino Virtual):**
    
    - **8 bits en UNI / 12 bits en NNI**.
    - Identifica el camino virtual (_Virtual Path_), el cual agrupa jerárquicamente un conjunto o haz de canales virtuales.
- **VCI (_Virtual Channel Identifier_ / Identificador de Canal Virtual):**
    
    - **16 bits (2 bytes)**.
    - Identifica la conexión o canal virtual específico (_Virtual Channel_) dentro del camino VPI. El par conjunto **VPI/VCI** funciona de manera equivalente al DLCI en Frame Relay y posee únicamente significado local.
- **PT (_Payload Type_ / Tipo de Carga Útil - 3 bits):**
    
    - **Primer bit:** Indica si la celda transporta datos de usuario (`0`) o mensajes de operación y mantenimiento (`1`, tramas OAM - _Operations and Maintenance_).
    - **Segundo bit:** Indica la presencia de congestión en la red.
    - **Tercer bit:** Indica el tipo de unidad de datos SDU (_Service Data Unit_) en los procesos de adaptación.
- **CLP (_Cell Loss Priority_ / Prioridad de Pérdida de Celda - 1 bit):**
    
    - Determina la prioridad de descarte de la celda (equivalente al bit DE de Frame Relay).
    - `CLP = 0`: Alta prioridad (tráfico garantizado).
    - `CLP = 1`: Celda descartable en caso de que los conmutadores de la red sufran congestión.
- **HEC (_Header Error Control_ / Control de Errores de Cabecera - 8 bits / 1 byte):**
    
    - Código CRC calculado exclusivamente sobre los 4 bytes restantes de la cabecera (no chequea el cuerpo de datos).
    - Permite detectar múltiples errores y corregir automáticamente **1 bit erróneo** en la cabecera. La capa física utiliza también este campo para realizar la delimitación de inicio y fin de celdas en el flujo de bits.

## explicar la red ATM
La red **ATM** (_Asynchronous Transfer Mode_ / Modo de Transferencia Asíncrono) es una tecnología de conmutación y transmisión de datos de la **Capa de Enlace de Datos (Capa 2)** orientada a la conexión. Fue diseñada para transportar flujos integrados de voz, video y datos con altas velocidades y garantías estrictas de calidad de servicio.
### 1. La Celda ATM (PDU)

A diferencia de los protocolos que utilizan tramas de tamaño variable, la unidad fundamental de datos en ATM se denomina **celda** y tiene una **longitud fija de 53 bytes**:

- **Cabecera (_Header_):** 5 bytes destinados al control, direccionamiento y detección de errores.
- **Carga Útil (_Payload_ / Datos):** 48 bytes para transportar la información del usuario.

El uso de unidades fijas de 53 bytes permite que el procesamiento en los conmutadores se realice por hardware de forma constante, garantizando un **retardo fijo y pequeño (baja latencia)**.

### 2. Estructura de la Cabecera y Campos Clave

La cabecera de 5 bytes varía según el tipo de interfaz:

- **UNI (_User-to-Network Interface_):** Interfaz entre el equipo del usuario y el nodo de acceso a la red. Incluye el campo **GFC (_Generic Flow Control_)** de 4 bits para regular el flujo en la periferia.
- **NNI (_Network-to-Network Interface_):** Interfaz exclusiva entre conmutadores internos del proveedor. No utiliza GFC y reasigna esos 4 bits para ampliar el direccionamiento.

Los campos de la cabecera son:

- **VPI / VCI (_Virtual Path Identifier / Virtual Channel Identifier_):** Identificadores lógicos jerárquicos con significado puramente local que equivalen funcionalmente al DLCI de Frame Relay. Los **canales virtuales (VC)** viajan agrupados jerárquicamente dentro de **caminos virtuales (VP)**.
- **PT (_Payload Type_ - 3 bits):** Indica si la celda lleva datos de usuario o celdas de operación y mantenimiento (**OAM**), además de señalar presencia de congestión.
- **CLP (_Cell Loss Priority_ - 1 bit):** Determina la prioridad de descarte (equivalente al bit DE en Frame Relay). Si `CLP = 0`, la celda es de alta prioridad; si `CLP = 1`, la celda es descartable si la red se satura.
- **HEC (_Header Error Control_ - 8 bits / 1 byte):** Código CRC calculado sobre los otros 4 bytes de la cabecera. Permite detectar errores, corregir automáticamente **1 bit erróneo** en la cabecera y sirve a la capa física para realizar la **delimitación de celdas**.
### 3. Conmutación y Tipos de Nodos

ATM utiliza señalización para negociar y establecer circuitos virtuales antes de transmitir datos. En la red existen dos tipos principales de conmutadores:

- **VP Switch (_Virtual Path Switch_):** Conmuta caminos virtuales completos modificando únicamente el valor del VPI y manteniendo constante el VCI.
- **VC Switch (_Virtual Channel Switch_):** Conmuta canales virtuales cambiando tanto el VPI como el VCI en función de sus tablas lógicas.

### 4. Capa de Adaptación ATM (AAL)

Dado que un paquete IP o una trama de datos no cabe directamente en los 48 bytes de datos de una celda, ATM incorpora la subcapa **AAL (_ATM Adaptation Layer_)**:

1. **Subcapa de Convergencia:** Recibe el bloque de datos de la capa superior y le añade información de control según el tipo de tráfico (por ejemplo, marcas de tiempo o comprobación CRC).
2. **Subcapa SAR (_Segmentation and Reassembly_):** Segmenta las PDUs en bloques de 48 bytes para enviarlas a la capa ATM y las reensambla en el receptor.

Existen diferentes tipos de AAL según la clase de servicio:

- **AAL1 (Clase A):** Tasa de bit constante (CBR), orientada a la conexión y con sincronización (ej. voz y video sin comprimir / isócronos).
- **AAL2 (Clase B):** Tasa de bit variable (VBR), orientada a la conexión y con sincronización (ej. voz y video comprimidos).
- **AAL3/4 y AAL5 (Clases C y D):** Orientadas al transporte de datos (tasa variable, sin sincronización de reloj).


### 5. Calidad de Servicio (QoS) y Control de Tráfico

Al solicitar una conexión, el usuario especifica una **categoría de servicio** (como CBR, VBR, ABR o UBR), **descriptores de tráfico** (como PCR - tasa pico, SCR - tasa sostenida, MBS - tamaño de ráfaga) y **parámetros de QoS** (variación de retardo, retardo máximo y tasa de pérdida de celdas):

- **CAC (_Call Admission Control_):** El nodo evalúa si la red dispone de recursos suficientes para cumplir los requisitos solicitados antes de aceptar la conexión.
- **UPC (_User Parameter Control_):** Una vez establecida la conexión, la red ejecuta una función de policía que verifica que el tráfico no supere los límites acordados. Si el usuario excede las tasas contratadas, las celdas en exceso son marcadas con `CLP = 1` para ser descartadas prioritariamente en caso de congestión.

### 6. Evolución e Implementación

Aunque ATM fue diseñado originalmente para operar extremo a extremo (tanto en redes LAN como WAN), en las redes de área local no prosperó debido a su elevada complejidad y costo frente al rápido avance de **Ethernet**. Su uso quedó circunscrito principalmente al **núcleo (_core_ / _backbone_)** de las redes de los proveedores de telecomunicaciones.

## dar las características principales de ATM
Las características principales de **ATM** (_Asynchronous Transfer Mode_) según las fuentes de la asignatura son:

1. **Unidad de Datos de Tamaño Fijo (Celda de 53 bytes):**
    
    - ATM no utiliza tramas de longitud variable, sino **celdas fijas de 53 bytes**, compuestas por **5 bytes de cabecera** (_header_) y **48 bytes de carga útil** (_payload_).
    - Al ser de longitud fija, el tiempo de procesamiento en los conmutadores se realiza por hardware de forma constante, garantizando un **retardo bajo y fijo (baja latencia)**.
2. **Protocolo Orientado a la Conexión:**
    
    - Antes de transferir información de usuario, se requiere una fase de señalización para negociar y establecer previamente un circuito virtual de extremo a extremo.
3. **Identificación Jerárquica de Circuitos Virtuales (Par VPI / VCI):**
    
    - El direccionamiento lógico (equivalente al DLCI de Frame Relay) se realiza mediante una estructura compuesta e interactiva: el **VPI** (_Virtual Path Identifier_) y el **VCI** (_Virtual Channel Identifier_).
    - Los **canales virtuales (VC)** viajan jerárquicamente agrupados dentro de **caminos virtuales (VP)**. Esto permite la existencia de dos tipos de nodos conmutadores: **VP Switches** (conmutan caminos completos modificando solo el VPI) y **VC Switches** (conmutan modificando tanto el VPI como el VCI).
4. **Formatos de Cabecera Diferenciados (UNI vs. NNI):**
    
    - **UNI (_User-to-Network Interface_):** Interfaz entre el equipo del usuario y el conmutador de la red. Incluye el campo **GFC** (_Generic Flow Control_) de 4 bits para controlar el flujo en el acceso periférico.
    - **NNI (_Network-to-Network Interface_):** Interfaz exclusiva entre switches internos de la red. No requiere GFC, por lo que reasigna esos 4 bits para ampliar la capacidad de direccionamiento del campo VPI.
5. **Campos de Control de la Cabecera:**
    
    - **PT (_Payload Type_, 3 bits):** Distingue si la celda transporta datos de usuario o información de operación y mantenimiento (**OAM**), además de señalar la presencia de congestión.
    - **CLP (_Cell Loss Priority_, 1 bit):** Determina la prioridad de descarte (equivalente al bit DE en Frame Relay); un valor `CLP = 1` indica que la celda es descartable en caso de saturación en la red.
    - **HEC (_Header Error Control_, 1 byte / 8 bits):** Código CRC calculado sobre los 4 bytes restantes de la cabecera que permite detectar errores y corregir **1 bit erróneo**. Asimismo, la capa física utiliza el HEC para la **delimitación de celdas** (_framing_).
6. **Soporte Nativo de Calidad de Servicio (QoS):**
    
    - Permite definir y garantizar parámetros estrictos de calidad de servicio como el retardo máximo, la variación del retardo (_jitter_) y la tasa de pérdida de celdas.
    - Ofrece distintas **categorías de servicio**: **CBR** (tasa constante), **VBR** (tasa variable para tiempo real y no tiempo real), **ABR** (tasa disponible) y **UBR** (tasa no especificada / _best effort_).
7. **Capa de Adaptación ATM (AAL - _ATM Adaptation Layer_):**
    
    - Adapta las PDU de las capas superiores (como datagramas IP o bloques de voz) dividiéndolas en la subcapa **SAR** (_Segmentation and Reassembly_) en bloques de 48 bytes para encajarlas en las celdas.
    - Incluye variantes según el tráfico: **AAL1** (voz/video no comprimido / CBR), **AAL2** (voz/video comprimido / VBR), **AAL3/4** y **AAL5** (datos IP).
8. **Mecanismos de Control de Tráfico (CAC y UPC):**
    
    - **CAC (_Call Admission Control_):** Al solicitar la conexión, el nodo verifica si hay recursos disponibles para garantizar la QoS requerida antes de aceptar la solicitud.
    - **UPC (_User Parameter Control_):** Una vez activa la conexión, la red ejecuta una función de policía que vigila que el usuario no supere los descriptores de tráfico contratados (como la tasa pico PCR o la tasa sostenida SCR); las celdas excedentes se marcan con `CLP = 1`.

## Explicar la arquitectura de ATM
La arquitectura de **ATM** (_Asynchronous Transfer Mode_) es una tecnología de conmutación de Capa 2 orientada a la conexión, diseñada para integrar el transporte de voz, video y datos a altas velocidades con garantías estrictas de calidad de servicio.

A continuación, se detallan los pilares fundamentales que componen su arquitectura:

### 1. La Celda ATM y la Estructura de Cabecera

A diferencia de los protocolos de trama de longitud variable, la unidad básica de transmisión en ATM es la **celda de tamaño fijo de 53 bytes**:

- **Carga útil (_Payload_):** 48 bytes destinados a la información del usuario.
- **Cabecera (_Header_):** 5 bytes destinados al control, direccionamiento local y chequeo de errores de la cabecera.

El procesamiento en los conmutadores se realiza por hardware a ritmo constante, lo que garantiza un **retardo pequeño y fijo (baja latencia)**.

Existen dos formatos de cabecera según la ubicación en la red:

- **UNI (_User-to-Network Interface_):** Interfaz entre el equipo del usuario y el conmutador de acceso. Incluye un campo **GFC (_Generic Flow Control_)** de 4 bits para regular el tráfico en la periferia de la red.
- **NNI (_Network-to-Network Interface_):** Interfaz entre nodos/switches internos del proveedor. Prescinde del campo GFC y utiliza esos 4 bits para ampliar el campo de direccionamiento **VPI**.

Los campos principales de la cabecera incluyen:

- **PT (_Payload Type_, 3 bits):** Distingue si la celda transporta datos de usuario o celdas administrativas de operación y mantenimiento (**OAM**), e indica además si hay congestión en la red.
- **CLP (_Cell Loss Priority_, 1 bit):** Determina la prioridad de descarte (equivalente al bit DE de Frame Relay); un valor `CLP = 1` indica que la celda es descartable en caso de saturación.
- **HEC (_Header Error Control_, 1 byte):** Código CRC calculado sobre los otros 4 bytes de la cabecera. Permite detectar errores, corregir **1 bit erróneo** en la cabecera y es utilizado por la capa física para la **delimitación de celdas** (_cell framing_).

### 2. Direccionamiento Jerárquico (VPI / VCI) y Conmutación

ATM es un protocolo **orientado a la conexión** que utiliza direccionamiento lógico de alcance local mediante un par jerárquico:

- **VPI (_Virtual Path Identifier_):** Identifica el camino virtual.
- **VCI (_Virtual Channel Identifier_):** Identifica el canal virtual específico dentro de ese camino.

Los **canales virtuales (VC)** viajan agrupados jerárquicamente dentro de **caminos virtuales (VP)**. Esto permite disponer de dos tipos de nodos de conmutación:

- **VP Switch:** Conmuta caminos virtuales completos modificando únicamente el valor del VPI y manteniendo invariable el VCI (permitiendo mover haces completos de conexiones).
- **VC Switch:** Conmuta canales alterando tanto el VPI como el VCI según sus tablas lógicas.

### 3. Modelo de Referencia de Capas en ATM

La pila de protocolos de ATM se organiza en las siguientes subcapas:

1. **Capa Física:** Funciona sobre redes ópticas de alta velocidad (como la jerarquía digital sincrónica SDH / SONET). Realiza el monitoreo de errores, la inserción de celdas vacías para mantener el sincronismo y la delimitación de celdas mediante la verificación continua del campo **HEC**.
2. **Capa ATM:** Ejecuta las funciones de conmutación, multiplexación de celdas y gestión de cabeceras.
3. **Capa de Adaptación ATM (AAL - _ATM Adaptation Layer_):** Adapta las PDU de las capas superiores dividiéndolas para encajarlas en los 48 bytes de datos de las celdas. Se estructura en dos subcapas:
    - **CS (_Convergence Sublayer_):** Agrega marcas de tiempo (_timestamps_) o secuencias de comprobación según los requerimientos del tráfico.
    - **SAR (_Segmentation and Reassembly_):** Segmenta el bloque de datos de la subcapa CS en fragmentos de 48 bytes en el emisor y los reensambla en el receptor.

**Variantes de AAL según la clase de tráfico:**

- **AAL1 (Clase A):** Tasa constante (CBR), orientada a conexión y con sincronización de reloj (ej. voz y video sin comprimir / isócrono).
- **AAL2 (Clase B):** Tasa variable (VBR), orientada a conexión y con sincronización (ej. voz y video comprimidos).
- **AAL3/4 y AAL5 (Clases C y D):** Tráfico de datos orientado o no orientado a la conexión sin sincronización de reloj entre origen y destino.

### 4. Calidad de Servicio (QoS) y Control de Tráfico

Al solicitar el establecimiento de un circuito virtual, la red aplica mecanismos estricto de control:

- **Categorías de Servicio:** El usuario elige entre **CBR** (tasa constante), **rt-VBR / nrt-VBR** (tasa variable de tiempo real / no tiempo real), **ABR** (tasa disponible) o **UBR** (_best effort_).
- **Descriptores de Tráfico:** Se especifican parámetros como la tasa pico (**PCR**), tasa sostenida (**SCR**), tamaño máximo de ráfaga (**MBS**) y tasa mínima (**MCR**).
- **Parámetros de QoS:** Se acuerdan el retardo máximo, la variación en el retardo de celdas (**CDV / jitter**) y la tasa de pérdida de celdas (**CLR**).
- **CAC (_Call Admission Control_):** Antes de aceptar la conexión, la red verifica si dispone de recursos suficientes para garantizar la calidad de servicio solicitada.
- **UPC (_User Parameter Control_):** Función de policía en el nodo de ingreso que vigila que el flujo transmitido respete las tasas negociadas; si el usuario excede las tasas, las celdas en exceso son marcadas con `CLP = 1`.

### 5. Ámbito de Despliegue

Aunque fue diseñado inicialmente para operar de extremo a extremo (tanto en redes LAN como WAN), su elevada complejidad y costo frente al desarrollo de **Ethernet** hicieron que no prosperara en redes de área local. Por ello, el uso de ATM quedó acotado al **núcleo (_core_ / _backbone_)** de las redes de transporte de los proveedores de servicios.


## dar el formato de la celda ATM versus el formato de la cabecera
La estructura de **ATM** (_Asynchronous Transfer Mode_) se divide claramente entre la **celda completa** (unidad de datos de tamaño fijo) y la **cabecera de control**.

---

### 1. Formato General de la Celda ATM (53 Bytes)

La celda ATM tiene una longitud constante de **53 bytes** (u octetos), dividida en dos partes principales:

```
+----------------------------+----------------------------------------+
|   Cabecera / Header (5 B)  |   Carga Útil / Payload / Datos (48 B)  |
+----------------------------+----------------------------------------+
```

- **Cabecera (_Header_):** Ocupa **5 bytes** (40 bits) y contiene la información necesaria para el direccionamiento, control de tráfico y verificación de errores del encabezado.
- **Carga útil (_Payload_):** Ocupa **48 bytes** (384 bits) para transportar los datos del usuario procedentes de las capas superiores.

---

### 2. Formato de la Cabecera ATM (UNI vs. NNI)

La cabecera de 5 bytes tiene dos formatos diferenciados según el tipo de interfaz en el que circula la celda:

- **UNI (_User-to-Network Interface_):** Interfaz entre el equipo del usuario y el conmutador de la red.
- **NNI (_Network-to-Network Interface_):** Interfaz exclusiva entre los conmutadores internos de la red.

#### Estructura campo por campo (40 bits / 5 Bytes):

|Campo|Interfaz UNI (Usuario-Red)|Interfaz NNI (Red-Red)|Descripción y Función|
|:--|:--|:--|:--|
|**GFC** (_Generic Flow Control_)|**4 bits**|_No existe_|Control genérico de flujo en el acceso del usuario para regular el tráfico entrante.|
|**VPI** (_Virtual Path Identifier_)|**8 bits**|**12 bits**|Identificador de camino virtual (en NNI se amplía utilizando los 4 bits del GFC).|
|**VCI** (_Virtual Channel Identifier_)|**16 bits**|**16 bits**|Identificador de canal virtual dentro del camino VPI.|
|**PT** (_Payload Type_)|**3 bits**|**3 bits**|Tipo de carga útil (distingue datos de usuario de tramas OAM e indica congestión).|
|**CLP** (_Cell Loss Priority_)|**1 bit**|**1 bit**|Prioridad de pérdida de celda (`0` = alta prioridad, `1` = celda descartable en congestión).|
|**HEC** (_Header Error Control_)|**8 bits** (1 B)|**8 bits** (1 B)|Código CRC de comprobación de errores calculado sobre los otros 4 bytes de la cabecera.|

---

### 3. Descripción de los Campos de la Cabecera

1. **GFC (4 bits - Solo en UNI):** Realiza el control de flujo en la periferia de la red para evitar que el usuario sobrepase los límites acordados.
2. **VPI / VCI (24 bits totales):** Forman el par de identificadores lógicos de circuito virtual con significado puramente local que permite conmutar celdas en la red.
3. **PT (3 bits):** El primer bit indica si la celda es de datos de usuario (`0`) o de operación y mantenimiento OAM (`1`); el segundo bit notifica la presencia de congestión.
4. **CLP (1 bit):** Determina qué celdas pueden ser descartadas primero si un conmutador se satura (equivalente al bit DE en Frame Relay).
5. **HEC (8 bits / 1 byte):** Ofrece un control de errores mediante un polinomio CRC sobre los 4 bytes de cabecera. Permite detectar errores y **corregir hasta 1 bit erróneo** en el encabezado, además de ayudar a la capa física en la **delimitación de celdas**.

## en ATM, explicar UNI vs NNI
En la arquitectura de redes **ATM**, la distinción entre **UNI** y **NNI** define el límite entre el acceso del usuario y el núcleo (_core_) de la red, lo que se traduce en una variación en la estructura de la cabecera de la celda:

### 1. Ubicación y Función de las Interfaces

- **UNI (_User-to-Network Interface_ / Interfaz Usuario-Red):** Es el punto de conexión entre el equipo o terminal del usuario final y el nodo/conmutador de acceso a la red ATM.
- **NNI (_Network-to-Network Interface_ / Interfaz Red-Red):** Es la interfaz de conexión exclusiva entre los conmutadores (_switches_) internos de la red del proveedor.

### 2. Diferencias en la Cabecera de la Celda (5 Bytes)

Aunque la celda ATM mantiene siempre una longitud constante de **53 bytes** (5 bytes de cabecera y 48 bytes de carga útil), los 40 bits de la cabecera se distribuyen de manera distinta según la interfaz:

- **Campo GFC (_Generic Flow Control_ / Control Genérico de Flujo):**
    
    - **UNI:** Incluye un campo **GFC de 4 bits**. Se utiliza para regular el tráfico en el acceso del usuario y verificar que no sobrepase los parámetros contratados en la periferia.
    - **NNI:** **Prescinde del campo GFC**. Como la red valida el tráfico en el ingreso, los conmutadores internos no requieren volver a ejecutar el control de flujo en el núcleo.
- **Tamaño del campo VPI (_Virtual Path Identifier_ / Identificador de Camino Virtual):**
    
    - **UNI:** Ocupa **8 bits**.
    - **NNI:** Los 4 bits liberados al eliminar el campo GFC se reasignan para ampliar el VPI, alcanzando **12 bits**. Esto permite a los conmutadores internos gestionar una cantidad mucho mayor de caminos virtuales dentro del _backbone_ de la red.
- **Campos Idénticos en ambas interfaces:**
    
    - **VCI (_Virtual Channel Identifier_):** Mantiene **16 bits** tanto en UNI como en NNI.
    - **PT (_Payload Type_ - 3 bits), CLP (_Cell Loss Priority_ - 1 bit) y HEC (_Header Error Control_ - 1 byte):** Conservan exactamente la misma función y tamaño en ambos formatos.

## explicar VPI, VCI en ATM
En **ATM** (_Asynchronous Transfer Mode_), el par **VPI** (_Virtual Path Identifier_ / Identificador de Camino Virtual) y **VCI** (_Virtual Channel Identifier_ / Identificador de Canal Virtual) constituye la estructura de direccionamiento lógico que se incluye dentro de la cabecera de la celda.

Conceptualmente, el par VPI/VCI cumple una función equivalente al **DLCI** en Frame Relay, permitiendo diferenciar múltiples circuitos lógicos que comparten un mismo acceso físico.

### Principales aspectos de VPI y VCI

- **Estructura Jerárquica (Caminos y Canales):**
    
    - A diferencia del DLCI (que es un identificador plano de un solo nivel), el par VPI/VCI establece una **organización jerárquica**.
    - Los **canales virtuales** (_Virtual Channels_ - VC), identificados individualmente por el **VCI**, viajan agrupados jerárquicamente dentro de **caminos virtuales** (_Virtual Paths_ - VP), identificados por el **VPI**. Es decir, un VPI agrupa un haz o conjunto de VCIs.
- **Significado Local:**
    
    - El par VPI/VCI posee **significado estrictamente local** entre dos nodos o switches contiguos. A medida que una celda atraviesa la red, los valores de VPI y VCI van cambiando mediante tablas de conmutación que concatenan las distintas combinaciones de entrada y salida.
- **Conmutación en la Red (VP Switch vs. VC Switch):** La existencia de esta jerarquía permite disponer de dos tipos de nodos conmutadores en la red:
    
    1. **VP Switch (_Virtual Path Switch_):** Conmuta caminos virtuales completos. Modifica únicamente el valor del **VPI** y mantiene **invariable el VCI**. Esto permite al proveedor de red reenrutar o gestionar un haz completo de conexiones simultáneamente (por ejemplo, ante la pérdida de un nodo) con gran simplicidad administrativa.
    2. **VC Switch (_Virtual Channel Switch_):** Conmuta canales virtuales individuales. Al recibir la celda, altera tanto el **VPI** como el **VCI** según sus tablas internas de conmutación de canales.
- **Distribución de Bits según la Interfaz:**
    
    - **UNI (_User-to-Network Interface_ - Interfaz Usuario-Red):** El VPI utiliza **8 bits** y el VCI utiliza **16 bits**.
    - **NNI (_Network-to-Network Interface_ - Interfaz Red-Red):** Como en el núcleo de la red no se utiliza el campo de control de flujo genérico (GFC de 4 bits), esos 4 bits se reasignan para ampliar el VPI a **12 bits**, mientras que el VCI mantiene sus **16 bits**.

## para que sirve la cirtual channel connection
Una **Virtual Channel Connection (VCC)** o **Conexión de Canal Virtual** en ATM es el circuito lógico básico de extremo a extremo que se establece para transportar celdas de información entre dos puntos de la red.

### Funciones Principales de una VCC

- **Transporte de tráfico según el tipo de comunicación:**
    
    - **Usuario - Usuario:** Se establece entre dos extremos terminales para transmitir directamente datos, voz o video entre los usuarios.
    - **Usuario - Red:** Se utiliza para la comunicación entre el usuario y el nodo de acceso, principalmente para intercambiar mensajería de señalización (solicitudes de conexión) o agregar tráfico.
    - **Red - Red:** Se utiliza internamente entre los conmutadores del proveedor para tareas administrativas, intercambio de información de ruteo o control del estado de la red.
- **Integración dentro de la jerarquía ATM:**
    
    - Cada VCC se identifica localmente mediante un número **VCI** (_Virtual Channel Identifier_).
    - Múltiples VCCs viajan agrupadas de forma jerárquica dentro de un **camino virtual** (_Virtual Path_), el cual se identifica mediante el parámetro **VPI**.
- **Negociación y Garantía de Calidad de Servicio (QoS):**
    
    - Al solicitar el establecimiento de una VCC, el usuario debe indicar a la red la **categoría de servicio** (CBR, VBR, ABR o UBR), los **descriptores de tráfico** (como la tasa pico PCR o la tasa sostenida SCR) y los **parámetros de QoS** requeridos (retardo máximo, variación del retardo o tolerancia a la pérdida de celdas).
    - La red ejecuta la función **CAC** (_Call Admission Control_) para verificar si existen recursos libres suficientes en la ruta para garantizar la calidad exigida antes de aceptar y abrir la VCC.
    - Una vez activa la VCC, el nodo de ingreso ejecuta la función de policía **UPC** (_User Parameter Control_) para supervisar que el flujo transmitido por la conexión respete las tasas acordadas.

## explicar el diagrama de estados en atm 
En la arquitectura de **ATM** (_Asynchronous Transfer Mode_), existen dos diagramas de estados fundamentales que gestionan el procesamiento de celdas a nivel físico y de enlace:

1. **Diagrama de estados de control y corrección de errores de cabecera (HEC)**.
2. **Diagrama de estados de delimitación y sincronización de celdas en la capa física**.
### 1. Diagrama de Estados de Corrección y Detección de Errores de Cabecera (HEC)

Este mecanismo opera utilizando el octeto **HEC** (_Header Error Control_) de 8 bits para verificar la integridad de los 4 bytes de cabecera de cada celda de 53 bytes. Permite conmutar entre dos modos:

- **Modo de Corrección (_Correction Mode_):**
    - **Estado inicial:** El receptor inicia habitualmente en este modo.
    - **Comportamiento:** Mientras las celdas recibidas tengan una cabecera correcta (CRC del HEC válido), permanece en este modo.
    - **Transición por error único:** Si detecta una celda con un **único bit erróneo** en la cabecera, el sistema **corrige automáticamente el bit** y conmuta de inmediato al **Modo de Detección**.
- **Modo de Detección (_Detection Mode_):**
    - **Comportamiento:** Permanece en este modo para prevenir que errores severos o continuos dañen la transmisión.
    - **Si llega otra celda con error:** Si en la celda siguiente o subsiguiente se detecta un nuevo error en la cabecera, la celda es **descartada directamente** sin intentar corregirla.
    - **Retorno al Modo de Corrección:** Una vez que se procesa una ráfaga continua de celdas con cabeceras correctas, el receptor interpreta que el error fue un evento aislado al azar y regresa al **Modo de Corrección**.

> **Razón de diseño:** Como ATM transporta celdas muy pequeñas sobre redes ópticas de muy baja tasa de error, una tasa de más de 1 bit erróneo por cabecera de 4 bytes se considera inaceptable o síntoma de pérdida de sincronismo.

### 2. Diagrama de Estados de Delimitación y Sincronización de Celdas (_Cell Delineation_)

Dado que ATM no utiliza marcas de inicio o fin de trama (_flags_) entre celdas consecutivas, la capa física utiliza el cálculo iterativo del campo **HEC** para determinar dónde empieza y termina cada celda de 53 bytes. Este proceso recorre tres estados:

```
  +------------------+
  | CAPTURA / HUNTING| <------------------------------------+
  +------------------+                                      |
            | (HEC correcto)                                |
            v                                               |
  +------------------+                                      |
  |  PRESINCRONISMO  | --(HEC incorrecto)--> Captura        |
  +------------------+                                      |
            | (X celdas correctas consecutivas)             |
            v                                               |
  +------------------+                                      |
  |   SINCRONISMO    | --(Alpha celdas erróneas seguidas)---+
  +------------------+
```

1. **Estado de Captura (_Hunting State_):**
    
    - El receptor recibe un flujo continuo de bits sin estructura definida.
    - Toma bloques de 53 bytes y calcula el HEC. Si el cálculo falla, avanza **bit a bit** en el flujo de datos y vuelve a calcular.
    - Tan pronto como un cálculo de HEC resulta correcto, asume que ha encontrado el inicio de una cabecera y pasa al estado de **Presincronismo**.
2. **Estado de Presincronismo (_Presync State_):**
    
    - El receptor se desplaza exactamente **53 bytes** (384 bits) desde la posición hallada y vuelve a calcular el HEC de la siguiente celda.
    - Si el HEC da **incorrecto**, se considera que la coincidencia anterior fue por casualidad y regresa al estado de **Captura** (_Hunting_) para seguir probando bit a bit.
    - Si el HEC da **correcto**, el proceso se repite. Tras verificar una cantidad \(X\) de celdas consecutivas con HEC válido, confirma la estructura de trama y pasa al estado de **Sincronismo**.
3. **Estado de Sincronismo (_Sync State_):**
    
    - Es el estado operativo normal de la red. El receptor procesa las celdas de 53 bytes de manera sincrónica a ritmo constante.
    - En este estado se aplican las reglas de comprobación del diagrama de HEC (modo detección/corrección).
    - Si se reciben \(\alpha\) celdas consecutivas con HEC incorrecto, el sistema concluye que no se trata de errores aislados, sino de la **pérdida total del encuadre o sincronismo** de la línea, regresando al estado de **Captura** (_Hunting_) para enganchar nuevamente la alineación de celdas.

## en atm, explicar la funcion de la capa física
En la arquitectura de protocolos de **ATM**, la **Capa Física** se ubica en la base del modelo y está diseñada para operar sobre medios de transmisión de alta velocidad y muy baja tasa de error, habitualmente sobre redes ópticas sincrónicas como **SDH / SONET**.

### Funciones Principales de la Capa Física

#### 1. Delimitación de Celdas (_Cell Delineation_)

Dado que ATM no utiliza marcas o banderas (_flags_) de inicio y fin para separar sus celdas de 53 bytes, la capa física es la encargada de determinar de forma dinámica dónde empieza y termina cada celda dentro del flujo continuo de bits recibidos. Para lograr el encuadre, la capa física ejecuta un algoritmo basado en el cálculo del campo **HEC** (_Header Error Control_) que recorre tres estados:

- **Estado de Captura (_Hunting_):** El receptor analiza el flujo de bits recibidos comprobando la validez del HEC de a un bit a la vez hasta encontrar un cálculo correcto.
- **Estado de Presincronismo (_Presync_):** Una vez hallado un HEC válido, se desplaza exactamente 53 bytes para volver a calcular el HEC de la siguiente celda; si se confirma de forma consecutiva en un número determinado de celdas, se establece el encuadre.
- **Estado de Sincronismo (_Sync_):** Es el estado operativo sincrónico normal. Si posteriormente se detectan múltiples celdas seguidas con HEC incorrecto, el receptor asume que se perdió la alineación de trama y regresa al estado de captura.

#### 2. Monitoreo y Control de Errores de Cabecera

La capa física verifica la integridad de los 5 bytes de la cabecera mediante el cálculo del código CRC de 8 bits contenido en el campo **HEC** sobre los 4 bytes anteriores. Esto le permite corregir automáticamente **1 bit erróneo** en la cabecera (en modo corrección) o descartar la celda sin procesarla si se detectan errores persistentes en celdas consecutivas (en modo detección).

#### 3. Inserción de Celdas Vacías (_Idle Cell Insertion_)

Dado que la capa física física sincrónica (como SDH) requiere mantener una transmisión constante de bits, la capa física de ATM **inserta celdas vacías (_idle cells_)** cuando las capas superiores no tienen tráfico de usuario para enviar. Esto garantiza mantener la cadencia del enlace y la sincronización entre el emisor y el receptor.

#### 4. Adaptación y Encuadre sobre el Medio de Transporte (_Framing_)

Se encarga de empaquetar y adaptar el flujo de celdas ATM para transportarlo sobre la infraestructura física o jerarquía digital subyacente (por ejemplo, dentro de los contenedores de tramas SDH a velocidades como 155 Mbps - STM-1, 622 Mbps - STM-4, o superiores).

## en atm explicar que es el HEC y para que se calcula
El **HEC** (_Header Error Control_ o Control de Errores de Cabecera) es el campo de control que ocupa el **último octeto (1 byte / 8 bits)** dentro de la cabecera de 5 bytes de una celda ATM.

Se calcula aplicando un algoritmo de redundancia cíclica (CRC de 8 bits) exclusivamente sobre los primeros 4 bytes de la cabecera de la celda (no chequea la carga útil de datos).
### ¿Para qué se calcula el HEC?

El HEC cumple **dos funciones fundamentales** en la red ATM:

#### 1. Control y Corrección de Errores en la Cabecera

- **Protección del direccionamiento:** Dado que la cabecera contiene la información de enrutamiento local (VPI/VCI), un error no detectado en la cabecera provocaría que la celda se entregara a un circuito virtual equivocado.
- **Corrección de errores:** Permite detectar errores y **corregir automáticamente 1 bit erróneo** en los 4 bytes de cabecera.
- **Diagrama de estados de error:** Opera en dos modos para evitar procesar celdas con fallas graves:
    - **Modo de Corrección:** Si detecta una celda con un único bit erróneo en la cabecera, lo corrige de inmediato y conmuta al modo de detección.
    - **Modo de Detección:** Si en este modo se recibe otra celda con la cabecera errónea, la celda se **descarta directamente** sin intentar corregirla. Al recibir una serie de celdas consecutivas correctas, retorna al modo de corrección.

#### 2. Delimitación y Sincronización de Celdas (_Cell Delineation_)

A diferencia de otros protocolos de capa de enlace, ATM no utiliza banderas (_flags_) ni delimitadores de inicio y fin para separar sus celdas de 53 bytes. La Capa Física utiliza el cálculo continuo del HEC para identificar la estructura y los límites de las celdas mediante un proceso de tres estados:

1. **Estado de Captura (_Hunting_):** El receptor toma bloques del flujo continuo de bits y calcula el HEC moviéndose **bit a bit** hasta obtener un cálculo correcto.
2. **Estado de Presincronismo (_Presync_):** Una vez hallado un HEC válido, se desplaza exactamente **53 bytes** y vuelve a calcular el HEC. Si confirma el cálculo en un número determinado de celdas consecutivas, establece la alineación.
3. **Estado de Sincronismo (_Sync_):** Es el estado de operación normal. Si se detectan múltiples celdas consecutivas con HEC incorrecto, el receptor asume que perdió el encuadre y regresa al estado de captura para volver a sincronizar.
