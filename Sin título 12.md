En las redes de comunicación, los protocolos y servicios **orientados a la conexión** (cuyo máximo exponente en la capa de transporte es **TCP**, y en capas de red/enlace los **circuitos virtuales**) exigen establecer una sesión lógica previa entre emisor y receptor antes de transmitir datos reales, manteniendo el estado de la comunicación y liberándola al finalizar.

---

### 🟢 Ventajas

1. **Garantía de Fiabilidad y Entrega Completa:**
    
    - Al requerir confirmación explícita (**ACK**) para cada segmento o bloque de datos enviado, el sistema detecta pérdidas o errores por temporizador (_timeout_) y **retransmite automáticamente** los paquetes perdidos hasta asegurar una copia fiel de la información.
2. **Reorganización y Entrega Ordenada:**
    
    - Asigna números de secuencia a cada trama o segmento, lo que permite al receptor **reensamblar los datos en el orden exacto de origen**, solucionando la llegada desordenada producida por rutas IP heterogéneas.
3. **Control de Flujo:**
    
    - Utiliza mecanismos de **ventana deslizante** (_sliding window_) para adaptar la tasa de transferencia a la capacidad de procesamiento y almacenamiento en búfer del receptor, evitando la saturación del equipo destino.
4. **Control y Adaptación ante la Congestión:**
    
    - Realiza un seguimiento del estado de la red (_stateful_) y reduce automáticamente el tamaño de la ventana de envío cuando detecta caídas o demoras excesivas en los acuses de recibo.
5. **Verificación Previa del Estado del Receptor:**
    
    - Mediante el intercambio inicial de señales (_3-way handshake_: SYN, SYN-ACK, ACK), se verifica que el destinatario esté activo, disponible y listo para procesar la información antes de transmitir la carga útil.

---

### 🔴 Desventajas

1. **Mayor Retardo e Ineficiencia Inicial (Latencia):**
    
    - El requerimiento de completar el saludo de tres vías (_handshake_) antes de enviar datos, sumado al proceso formal de desconexión de cuatro vías (FIN, ACK), introduce una demora fija de establecimiento y liberación que desacelera las comunicaciones cortas.
2. **Alta Sobrecarga de Red y Procesamiento (_Overhead_):**
    
    - Las cabeceras de control son considerablemente más voluminosas (por ejemplo, mínimo **20 bytes** en TCP frente a 8 bytes en UDP). Además, el constante intercambio de mensajes de confirmación (ACKs) y la gestión de temporizadores consumen mayor ancho de banda y capacidad de CPU en los equipos.
3. **Inadecuado para Aplicaciones en Tiempo Real:**
    
    - En transmisiones de audio o video en vivo (VoIP, streaming interactivo, juegos en línea), las pausas generadas por la retransmisión de un paquete perdido provocan congelamientos o descalces temporales. En estos escenarios es preferible descartar una pequeña pérdida imperceptible a sufrir latencia acumulada.
4. **Mantenimiento de Estado y Consumo de Recursos:**
    
    - Al ser un sistema con estado (_stateful_), los nodos de extremo deben mantener registros activos de secuencias, puertos efímeros y buffers en memoria para cada conexión simultánea, limitando el número total de clientes concurrentes si no se escalan los recursos.

---

💡 **¿Te gustaría que preparemos un cuadro comparativo enfocado en las aplicaciones prácticas donde se justifica elegir TCP sobre UDP y viceversa?**