Los atributos de calidad de software se estructuran a través del modelo **ISO/IEC 25000 / 25010**, enfocado en la **visión de producto**. Este estándar clasifica la calidad del producto de software en **8 características principales** y sus correspondientes **sub-características (o sub-atributos)**.

---

### 1. Adecuación Funcional

- **Concepto general:** Representa la capacidad del software para proporcionar funciones que satisfacen las necesidades establecidas e implícitas al ser utilizado bajo condiciones específicas (que el software haga lo que dice que hace).
- **Sub-atributos y conceptos:**
    - **Completitud funcional:** Grado en el que el conjunto de funciones cubre todas las tareas y objetivos especificados por el usuario.
    - **Corrección funcional:** Capacidad de proveer resultados o efectos correctos con el grado de precisión requerido.
    - **Pertinencia funcional:** Grado en que las funciones facilitan la realización de tareas y objetivos específicos de la aplicación.
- **Ejemplo del origen:** Una calculadora debe realizar operaciones matemáticas correctamente (si se pide sumar, debe sumar y no restar ni multiplicar) y no debe incluir funciones ajenas a su propósito, como enviar correos electrónicos.

---

### 2. Eficiencia de Desempeño

- **Concepto general:** Evaluación del desempeño del software en relación con la cantidad de recursos utilizados bajo condiciones determinadas.
- **Sub-atributos y conceptos:**
    - **Comportamiento temporal:** Tiempos de respuesta, procesamiento y latencia de la aplicación.
    - **Utilización de recursos:** Cantidad y tipo de recursos consumidos (memoria RAM, procesador/CPU, ancho de banda).
    - **Capacidad:** Límites máximos de parámetros del sistema (ej. cantidad de usuarios o transacciones en simultáneo).
- **Ejemplo del origen:** Un sistema de venta de entradas para espectáculos masivos o partidos de fútbol que soporta miles de usuarios conectados en simultáneo sin colapsar la memoria ni ralentizar el tiempo de respuesta. Otro caso es el límite explícito de plataformas como SharePoint o bases Access diseñadas para tolerar eficientemente hasta 100.000 registros.

---

### 3. Compatibilidad

- **Concepto general:** Capacidad de dos o más sistemas o componentes para intercambiar información y/o ejecutar sus funciones requeridas compartiendo el mismo entorno de hardware o software.
- **Sub-atributos y conceptos:**
    - **Coexistencia:** Capacidad de compartir un entorno común con otros programas sin afectar negativamente a ninguna de las partes.
    - **Interoperabilidad:** Capacidad de dos o más sistemas para intercambiar información y utilizar los datos intercambiados.
- **Ejemplo del origen:**
    - **Coexistencia:** Un antivirus (como McAfee) instalado en un equipo que no genera conflictos ni cuelga otros software en ejecución.
    - **Interoperabilidad:** Las herramientas del paquete Office, donde se puede copiar una tabla formateada en Excel, pegarla en un correo electrónico y luego volver a pegarla en Excel manteniendo la capacidad de edición.

---

### 4. Usabilidad

- **Concepto general:** Capacidad del software para ser entendido, aprendido, usado y resultar atractivo al usuario bajo condiciones especificadas.
- **Sub-atributos y conceptos:**
    - **Capacidad de aprendizaje:** Sencillez con la que los usuarios aprenden a operar la aplicación.
    - **Reconocimiento de la adecuación:** Facilidad con la que el usuario entiende si el software satisface sus necesidades.
    - **Capacidad de ser usado (Operabilidad):** Facilidad para operar y controlar la interfaz.
    - **Protección contra errores de usuario:** Capacidad de prevenir que el usuario cometa errores o mitigar fallas en la interacción.
    - **Estética de la interfaz de usuario:** Diseño visual e interfaz agradable y apropiada.
    - **Accesibilidad:** Facilidad de uso para personas con diferentes capacidades o limitaciones físicas/cognitivas.
- **Ejemplo del origen:**
    - **Industria pesada vs. oficina:** Diseñar botones grandes para operarios de fábrica que usan guantes de protección.
    - **Cajeros bancarios:** Mantener interfaces optimizadas para el teclado numérico (donde operan a alta velocidad sin mirar) en lugar de imponer el uso del mouse, el cual reduciría su productividad hasta en un 60%.
    - **Manejo de errores:** Evitar mostrar pantallas con errores crudos de código como `segmentation fault` o excepciones de base de datos.

---

### 5. Fiabilidad (Confiabilidad)

