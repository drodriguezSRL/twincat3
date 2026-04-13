## Buenas prácticas y errores comunes

### ✅ Buenas prácticas

- **Nombra las etapas y transiciones de forma descriptiva**: `Step_Rojo`, `Trans_FinTemporizador` en lugar de `Step0`, `Trans0`.
- **Usa Entry Actions para inicializar** salidas y temporizadores al entrar en una etapa, en lugar de Step Actions. Así evitas que el código de inicialización se ejecute en cada ciclo.
- **Siempre inicializa los temporizadores**: llama al bloque `TON` primero con `IN := FALSE` y luego con `IN := TRUE` en la Entry Action para asegurarte de que el temporizador arranque limpio.
- **Incluye siempre una lógica de reset** usando `SFCInit` o `SFCReset` para poder recuperar el sistema ante fallos.
- **Documenta cada etapa y transición** con comentarios breves que expliquen qué ocurre y qué condición se espera.
- **Evita las transiciones `TRUE` en bucles cerrados** sin ninguna etapa intermedia, ya que pueden causar que el ciclo se ejecute completamente en un único scan y el comportamiento sea impredecible.

### ❌ Errores comunes

| Error | Causa habitual | Solución |
|---|---|---|
| La etapa nunca avanza | La condición de transición nunca es `TRUE` | Revisa la expresión booleana; usa Watch para ver el valor de las variables |
| El temporizador no funciona | El bloque `TON` no se llama cíclicamente | Asegúrate de que la llamada a `TON` está en una Step Action (no solo en Entry) o llámalo también desde MAIN |
| El SFC se queda en Init | La señal `bStart` nunca es `TRUE` | Fuerza la variable en modo Online para verificar |
| Todas las luces están encendidas a la vez | Las salidas no se apagan al cambiar de etapa | Asegúrate de apagar explícitamente las salidas en la Entry Action de cada etapa |
| Error de compilación: "variable no declarada" | Falta declarar una variable de flag SFC | Declara `SFCInit`, `SFCError`, etc. en la zona VAR del POU |
