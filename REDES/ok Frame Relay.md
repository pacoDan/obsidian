## Características

**Frame Relay** es un protocolo de transporte de redes de área amplia (WAN) que opera en el nivel de enlace de datos (Capa 2 del modelo OSI). A continuación se detallan sus características fundamentales:

### 1. Nivel de Operación y Estructura de Trama
* **Protocolo de Capa 2 (Enlace de Datos):** Nació como un desarrollo derivado del estándar HDLC (específicamente la especificación LAPF) para redes WAN.
* **Orientado a la Conexión:** Requiere que se establezca una conexión lógica antes de transmitir los datos de usuario.
* **Tramas de Longitud Variable:** Transporta unidades de datos de tamaño variable (pudiendo alcanzar hasta 4096 bytes), a diferencia de tecnologías como ATM que usan celdas fijas.
* **Delimitación de Tramas:** Emplea banderas o *flags* (secuencia `0x7E`) para delimitar el inicio y el fin de la trama, utilizando la técnica de **inserción de ceros** (*bit stuffing*) para evitar que la secuencia del *flag* aparezca en los datos de usuario.

### 2. Circuitos Virtuales y Multiplexación
* **Multiplexación de Canales Lógicos:** Permite compartir un único acceso físico (cable o interfaz serial) para comunicarse con múltiples destinos mediante canales lógicos independientes.
* **Circuitos Virtuales Permanentes (PVC):** Funciona principalmente mediante configuraciones estáticas o permanentes en la red del proveedor (*Permanent Virtual Circuits*).
* **Identificador DLCI:** Cada canal lógico o circuito virtual dentro del enlace de acceso se identifica mediante un número de alcance local llamado **DLCI** (*Data Link Connection Identifier*).

### 3. Gestión de Tráfico y Ancho de Banda
* **CIR (*Committed Information Rate*):** Tasa de información comprometida o ancho de banda que el proveedor de servicios garantiza entregar bajo condiciones normales.
* **EIR (*Excess Information Rate*):** Tasa de tráfico en exceso por encima del CIR, la cual la red intentará entregar solo si hay capacidad disponible (*best effort*).
* **Marcado de Elegibilidad de Descarte (Bit DE):** 
  * Las tramas dentro del CIR viajan con el bit `DE = 0` (*Discard Eligibility*).
  * Cuando el tráfico supera el CIR pero está dentro del EIR, el nodo de ingreso marca la trama con `DE = 1`.
  * En situaciones de congestión en la red, los conmutadores descartan primero las tramas que tienen `DE = 1`. Si el tráfico excede la suma de CIR + EIR, es descartado directamente al ingresar.

### 4. Control de Errores y Congestión
* **Sin Control de Flujo ni Retransmisión en Capa 2:** No retransmite tramas perdidas ni realiza un control de flujo directo sobre el emisor; delega la confiabilidad y el control de errores a los protocolos de capas superiores como TCP.
* **Detección de Errores (FCS):** Cuenta con un campo **FCS** (*Frame Check Sequence*) con CRC para detectar errores de transmisión. Si una trama contiene errores, es **descartada silenciosamente** por el nodo sin solicitar retransmisión.
* **Notificación Explícita de Congestión:** Informa la presencia de congestión en la red activando bits específicos en la cabecera:
  * **FECN (*Forward Explicit Congestion Notification*):** Notificación hacia adelante (enviada en la dirección del tráfico hacia el receptor) para indicar que la ruta experimenta congestión.
  * **BECN (*Backward Explicit Congestion Notification*):** Notificación hacia atrás (enviada hacia el emisor) para indicarle que debe reducir su velocidad de transmisión.

## Que permite

Frame Relay permite lo siguiente:

* **Multiplexar múltiples canales lógicos sobre un único acceso físico:** A diferencia de protocolos como HDLC (que exigen un circuito físico dedicado para cada destino), Frame Relay permite comunicarse con múltiples sitios desde una sola interfaz física mediante el uso de **circuitos virtuales** e identificadores **DLCI** (*Data Link Connection Identifier*).
* **Sustituir enlaces físicos dedicados por circuitos virtuales:** Permite interconectar diversas sucursales u oficinas a través de la red del proveedor mediante **circuitos virtuales permanentes (PVCs)**, lo cual resulta sustancialmente más económico que contratar enlaces físicos punto a punto para cada par de ubicaciones.
* **Aprovechar el ancho de banda mediante tráfico en ráfagas:** Permite contar con una tasa de transmisión garantizada (**CIR** o *Committed Information Rate*) y, al mismo tiempo, aprovechar la capacidad excedente de la red para transmitir ráfagas de datos por encima de esa tasa (**EIR** o *Excess Information Rate*).
* **Encapsular datos en tramas de longitud variable:** Permite transportar de forma transparente paquetes de capas superiores (como datagramas IP) ajustándose al tamaño de los datos mediante tramas de tamaño variable (de hasta 4096 bytes).

## Que es protocolo de señalizacion

En Frame Relay, el **protocolo de señalización** opera dentro del **plano de control** de la red y se encarga del intercambio de mensajes de control e información de estado entre el equipo del usuario y la red.
A diferencia del **plano de usuario** —donde se utiliza el protocolo **LAPF** para transportar las tramas con los datos propiamente dichos—, el plano de control gestiona la conectividad y el estado de los circuitos virtuales.

### Principales funciones de la señalización

1. **Gestión de Circuitos Virtuales Conmutados (SVC):**
   * Permite solicitar el **establecimiento, mantenimiento y liberación** dinámica de una conexión bajo demanda.
   * Funciona de manera análoga a un llamado telefónico en RDSI/ISDN: el terminal del usuario envía un mensaje a la red solicitando comunicarse con un destino específico, la red reserva el camino lógico y, al finalizar la transmisión, se emite un mensaje para cerrar la sesión.

