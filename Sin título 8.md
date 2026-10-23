Las redes de área metropolitana (**MAN**) y de área amplia (**WAN**) corporativas son infraestructuras críticas que permiten a las empresas conectar sus sucursales, centros de datos y oficinas centrales de forma segura y eficiente.

  

Tomando como referencia a los principales operadores de telecomunicaciones del mercado argentino — cuyos nombres de dominio y servicios se pueden verificar en **NIC Argentina** bajo marcas como _telecom.com.ar_, _movistar.com.ar_ o _claro.com.ar_— a continuación se describen estas redes y sus tecnologías subyacentes.

  

### 1. Infraestructura y Cobertura: Redes MAN y WAN Privadas

Las grandes empresas de telecomunicaciones operan **redes WAN troncales** (de alcance nacional e internacional) y **redes MAN** (desplegadas en el ámbito urbano de las principales ciudades).

  

- **Red MAN (Metropolitan Area Network):** Interconecta edificios gubernamentales, sedes bancarias, universidades y antenas celulares dentro de una misma ciudad o área metropolitana mediante anillos de fibra óptica de alta redundancia.
    
      
    
- **Red WAN (Wide Area Network):** Extiende esa conectividad a lo largo de todo el país y el exterior, uniendo las distintas MAN provinciales mediante enlaces troncales terrestres (fibra óptica oscura o iluminada) y enlaces satelitales o subacuáticos.
    
      
    

### 2. Tecnologías Involucradas

#### A. Multiprotocol Label Switching (IP/MPLS)

Es la tecnología clásica y fundamental de transporte para las Redes Privadas Virtuales (VPN-MPLS) que comercializan operadores como Telecom, Movistar y Claro para el sector corporativo.

  

- **Funcionamiento:** En lugar de enrutar cada paquete analizando su dirección IP completa salto por salto, MPLS añade una "etiqueta" corta al paquete en el ingreso de la red. Los routers intermedios conmutan el tráfico basándose únicamente en esa etiqueta, lo que acelera drásticamente el reenvío.
    
      
    
- **Calidad de Servicio (QoS):** Permite priorizar el tráfico crítico (como telefonía IP/VoIP o videoconferencias) por encima del tráfico de datos genérico, garantizando anchos de banda simétricos y baja latencia.
    
      
    

#### B. Redes definidas por software para WAN (SD-WAN)

Actualmente, las operadoras complementan o reemplazan las arquitecturas MPLS tradicionales con **SD-WAN**, una tecnología que desacopla el hardware de red del plano de control.

  

- **Funcionamiento:** Utiliza un controlador centralizado basado en la nube para gestionar de manera inteligente múltiples enlaces de acceso (fibras dedicadas, conexiones 4G/5G corporativas o internet comercial).
    
      
    
- **Ventajas:** Permite rutear de forma dinámica las aplicaciones empresariales por el camino más eficiente en tiempo real, simplifica la administración centralizada de políticas de seguridad y reduce costos operativos frente a los enlaces dedicados tradicionales.
    
      
    

#### C. Ethernet Carrier-Grade (EoMPLS / VPLS)

Tecnología utilizada en las redes MAN para ofrecer servicios de capa 2 (nivel de enlace) transparente entre sucursales distantes de una misma compañía.

  

- **Funcionamiento:** Permite que dos o más oficinas remotas se comporten como si estuvieran conectadas al mismo switch físico local (LAN extendida), facilitando la configuración de redes corporativas sin que la empresa deba administrar enrutadores complejos en cada locación.
    
      
    

_¿Le interesa conocer cómo se estructuran los protocolos de encapsulamiento o la jerarquía de estas redes a nivel de núcleo (Core) y distribución?_