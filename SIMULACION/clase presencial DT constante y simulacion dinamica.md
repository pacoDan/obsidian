A continuación se presenta la recopilación estructurada de todo el contenido de la clase sobre **Modelos de Simulación y Dinámica de Sistemas**, dividida en preguntas y respuestas, estructura temática y recopilación de tips y recomendaciones.

---

### 1. Recopilación de Preguntas y Respuestas

#### **Ejercicio 1: El Proveedor de Leche**

- **P: Al leer un enunciado donde los datos están dados por unidad de tiempo (ej. 300 a 400 litros por día), ¿qué es lo primero que se destaca?**
    - **R:** Destaca que la Función de Densidad de Probabilidad (FDP) está expresada como una **densidad** (cantidad por unidad de tiempo). Esto indica que se trata de un problema de **\(\Delta t\) constante** (con \(\Delta t = 1\) día).
- **P: ¿Cuál es la definición de una variable de estado?**
    - **R:** Es aquella variable que permite observar cómo evoluciona la situación del sistema a lo largo del tiempo, aumentando o disminuyendo debido a la ocurrencia de eventos.
- **P: En el problema del proveedor de leche, ¿por qué el stock de leche NO se tomó como variable de estado?**
    - **R:** Porque al final de cada \(\Delta t\) (cada día) la leche no vendida se derrocha. Por lo tanto, no existe un stock físico que se acumule día a día.
- **P: ¿Qué variable se eligió en su lugar como variable de estado?**
    - **R:** El **beneficio acumulado** (el dinero que ingresa diariamente).
- **P: ¿Qué eventos hacen aumentar y disminuir dicha variable de estado?**
    - **R:** Lo hacen aumentar las **ventas**, y lo hacen disminuir el **faltante** y el **desperdicio**.
- **P: Si se simulan 30.000 o 300.000 días, ¿sirve informar el beneficio acumulado como resultado final?**
    - **R:** No, porque el valor acumulado depende totalmente del tiempo final de simulación (\(T_F\)) elegido. Lo adecuado es informar un resultado en un período estandarizado más corto, como el **beneficio promedio mensual** (o diario multiplicado por 30).

#### **Ejercicio 2: Empresa Constructora y Ladrillos**

- **P: ¿Cuál es la variable de estado en el problema de la constructora?**
    - **R:** El **stock de ladrillos**, dado que los ladrillos no se tiran al final de la jornada sino que se acumulan y evolucionan en la obra.
- **P: ¿Cuándo es un error definir el beneficio como variable de estado?**
    - **R:** Cuando existe un stock físico real en el problema que evoluciona con el tiempo. A partir de ese stock físico se deben calcular posteriormente los beneficios o costos.

#### **Ejercicio 3: Depósito y Estrategias de Simulación**

- **P: Si un problema tiene intervalos de arribo en minutos, ¿por qué no conviene resolverlo siempre por \(\Delta t\) constante de 1 minuto?**
    - **R:** Por **eficiencia computacional**. Con \(\Delta t = 1\) minuto se procesan muchísimos ciclos donde no ocurre ningún evento, mientras que la simulación **evento a evento** salta directamente a los instantes donde hay cambios, siendo mucho más eficiente.
- **P: En la comparativa de ejercicios de stock, ¿qué distingue al Caso 3 frente al Caso 2?**
    - **R:** En el Caso 3, aunque las ventas ocurren en minutos, la demora del proveedor y el costo de almacenamiento están en días. Por la **granularidad de los costos**, se resuelve como \(\Delta t\) constante de 1 día, pero utiliza una **subrutina interna de eventos** para calcular las ventas diarias acumuladas en el lapso laboral (ej. 8 horas = 480 minutos).

#### **Dinámica de Sistemas y Diagramas de Bloques**

- **P: ¿Qué instrumento matemático describe un sistema donde el estado actual es igual al anterior más las entradas menos las salidas por el \(\Delta t\)?**
    - **R:** Un **sistema de ecuaciones diferenciales**, resuelto mediante métodos numéricos integrados como Euler o Runge-Kutta (de 2º y 4º orden).
- **P: ¿Quién desarrolló la Dinámica de Sistemas y qué herramientas utiliza?**
    - **R:** Fue desarrollada por Jay Forrester (MIT), siendo la única técnica de simulación creada por un ingeniero de sistemas. Utiliza diagramas causales y diagramas de bloques (software como Stella/Ithink).
- **P: ¿Cuáles son los 4 elementos principales de un diagrama de bloques?**
    - **R:**
        1. **Variable de Almacenamiento (Stock / Caja):** Representa variables de estado, acumuladores, contadores o registros.
        2. **Variable de Flujo (Flow / Flecha con válvula):** Modifica los almacenes haciendo aumentar o disminuir su nivel.
        3. **Función / Constante (Converter / Pelotita):** Contiene constantes, FDP, variables de control o cálculos auxiliares.
        4. **Conector (Flecha simple):** Une elementos para transmitir información o dependencia matemática.

---

### 2. Estructura del Contenido de la Clase

#### **I. Revisión de Ejercicios y Enfoques de Simulación Discreta**

