## El estándar IEC 61131-3 y los lenguajes de programación PLC

El estándar **IEC 61131-3** define los lenguajes de programación para autómatas programables (PLCs).  

Establece cinco lenguajes:

| Lenguaje | Tipo | Descripción breve |
|---|---|---|
| **LD** — Ladder Diagram | Gráfico | Diagrama de contactos. Similar a circuitos eléctricos. |
| **FBD** — Function Block Diagram | Gráfico | Bloques de función interconectados. |
| **SFC** — Sequential Function Chart | Gráfico | Diagrama de etapas y transiciones para secuencias. |
| **ST** — Structured Text | Texto | Similar a Pascal/C. Muy versátil. |
| **IL** — Instruction List | Texto | Lista de instrucciones de bajo nivel (en desuso). |

En este manual nos centraremos en **SFC**, aunque veremos que las acciones de cada etapa pueden programarse en **ST**, lo que hace del SFC un lenguaje muy potente y flexible.

### Unidades de organización de programa (POUs)

En TwinCAT 3 el código se organiza en **POUs** (Program Organization Units):

- **PROGRAM**: se ejecuta cíclicamente desde la tarea. Es el punto de entrada principal.
- **FUNCTION\_BLOCK**: bloque reutilizable con estado interno (variables persistentes entre ciclos).
- **FUNCTION**: bloque sin estado; siempre devuelve el mismo resultado ante las mismas entradas.
