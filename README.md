# Skills para trabajar en R

Este repositorio contiene 3 skills en español basados en las prácticas del libro *Introducción a la Programación II*:

- `r-read-data`: leer y validar datos
- `r-work-data`: transformar datos ordenados
- `r-graphics-data`: graficar datos con `ggplot2`

## Estructura

```text
skills/
  r-read-data/SKILL.md
  r-work-data/SKILL.md
  r-graphics-data/SKILL.md
```

## Requisitos

- Tener un sistema que soporte skills de agente en formato `SKILL.md`.
- Tener acceso al directorio de skills del usuario, que en este entorno suele ser `~/.agents/skills/`.

## Cómo descargarlo

1. Descargá este repositorio como ZIP o clonalo con Git.
2. Descomprimilo o abrilo en tu máquina.
3. Verificá que exista la carpeta `skills/` con sus 3 subcarpetas.

## Cómo instalarlo en el directorio de skills

1. Copiá las carpetas dentro de tu directorio de skills local.
2. El destino esperado suele ser `~/.agents/skills/`.
3. Cada skill debe quedar en una carpeta propia, por ejemplo:

```text
~/.agents/skills/r-read-data/SKILL.md
~/.agents/skills/r-work-data/SKILL.md
~/.agents/skills/r-graphics-data/SKILL.md
```

## Cómo usarlo

Una vez instalados, podés pedir tareas como estas:

- “Leé este CSV y revisá su estructura”
- “Filtrá y resumí esta tabla por especie”
- “Hacé un gráfico de líneas con facetas”

El agente debería activar el skill correspondiente según la tarea.

## Actualización

Si cambiás un `SKILL.md`, volvé a copiarlo al directorio de skills para que el agente use la versión nueva.

## Notas

- Los 3 skills están escritos en español.
- El skill de trabajo incluye `dplyr`, `tidyr`, pivots y joins porque el libro los usa como parte del flujo normal de análisis.
- Si tu entorno usa otra ruta para skills, ajustá los pasos anteriores a esa ubicación.
