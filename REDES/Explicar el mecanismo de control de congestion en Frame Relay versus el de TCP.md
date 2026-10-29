El mecanismo de control de congestión difiere sustancialmente entre **Frame Relay** y **TCP**, debido a que operan en capas distintas del modelo de red y aplican filosofías opuestas para el manejo del tráfico en exceso y la pérdida de datos.

---

### 1. Control de Congestión en Frame Relay (Capa 2)

En la Capa de Enlace (Capa 2), Frame Relay **no realiza un control activo de la congestión ni efectúa retransmisiones** de tramas en los conmutadores de la red. En su lugar, utiliza un esquema de **notificación explícita de congestión** y **descarte selectivo**:

- **Notificación Explícita de Congestión (FECN y BECN):** Cuando la cola de un nodo de la red se satura, el conmutador no detiene el tráfico, sino que marca bits especiales en las cabeceras de las tramas que circulan por él:
    - **FECN (_Forward Explicit Congestion Notification_):** Se activa en `1` en las tramas que viajan hacia adelante (hacia el receptor) para avisarle que la ruta por la que transitan experimenta congestión.
    - **BECN (_Backward Explicit Congestion Notification_):** Se activa en `1` en las tramas que viajan en sentido contrario (hacia el emisor) para avisarle directamente al origen que debe reducir su velocidad de transmisión.
- **Elegibilidad de Descarte (Bit DE):** El nodo de ingreso clasifica el tráfico que supera la tasa garantizada (CIR) dentro de la ráfaga en exceso (EIR) fijando el bit **`DE = 1`** (_Discard Eligibility_). Si surge congestión en algún conmutador intermedio, las tramas marcadas con `DE = 1` son las primeras en ser eliminadas para resguardar el tráfico garantizado (`DE = 0`).
- **Delegación a las capas superiores:** Si la congestión fuerza el descarte de tramas, Frame Relay las elimina de manera silenciosa sin solicitar retransmisión en Capa 2. Delega por completo la detección de la pérdida, la retransmisión y la reducción efectiva de la velocidad de transmisión a los protocolos de transporte de capas superiores como TCP.

---

### 2. Control de Congestión en TCP (Capa 4)

En la Capa de Transporte (Capa 4), TCP aplica un **control activo de congestión de extremo a extremo** administrado de forma independiente por los hosts (emisor y receptor). Para ajustar dinámicamente la tasa de transmisión y evitar saturar la red, TCP evalúa la **Ventana de Congestión (`cwnd`)**:

- **Ventana Permitida:** La cantidad de datos que el emisor puede enviar sin esperar confirmación se calcula como el valor mínimo entre la ventana de congestión y el crédito otorgado por el receptor: \[\text{Ventana Permitida} = \min(\text{Ventana de Congestión}, \text{Crédito de Recepción})\]
- **Algoritmo de Comienzo Lento (_Slow Start_):** Al iniciar una conexión, la ventana de congestión comienza en un valor pequeño (`cwnd = 1` segmento). Por cada confirmación (ACK) recibida con éxito, la `cwnd` se incrementa en uno, aumentando exponencialmente el flujo de datos enviados por RTT para sondear la capacidad de la red.
- **Reacción ante Temporizador Agotado (RTO / _Timeout_):** Si la red se congestiona severamente y se pierde un paquete provocando que caduque el temporizador de retransmisión (RTO), TCP asume una congestión grave, reinicia la ventana de congestión a `cwnd = 1` y vuelve a ejecutar el comienzo lento (_slow start_).
- **Retransmisión Rápida (_Fast Retransmit_):** Si el emisor recibe 3 confirmaciones (ACKs) duplicadas para el mismo segmento, deduce que ese paquete específico se perdió mientras los demás continúan fluyendo, y retransmite inmediatamente el segmento faltante sin esperar a que expire el RTO.
- **Recuperación Rápida (_Fast Recovery_):** Tras ejecutar una retransmisión rápida por 3 ACKs duplicados, TCP no reinicia la ventana a 1 segmento, sino que reduce la `cwnd` a la mitad y continúa transmitiendo, evitando la caída drástica del rendimiento y previniendo el fenómeno de sincronización global.

### 3. Cuadro Comparativo

|Característica|Frame Relay|TCP|
|:--|:--|:--|
|**Capa del Modelo**|Capa 2 (Enlace de Datos).|Capa 4 (Transporte).|
|**Ubicación de la Gestión**|Nodos intermedios / Conmutadores de la red.|Equipos terminales / Hosts de extremo a extremo.|
|**Estrategia ante Congestión**|Notificación explícita (FECN/BECN) y descarte selectivo (bit DE = 1).|Ajuste dinámico de la ventana de congestión (`cwnd`) y retransmisión de datos.|
|**Retransmisión de Pérdidas**|**No retransmite** en Capa 2; elimina la trama.|**Retransmite automáticamente** los segmentos perdidos (ARQ).|
|**Mecanismos Clave**|Bits FECN, BECN, DE, ancho de banda CIR / EIR.|_Slow Start_, _Fast Retransmit_, _Fast Recovery_, RTO.|

