# Introducción a TwinCAT3 con SFC

> **Creado por:** David Rodríguez Martínez y Claude AI  
> **Asignatura:** Automatización Industrial  
> **Nivel:** Grado Universitario  
> **Herramienta:** Beckhoff TwinCAT 3 (XAE)  
> **Lenguaje:** Sequential Function Chart (SFC) — IEC 61131-3

## Introducción a TwinCAT3

**TwinCAT** (The Windows Control and Automation Technology) es la plataforma de automatización software desarrollada por **Beckhoff Automation**. Su tercera versión (TwinCAT 3) transforma prácticamente cualquier PC con Windows en un controlador en tiempo real capaz de ejecutar lógica PLC, control de movimiento (NC/CNC) y robótica.

### ¿Por qué TwinCAT3?

- Se integra como un plugin dentro de **Microsoft Visual Studio**, unificando en un único entorno la programación, la configuración hardware y el diagnóstico.
- Soporta todos los lenguajes del estándar **IEC 61131-3** (LD, FBD, ST, IL y SFC), así como **C/C++**, MATLAB® y Simulink®.
- Dispone de una versión **gratuita de ingeniería (XAE)** descargable desde la web de Beckhoff, ideal para el aprendizaje sin necesidad de hardware real.
- Es ampliamente usado en la industria europea, lo que hace que su dominio sea un valor diferencial en el mercado laboral.


>💡 _El estándar **IEC 61131-3** es la parte 3 de la norma internacional IEC 61131, dedicada específicamente a los lenguajes de programación para autómatas programables (PLCs), con el objetivo principal de que un ingeniero pueda programar PLCs de distintos frabricantes con los mismos conceptos y lenguajes, reduciendo la curva de aprendizaje y facilitando el mantenimiento del código industrial. En esencia, establece:_  
> - _Cinco lenguajes de programación estandarizados (LD, FBD, ST, IL y SFC) que cualquier fabricante de PLCs puede implementar, garantizando portabilidad y uniformidad._  
> - _Los tipos de datos básicos y compuestos que deben estar disponibles (BOOL, INT, REAL, TIME, STRING, arrays, structs…)._  
> - _Los tipos de POUs o "program organization units" (Program, Function Block, Function) y cómo se organizan y comunican entre sí._  
> - _El modelo de ejecución: ciclo de scan, tareas, y cómo se instancian y llaman los bloques de función._
> - _Variables y su alcance: locales, globales, de entrada/salida, remanentes, etc._  

### Componentes principales

| Componente | Descripción |
|---|---|
| **TwinCAT XAE** | Entorno de desarrollo (_eXtended Automation Engineering_). Basado en Visual Studio. |
| **TwinCAT XAR** | Runtime en tiempo real (_eXtended Automation Runtime_). Ejecuta el código de control. |
| **TwinCAT PLC** | Módulo de programación PLC dentro del XAE. |
| **I/O** | Módulo de configuración de hardware y mapeo de variables. |

![TwinCAT Interface](/docs/img/twinCAT_interface.png)