2. **Gestión del estado de Circuitos Virtuales Permanentes (PVC) / LMI:**
   * Para conexiones estáticas (PVC), la señalización a nivel de interfaz local (**LMI** - *Local Management Interface* o estándares como **Q.933**) permite al equipo del usuario y al conmutador de la red intercambiar mensajes periódicos (*keep-alive*) para verificar la integridad del enlace físico e informar qué identificadores de canal (**DLCI**) están activos, eliminados o con problemas.

### Protocolos asociados
* **LAPC** (*Link Access Procedure for Control*): Es el protocolo de capa de enlace especificador del plano de control en Frame Relay.
* **Q.933 / LMI**: Estándares que definen los tipos de mensajes (solicitud de conexión, confirmación, reporte de estado de PVCs, etc.) que transitan por el plano de control.


## Que es LAPD y LAPF en Frame relay
	
En las redes de área amplia (WAN) y dentro del contexto de **Frame Relay**, tanto **LAPD** como **LAPF** son protocolos de nivel de enlace de datos (Capa 2 del modelo OSI) derivados del estándar **HDLC** (_High-Level Data Link Control_).

Frame Relay fue concebido originalmente para operar sobre el canal D en redes **ISDN / RDSI** (_Red Digital de Servicios Integrados_). Dentro de esta arquitectura, **LAPD** y **LAPF** se dividen la responsabilidad entre el **plano de control** y el **plano de usuario**:

### 1. **LAPD (_Link Access Procedure on the D-channel_)**

- **¿Qué es?:** Es el protocolo de procedimiento de acceso al enlace diseñado para operar sobre el **canal D** de las redes ISDN/RDSI.
- **Función en el Plano de Control:** Actúa dentro del **plano de control** y de la señalización. Es la base sobre la cual se definen los protocolos de señalización (como LAPC) para gestionar la conectividad, el llamado y el establecimiento de circuitos virtuales en la red.

### 2. **LAPF (_Link Access Procedure for Frame-Mode Bearer Services_)**

- **¿Qué es?:** Es la especificación del protocolo de capa de enlace propia de **Frame Relay** destinada al transporte de tramas de datos.
- **Función en el Plano de Usuario:** Opera exclusivamente en el **plano de usuario** y define el formato de trama que intercambian los equipos de usuario con la red para transportar los datos propiamente dichos.
- **Características del formato LAPF:**
    - Define la estructura de las tramas de Frame Relay delimitadas por banderas (_flags_ `0x7E`), la cabecera con la dirección lógica (**DLCI**), la carga útil de datos de tamaño variable y la secuencia de chequeo **FCS / CRC**.
    - Corresponde a una versión simplificada de la capa de enlace que no ejecuta todas las funciones de un protocolo clásico de Capa 2 (no realiza control de flujo ni retransmisión/corrección de errores en Capa 2), delegando la confiabilidad a los protocolos de capas superiores como TCP.

### Resumen comparativo

|Característica|**LAPD**|**LAPF**|
|:--|:--|:--|
|**Significado**|_Link Access Procedure on the D-channel_|_Link Access Procedure for Frame-Mode Bearer Services_|
|**Plano de operación**|**Plano de Control** (señalización)|**Plano de Usuario** (datos de usuario)|
|**Entorno de origen**|Canal D de redes ISDN / RDSI|Versión simplificada de Capa 2 para Frame Relay|
|**Función principal**|Intercambio de mensajes para gestión y establecimiento de enlaces|Encapsular y transportar tramas de datos utilizando el campo DLCI|

El **canal D** (canal de datos/señalización) proviene originalmente de la arquitectura de las redes **ISDN / RDSI** (*Red Digital de Servicios Integrados*). 

Frame Relay fue diseñado en sus orígenes para ser utilizado sobre el canal D de las redes ISDN con el fin de ofrecer servicios de transporte de datos orientados a tramas (*frame-mode bearer services*).


### Funciones y características clave del Canal D

1. **Plano de Control y Señalización:**
   * En las conexiones ISDN / RDSI se diferencian dos tipos de canales:
     * **Canales B (*Bearer*):** Destinados al transporte de la voz o datos de usuario.
     * **Canal D (*Data / Delta*):** Destinado al **plano de control y señalización**.
   * A través del canal D transitan los mensajes de gestión para solicitar, establecer, mantener y liberar llamadas o circuitos virtuales.

2. **Protocolo LAPD:**
   * Sobre el canal D opera el protocolo de enlace **LAPD** (*Link Access Procedure on the D-channel*). 
   * LAPD se encarga de estructurar los mensajes de señalización en el plano de control.

3. **Evolución hacia Frame Relay (LAPF):**
   * Al adaptar este esquema para el transporte eficiente de datos, Frame Relay tomó como referencia la tecnología del canal D y derivó de LAPD el protocolo **LAPF** (*Link Access Procedure for Frame-Mode Bearer Services*).
   * Mientras que el canal D (con LAPD/Q.933) maneja la señalización y control en el **plano de control**, las tramas LAPF de Frame Relay se encargan de transportar los datos de usuario en el **plano de usuario**.




## Que es PDH

**PDH** corresponde a la **Jerarquía Digital Plesiócrona** (_Plesiochronous Digital Hierarchy_), una tecnología de red de transporte digital utilizada en telecomunicaciones para multiplexar y canalizar múltiples comunicaciones digitales sobre enlaces o troncales (_trunks_).

Sus características principales según las fuentes son:

- **Estructura jerárquica de velocidades:** Emplea niveles de multiplexación estandarizados como **E1** (2 Mbps, que agrupa canales de 64 kbps), **E2** (8 Mbps) y **E3** (34 Mbps).
- **Uso en redes de transporte y telefonía:** Se ha utilizado históricamente para interconectar centrales telefónicas y transportar canales de voz digitalizada o líneas dedicadas de datos.
- **Base para tecnologías WAN:** Sirve como la infraestructura de capa física/transporte sobre la cual operan otros protocolos de nivel de enlace de área amplia (WAN), como Frame Relay o enlaces seriales.

