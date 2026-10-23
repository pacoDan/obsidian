Teniendo en cuenta que en la exposición oral del **TP6** no se proyecta código sintáctico ni scripts, la presentación debe enfocarse en la **metodología de modelado, el análisis estadístico de datos, la lógica del sistema y los resultados comparativos de gestión**.

A continuación se presenta la distribución estratégica de temas para **5 integrantes**:

---

### **1. Integrante 1: Introducción, Contexto Real y Problemática**

- **Presentación del caso de estudio:** Exponer la organización o servicio analizado (por ejemplo, el servicio urbano de grúas).
- **Diagnóstico de la problemática:** Explicar el cuello de botella actual, las fallas operativas o las demoras excesivas que motivaron el estudio.
- **Objetivos del proyecto:** Definir las metas operativas de la simulación (reducir tiempos de espera, optimizar la dotación de personal o evaluar la capacidad del sistema).

### **2. Integrante 2: Modelado Conceptual, Vector de Variables y Eventos**

- **Reglas de negocio y flujo del sistema:** Describir la categorización de solicitudes (ej. urgentes vs. leves, o atenciones por canales digitales/físicos).
- **Definición formal del Vector de Variables:**
    - **Exógenas:** Intervalos entre arribos y tiempos de atención.
    - **De Control:** Recursos y restricciones modificables (cantidad de operadores/grúas asignadas o capacidad máxima de colas).
    - **De Estado:** Entidades o llamadas presentes en el sistema en un instante de tiempo.
    - **De Resultado:** Métricas clave de desempeño (% de no atendidos/arrepentidos, tiempo ocioso y promedio de tiempo de espera).
- **Lógica del modelo evento a evento:** Presentar el diagrama conceptual de flujo o la estructura de las tablas de eventos sin mostrar código fuente.

### **3. Integrante 3: Tratamiento de Datos y Ajuste de Distribuciones (FDPs)**

- **Origen y limpieza del dataset real:** Explicar conceptualmente el procesamiento de datos (homogeneización de textos, corrección de registros mal cargados y filtrado de datos).
- **Ajuste de Funciones de Distribución de Probabilidad (FDP):** Mostrar los histogramas de frecuencia y las FDPs seleccionadas para los arribos y los tiempos de servicio (mencionando herramientas de ajuste como Fitter, Kairos o SciPy Stats).
- **Verificación de parámetros:** Justificar por qué las distribuciones elegidas representan fielmente el comportamiento del sistema real.

### **4. Integrante 4: Experimentos y Análisis Comparativo de Escenarios**

- **Escenario Base / Actual:** Presentar el diagnóstico simulado de la situación de partida y evidenciar el porcentaje de insatisfacción o colapso.
- **Planteo de Escenarios Alternativos:** Exponer las distintas combinaciones probadas al modificar las variables de control (aumentar/reducir personal o ajustar el tamaño de las colas).
- **Tableros de resultados visuales:** Mostrar gráficos y tablas sintetizadas comparando las métricas obtenidas entre escenarios (evitando saturar las diapositivas con números excesivos o tablas ilegibles).

### **5. Integrante 5: Trade-offs Operativos, Recomendación de Gestión y Cierre**

- **Análisis de _trade-offs_:** Discutir el balance entre los costos del sistema (tiempo ocioso de recursos o costos de contratación) y la calidad del servicio (tiempos de espera y atención).
- **Recomendación a la dirección:** Justificar la propuesta óptima de solución según las prioridades del negocio o del cliente (por ejemplo, priorizar casos urgentes o maximizar la satisfacción general).
- **Conclusión y sesión de preguntas:** Cerrar la exposición respetando el tiempo máximo de presentación (habitualmente 10 minutos) y dar paso a las preguntas de los docentes.

---

📊 ¿Querés que diseñemos el contenido específico de las diapositivas para alguno de estos integrantes?