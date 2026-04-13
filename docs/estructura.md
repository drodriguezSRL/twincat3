## Anexo B — Estructura mínima de un proyecto SFC en TwinCAT 3

```
📁 TwinCAT XAE Project
└── 📁 PLC
    └── 📁 PLC_MiProyecto
        ├── 📁 GVLs
        │   └── GVL_IO.TcGVL      ← Variables globales de E/S
        ├── 📁 POUs
        │   ├── MAIN.TcPOU        ← Programa principal (ST): instancia y llama al FB
        │   └── FB_MiSecuencia.TcPOU  ← Function Block en SFC
        └── 📁 TASK CONFIGURATION
            └── PlcTask            ← Tarea cíclica (tiempo de ciclo típico: 10 ms)
```
