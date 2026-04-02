# 🤖 Bot RPA de Automatización de Reportes

Automatización del procesamiento de archivos CSV usando **Power Automate Desktop** como orquestador y **Python** para el procesamiento de datos y generación de reportes Excel.

---

**Tecnologías utilizadas:**
- 🔵 Power Automate Desktop — orquestación del flujo RPA
- 🐍 Python — procesamiento de datos y generación de reportes
- 📊 pandas — manipulación de datos
- 📁 openpyxl — generación y formato de archivos Excel

---

##  Arquitectura del flujo

```
[Power Automate Desktop]
        │
        ▼
Detecta archivo CSV nuevo en carpeta /input
        │
        ▼
Ejecuta script Python con la ruta del archivo
        │
        ▼
Python procesa el CSV y genera reporte Excel en /output
        │
        ▼
Power Automate mueve el CSV a /procesados
        │
        ▼
Notificación de éxito o error en pantalla
```

---

##  Estructura del proyecto

```
rpa-reporte-bot/
├── input/              # Carpeta de entrada — depositar CSVs aquí
├── output/             # Reportes Excel generados
├── procesados/         # CSVs ya procesados (historial)
├── procesar.py         # Script Python principal
├── requirements.txt    # Dependencias Python
└── README.md
```

---

##  Instalación

### 1. Clonar el repositorio

```bash
git clone https://github.com/tu-usuario/rpa-reporte-bot.git
cd rpa-reporte-bot
```

### 2. Instalar dependencias Python

```bash
pip install -r requirements.txt
```

### 3. Instalar Power Automate Desktop

Disponible gratuitamente para Windows 10/11:  
🔗 https://flow.microsoft.com/desktop

---

##  Configuración del flujo en Power Automate Desktop

Crear un nuevo flujo con las siguientes acciones:

| # | Acción | Configuración |
|---|--------|--------------|
| 1 | Obtener archivos en carpeta | Ruta: `C:\rpa-reporte-bot\input`, Filtro: `*.csv` |
| 2 | For each | Variable: `%ArchivosCSV%` |
| 3 | Ejecutar aplicación | App: `python`, Args: `C:\rpa-reporte-bot\procesar.py %CurrentItem.FullName%` |
| 4 | If (condición) | `%ResultadoPython% contains 'REPORTE_OK'` |
| 5 | Mover archivo | Destino: `C:\rpa-reporte-bot\procesados\` |
| 6 | Mostrar notificación | Mensaje de éxito o error según resultado |

---

##  Uso

1. Colocar uno o varios archivos `.csv` en la carpeta `input/`
2. Ejecutar el flujo desde Power Automate Desktop
3. El reporte Excel aparecerá en la carpeta `output/` con timestamp
4. El CSV original se moverá automáticamente a `procesados/`

### Formato esperado del CSV de entrada

```
nombre,ventas,region
Ana,1500,Norte
Carlos,2300,Sur
...
```

---

## 📊 Output generado

Cada ejecución genera un archivo `.xlsx` con dos hojas:

- **Datos** — tabla completa con los datos procesados y columna de origen
- **Resumen** — cantidad de filas procesadas por archivo

Los encabezados tienen formato destacado (fondo azul oscuro, texto blanco).

---

## 🧠 Conceptos demostrados

- Integración entre herramienta RPA y script Python
- Orquestación de procesos con Power Automate Desktop
- Manejo de errores y notificaciones en flujos RPA
- Procesamiento y consolidación de datos con pandas
- Generación de reportes Excel con formato usando openpyxl
- Ciclo completo de automatización: trigger → procesamiento → output → archivo histórico

---

## 📬 Contacto

**Virginia Garcia**  
[LinkedIn](https://www.linkedin.com/in/garcia-virginia/) · [GitHub](https://github.com/virginia-garcia)