En la evolución de las redes de transporte, PDH es frecuentemente comparada y complementada o sustituida por **SDH** (_Jerarquía Digital Sincrónic_a).


## Como funciona el circuito tipico en FR


Un **circuito típico en Frame Relay** funciona mediante la interconexión de distintas sedes (por ejemplo, una casa central y sus sucursales) utilizando **circuitos virtuales** sobre una infraestructura física compartida,,.

El funcionamiento se desglosa en las siguientes etapas y componentes clave:

### 1. Enlace Físico de Acceso (Última Milla)

Cada ubicación (equipo del usuario o DTE, como un router) se conecta al nodo más cercano de la red del proveedor (DCE) mediante un **único enlace o interfaz serial física**,,.

### 2. Multiplexación de Circuitos Virtuales (PVC)

En lugar de instalar enlaces físicos dedicados punto a punto hacia cada sucursal (lo cual resulta costoso e ineficiente), Frame Relay permite multiplexar múltiples canales lógicos o **Circuitos Virtuales Permanentes (PVC)** sobre ese único acceso físico,,.

### 3. Identificación por DLCI

Para distinguir a cuál de los destinos va dirigida cada trama que sale por la interfaz física, se utiliza un número de alcance local denominado **DLCI** (_Data Link Connection Identifier_),,:

- Por ejemplo, en un único enlace físico, el router asigna el `DLCI 16` para el tráfico dirigido a la Sucursal A, el `DLCI 17` para la Sucursal B, etc.,.

### 4. Conmutación en la Red del Proveedor

Cuando una trama ingresa al conmutador de la red del proveedor:

1. El conmutador lee el **DLCI de entrada**.
2. Consulta su tabla de conmutación interna (configurada previamente de forma estática por el proveedor),.
3. Reemplaza el DLCI por el correspondiente a la siguiente interfaz de salida y reenvía la trama,.
4. La **concatenación** de estos valores de DLCI en los distintos nodos de la red conforma la trayectoria completa del circuito virtual de extremo a extremo.

### 5. Gestión del Tráfico (CIR, EIR y Bit DE)

El circuito se gestiona según las tasas de tráfico contratadas:

- **CIR (_Committed Information Rate_):** Es el ancho de banda garantizado por el proveedor. Las tramas dentro de este margen viajan con el bit `DE = 0`,.
- **EIR (_Excess Information Rate_):** Permite aprovechar la capacidad vacante de la red para enviar ráfagas de datos por encima del CIR (_best effort_).
- **Bit DE (_Discard Eligibility_):** Si el tráfico transmitido excede la tasa CIR, el conmutador de ingreso marca esas tramas con `DE = 1`. En caso de que se produzca congestión en algún nodo intermedio de la red, las tramas marcadas con `DE = 1` serán las primeras en ser descartadas.


## Que es un circuito virtual y como funciona en Frame Relay

Un **circuito virtual** es una conexión o canal lógico establecido sobre una infraestructura física compartida. A diferencia de un circuito físico dedicado —el cual reserva recursos físicos exclusivos de extremo a extremo independientemente de si se transmiten datos o no—, el circuito virtual permite vincular sitios mediante configuraciones lógicas en los nodos de la red sin necesidad de asignar enlaces físicos individuales para cada destino.

Existen dos modalidades principales de circuitos virtuales:

- **Circuito Virtual Permanente (PVC - _Permanent Virtual Circuit_):** Se establece mediante una configuración estática previa realizada por el proveedor en los nodos de la red y permanece disponible de manera continua.
- **Circuito Virtual Conmutado (SVC - _Switched Virtual Circuit_):** Se establece y se libera de forma dinámica bajo demanda mediante mensajes de señalización.

### Funcionamiento de los Circuitos Virtuales en Frame Relay

En Frame Relay, el circuito virtual opera a través de los siguientes mecanismos principales:

1. **Multiplexación sobre una única interfaz de acceso:** Un equipo de usuario (router) se conecta al nodo del proveedor mediante un único enlace físico serial. A través de esa misma interfaz física se multiplexan múltiples canales o circuitos virtuales que permiten comunicarse de forma independiente con distintos destinos.
    
2. **Identificación mediante el campo DLCI:** Cada circuito virtual que transita por la interfaz física se identifica mediante un número llamado **DLCI** (_Data Link Connection Identifier_). El valor del DLCI tiene un significado o ámbito exclusivamente local entre el equipo del usuario y el nodo de acceso al que se conecta.
    
3. **Conmutación e interconexión en la red:**
    
    - Cuando una trama ingresa a un conmutador de Frame Relay, el nodo lee el **DLCI de entrada** y consulta su tabla de conmutación interna.
    - La tabla del nodo asocia el puerto y el DLCI de entrada con un puerto de salida y un nuevo **DLCI de salida**.
    - El nodo reemplaza el valor de DLCI en la cabecera de la trama y la reenvía hacia el siguiente conmutador.
    - La **concatenación secuencial** de estos valores de DLCI locales a través de los distintos conmutadores de la red forma la trayectoria lógica completa del circuito virtual de extremo a extremo.
4. **Gestión de tráfico del circuito virtual:**
    - **CIR (_Committed Information Rate_):** Cada circuito virtual tiene contratada una tasa garantizada de información.
    - **Bit DE (_Discard Eligibility_):** Si el usuario transmite tramas por encima de la tasa CIR (aprovechando la capacidad en exceso o EIR), el nodo de ingreso marca esas tramas fijando el bit `DE = 1`.
    - Si ocurre congestión en la red, los nodos conmutadores descartarán prioritariamente aquellas tramas marcadas con `DE = 1` para proteger el tráfico garantizado del resto de los circuitos.

