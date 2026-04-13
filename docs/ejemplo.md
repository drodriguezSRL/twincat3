## Ejemplo práctico: Semáforo secuencial

En este ejemplo programaremos un semáforo simple con tres luces (rojo, ámbar, verde) con los siguientes tiempos:

| Fase | Luz | Duración |
|---|---|---|
| 1 | 🔴 Rojo | 5 segundos |
| 2 | 🟡 Ámbar | 2 segundos |
| 3 | 🟢 Verde | 5 segundos |
| 4 | 🟡 Ámbar | 2 segundos |
| → vuelta al paso 1 | | |

### Diagrama SFC resultante

```
         [Init]          ← Etapa inicial (doble borde)
            │
         [bStart]        ← Transición: espera señal de inicio
            │
       [Step_Rojo]       ← Enciende luz roja
            │
   [tTempRojo.Q / 5s]    ← Transición: espera 5 segundos
            │
      [Step_Ambar1]      ← Enciende luz ámbar
            │
   [tTempAmbar.Q / 2s]   ← Transición: espera 2 segundos
            │
      [Step_Verde]       ← Enciende luz verde
            │
   [tTempVerde.Q / 5s]   ← Transición: espera 5 segundos
            │
      [Step_Ambar2]      ← Enciende luz ámbar
            │
   [tTempAmbar2.Q / 2s]  ← Transición: espera 2 segundos
            │
         [Jump]          ← Salto de vuelta a Step_Rojo
```

### Declaración de variables del FB_Semaforo

```pascal
FUNCTION_BLOCK FB_Semaforo
VAR_INPUT
    bStart  : BOOL;
    bReset  : BOOL;
END_VAR
VAR_OUTPUT
    bRojo   : BOOL;
    bAmbar  : BOOL;
    bVerde  : BOOL;
END_VAR
VAR
    tRojo    : TON;
    tAmbar1  : TON;
    tVerde   : TON;
    tAmbar2  : TON;
    SFCInit  : BOOL;   (* Flag de reset del SFC *)
END_VAR
```

### Acciones de cada etapa

**Entry action de `Step_Rojo`** (se ejecuta una sola vez al entrar):

```pascal
bRojo  := TRUE;
bAmbar := FALSE;
bVerde := FALSE;
tRojo(IN := FALSE, PT := T#5S);
tRojo(IN := TRUE,  PT := T#5S);
```

**Entry action de `Step_Ambar1`**:

```pascal
bRojo  := FALSE;
bAmbar := TRUE;
bVerde := FALSE;
tAmbar1(IN := FALSE, PT := T#2S);
tAmbar1(IN := TRUE,  PT := T#2S);
```

**Entry action de `Step_Verde`**:

```pascal
bRojo  := FALSE;
bAmbar := FALSE;
bVerde := TRUE;
tVerde(IN := FALSE, PT := T#5S);
tVerde(IN := TRUE,  PT := T#5S);
```

**Entry action de `Step_Ambar2`**:

```pascal
bRojo  := FALSE;
bAmbar := TRUE;
bVerde := FALSE;
tAmbar2(IN := FALSE, PT := T#2S);
tAmbar2(IN := TRUE,  PT := T#2S);
```

### Condiciones de transición

| Transición | Condición |
|---|---|
| Init → Step_Rojo | `bStart` |
| Step_Rojo → Step_Ambar1 | `tRojo.Q` |
| Step_Ambar1 → Step_Verde | `tAmbar1.Q` |
| Step_Verde → Step_Ambar2 | `tVerde.Q` |
| Step_Ambar2 → (jump) Step_Rojo | `tAmbar2.Q` |

### Instanciar el Function Block en MAIN

Abre el POU **MAIN** (lenguaje ST) y escribe:

```pascal
PROGRAM MAIN
VAR
    instSemaforo : FB_Semaforo;
END_VAR

(* Gestión del reset *)
instSemaforo.bReset := GVL_IO.bReset;
instSemaforo.SFCInit := GVL_IO.bReset;

(* Señal de inicio *)
instSemaforo.bStart := GVL_IO.bStart;

(* Llamada al Function Block *)
instSemaforo();

(* Mapear salidas *)
GVL_IO.bRojo  := instSemaforo.bRojo;
GVL_IO.bAmbar := instSemaforo.bAmbar;
GVL_IO.bVerde := instSemaforo.bVerde;
```

> `[CAPTURA SUGERIDA: Diagrama SFC completo del semáforo en el editor de TwinCAT, con los cuatro pasos visibles y los saltos de retorno]`

---
