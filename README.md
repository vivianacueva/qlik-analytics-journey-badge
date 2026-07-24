# Qlik Analytics Journey — Badge Qlik Cloud Analyze

Repositorio de práctica y documentación de mi recorrido hacia el badge **Qlik Cloud Analyze** (módulo *Data Modeling with Qlik Cloud Analytics*), dentro de la suscripción Qlik Student Learning.

## 🎯 Objetivo

Registrar el proceso de construcción de un modelo de datos en Qlik Sense: desde la carga de datos hasta un esquema en estrella optimizado, documentando decisiones técnicas y avances por módulo.

## 🏗️ Arquitectura del modelo

- **3 capas QVD**: extracción → transformación → carga final (Extract / Transform / Load layers)
- **Esquema en estrella** como resultado final del modelado
- Capturas de pantalla del Data Model Viewer y Debugger en `/docs/screenshots`

## 🧭 Estructura del badge (5 módulos)

| # | Módulo | Estado |
|---|--------|--------|
| 1 | Cargando datos (conexión y carga) | ✅ En curso / avanzado |
| 2 | Transformación de datos | ⏳ Pendiente |
| 3 | Creando el master calendar | ⏳ Pendiente |
| 4 | Estructuración del modelo | ⏳ Pendiente |
| 5 | Finalización de los datos | ⏳ Pendiente |

### Módulo 1 — Cargando datos (detalle de avance)

- **Desde base de datos (SQL Server, conexión `ABC`)**: tablas `Orders`, `OrderDetails` (sección `DB_Measures`) y `Customers`, `Divisions` (sección `DB_Dimensions`)
- **Desde Data Catalog**: archivo Excel (`Employees`), Excel multi-hoja (`Teams`), CSV (`Offices`), archivo de ancho fijo (`Org_structure`), inclusión de script externo `.qvs` (generación de emails)
- Uso de variables (`vFileLocation`, `vDBConn`) y *find & replace* para desacoplar rutas/conexiones del script

## 📂 Estructura del repositorio

```
/scripts            → scripts exportados del Data Load Editor, uno por módulo
/docs/screenshots    → capturas de apoyo (Data Model Viewer, debugger, etc.)
README.md
.gitignore
```

## 🛠️ Herramientas

Qlik Sense (Qlik Cloud), Git / GitHub, Git Bash

---
*Actualizado a medida que avanzo en cada módulo del learning path.*