## Que es un circuito virtual conmmutado en Frame Relay

Un **Circuito Virtual Conmutado** (_SVC - Switched Virtual Circuit_) en Frame Relay es un canal lógico temporal que se establece dinámicamente bajo demanda para transmitir datos y se libera automáticamente una vez finalizada la comunicación.

### Principales características y funcionamiento
1. **Establecimiento bajo demanda (análogo a una llamada telefónica):**
    - A diferencia de los Circuitos Virtuales Permanentes (PVC), que son configurados estáticamente por el proveedor y permanecen siempre activos, los SVC operan bajo el esquema de "marcado, transferencia y desconexión".
    - Cuando un terminal o router necesita enviar información a un destino, emite un mensaje a la red solicitando abrir la conexión.
2. **Uso del Plano de Control y Señalización:**    
    - Requiere de protocolos de señalización en el **plano de control** (como los estándares **Q.933** / **LAPC**) para el intercambio de mensajes administrativos con la red.
    - La red evalúa si existen caminos e identificadores **DLCI** disponibles y si puede garantizar la calidad de servicio solicitada antes de confirmar el enlace.
3. **Ciclo de vida de la conexión:**
    - **Establecimiento:** El origen envía una solicitud de llamada indicando la dirección del destinatario.
    - **Transferencia de datos:** Una vez aceptada la llamada por el receptor y reservado el DLCI temporal, los datos del usuario se transmiten en el **plano de usuario** utilizando el protocolo de enlace **LAPF**.
    - **Liberación:** Al concluir la transferencia de datos, se envía un mensaje de señalización para cerrar el circuito y liberar el DLCI y los recursos de conmutación en los nodos de la red.

## Dar diferencias entre circuito virtual conmutado y circuito virtual permamente, de frame relay

Las principales diferencias entre un **Circuito Virtual Permanente (PVC)** y un **Circuito Virtual Conmutado (SVC)** en Frame Relay abarcan su modo de establecimiento, el uso de planos de la red y su adopción práctica:
### 1. Naturaleza y Modo de Establecimiento
- **Circuito Virtual Permanente (PVC):**
    - **Estático y continuo:** Es una conexión lógica fija que configura el proveedor de servicios de manera estática en los nodos de la red al momento de contratar el servicio.
    - **Siempre disponible:** Permanece activo y listo para transmitir datos en todo momento entre las sedes interconectadas, sin necesidad de realizar ninguna fase previa de marcado o solicitud de llamada.
- **Circuito Virtual Conmutado (SVC):**
    - **Dinámico y bajo demanda:** Es un canal temporal que se establece dinámicamente cuando un usuario necesita enviar información y se libera de forma automática una vez concluida la transmisión.
    - **Semejante a una llamada telefónica:** Funciona con la lógica de "marcado, transferencia de datos y desconexión".
### 2. Intervención del Plano de Control y Señalización
- **PVC:**
    - Trabaja directamente en el **plano de usuario** transportando las tramas de datos mediante la especificación de enlace **LAPF**.
    - No requiere intercambio de mensajes de señalización en el plano de control para abrir o cerrar la conexión, ya que la ruta de conmutación de los identificadores **DLCI** ya está escrita de antemano en las tablas de los nodos.
- **SVC:**
    - Requiere una interacción constante con el **plano de control** mediante protocolos de señalización (como **LAPC** sobre el canal D de ISDN) para gestionar el establecimiento, la negociación de recursos y la liberación del circuito.
    - Una vez aceptada y abierta la llamada en el plano de control, pasa a utilizar el **plano de usuario** (LAPF) para enviar la información útil.

### 3. Adopción y Uso Comercial

- **PVC:** Fue la modalidad **más popular y ampliamente utilizada** en el ámbito corporativo para interconectar sucursales con casas centrales a través de la red WAN del proveedor.
- **SVC:** Tuvo una **difusión y adopción mucho menor** en la práctica, quedando relegado a casos puntuales de transmisiones muy esporádicas entre puntos remotos.

### Tabla Comparativa Resumida

|Característica|Circuito Virtual Permanente (PVC)|Circuito Virtual Conmutado (SVC)|
|:--|:--|:--|
|**Configuración**|Estática (realizada previamente por el proveedor)|Dinámica (establecida automáticamente bajo demanda)|
|**Disponibilidad**|Continua / Siempre activo|Temporal / Solo durante la sesión|
|**Funcionamiento**|Similar a un enlace dedicado punto a punto virtual|Análogo a una llamada telefónica|
|**Uso de Señalización**|No requiere señalización previa para transmitir|Requiere señalización en el plano de control (LAPC)|
|**Popularidad en la red**|Muy alta (estándar práctico en Frame Relay)|Baja en entornos corporativos|


## Que permite frame relay en las mallas o circuitos
En el contexto de la topología de red y el diseño de circuitos WAN, **Frame Relay** aporta ventajas fundamentales al utilizar **mallas (topologías en malla parcial o _full mesh_)**:
### 1. Multiplexación de múltiples circuitos virtuales sobre un único acceso físico

- **Reducción de cableado e interfaces:** En una topología en malla tradicional punto a punto (por ejemplo, con HDLC), interconectar \(N\) sedes requiere contratar y cablear un enlace físico individual para cada par de ubicaciones.
- **Solución de Frame Relay:** Cada sede solo necesita **un único enlace o interfaz física serial** conectada al nodo del proveedor. Sobre esa misma interfaz se multiplexan de forma lógica múltiples **Circuitos Virtuales Permanentes (PVC)** dirigidos a los distintos destinos.

### 2. Creación de mallas completas (_Full Mesh_) a bajo costo

