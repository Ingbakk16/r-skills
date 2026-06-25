---
name: r-graphics-data
description: Skill en español para graficar datos en R con ggplot2: capas, aes, geoms, escalas, facetas y gráficos derivados de resúmenes.
license: MIT
---

# Graficar datos en R

Usa este skill cuando la tarea sea construir gráficos claros, reproducibles y expresivos con `ggplot2`.

## Objetivo

Traducir datos a gráficos por capas, eligiendo la geometría y las estéticas adecuadas según la pregunta de análisis.

## Cuándo usarlo

- Crear gráficos de puntos, líneas, barras, histogramas y boxplots
- Comparar variables numéricas o categóricas
- Separar paneles con facetas
- Visualizar resultados resumidos con `dplyr` antes de graficar
- Resolver overplotting o problemas de legibilidad

## Principios

- Un gráfico empieza con datos y mapeos, luego suma capas.
- Diferencia entre mapear una estética y fijarla con un valor constante.
- Si el gráfico requiere un resumen, calcula primero el resumen y después grafica.
- Usa la geometría que mejor responda la pregunta, no la que sea más fácil escribir.

## Flujo recomendado

1. Definir la pregunta visual.
2. Elegir variables y tipo de gráfico.
3. Construir `ggplot(data, aes(...))`.
4. Añadir la geometría correcta.
5. Ajustar color, tamaño, facetas o transparencia si hace falta.
6. Verificar si el gráfico comunica la relación real entre variables.

## Funciones habituales

- `ggplot2::ggplot()`
- `ggplot2::aes()`
- `ggplot2::geom_point()`
- `ggplot2::geom_line()`
- `ggplot2::geom_bar()`
- `ggplot2::geom_histogram()`
- `ggplot2::geom_boxplot()`
- `ggplot2::geom_violin()`
- `ggplot2::facet_wrap()`
- `ggplot2::facet_grid()`

## Ejemplos de referencia

### Esperanza de vida a lo largo del tiempo

```r
paises |> 
  dplyr::group_by(continente, anio) |> 
  dplyr::summarise(esperanza_de_vida_media = mean(esperanza_de_vida)) |> 
  ggplot(aes(anio, esperanza_de_vida_media)) +
  geom_point() +
  geom_smooth(method = "lm")
```

### Gráfico por continente

```r
ggplot(paises, aes(anio, esperanza_de_vida)) +
  geom_line(aes(color = continente, group = pais)) +
  geom_point()
```

### Distribución de precios de diamantes

```r
ggplot(diamantes, aes(claridad, precio)) +
  geom_boxplot()
```

### Facetas por color

```r
ggplot(diamantes, aes(quilate, precio)) +
  geom_point(aes(color = color)) +
  facet_wrap(~ color)
```

### Temperatura mensual

```r
datos_estaciones |> 
  dplyr::group_by(estacion, mes = lubridate::floor_date(fecha, "month")) |> 
  dplyr::summarise(temperatura_media = mean(temperatura_abrigo_150cm, na.rm = TRUE)) |> 
  ggplot(aes(mes, temperatura_media, color = estacion)) +
  geom_line()
```

## Patrones clave

### Nube de puntos

```r
ggplot(datos, aes(x = pib_per_capita, y = esperanza_de_vida)) +
  geom_point()
```

### Línea temporal por grupo

```r
ggplot(datos, aes(anio, esperanza_de_vida, group = pais)) +
  geom_line()
```

### Barras de frecuencia

```r
ggplot(datos, aes(corte)) +
  geom_bar()
```

### Resumen y gráfico

```r
datos |> 
  dplyr::group_by(continente, anio) |> 
  dplyr::summarise(promedio = mean(esperanza_de_vida, na.rm = TRUE)) |> 
  ggplot(aes(anio, promedio)) +
  geom_line()
```

### Paneles

```r
ggplot(datos, aes(quilate, precio)) +
  geom_point(aes(color = color)) +
  facet_wrap(~ color)
```

## Guardrails

- No uses `aes(color = "red")` si quieres un color fijo; eso mapea una cadena como dato.
- No combines demasiadas variables sin justificar la lectura visual.
- Si hay demasiados puntos superpuestos, reduce tamaño, usa transparencia o cambia la geometría.
- Si una línea depende de grupos, asegúrate de especificar `group`.
- Si el gráfico nace de un resumen, conserva nombres de columnas claros para el eje y.

## Errores comunes

- Olvidar `group =` en series temporales por entidad.
- Usar una geometría inadecuada para la pregunta.
- Pensar que `+` y `|>` se usan igual: el pipe termina cuando empieza `ggplot()`.
- Mapear una estética dentro de `aes()` cuando se quería fijar un valor constante.

## Checklist rápido

- ¿El gráfico responde la pregunta?
- ¿Las estéticas están mapeadas correctamente?
- ¿Hace falta resumir antes de graficar?
- ¿Hay overplotting o paneles que mejoren la lectura?
