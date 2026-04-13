## Ejercicios propuestos

### Ejercicio 1 — Semáforo con modo nocturno ⭐

Amplía el semáforo del ejemplo con un modo nocturno: cuando la entrada `bNoche` sea `TRUE`, el semáforo debe parpadear únicamente la luz ámbar cada segundo, ignorando el ciclo normal. Usa una **ramificación alternativa** para seleccionar entre el modo diurno y nocturno.

### Ejercicio 2 — Control de una cinta transportadora ⭐⭐

Diseña un SFC que controle una cinta transportadora con las siguientes especificaciones:
- Al pulsar `bStart`, la cinta (`bMotor`) arranca.
- Un sensor de presencia (`bSensorFin`) detecta cuando una pieza llega al final.
- Al detectar la pieza, la cinta se detiene 3 segundos, luego un pistón (`bPiston`) avanza, espera 2 segundos, retrocede y la cinta vuelve a arrancar.
- Un pulsador de emergencia `bStop` detiene todo inmediatamente y reinicia la secuencia.

### Ejercicio 3 — Llenado de depósito ⭐⭐

Programa el control de llenado de un depósito con:
- Electroválvula de entrada (`bValvulaEntrada`) y de salida (`bValvulaSalida`).
- Sensor de nivel bajo (`bNivelBajo`) y nivel alto (`bNivelAlto`).
- La secuencia: abrir válvula de entrada → esperar nivel alto → cerrar entrada → abrir salida → esperar nivel bajo → cerrar salida → repetir.

### Ejercicio 4 — Control paralelo de dos cintas ⭐⭐⭐

Diseña un SFC con **ramificación paralela** que controle dos cintas transportadoras independientes que deben sincronizarse al final: la línea principal no puede continuar hasta que ambas cintas hayan procesado su pieza correspondiente.