- Permite que cualquier sucursal u oficina se comunique directamente con cualquier otra (_any-to-any_ / _full mesh_) sin necesidad de pasar obligatoriamente por la sede central (evitando cuellos de botella y disminuyendo la latencia de procesamiento).
- Como los circuitos son **lógicos y no físicos**, el costo de interconectar múltiples sedes mediante circuitos virtuales es significativamente menor que mantener múltiples líneas dedicadas reales.

### 3. Identificación local mediante DLCI

- Cada circuito virtual o canal lógico que transita por la interfaz física se identifica mediante un número de alcance local denominado **DLCI** (_Data Link Connection Identifier_).
- Esto permite asignar un DLCI distinto para cada destino dentro de la malla utilizando la misma interfaz física.

### 4. Gestión de tráfico por circuito dentro de la malla

- **CIR (_Committed Information Rate_):** Se puede definir un ancho de banda garantizado de forma independiente para cada enlace de la malla.
- **EIR (_Excess Information Rate_) y bit DE (_Discard Eligibility_):** Permite aprovechar el ancho de banda excedente de la red para enviar ráfagas de datos por encima del CIR. Las tramas en exceso se marcan con el bit `DE = 1` para ser descartadas únicamente en caso de congestión en los nodos de la malla.

### 5. Alta escalabilidad

- Si la empresa incorpora una nueva sucursal a la malla, basta con contratar su enlace físico de acceso e informar al proveedor qué nuevos PVC (y DLCIs) deben habilitarse. No es necesario modificar el cableado ni agregar tarjetas de interfaz físicas en las demás sedes ya existentes.

## Dar y especificar formato de la trama Frame Relay, dar y ejemplificar cada campo

La trama de **Frame Relay** (especificada bajo el protocolo de enlace **LAPF**) tiene una estructura orientada al bit con campos delimitadores, cabecera de dirección, carga útil de tamaño variable y control de errores.

### Esquema del formato de la trama (LAPF)

```
+--------------+-------------------------------+-----------------------+---------------+--------------+
| Flag (1 B)   | Cabecera / Dirección (2-4 B)  | Datos (hasta 4096 B)  | FCS (2 B)     | Flag (1 B)   |
+--------------+-------------------------------+-----------------------+---------------+--------------+
```

En la configuración estándar de cabecera de **2 bytes (16 bits)**, los campos internos se distribuyen de la siguiente manera:
```
Byte 1: | DLCI (primeros 6 bits) | C/R (1 bit) | EA = 0 (1 bit) |
Byte 2: | DLCI (últimos 4 bits)  | FECN (1 bit)| BECN (1 bit) | DE (1 bit) | EA = 1 (1 bit) |
```
### Descripción y ejemplo de cada campo

#### 1. Flag (Delimitador de inicio y fin)

- **Tamaño:** 1 byte al inicio y 1 byte al final de la trama.
- **Valor / Patrón:** Secuencia binaria fija `01111110` (`0x7E` en hexadecimal).
- **Función:** Delimita el principio y el cierre de la trama. Para evitar que esta secuencia se confunda con los datos de usuario o la cabecera, se aplica la técnica de **inserción de ceros** (_bit stuffing_), añadiendo un `0` automático cada vez que aparecen cinco unos consecutivos.
- **Ejemplo:** La trama comienza con la secuencia `01111110` para sincronizar al receptor.


#### 2. Cabecera de Dirección (Address Field)

- **Tamaño:** Mínimo 2 bytes (16 bits), ampliable a 3 o 4 bytes según el uso del bit **EA**.
    
- **Subcampos incluidos:**
    
    - **DLCI (_Data Link Connection Identifier_):**
        
        - **Tamaño:** 10 bits en la cabecera básica de 2 bytes (6 bits en el primer byte y 4 bits en el segundo).
        - **Función:** Identifica el canal lógico o **circuito virtual (PVC/SVC)** que une de forma local al usuario con el nodo de la red.
        - **Ejemplo:** `DLCI = 16` identifica el circuito hacia la Sucursal A, mientras que `DLCI = 17` identifica el circuito hacia la Sucursal B sobre la misma interfaz física.
    - **C/R (_Command / Response_):**
        
        - **Tamaño:** 1 bit.
        - **Función:** Reservado para aplicaciones del usuario para indicar si la trama transporta un comando o una respuesta. No es interpretado por los conmutadores de Frame Relay.
        - **Ejemplo:** Fijado en `0` o `1` según la aplicación.
    - **EA (_Extended Address_):**
        
        - **Tamaño:** 1 bit en el último extremo de cada byte de dirección.
        - **Función:** Indica si la cabecera de dirección continúa en el siguiente byte. Un valor `0` indica que la cabecera continúa; un valor `1` indica que es el último byte de la cabecera.
        - **Ejemplo:** En una cabecera de 2 bytes, el primer byte lleva `EA = 0` y el segundo byte lleva `EA = 1`.
    - **FECN (_Forward Explicit Congestion Notification_):**
        
        - **Tamaño:** 1 bit.
        - **Función:** Notificación explícita de congestión hacia adelante. Si un nodo de la red se congestiona, activa este bit en `1` para avisarle al nodo **receptor** (en la dirección del tráfico) que la ruta está experimentando congestión.
        - **Ejemplo:** `FECN = 1` informa a la sucursal de destino que hay retrasos en el camino.
    - **BECN (_Backward Explicit Congestion Notification_):**
        
        - **Tamaño:** 1 bit.
        - **Función:** Notificación explícita de congestión hacia atrás. El nodo conmutador congestionado activa este bit en `1` en las tramas que viajan en sentido opuesto hacia el **emisor** para indicarle que disminuya su velocidad de transmisión.
        - **Ejemplo:** `BECN = 1` avisa a la casa central que debe reducir la velocidad con la que envía tráfico hacia la red.
    - **DE (_Discard Eligibility_):**
        
        - **Tamaño:** 1 bit.
        - **Función:** Elegibilidad de descarte. Indica si la trama puede ser descartada en caso de que la red sufra congestión. El tráfico que va dentro de la tasa garantizada (**CIR**) lleva `DE = 0`. Si el usuario envía tramas por encima del CIR (aprovechando la tasa en exceso o **EIR**), el conmutador de ingreso marca esas tramas fijando `DE = 1`.
        - **Ejemplo:** Una ráfaga de datos que supera el ancho de banda contratado entra a la red con `DE = 1`. Si un conmutador intermedio se satura, descartará primero las tramas que tengan `DE = 1` para proteger las tramas con `DE = 0`.

