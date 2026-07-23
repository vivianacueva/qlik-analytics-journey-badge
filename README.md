# 📊 Qlik Analytics Journey — Modelo de Datos y Arquitectura en 3 Capas

Proyecto desarrollado como parte de la ruta oficial **Qlik Analytics Journey Badge**, dentro del programa de acceso estudiantil de mi Máster en Business Intelligence (UNIR). El objetivo es construir un modelo de datos robusto en Qlik Sense/Qlik Cloud siguiendo buenas prácticas de arquitectura: separación en capas, trazabilidad y un modelo en estrella optimizado para análisis.

> 🎓 **Contexto:** Proyecto de portafolio — Analista de Datos / Ingeniera Industrial especializada en BI (Qlik Sense, Power BI, SQL, R, Python).

---

## 🎯 Objetivo del proyecto

- Diseñar una arquitectura de datos en **3 capas (Extract → Transform → Business)** siguiendo las buenas prácticas recomendadas por Qlik.
- Construir un **modelo en estrella (Star Schema)** limpio, sin relaciones circulares ni sincretismos no deseados.
- Documentar el flujo completo de datos, desde el origen hasta el dashboard final, como evidencia de proceso analítico profesional.

---

## 🏗️ Arquitectura de datos: modelo de 3 capas QVD

El proyecto sigue el patrón estándar de capas QVD, que separa responsabilidades y mejora el rendimiento y mantenibilidad de la carga:

| Capa | Script | Función |
|------|--------|---------|
| **1. Extract (Extracción)** | `01_extract_layer.qvs` | Conecta con las fuentes originales (BD, Excel, API, etc.) y genera QVDs "en crudo", sin transformar. Aísla el modelo de cambios en el origen. |
| **2. Transform (Transformación)** | `02_transform_layer.qvs` | Limpieza, tipado, renombrado de campos, cálculos intermedios y resolución de calidad de datos. Genera QVDs listos para modelar. |
| **3. Business / Star Schema (Negocio)** | `03_business_layer.qvs` | Construye el modelo final: tablas de hechos y dimensiones, claves optimizadas, campos calculados de negocio. Es la capa que consume la app de análisis. |

**Diagrama del flujo de datos:**

<!-- 📌 MARCADOR: Pega aquí tu captura del flujo de las 3 capas -->
![Flujo de datos](docs/images/data_flow.png)

---

## ⭐ Modelo en estrella (Star Schema)

El modelo final sigue un esquema en estrella clásico: una tabla de hechos central conectada a dimensiones desnormalizadas, evitando relaciones many-to-many sin resolver y minimizando el uso de campos sintéticos.

**Captura del Data Model Viewer:**

<!-- 📌 MARCADOR: Pega aquí tu captura del Data Model Viewer de Qlik -->
![Data Model Viewer](docs/images/data_model_viewer.png)

**Tablas del modelo:**

<!-- 📌 MARCADOR: completa con tus tablas reales -->
- **Tabla de hechos:** `FactVentas` — [describe grano y métricas clave]
- **Dimensiones:**
  - `DimFecha` — [descripción]
  - `DimProducto` — [descripción]
  - `DimCliente` — [descripción]
  - `Dim...` — [descripción]

---

## ✅ Buenas prácticas aplicadas

- [x] Separación estricta entre capas de extracción, transformación y negocio.
- [x] Uso de `QUALIFY`/`UNQUALIFY` y renombrado explícito de campos para evitar joins no intencionados.
- [x] Claves primarias limpias, sin campos sintéticos innecesarios.
- [x] Comentarios en el código de carga (`.qvs`) explicando cada bloque.
- [x] Variables de entorno/rutas parametrizadas al inicio del script (sin rutas hardcodeadas dispersas).
- [x] Nomenclatura consistente en tablas y campos (`Dim`, `Fact`, `PascalCase`).

---

## 📂 Estructura del repositorio

```
qlik-analytics-journey/
├── README.md
├── scripts/
│   ├── 01_extract_layer.qvs
│   ├── 02_transform_layer.qvs
│   └── 03_business_layer.qvs
├── docs/
│   ├── images/
│   │   ├── data_model_viewer.png
│   │   ├── star_schema.png
│   │   └── data_flow.png
│   └── architecture.md
└── data/
    └── sample/
```

---

## 🛠️ Tecnologías utilizadas

`Qlik Sense` · `Qlik Cloud` · `Data Modeling` · `Star Schema` · `SQL`

---

## 👩‍💻 Autora

**Viviana** — Analista de Datos e Ingeniera Industrial
📍 Madrid, España
🔗 [LinkedIn](#) · [Portafolio](#)

<!-- 📌 MARCADOR: añade tus enlaces reales -->
