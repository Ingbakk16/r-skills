---
name: r-documentacion
description: Skill en español para documentar funciones, paquetes y proyectos en R: roxygen2, datos documentados, README, viñetas y website con pkgdown.
license: MIT
---

# Documentación en R

Usa este skill cuando la tarea sea escribir o mejorar documentación para funciones, datos, paquetes o proyectos de R.

## Objetivo

Ayudar a escribir documentación clara, reproducible y útil para personas que usan o mantienen código en R.

## Cuándo usarlo

- Documentar una función nueva
- Escribir o mejorar la ayuda de una función
- Documentar datos incluidos en un paquete
- Crear o actualizar un `README`
- Crear una viñeta o artículo de uso
- Generar un sitio web del paquete con `pkgdown`
- Explicar qué hace un paquete y cómo se usa

## Principios

- La documentación existe para humanos, no para la computadora.
- Explicá qué hace el código, por qué existe y cómo se usa.
- Mostrá ejemplos que corran sin errores.
- Mantené la documentación cerca del código que describe.
- Si la función cambió, la documentación también debe cambiar.

## Flujo recomendado

1. Escribir o revisar el código primero.
2. Definir qué necesita saber una persona usuaria.
3. Documentar funciones con `roxygen2`.
4. Generar la documentación con `devtools::document()`.
5. Revisar la ayuda con `?funcion`.
6. Si hace falta, crear o actualizar `README`, viñetas y sitio web.

## Funciones y herramientas clave

- `roxygen2`
- `devtools::document()`
- `usethis::use_readme_rmd()`
- `usethis::use_vignette()`
- `usethis::use_pkgdown()`
- `usethis::use_pkgdown_github_pages()`
- `devtools::build_readme()`
- `pkgdown::build_site()`

## Documentación de funciones

Usá comentarios `#'` arriba de la función y etiquetas como:

- `@param` para argumentos
- `@returns` o `@return` para la salida
- `@examples` para ejemplos reproducibles
- `@export` cuando la función deba quedar disponible al cargar el paquete

### Patrón mínimo

```r
#' Suma dos números
#'
#' Suma `x` e `y` y devuelve el resultado.
#'
#' @param x Un número.
#' @param y Un número.
#' @returns Un número.
#' @examples
#' suma(1, 2)
suma <- function(x, y) {
  x + y
}
```

## Ejemplos de referencia

### Documentar `suma()`

```r
#' Suma dos números
#'
#' Suma `x` e `y` y devuelve el resultado.
#'
#' @param x Un número.
#' @param y Un número.
#' @returns Un número.
#' @examples
#' suma(1, 2)
#' suma(10, 5)
#' @export
suma <- function(x, y) {
  x + y
}
```

### Documentar datos meteorológicos

```r
#' Datos meteorológicos de estaciones
#'
#' Serie de observaciones meteorológicas descargadas del repositorio del curso.
#'
#' @format Un tibble con columnas como `fecha`, `estacion`, `temperatura_abrigo_150cm`
#' y otras variables meteorológicas.
#' @source Repositorio del curso.
"datos_estaciones"
```

### README y viñeta

En el material se usa `README.Rmd` para explicar instalación y uso breve, y una viñeta para mostrar el uso extendido del paquete con más contexto y ejemplos.

## Documentación de datos

Si el paquete incluye datos, documentalos con:

- descripción breve del conjunto
- `@format` con forma general de la tabla
- detalle de columnas relevantes
- `@source` si aplica

## README

El `README` debe responder rápido:

- qué hace el paquete
- cómo se instala
- cómo se usa
- un ejemplo breve

## Viñetas

Usá una viñeta cuando necesites explicar el uso del paquete con más detalle, más texto y más contexto que el README.

## Website

Si el paquete va a compartirse más ampliamente, documentalo con un sitio generado por `pkgdown`.

## Guardrails

- No documentes antes de entender el código.
- No dejes ejemplos que fallen o dependan de datos no reproducibles.
- No repitas en la descripción exactamente lo mismo que en el título.
- No mezcles demasiadas ideas en una sola sección.
- No conviertas este skill en un tutorial de código: su foco es la documentación.

## Errores comunes

- Omitir argumentos en la documentación.
- No documentar la salida de la función.
- Poner ejemplos que no corren.
- Olvidar documentar datos incluidos en el paquete.
- Dejar README, viñeta y sitio web desalineados con el código.

## Checklist rápida

- ¿La función tiene título, descripción y parámetros?
- ¿La salida está documentada?
- ¿Los ejemplos corren?
- ¿Los datos están documentados si el paquete los incluye?
- ¿El README explica instalación y uso?
- ¿Hace falta una viñeta o sitio web?