#### 3. Campo de Datos / Carga Útil (Payload / Information)

- **Tamaño:** Variable, pudiendo alcanzar hasta 4096 bytes.
- **Función:** Transporta de forma transparente los datos o paquetes de los protocolos de capas superiores (como datagramas IP).
- **Ejemplo:** Un datagrama IPv4 de 1500 bytes correspondiente a una transferencia de archivos.

#### 4. FCS (_Frame Check Sequence_ / Secuencia de Chequeo de Trama)

- **Tamaño:** 2 bytes (o 4 bytes según la especificación del CRC).
- **Función:** Campo de control de errores mediante un código CRC de 16 o 32 bits calculado sobre los campos de dirección y datos. Si el conmutador receptor detecta que la trama llegó con algún error de bit, la **descarta silenciosamente** sin realizar retransmisiones en Capa 2.
- **Ejemplo:** Un valor hexadecimal de comprobación de red (por ejemplo, `0x9E3A`) adjuntado al final de la trama.

## Que semejanzas tiene Frame Relay con Vlans y trunk (explicarlas)

Existen importantes **semejanzas conceptuales y operativas** entre **Frame Relay** (tecnología WAN de Capa 2) y el esquema de **VLANs y Enlaces Trunk / 802.1Q** (tecnología LAN de Capa 2). Ambas soluciones se diseñaron para resolver el mismo problema fundamental: **cómo compartir un único medio físico para transportar múltiples redes o canales lógicos independientes**.

A continuación se explican sus principales semejanzas:

### 1. Multiplexación de múltiples canales lógicos sobre una única interfaz física

- **Frame Relay:** Permite que un router o equipo de usuario (DTE) utilice una sola interfaz serial física para comunicarse con múltiples sedes remotas a través de **circuitos virtuales (PVCs)** independientes.
- **VLANs / Trunking:** Un enlace _Trunk_ (bajo la norma IEEE 802.1Q) permite transportar el tráfico de múltiples **VLANs** distintas a través de un único cable o puerto físico de un switch.
- **Semejanza:** En ambos casos se evita la necesidad de instalar o contratar un enlace físico individual para cada destino o red, optimizando drásticamente la infraestructura.

### 2. Identificación por etiquetas/números en la cabecera de Capa 2 (_Tagging_)

- **Frame Relay:** Utiliza el campo **DLCI** (_Data Link Connection Identifier_) en la cabecera de la trama (LAPF) para indicar a qué circuito virtual pertenece la trama.
- **VLANs / Trunking:** Modifica la trama Ethernet insertando una etiqueta **802.1Q** que contiene el **VLAN ID** (número de VLAN de 12 bits) para identificar la red lógica de origen/destino.
- **Semejanza:** Ambos protocolos basan el reenvío multiplexado en la inclusión de un **identificador numérico local dentro de la cabecera de Capa 2**, permitiendo que el conmutador (switch de red o conmutador Frame Relay) sepa por qué canal lógico debe enviar la información.


### 3. Aislamiento y segmentación de tráfico en la Capa de Enlace

- **Frame Relay:** Separa de forma transparente los circuitos virtuales entre diferentes sedes u organizaciones; los datos de un circuito virtual no pueden filtrarse hacia otro.
- **VLANs:** Separan el switch físico en múltiples dominios de broadcast independientes; las tramas enviadas dentro de una VLAN están aisladas de las demás.
- **Semejanza:** Ambas tecnologías crean **entornos virtuales cerrados y privados** sobre una misma infraestructura física compartida.


### 4. Nivel de operación (Capa 2) y necesidad de Capa 3 para enrutar

- **Frame Relay:** Opera en la **Capa 2 (Enlace de Datos)**. Para interconectar o enviar paquetes entre diferentes circuitos virtuales (por ejemplo, enrutar entre subsistemas IP), se requiere un dispositivo de **Capa 3 (Router)**.
- **VLANs:** Operan en la **Capa 2**. Para permitir la comunicación entre hosts que están en VLANs distintas, es indispensable la intervención de un dispositivo de **Capa 3 (Router o Switch Layer 3)**.
- **Semejanza:** Ninguna de las dos tecnologías realiza enrutamiento IP por sí sola; ambas se limitan a la conmutación de tramas mediante sus identificadores de Capa 2 (DLCI o VLAN ID) y delegan el enrutamiento inter-canal/inter-VLAN a la Capa 3.

### Tabla Comparativa Resumida

|Concepto|Frame Relay (WAN)|VLANs y Trunking 802.1Q (LAN)|
|:--|:--|:--|
|**Nivel OSI**|Capa 2 (Enlace de Datos)|Capa 2 (Enlace de Datos)|
|**Enlace Físico Compartido**|Interfaz serial de acceso al proveedor|Enlace _Trunk_ entre switches o hacia un router|
|**Identificador de Capa 2**|**DLCI** (_Data Link Connection Identifier_)|**VLAN ID** (Etiqueta 802.1Q)|
|**Canal Lógico Interno**|Circuito Virtual (PVC / SVC)|VLAN (Dominio de broadcast virtual)|
|**Interconexión entre Canales**|Requiere procesamiento en Capa 3 (Router)|Requiere procesamiento en Capa 3 (Router / L3 Switch)|


## Definir análisis de trafico en frame relay, explicar CIR, EIR, TC, BC, CIR

