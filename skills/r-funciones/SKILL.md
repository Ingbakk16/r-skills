---
name: r-funciones
description: Skill en español para crear, usar y probar funciones en R: esqueleto, argumentos, validación, mensajes de error y buenas prácticas de diseño.
license: MIT
---

# Funciones en R

Usa este skill cuando la tarea sea convertir código repetido en una función, diseñar una función nueva o revisar si una función está bien construida.

## Objetivo

Ayudar a escribir funciones claras, reutilizables y seguras, con un flujo de trabajo práctico para probarlas y mejorarlas.

## Cuándo usarlo

- Convertir un bloque de código en una función
- Elegir nombres claros para funciones y argumentos
- Definir valores por defecto
- Validar que los argumentos sean correctos
- Agregar mensajes de error útiles
- Probar una función con distintos tipos de entradas
- Cargar funciones con `source()` o desarrollarlas dentro de un paquete

## Principios

- Escribí funciones para evitar copiar y pegar.
- Partí de un código que ya funciona y después generalizalo.
- Usá nombres descriptivos y preferentemente verbos para funciones.
- Las funciones deben hacer una sola cosa bien.
- Si un argumento no es válido, frená con un error claro.
- Probá la función con casos buenos, raros y malos.

## Flujo recomendado

1. Escribir primero el código para un caso concreto.
2. Identificar qué parte cambia y convertirla en argumento.
3. Encapsular el código dentro de `function()`.
4. Probar la función con valores esperados.
5. Probar con vectores, caracteres, `TRUE/FALSE` y `NA`.
6. Agregar validación y mensajes de error si hace falta.
7. Si la función se va a reutilizar mucho, pasarla al flujo de documentación en `r-documentacion`.

## Esqueleto

```r
nombre_de_funcion <- function(arg1, arg2 = valor_por_defecto) {
  # código
}
```

## Funciones y patrones clave

- `function()` para crear funciones
- `return()` cuando ayuda a leer el código, aunque no siempre es necesario
- `if`, `else` y `else if` para validar o bifurcar comportamiento
- `is.numeric()`, `is.character()`, `is.logical()` para chequear tipos
- `cli::cli_abort()` para errores claros
- `cli::cli_inform()` para mensajes informativos
- `source()` para cargar scripts con funciones
- `load_all()` cuando la función vive dentro de un paquete en desarrollo

## Ejemplos de referencia

### Convertir pulgadas a centímetros

```r
pulgadas_a_centimetros <- function(medida_pulgadas) {
  medida_pulgadas * 2.54
}
```

### Revisar proporción de faltantes

```r
proporcion_faltantes <- function(x) {
  mean(is.na(x))
}
```

### Calcular proporción respecto al total

```r
proporcion_total <- function(x) {
  x / sum(x, na.rm = TRUE)
}
```

### Descargar y leer una estación

```r
leer_estacion <- function(id_estacion, ruta_archivo) {
  if (!file.exists(ruta_archivo)) {
    cli::cli_inform("Descargando archivo de estación.")
    download.file(
      paste0("https://raw.githubusercontent.com/rse-r/intro-programacion/main/datos/", id_estacion, ".csv"),
      ruta_archivo
    )
  }

  readr::read_csv(ruta_archivo)
}
```

## Patrón recomendado

### 1. Generalizar código

```r
pulgadas_a_centimetros <- function(medida_pulgadas) {
  medida_pulgadas * 2.54
}
```

### 2. Validar entradas

```r
pulgadas_a_centimetros <- function(medida_pulgadas) {
  if (!is.numeric(medida_pulgadas)) {
    cli::cli_abort("`medida_pulgadas` debe ser numérico.")
  }

  medida_pulgadas * 2.54
}
```

### 3. Dar mensajes útiles

```r
leer_estacion <- function(ruta) {
  if (!file.exists(ruta)) {
    cli::cli_abort("El archivo no existe en la ruta indicada.")
  }

  cli::cli_inform("Leyendo archivo de estación.")
  readr::read_csv(ruta)
}
```

## Guardrails

- No aceptes cualquier tipo de entrada sin validar.
- No devuelvas mensajes confusos o técnicos si puedes ser más claro.
- No mezcles demasiadas responsabilidades en una sola función.
- No uses nombres vagos como `hacer_cosa()` o `funcion1()`.
- No dependas de variables externas si la función puede recibirlas como argumento.

## Errores comunes

- Olvidar pasar un argumento como parámetro y dejarlo como valor fijo.
- No probar la función con entradas no numéricas o vacías.
- Usar `return()` de más sin necesidad.
- Devolver resultados inesperados con vectores cuando se esperaba un único valor.
- Agregar documentación larga dentro de este skill en vez de dejar eso para `r-documentacion`.

## Relación con documentación

Una vez que la función funciona, documentala en `r-documentacion`. Este skill solo deja indicado que una función útil debería tener ayuda, ejemplos y descripción clara.

## Checklist rápida

- ¿La función reemplaza código repetido?
- ¿El nombre describe bien lo que hace?
- ¿Los argumentos son claros y necesarios?
- ¿La salida es predecible?
- ¿Se probaron casos correctos e incorrectos?
- ¿Si va a reutilizarse, ya quedó lista para documentarse?
