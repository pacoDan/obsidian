He generado la representación gráfica esquemática comparativa entre un **sistema orientado a la conexión (TCP)** y un **sistema sin conexión (UDP)**, la cual ya se encuentra disponible en tu panel de Studio como `esquema_conexion_vs_sin_conexion.png`.

---

### Explicación del Esquema

```
========================================================================================
SISTEMA ORIENTADO A LA CONEXIÓN (TCP)        SISTEMA SIN CONEXIÓN (UDP)
========================================================================================
Cliente TCP              Servidor TCP       Emisor UDP              Receptor UDP
    │                         │                 │                         │
    ├─ 1. SYN (Seq = x) ─────>│                 ├─ Datagrama 1 ──────────>│
    │<─ 2. SYN-ACK ───────────┤                 ├─ Datagrama 2 ──────────>│
    ├─ 3. ACK ───────────────>│                 ├─ Datagrama 3 (PÉRDIDA) ─X  (Sin retransmisión)
    │                         │                 ├─ Datagrama 4 ──────────>│
    │ [Sesión Establecida]    │                 │                         │
    ├─ Datos (Seq, Payload) ─>│                 └─ (Sin Handshake, Sin ACK, Sin Estado)
    │<─ ACK (AckNum) ─────────┤
    │                         │
    ├─ FIN ──────────────────>│
    │<─ ACK ──────────────────┤
    │<─ FIN ───────────────-──┤
    ├─ ACK ──────────────────>│
    │ [Sesión Liberada]       │
========================================================================================
```

---

### 1. Sistema Orientado a la Conexión (TCP)

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

---

### 2. Sistema Sin Conexión (UDP)

En UDP, la comunicación es directa, liviana y sin conservación de estado (_stateless_):

- **Sin Handshake ni Inicio:** El emisor envía los datagramas inmediatamente a la red sin verificar previamente si el receptor está activo o en condiciones de recibirlos.
- **Sin ACKs ni Retransmisiones:** No existen mensajes de acuse de recibo. Si un datagrama se pierde en la red debido a congestión o fallos, el protocolo de transporte lo ignora y no lo retransmite.
- **Sin Cierre Formal:** Al no existir una sesión o canal lógico abierto, no hay intercambio de banderas de finalización.
- **Mínimo Overhead:** La cabecera fija es de solo **8 bytes** (frente a los 20 bytes mínimos de TCP), lo que reduce drásticamente la latencia y el procesamiento de red.

---

💡 **¿Te gustaría que analicemos una captura de Wireshark para observar las banderas TCP (SYN, ACK, FIN) o un flujo UDP directamente sobre el tráfico de red real?**