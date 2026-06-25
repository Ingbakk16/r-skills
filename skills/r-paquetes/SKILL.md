---
name: r-paquetes
description: Skill en español para crear, estructurar y desarrollar paquetes de R: create_package, use_r, load_all, DESCRIPTION, NAMESPACE, datos, Git y GitHub.
license: MIT
---

# Paquetes de R

Usa este skill cuando la tarea sea iniciar, organizar o desarrollar un paquete de R.

## Objetivo

Ayudar a convertir funciones sueltas en un paquete reutilizable, reproducible y ordenado.

## Cuándo usarlo

- Crear un paquete nuevo
- Entender la estructura de un paquete
- Agregar funciones a `R/`
- Configurar `DESCRIPTION` y `NAMESPACE`
- Cargar funciones mientras se desarrolla con `load_all()`
- Guardar datos dentro del paquete
- Inicializar Git y publicar en GitHub

## Principios

- Un paquete tiene sentido cuando una función ya se reutiliza o probablemente se reutilizará.
- El desarrollo debe ser incremental.
- `DESCRIPTION` es parte central del paquete, no un detalle secundario.
- Durante el desarrollo se trabaja sobre el código fuente.
- Los datos y el código también se pueden empaquetar.

## Estructura básica

- `DESCRIPTION`
- `NAMESPACE`
- `R/`
- `data/`
- `tests/`
- `vignettes/`
- `README`

## Flujo recomendado

1. Definir qué función o grupo de funciones merece un paquete.
2. Crear la estructura con `usethis::create_package()`.
3. Agregar funciones con `usethis::use_r()`.
4. Probar el código con `devtools::load_all()`.
5. Ajustar `DESCRIPTION` y dependencias.
6. Agregar datos si hacen falta con `usethis::use_data()`.
7. Inicializar Git con `usethis::use_git()`.
8. Publicar en GitHub con `usethis::use_github()` si corresponde.

## Herramientas clave

- `usethis::create_package()`
- `usethis::use_r()`
- `devtools::load_all()`
- `usethis::use_data()`
- `usethis::use_git()`
- `usethis::use_github()`
- `source()` cuando solo querés cargar un script

## Ejemplos de referencia

### Crear un paquete de prueba

```r
usethis::create_package("~/Documentos/Courses/paqueteprueba")
```

### Agregar una función al paquete

```r
usethis::use_r("funcion_prueba")

suma <- function(x, y) {
  x + y
}
```

### Cargar el paquete en desarrollo

```r
devtools::load_all()
suma(2, 2)
```

### Guardar datos dentro del paquete

```r
datos <- sample(1000)
usethis::use_data(datos)
```

### Activar Git en el proyecto

```r
usethis::use_git()
```

## Guardrails

- No mezcles la lógica de una función con el armado completo del paquete sin necesidad.
- No uses `library()` dentro del código fuente del paquete.
- No olvides que las dependencias deben declararse en `DESCRIPTION`.
- No cargues el paquete “a mano” si `load_all()` resuelve el ciclo de desarrollo.

## Errores comunes

- Crear código fuera de `R/`.
- No completar `DESCRIPTION`.
- Usar funciones de otros paquetes sin declararlas como dependencia.
- Olvidar que los datos del paquete también necesitan un flujo específico.
- Confundir desarrollo de paquete con uso normal del paquete instalado.

## Checklist rápida

- ¿El paquete tiene estructura válida?
- ¿Las funciones viven en `R/`?
- ¿`DESCRIPTION` está completo?
- ¿Las dependencias están declaradas?
- ¿Se puede cargar con `load_all()`?
- ¿Git y GitHub están configurados si hace falta compartirlo?
