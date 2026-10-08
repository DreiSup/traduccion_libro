# Proyecto: traducción de libro EN → ES (uso personal)

## Estructura del repo
```
original/libro.pdf     # PDF original (texto seleccionable)
md_en/cap_XX.md        # capítulos extraídos en inglés
es/cap_XX.md           # capítulos traducidos
glosario.md            # términos fijos EN → ES
progreso.md            # estado de cada capítulo
scripts/               # extraer.py, ensamblar.py
salida/libro_es.pdf    # resultado final
```

## Reglas de sesión
- Al empezar: leer `progreso.md` y continuar donde se quedó.
- La sesión es efímera: hacer commit y push al terminar cada capítulo.
- No pasar de fase sin confirmación del usuario.

## Fase 1 — Extracción
- Convertir el PDF a Markdown con `pymupdf4llm`.
- Dividir por capítulos usando el índice interno del PDF (`doc.get_toc()`); si no existe, por encabezados.
- Limpiar cabeceras y pies repetidos, números de página y palabras cortadas con guion a final de línea.
- Guardar en `md_en/cap_XX.md` (XX = 01, 02...).
- Mostrar la lista de capítulos detectados (título + nº de palabras) y PARAR.

## Fase 2 — Traducción
Antes de cada capítulo, leer `glosario.md`.

Reglas:
- Español de España, natural y fluido, sin calcos del inglés. Mismo registro que el original.
- Conservar la estructura Markdown exacta: encabezados, listas, cursivas, negritas y notas al pie.
- Un párrafo de origen = un párrafo de destino. No resumir, no omitir y no añadir nada.
- Nombres propios: no traducir. Obras citadas: usar el título oficial en español si existe.
- Modismos y juegos de palabras: adaptar al equivalente español. Si se pierde algo importante, añadir una nota breve `[N. del T.: ...]`.
- Cifras y unidades: mantener las del original.
- Capítulos largos: traducir por secciones de ~2.500 palabras, sin cortar párrafos.
- Términos clave nuevos: añadirlos a `glosario.md` (`término EN → término ES | nota`).

Al terminar cada capítulo:
1. Verificar que el nº de párrafos coincide entre `md_en/` y `es/` (si no coincide, revisar omisiones).
2. Actualizar `progreso.md`.
3. Commit + push: `traduce cap XX`.

## Fase 3 — Revisión
- Pasada de coherencia de todo `es/` contra `glosario.md`.
- Informe de discrepancias antes de corregir.

## Fase 4 — PDF final (PROPUESTA, pendiente de confirmar)
- Markdown → HTML (`markdown`) → PDF (`weasyprint`) con CSS propio.
- Formato: A5, fuente serif, salto de página por capítulo, índice al inicio.
- Salida: `salida/libro_es.pdf`.
