# Índice de skills

Este directorio agrupa los skills del paquete y sirve como portada rápida para saber qué hace cada uno y en qué orden conviene usarlos.

## Orden recomendado

1. `r-read-data`: leer datos de forma reproducible.
2. `r-work-data`: transformar, resumir y unir tablas.
3. `r-graphics-data`: visualizar resultados y relaciones.
4. `r-funciones`: convertir código en funciones reutilizables.
5. `r-paquetes`: crear y desarrollar paquetes de R.
6. `r-documentacion`: documentar funciones, datos, paquetes y proyectos.
7. `r-testing-dependencias`: declarar dependencias y escribir tests.

## Skills disponibles

- `r-read-data` - leer CSV/XLSX, descargar archivos y revisar estructura.
- `r-work-data` - usar `dplyr` y `tidyr` para manipular datos ordenados.
- `r-graphics-data` - construir gráficos con `ggplot2`.
- `r-funciones` - escribir y probar funciones en R.
- `r-paquetes` - estructurar, crear y desarrollar paquetes.
- `r-documentacion` - documentar con `roxygen2`, README, viñetas y `pkgdown`.
- `r-testing-dependencias` - declarar dependencias y testear con `testthat`.

## Ejemplos de referencia

- Descargar y leer pingüinos desde Zenodo.
- Calcular proporciones y resúmenes con `group_by()` y `summarise()`.
- Pasar datos meteorológicos de ancho a largo con `pivot_longer()`.
- Graficar esperanza de vida por continente y año con `ggplot2`.
- Encapsular código repetido en una función como `pulgadas_a_centimetros()`.
- Crear un paquete con `usethis::create_package()` y cargarlo con `load_all()`.
- Documentar una función simple con `roxygen2`.
- Declarar una dependencia con `usethis::use_package()` y testear con `testthat`.
