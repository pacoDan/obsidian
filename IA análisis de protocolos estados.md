En el **análisis de protocolos** y la ingeniería del conocimiento, los **estados** representan las distintas situaciones, conclusiones o diagnósticos intermedios y finales por los que transita la mente del especialista a lo largo de su proceso de razonamiento para resolver un problema.

---

### 1. Conceptualización como espacio de estados

El proceso de resolución del experto se modela como la navegación por un **espacio de estados**:

- **Estado inicial:** Corresponde al punto de partida donde no se conoce la solución o el diagnóstico.
- **Estados intermedios:** Hipótesis, deducciones preliminares o diagnósticos provisionales que el especialista va formulando a medida que analiza la información inicial (por ejemplo, pensar que un paciente presenta _coronavirus/COVID-19_).
- **Estado meta o final:** La solución definitiva o diagnóstico concluyente al que arriba el experto (por ejemplo, determinar que se trata de _gripe clase A_ o reconocer que la madera es un _abeto_).

---

### 2. Su rol en las etapas del análisis de protocolos

- **Relación con los operadores y condiciones:** Para transitar de un estado a otro (o de la incertidumbre inicial a un nuevo estado), el especialista utiliza un **operador**, que es la frase o medio verbal que permite ese pasaje. A su vez, para alcanzar cada estado se evalúan **condiciones** específicas del dominio (como los síntomas observados o las características y valores del objeto de estudio).
- **Correspondencia 1 a 1 con las reglas:** En la etapa de interpretación, cada estado genera una regla de razonamiento independiente. Por convención metodológica, en un protocolo debe mantenerse una estricta consistencia: **la cantidad de estados debe ser igual a la cantidad de operadores y a la cantidad de reglas de razonamiento**.
- **Forma de representación en la codificación:** Al estructurar los elementos del protocolo, el analista puede clasificarlos de dos formas válidas según su preferencia:
    1. **Como conceptos:** Se ubican en la tabla como conceptos independientes, lo que luego exige explicitar sus relaciones con la entidad principal mediante _relaciones implícitas_ (por ejemplo, `paciente puede tener coronavirus`).
    2. **Como valores:** Se sitúan como valores de una característica implícita asociada al concepto principal (por ejemplo, asociando a `paciente` la característica implícita `diagnóstico` con valores `COVID-19` y `gripe clase A`), en cuyo caso esa relación ya queda cubierta dentro de la tabla y no se repite en las relaciones implícitas.

---

### 3. Consideraciones clave sobre los estados

- **Tratamiento atómico:** En el protocolo, los estados y las condiciones requeridas para alcanzarlos se analizan de manera **atómica e independiente**; no se anidan ni se encadenan como un árbol de búsqueda. Su integración y dependencia mutua se modela posteriormente en etapas avanzadas mediante herramientas como el _mapa de conocimientos_.
- **Vínculo con las incertidumbres:** Las incertidumbres señaladas en el protocolo no se aplican a cualquier duda lingüística, sino exclusivamente a aquellas expresiones verbales asociadas a un **cambio de estado** (por ejemplo, giros en potencial como _«podríamos pensar que»_ o _«estaríamos ante un»_).
- **Alineación con el objetivo del protocolo:** Todos los estados identificados deben responder estrictamente al **objetivo único** definido para el protocolo (si el objetivo es determinar un diagnóstico clínico, los estados deben ser patologías; si es identificar un tipo de madera, deben ser especies forestales).

---

🌿 Si querés, podemos revisar cómo se distingue formalmente un **operador** de una simple **relación** o de una **incertidumbre** al momento de marcar el cambio de estado en la transcripción.