Para reemplazar las costosas y rígidas WAN propietarias tradicionales (como los circuitos dedicados MPLS) utilizando redes públicas (Internet, conexiones de banda ancha, LTE/5G) sin sacrificar la seguridad, la industria ha adoptado arquitecturas y paradigmas modernos.

A continuación se detallan las principales alternativas surgidas, junto con sus arquitecturas, topologías y tecnologías subyacentes:

### 1. Principales Alternativas Tecnológicas

- **SD-WAN (Software-Defined Wide Area Network):** Es la base de conectividad moderna. Desacopla el hardware de red del plano de control, permitiendo utilizar múltiples enlaces públicos de bajo costo de manera inteligente y dinámica.
- **SASE (Secure Access Service Edge):** Unifica la red SD-WAN con funciones de seguridad avanzadas entregadas nativamente desde la nube (Cloud-native). Resuelve el problema de la seguridad en la WAN pública integrando la protección directamente en el borde de servicio.
- **SSE (Security Service Edge):** Subconjunto de SASE enfocado exclusivamente en la capa de seguridad basada en la nube (ideal para organizaciones que ya cuentan con SD-WAN pero necesitan robustecer sus políticas de acceso y protección).

### 2. Arquitecturas Involucradas

- **Arquitectura de Superposición (Overlay Architecture):** Se construye una red lógica virtual (_overlay_) sobre la infraestructura física de transporte público (_underlay_). Los paquetes se encapsulan de forma transparente para viajar de manera segura a través de Internet.
- **Borde de Servicio Distribuido (Cloud-Native PoPs):** A diferencia de las WAN tradicionales (donde todo el tráfico corporativo debía pasar obligatoriamente por un centro de datos centralizado para ser inspeccionado), SASE/SD-WAN distribuyen puntos de presencia (_Points of Presence - PoPs_) globales en la nube. Esto permite aplicar inspección de seguridad cerca del usuario o de la sucursal, optimizando la latencia hacia aplicaciones SaaS y la nube pública.
- **Modelo Zero Trust (Confianza Cero):** La arquitectura abandona la idea del "perímetro seguro de red". Ningún usuario, dispositivo o sucursal es confiable por defecto, por lo que cada conexión y flujo de datos debe ser autenticado y autorizado de forma continua.

### 3. Topologías de Red

- **Topología Híbrida y Multi-transporte:** Combina enlaces de Internet de fibra comercial, conexiones de banda ancha fija y accesos inalámbricos (4G/5G) en una misma sucursal.
- **Malla Dinámica (Dynamic Mesh):** Las sucursales pueden establecer comunicación directa de manera segura entre sí a través de Internet (creando túneles bajo demanda) sin necesidad de retransmitir el tráfico obligatoriamente a través de una sede central o nodo concentrador físico.
- **Centralización de Gestión (Control Plane Centralizado):** Las políticas de seguridad y enrutamiento se definen desde una consola central en la nube y se distribuyen automáticamente (_Zero-Touch Provisioning_) a todos los dispositivos de borde (_Edge_) de la red.

### 4. Tecnologías y Protocolos Clave de Seguridad

- **Cifrado IPsec y TLS:** Creación de túneles virtuales cifrados de extremo a extremo para proteger los datos en tránsito sobre la red pública de Internet.
- **ZTNA (Zero Trust Network Access):** Reemplaza a las tradicionales y vulnerables VPNs de acceso remoto, otorgando acceso granular exclusivamente a aplicaciones específicas según la identidad del usuario y el contexto del dispositivo, en lugar de otorgar acceso a toda la red.
- **FWaaS (Firewall-as-a-Service):** Cortafuegos de nueva generación alojados en la nube que aplican políticas consistentes de filtrado de tráfico e inspección de paquetes (Deep Packet Inspection) sin importar dónde se encuentre el usuario.
- **SWG y CASB (Secure Web Gateway & Cloud Access Security Broker):** Tecnologías integradas para monitorear, bloquear amenazas web y garantizar el cumplimiento normativo en el uso de aplicaciones en la nube y servicios SaaS.