1. **Modelos con \(\Delta t\) Constante puro:**
    - Detección mediante datos en **densidades** (cantidad/unidad de tiempo).
    - Criterios de elección de Variable de Estado según la persistencia del recurso.
    - Presentación de resultados independientes del \(T_F\) (mensualización/promedios).
2. **Modelos Evento a Evento:**
    - Justificación por **eficiencia computacional** (eliminación de \(\Delta t\) inactivos).
3. **Modelos Híbridos (\(\Delta t\) Constante con Subrutinas Internas de Eventos):**
    - Determinación según la **granularidad de costos** (ej. costos por día).
    - Manejo de jornadas laborales limitadas (ej. 8 horas/día) mediante bucles internos de minutos.

#### **II. Fundamentos de Dinámica de Sistemas (System Dynamics)**

1. **Origen y Conceptos:**
    - Aportes de Jay Forrester (MIT).
    - De diagramas causales a diagramas de bloques.
    - Modelado continuo basado en **sistemas de ecuaciones diferenciales** y métodos numéricos (Euler, Runge-Kutta 2º/4º orden).
2. **Software de Aplicación:**
    - Uso de **Stella / Ithink** (mención de Vensim, Powersim, ProModel).

#### **III. Construcción e Implementación en Stella/Ithink**

1. **Elementos del Diagrama de Bloques:**
    - **Stock (Caja):** Ecuaciones diferenciales, inicialización obligatoria (`init stock`), uso como variables de estado, acumuladores o guardado de fechas (`FLL`).
    - **Flow (Flujo):** Tasas de entrada/salida.
    - **Converter (Pelotita):** FDP, constantes y variables de control.
    - **Connector (Flecha):** Relaciones de información.
2. **Solapas del Software:**
    - _Map / Lienzo:_ Diagramación visual libre.
    - _Model:_ Detección de errores y parámetros pendientes.
    - _Equation:_ Generación automática y edición de ecuaciones (`IF...THEN...ELSE`).
    - _Interface:_ Inclusión de _sliders_ (potenciómetros) para simular variando variables de control y generación de gráficos.
3. **Parámetros de Ejecución (`Run Specs`):**
    - Configuración de \(T_F\), \(\Delta t\), método de integración numérica y control de memoria.

---

### 3. Recopilación de Tips y Recomendaciones de la Cátedra

1. **Tip de Detección de Técnica (\(\Delta t\) Constante vs. Evento):**
    - Si los datos están expresados como una cantidad por unidad de tiempo (densidad), el problema debe encararse por **\(\Delta t\) constante**.
    - Si se cobra o restringe por día o por minuto, la **granularidad del costo** define la unidad mínima de tiempo que se puede utilizar en la simulación. No reduzcas la escala de tiempo si el costo está prefijado en una unidad mayor.
2. **Criterio para elegir la Variable de Estado:**
    - **Regla del desperdicio:** Si el recurso no vendido/sobrante se destruye o se vacía al final del período, la variable de estado pasa a ser el **beneficio acumulado**.
    - **Regla del stock físico:** Si el recurso físico permanece de un día para otro, la variable de estado **debe ser el stock físico**. Nunca pongas el beneficio como variable de estado si hay un stock real evolucionando.
3. **Escribir Eventos correctamente:**
    - Escribe siempre los nombres de los eventos comenzando con un **verbo en infinitivo** (ej.: _Recibir ladrillos_, _Emitir pedido_, _Vender productos_).
4. **Uso de Stocks Auxiliares en Dinámica de Sistemas:**
    - Recuerda que los Stocks (cajas) no solo sirven para representar variables de estado físicas o financieras; también son indispensables para construir **acumuladores, contadores de ocurrencias, registros de máximos/mínimos y almacenamiento de fechas futuras de arribo (`FLL`)**.
5. **Reglas de Diagramación estricta (Cuidado en el Parcial):**
    - **Conexiones exactas:** Asegúrate de que las flechas y conectores toquen exactamente el borde del elemento al que llegan. Las imprecisiones visuales en los diagramas de bloques son penalizadas en la corrección.
    - **Ingresos a un Stock:** Ninguna variable auxiliar o constante puede ingresar directamente a una caja/Stock; todo cambio en un Stock debe pasar obligatoriamente a través de una **Variable de Flujo**.
    - **Inicialización:** Cada caja agregada requiere un valor inicial (`init stock`). Si el elemento muestra un signo de interrogación, significa que falta definir su valor o ecuación inicial.
6. **Reporte de Resultados:**
    - En lugar de presentar beneficios acumulados totales (que cambian según los días simulados \(T_F\)), expresa las variables de resultado de forma estandarizada: **mensual, semanal o diaria**.
7. **Diferenciación conceptual para el Parcial:**
    - Ten clara la diferencia en las consignas entre un **Diagrama de Flujo** (condiciones iniciales, decisiones y procesos de simulación discreta) y un **Diagrama de Bloques** (Stocks, Flujos y Convertidores de Dinámica de Sistemas).
    - Recuerda que el examen parcial será de carácter **evaluativo e integrador**.