### Análisis de Tráfico en Frame Relay
El **análisis de tráfico** (o control de tráfico) en Frame Relay es el mecanismo mediante el cual el nodo de ingreso de la red mide y controla el volumen de datos transmitidos por un usuario a través de un circuito virtual. Su objetivo es verificar que la transmisión respete los límites de ancho de banda contratados, clasificando las tramas para entregarlas de forma garantizada, marcarlas para posible descarte en caso de congestión (bit DE = 1) o descartarlas de inmediato si superan el máximo permitido.

### Explicación de los Parámetros de Tráfico

- **CIR (Committed Information Rate / Tasa de Información Comprometida):** Es la velocidad o ancho de banda garantizado (en bits por segundo) que la red entrega al usuario en condiciones normales.
    
- **EIR (Excess Information Rate / Tasa de Información en Exceso):** Es la velocidad de transmisión por encima del CIR que la red intentará cursar únicamente si dispone de capacidad vacante (modo _best effort_).
    
- **Tc (Measurement Interval / Intervalo de Medición):** Es la ventana o periodo de tiempo (medido en segundos) sobre el cual la red evalúa y mide la cantidad de bits transmitidos por el usuario.
    
- **Bc (Committed Burst Size / Ráfaga Comprometida):** Es la cantidad máxima de bits que la red garantiza entregar de manera confiable durante el intervalo Tc.
    
- **Be (Excess Burst Size / Ráfaga en Exceso):** Es la cantidad máxima de bits por encima de Bc que el usuario puede enviar durante el intervalo Tc de forma no garantizada.

### Fórmulas de Relación (en Texto Plano)

- **CIR** = Bc / Tc =  RAFAGA COMPROMETIDA/ INTERVALO DE MEDICION
- **EIR** = Be / Tc
- **Bc** = CIR * Tc
- **Be** = EIR * Tc
- **Ráfaga Máxima Permitida en Tc** = Bc + Be

### Clasificación de las Tramas según el Tráfico Transmitido

1. **Tráfico dentro del CIR (menor o igual a Bc bits en el tiempo Tc):** Las tramas se entregan de forma garantizada y llevan el bit de elegibilidad de descarte en **DE = 0**.
    
2. **Tráfico en Zona EIR (mayor a Bc pero menor o igual a Bc + Be bits en Tc):** Las tramas se aceptan si la red tiene capacidad, pero el nodo las marca fijando el bit **DE = 1**. Si surge congestión en algún punto de la red, estas tramas marcadas serán las primeras en ser descartadas.
    
3. **Tráfico Excedente (mayor a Bc + Be bits en Tc):** Cualquier volumen de datos que supere la suma total de Bc + Be dentro del intervalo Tc es **descartado de inmediato** en el nodo de ingreso de la red.

## como hace la gestion del trafico en Frame relay
La gestión y control de tráfico en **Frame Relay** los ejecuta el nodo de ingreso a la red mediante una **función de policía** (_traffic policing_). Su objetivo principal es medir el volumen de datos que envía un usuario a través de un circuito virtual en un intervalo de tiempo determinado y clasificar o descartar las tramas según los límites de ancho de banda contratados.

### 1. Parámetros de Tráfico Contratados

La red administra el ancho de banda evaluando los siguientes parámetros de tráfico:

- **Tc (Measurement Interval / Intervalo de Medición):** Es la ventana o período de tiempo sobre el cual el nodo de la red mide y evalúa el tráfico transmitido por el usuario.
- **Bc (Committed Burst Size / Ráfaga Comprometida):** Es la cantidad máxima de bits que la red garantiza entregar durante el intervalo Tc bajo condiciones normales.
- **CIR (Committed Information Rate / Tasa de Información Comprometida):** Es la velocidad o ancho de banda garantizado (medido en bits por segundo) que la red entrega al usuario (calculado como **CIR = Bc / Tc**).
- **Be (Excess Burst Size / Ráfaga en Exceso):** Es la cantidad máxima de bits por encima de Bc que la red intentará entregar sin garantía (_best effort_) durante el intervalo Tc.
- **EIR (Excess Information Rate / Tasa de Información en Exceso):** Es la velocidad de transmisión por encima del CIR que la red intentará cursar únicamente si existe capacidad vacante en los nodos (calculada como **EIR = Be / Tc**).
- **Access Rate:** Es la velocidad de transmisión física total del enlace de acceso del usuario. La suma total permitida en la ráfaga (**Bc + Be**) coincide con la capacidad máxima de este acceso.

### 2. Clasificación del Tráfico y Marcado del Bit DE

Durante cada intervalo Tc, el nodo de ingreso cuenta los bits entrantes y clasifica las tramas en tres niveles:

1. **Tráfico dentro del CIR (hasta Bc bits en Tc):** La red garantiza la entrega de estas tramas y las deja viajar con el bit de elegibilidad de descarte en **DE = 0**.
2. **Tráfico en zona EIR (más de Bc y hasta Bc + Be bits en Tc):** Se acepta el tráfico en modo _best effort_, pero el nodo marca las tramas fijando el bit **DE = 1** (_Discard Eligibility_). Si algún nodo intermedio sufre congestión, las tramas marcadas con **DE = 1** serán las primeras en ser descartadas.
3. **Tráfico Excedente (más de Bc + Be bits en Tc):** Cualquier volumen de datos que sobrepase la ráfaga máxima combinada (Bc + Be) durante el intervalo Tc es **descartado de inmediato en el nodo de ingreso** de la red.

### 3. Notificación Explícita de Congestión (FECN y BECN)

Frame Relay **no realiza control de flujo** (no detiene al emisor ni retransmite tramas perdidas en Capa 2). Sin embargo, cuando un nodo de la red experimenta saturación, utiliza bits especiales en la cabecera para notificar la presencia de congestión:

