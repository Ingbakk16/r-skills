---
name: r-read-data
description: Skill en español para leer datos en R: descarga reproducible, importación de CSV/XLSX, inspección de estructura y verificación de tipos antes de analizar.
license: MIT
---

# Leer datos en R

Usa este skill cuando la tarea sea obtener datos desde archivos locales o remotos y dejarlos listos para análisis reproducible en R.

## Objetivo

Leer datos de forma programática, validar su estructura y detectar problemas antes de continuar con manipulación o gráficos.

## Cuándo usarlo

- Descargar archivos desde una URL
- Leer CSV, TSV, Excel u otros archivos tabulares
- Revisar columnas, filas y tipos de dato
- Confirmar que el archivo quedó en la carpeta correcta del proyecto
- Explorar un data frame con `str()` o `glimpse()`

## Principios

- Prefiere código reproducible antes que pasos manuales en la interfaz.
- Lee primero la estructura, después analiza.
- Si el archivo ya existe, evita volver a descargarlo sin necesidad.
- Usa rutas claras dentro del proyecto, como `datos/`.

## Patrón recomendado

1. Identificar la fuente del dato.
2. Guardar la URL o ruta en una variable con nombre claro.
3. Descargar o leer el archivo.
4. Inspeccionar la estructura con `str()` o `glimpse()`.
5. Verificar nombres de columnas, tipos y valores faltantes.

## Funciones habituales

- `download.file()`
- `readr::read_csv()`
- `readr::read_tsv()`
- `readxl::read_excel()`
- `str()`
- `dplyr::glimpse()`

## Ejemplos de referencia

### Descargar y leer pingüinos

```r
pinguinos_url <- "https://zenodo.org/records/12772944/files/pinguinos.csv?download=1"
pinguinos_archivo <- "datos/pinguinos.csv"

download.file(pinguinos_url, pinguinos_archivo)
pinguinos <- readr::read_csv(pinguinos_archivo)
str(pinguinos)
```

### Leer estaciones meteorológicas

```r
nh0437_url <- "https://raw.githubusercontent.com/rse-r/intro-programacion/main/datos/NH0437.csv"
nh0437_archivo <- "datos/NH0437.csv"

download.file(nh0437_url, nh0437_archivo)
nh0437 <- readr::read_csv(nh0437_archivo)
dplyr::glimpse(nh0437)
```

## Ejemplos generales

```r
url_datos <- "https://ejemplo.org/datos.csv"
archivo_datos <- "datos/datos.csv"

download.file(url_datos, archivo_datos)
datos <- readr::read_csv(archivo_datos)
str(datos)
```

```r
datos <- readxl::read_excel("datos/reporte.xlsx")
dplyr::glimpse(datos)
```

## Guardrails

- No asumas que el archivo existe ni que la carpeta destino está creada.
- No inventes nombres de columnas: inspecciona antes de proponer código posterior.
- Si el usuario pide leer un archivo específico, usa la función adecuada al formato.
- Si hay mensajes de tipo o parsing, explícalos y sugiere revisar columnas problemáticas.

## Errores comunes

- Leer un archivo sin comprobar la ruta.
- Usar `read_csv()` para un Excel.
- Saltar la inspección de estructura y asumir tipos incorrectos.
- Seguir aunque haya columnas mal interpretadas sin avisar.

## Checklist rápido

- ¿La fuente de datos quedó guardada en una variable?
- ¿La ruta usa carpetas del proyecto?
- ¿Ya se revisó `str()` o `glimpse()`?
- ¿Los tipos de columna parecen razonables?
