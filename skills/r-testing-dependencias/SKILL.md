---
name: r-testing-dependencias
description: Skill en español para declarar dependencias y escribir tests en R: Imports, Suggests, testthat, expect_xxx, R CMD check y cobertura de pruebas.
license: MIT
---

# Tests y dependencias en R

Usa este skill cuando la tarea sea declarar dependencias, escribir pruebas o revisar que un paquete siga funcionando correctamente.

## Objetivo

Ayudar a mantener paquetes confiables, con dependencias bien registradas y tests que detecten errores antes de compartir el código.

## Cuándo usarlo

- Agregar una dependencia a un paquete
- Decidir si un paquete va en `Imports` o `Suggests`
- Crear tests con `testthat`
- Verificar resultados esperados y mensajes de error
- Ejecutar `R CMD check`
- Revisar cobertura de tests
- Configurar integración continua

## Principios

- Si una función externa es esencial, debe quedar declarada como dependencia.
- No uses `library()` dentro del código fuente del paquete.
- Cada función importante debería tener al menos un test.
- Los tests deben cubrir resultados normales, bordes y errores.
- Los mensajes de error también se testean.

## Dependencias

### Dónde van

- `Imports`: paquetes necesarios para que el paquete funcione.
- `Suggests`: paquetes útiles para tests, desarrollo o funciones opcionales.

### Flujo recomendado

1. Detectar qué paquete usa tu función.
2. Declararlo en `DESCRIPTION`.
3. Llamar funciones con `paquete::funcion()`.
4. Evitar cargar paquetes completos con `library()` dentro del código del paquete.

### Herramienta útil

- `usethis::use_package("paquete")`

## Tests

### Configuración

- `usethis::use_testthat(3)`
- `usethis::use_test("nombre")`

### Expectativas comunes

- `expect_equal()`
- `expect_length()`
- `expect_true()` / `expect_false()`
- `expect_error()`
- `expect_warning()`
- `expect_message()`

## Ejemplos de referencia

### Declarar una dependencia

```r
usethis::use_package("dplyr")
```

### Configurar testthat

```r
usethis::use_testthat(3)
usethis::use_test("suma")
```

### Test de una suma

```r
test_that("la suma funciona", {
  expect_equal(suma(2, 2), 4)
})
```

### Test de error

```r
test_that("no suma caracteres", {
  expect_error(suma("1", 1), "num")
})
```

### Test de conversión

```r
test_that("convierte pulgadas a centímetros", {
  expect_equal(pulgadas_a_centimetros(1), 2.54)
})
```

## Flujo de verificación

1. Escribir la función.
2. Cargar el paquete con `load_all()`.
3. Probar la función manualmente.
4. Escribir tests.
5. Correr `devtools::test()`.
6. Correr `devtools::check()`.
7. Revisar cobertura con `devtools::test_coverage()`.

## Guardrails

- No declares dependencias de más.
- No uses `library()` dentro del código del paquete.
- No dejes sin testear las ramas de error.
- No asumas que un test manual alcanza para mantener el código seguro.
- No ignores warnings de `R CMD check`.

## Errores comunes

- Poner un paquete esencial en `Suggests`.
- Olvidar una dependencia usada por una función interna.
- Testear solo el caso feliz.
- No verificar el mensaje de error.
- Hacer tests frágiles que cambian por detalles irrelevantes.

## Checklist rápida

- ¿Las dependencias están bien separadas?
- ¿Se usan `paquete::funcion()` donde corresponde?
- ¿Hay tests para lo normal y para lo incorrecto?
- ¿`devtools::check()` pasa?
- ¿La cobertura es razonable?