- **Concepto general:** Capacidad del sistema o componente para desempeñar sus funciones especificadas bajo condiciones determinadas durante un período especificado.
- **Sub-atributos y conceptos:**
    - **Madurez:** Grado de confiabilidad alcanzado a medida que se detectan y corrigen las fallas a lo largo del tiempo.
    - **Disponibilidad:** Proporción de tiempo en que el sistema se encuentra operativo y accesible.
    - **Tolerancia a fallos:** Capacidad de mantener un nivel aceptable de funcionamiento ante fallos imprevistos de software o hardware.
    - **Capacidad de recuperación:** Rapidez y efectividad para restablecer el servicio y recuperar los datos afectados tras una falla.
- **Ejemplo del origen:** La aplicación móvil de MercadoLibre al escanear códigos QR; si la lectura falla en el primer intento o se escanea un QR inválido, la app muestra un mensaje claro sin congelarse ni cerrarse inesperadamente.

---

### 6. Seguridad

- **Concepto general:** Protección de la información y los datos para que solo las personas o sistemas autorizados tengan acceso a leerlos o modificarlos.
- **Sub-atributos y conceptos:**
    - **Confidencialidad:** Garantía de que los datos no sean accedidos por terceros no autorizados (protección contra filtraciones o hackeos).
    - **Integridad:** Prevención de modificaciones no autorizadas en la información o programas.
    - **No repudio:** Capacidad de probar que una acción ocurrió para impedir que el usuario niegue haberla realizado.
    - **Responsabilidad (Trazabilidad/Rastreabilidad):** Capacidad de rastrear de forma única e inequívoca las acciones realizadas por cada usuario.
    - **Autenticidad:** Verificación estricta de la identidad declarada por el usuario o entidad.
- **Ejemplo del origen:** Aplicaciones bancarias que requieren validación mediante usuario, contraseña y un segundo factor de autenticación (2FA / huella digital), registrando trazas e historiales inalterables para evitar que un cliente sostenga no haber realizado una transacción.

---

### 7. Mantenibilidad

- **Concepto general:** Facilidad con la que el software puede ser modificado para corregir defectos, mejorar el desempeño o adaptarlo a nuevos requerimientos.
- **Sub-atributos y conceptos:**
    - **Modularidad:** Estructuración del software en módulos independientes donde los cambios en uno tienen un impacto mínimo en los demás.
    - **Reusabilidad:** Capacidad de utilizar un componente o activo en más de un sistema o dentro del mismo.
    - **Analizabilidad:** Facilidad para diagnosticar deficiencias, causas de fallas o identificar partes del código a modificar.
    - **Capacidad de ser modificado (Modificabilidad):** Efectividad para implementar un cambio en el código sin introducir fallas secundarias.
    - **Capacidad de ser probado (Testabilidad):** Facilidad para diseñar y ejecutar casos de prueba que verifiquen las modificaciones realizadas.
- **Ejemplo del origen:** En la arquitectura de un banco, donde existen múltiples canales de entrada (cajeros, app móvil, sitio web, transacciones Swift), se utiliza un **único módulo contable reutilizado** para procesar los débitos y créditos en las cuentas, evitando duplicar código en cada canal.

---

### 8. Portabilidad

- **Concepto general:** Capacidad del software para ser transferido de forma eficaz de un entorno de hardware, software u operativo a otro.
- **Sub-atributos y conceptos:**
    - **Adaptabilidad:** Facilidad con la que el software se adapta a diferentes entornos de ejecución especificados.
    - **Capacidad de ser instalado (Instalabilidad):** Sencillez para instalar o desinstalar la aplicación en un entorno objetivo.
    - **Capacidad de ser reemplazado (Reemplazabilidad):** Facilidad para sustituir a otro software que cumple la misma función en el mismo entorno.
- **Ejemplo del origen:** Migrar una aplicación desde un servidor local (_On-Premise_) hacia la nube (como AWS), o realizar despliegues fluidos entre los entornos de _testing_, _staging_ y producción.

---

### Relación de Compromiso entre Atributos (_Trade-offs_)

Un principio clave expresado en el concepto de _**Good Enough Quality**_ es que **no es posible maximizar todos los atributos de calidad al 100% en un mismo proyecto**. Existe un balance (_trade-off_ o "manta corta"): incrementar al máximo la seguridad o la tolerancia a fallas (mediante duplicación de servidores y bases de datos) aumentará drásticamente el consumo de recursos y los costos de desarrollo. Por lo tanto, el equipo técnico y de negocio debe definir prioridades según las necesidades reales del dominio.

💡 **¿Te gustaría que preparemos un informe en PDF o una tabla comparativa en un documento para repasar este modelo antes del examen?**