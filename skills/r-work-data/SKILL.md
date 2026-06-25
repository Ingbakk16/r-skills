---
name: r-work-data
description: Skill en español para transformar datos ordenados en R: select, filter, mutate, group_by, summarise, reframe, pivot_longer, pivot_wider y joins.
license: MIT
---

# Trabajar datos en R

Usa este skill cuando la tarea sea transformar, resumir, reorganizar o unir data frames en formato ordenado.

## Objetivo

Ayudar a resolver tareas de análisis con `dplyr` y `tidyr` usando pasos claros, reproducibles y fáciles de leer.

## Cuándo usarlo

- Seleccionar columnas o filas
- Crear o modificar variables
- Agrupar y resumir datos
- Pasar de formato ancho a largo y viceversa
- Unir tablas por una o más claves
- Resolver análisis con `|>` y verbos encadenados

## Principios

- Cada verbo devuelve una nueva tabla.
- El orden de los pasos importa.
- Si vas a resumir por grupo, agrupa primero y resume después.
- Si necesitas más de un valor por grupo, usa `reframe()` en lugar de forzar `summarise()`.
- Para varias tablas, elige el join más seguro para no perder datos sin querer.

## Flujo recomendado

1. Confirmar la forma de los datos y las columnas disponibles.
2. Elegir el verbo o la secuencia de verbos adecuada.
3. Construir la transformación con `|>`.
4. Verificar el resultado intermedio si el problema es complejo.
5. Revisar `NA`, nombres y tamaño final de la tabla.

## Funciones habituales

- `dplyr::select()`
- `dplyr::filter()`
- `dplyr::mutate()`
- `dplyr::group_by()`
- `dplyr::summarise()`
- `dplyr::reframe()`
- `tidyr::pivot_longer()`
- `tidyr::pivot_wider()`
- `dplyr::left_join()`
- `dplyr::full_join()`
- `dplyr::inner_join()`
- `dplyr::anti_join()`

## Ejemplos de referencia

### Proporción aleta/pico

```r
pinguinos |> 
  dplyr::filter(especie != "Papua") |> 
  dplyr::mutate(proporcion_aleta_pico = largo_aleta_mm / largo_pico_mm) |> 
  dplyr::group_by(especie) |> 
  dplyr::summarise(promedio = mean(proporcion_aleta_pico, na.rm = TRUE))
```

### Resumir estaciones meteorológicas

```r
datos_estaciones |> 
  dplyr::group_by(estacion) |> 
  dplyr::summarise(
    cantidad = dplyr::n(),
    media_temp = mean(temperatura_abrigo_150cm, na.rm = TRUE)
  )
```

### Pasar de ancho a largo

```r
paises_largo <- tidyr::pivot_longer(
  paises_ancho,
  cols = c(starts_with("pob"), starts_with("esperanza"), starts_with("pib_per")),
  names_to = "variable_anio",
  values_to = "valor"
)
```

### Unir tablas de países y CO2

```r
dplyr::full_join(paises_2007, co2_2007, by = "pais")
```

## Patrones clave

### Filtrar y seleccionar

```r
datos |> 
  filter(especie == "Adelia") |> 
  select(especie, largo_pico_mm)
```

### Crear columnas

```r
datos |> 
  mutate(masa_corporal_kg = masa_corporal_g / 1000)
```

### Agrupar y resumir

```r
datos |> 
  group_by(especie) |> 
  summarise(promedio = mean(largo_aleta_mm, na.rm = TRUE))
```

### Varias filas por grupo

```r
datos |> 
  group_by(especie) |> 
  reframe(cuantil = quantile(masa_corporal_g, c(0.25, 0.75), na.rm = TRUE))
```

### Pasar de ancho a largo

```r
datos |> 
  pivot_longer(cols = starts_with("pib"), names_to = "variable", values_to = "valor")
```

### Pasar de largo a ancho

```r
datos |> 
  pivot_wider(names_from = variable, values_from = valor)
```

### Unir tablas

```r
left_join(datos_a, datos_b, by = c("pais", "anio"))
```

## Guardrails

- No mezcles manipulación y resumen sin explicar el objetivo lógico.
- No uses `summarise()` para devolver más de una fila por grupo si `reframe()` es mejor.
- No elijas `inner_join()` por defecto si puede borrar observaciones relevantes.
- Si `pivot_*()` cambia tipos o crea nombres raros, avisa y propone correcciones.
- Si hay `NA`, indícalo explícitamente cuando afecte medias, sumas o joins.

## Errores comunes

- Olvidar `na.rm = TRUE` en estadísticas con faltantes.
- Agrupar por una columna equivocada.
- Asumir que `pivot_longer()` o `pivot_wider()` no cambian la forma del objeto.
- Unir tablas con una sola clave cuando en realidad se necesitan dos.
- Usar `summarise()` para cálculos que devuelven varias filas por grupo.

## Checklist rápido

- ¿La secuencia de verbos está en el orden correcto?
- ¿La tabla final conserva las filas que el usuario necesita?
- ¿Se manejan bien los `NA`?
- ¿Las claves del join están completas?