- **FECN (Forward Explicit Congestion Notification):** El nodo congestionado activa este bit en **1** en las tramas que viajan en el sentido del tráfico (hacia el receptor) para informarle que la ruta está congestionada.
- **BECN (Backward Explicit Congestion Notification):** El nodo congestionado activa este bit en **1** en las tramas que viajan en sentido opuesto (hacia el emisor) para indicarle que debe reducir su velocidad de transmisión.

### 4. Responsabilidad de las Capas Superiores

Dado que Frame Relay descarta silenciosamente las tramas en exceso o por congestión sin retransmitirlas, la detección de pérdidas, el control final de la congestión y la retransmisión de datos quedan delegados por completo a los protocolos de capas superiores (como TCP).


## para que sirve el bit DE en Frame relay
En **Frame Relay**, el bit **DE** (_Discard Eligibility_ o "Elegible para descarte") se ubica en la cabecera de la trama y sirve para clasificar el tráfico y determinar la prioridad de descarte en caso de congestión en la red.

Sus funciones clave son:

- **Marcado de tramas descartables:** Un valor de **`DE = 1`** indica a los conmutadores de la red que esa trama en particular es elegible para ser eliminada si ocurre saturación.
- **Diferenciación entre el tráfico CIR y EIR:** Las tramas que se transmiten dentro del ancho de banda garantizado contratado (_Committed Information Rate_ o **CIR**) viajan con el bit en **`DE = 0`**. Si el usuario transmite tramas que superan la tasa CIR (aprovechando la tasa en exceso o **EIR**), el nodo de ingreso de la red marca esas tramas fijando el bit en **`DE = 1`**.
- **Protección del tráfico garantizado:** Cuando un nodo o conmutador intermedio experimenta congestión, utiliza el bit DE para saber qué paquetes descartar primero. Así, la red elimina en primer lugar las tramas marcadas con `DE = 1` para proteger las tramas con `DE = 0` que forman parte del tráfico garantizado.


## Control de flujo y congestión, que hace frame relay
En **Frame Relay**, el tratamiento del control de flujo y la congestión opera de la siguiente manera:
- **Control de flujo:** Frame Relay **no realiza control de flujo** en la Capa de Enlace (Capa 2). No dispone de ningún mecanismo ni mensajes para indicarle a un emisor que detenga o pause su transmisión si el receptor o la red están sobrecargados.
- **Control de congestión:** Frame Relay **tampoco realiza un control activo de la congestión** ni gestiona retransmisiones en Capa 2. En su lugar, ejecuta únicamente una **notificación explícita de congestión** mediante el marcado de bits en la cabecera de las tramas:
    - **FECN (_Forward Explicit Congestion Notification_):** Un nodo congestionado activa este bit (`FECN = 1`) en las tramas que viajan hacia adelante (en el sentido del tráfico) para notificar al receptor que existe congestión en la ruta.
    - **BECN (_Backward Explicit Congestion Notification_):** El nodo activa este bit (`BECN = 1`) en las tramas que viajan en sentido contrario (hacia el emisor) para indicarle que reduzca su tasa de transmisión.
    - **Bit DE (_Discard Eligibility_):** Permite identificar las tramas transmitidas en exceso por encima de la tasa garantizada (CIR). Si ocurre congestión en algún nodo intermedio, las tramas marcadas con `DE = 1` son las primeras en ser eliminadas para proteger el tráfico garantizado.
- **Delegación a las capas superiores:** Si un conmutador descarta tramas debido a la congestión o al exceso de tráfico, Frame Relay las elimina silenciosamente sin solicitar retransmisión en Capa 2. La detección de la pérdida de datos, la retransmisión y el control efectivo de la congestión quedan delegados a los protocolos de las capas superiores (como **TCP**).

## cada cuanto se realiza la notificación en frame relay
En **Frame Relay**, la frecuencia con la que se realizan las notificaciones depende del **tipo de notificación** dentro de la red:
### 1. Notificaciones de Congestión (FECN y BECN)

- **Frecuencia:** **Basada en eventos (asíncrona y en tiempo real).**
- **Funcionamiento:** No se envían en intervalos de tiempo fijos ni periódicos. Ocurren de manera dinámica en el instante preciso en que la cola de un conmutador supera el umbral de saturación:
    - **FECN (_Forward Explicit Congestion Notification_):** Se marca en `1` en las tramas que viajan en sentido del tráfico hacia el **receptor** mientras dure la congestión.
    - **BECN (_Backward Explicit Congestion Notification_):** Se marca en `1` en las tramas que viajan hacia el **emisor** para notificarle que debe reducir su velocidad de transmisión.

### 2. Evaluación de Tráfico e Intervalo de Medición (\(T_c\))

- **Frecuencia:** **Por cada ventana de tiempo \(T_c\) (_Measurement Interval_).**
- **Funcionamiento:** Para aplicar la función de policía de tráfico y evaluar los parámetros de ancho de banda contratados, la red contabiliza los bits en intervalos de tiempo \(T_c\) (calculados como \(T_c = B_c / \text{CIR}\)). Al finalizar cada ventana \(T_c\), el contador de ráfaga se reinicia para medir el tráfico del siguiente ciclo y determinar qué tramas llevan el bit `DE = 1` (_Discard Eligibility_).

### 3. Notificaciones de Estado del Enlace y PVCs (LMI)

- **Frecuencia:** **Periódica.**
- **Mensajes Keep-alive (Sondeo de enlace):** Se intercambian cada **10 segundos** (por defecto) entre el equipo del usuario (DTE) y el nodo de acceso (DCE) para verificar que la interfaz física continúe operativa.
- **Reporte de Estado Completo (_Full Status Report_):** Se envía cada 6 ciclos de _keep-alive_ (aproximadamente cada **60 segundos**) para informar qué circuitos virtuales permanentes (PVCs) están activos, inactivos o eliminados.
