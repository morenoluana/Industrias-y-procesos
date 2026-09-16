# Industrias y Procesos Biotecnológicos — UADE 2026

Material de estudio armado a partir de las cuatro clases teóricas de la cátedra y
las dos guías de trabajos prácticos de laboratorio.

## Qué hay acá

| Archivo | Qué es |
|---|---|
| `Resumen_Industrias_y_Procesos_Biotecnologicos.pdf` | Resumen integral de 60 páginas: clases 1 a 4, TP 1 y TP 2, diagramas, seis problemas resueltos paso a paso, formulario completo, tabla de valores típicos y 45 preguntas de examen con respuesta. |
| `app/biorreactor-explicado.html` | Curso interactivo desde cero: nueve lecciones cortas con simulaciones (flujo laminar vs turbulento con trazador, viscosidad, reología, potencia y cizalla, transferencia de oxígeno, airlift y escalado). |
| `app/parcial-resuelto.html` | Enunciado completo del primer parcial y resolución de cada punto, con modo examen para ocultar las respuestas y diagramas del fermentador de 50 L, la curva de kLa y la recta de gassing-out. |
| `app/sala-de-cultivo.html` | App de práctica: tarjetas, quiz, simulacro cronometrado, chuleta buscable y un biorreactor simulado que calcula Re, Np, P, P/V, v_tip y t_m. |
| `build/` | Fuentes HTML del resumen (`p1`…`p6`) y el archivo concatenado que se renderiza a PDF. |

## Regenerar el PDF

```bash
pip install playwright pymupdf
cd build && cat p1_head_c1.html p2_c2.html p3_c3.html p4_c4.html p5_tp.html p6_qa.html > resumen.html
python3 - <<'PY'
from playwright.sync_api import sync_playwright
with sync_playwright() as p:
    b = p.chromium.launch()
    pg = b.new_page()
    pg.goto('file://' + __import__('os').path.abspath('resumen.html'), wait_until='networkidle')
    pg.pdf(path='../Resumen_Industrias_y_Procesos_Biotecnologicos.pdf', format='A4',
           print_background=True,
           margin={'top':'14mm','bottom':'16mm','left':'13mm','right':'13mm'})
    b.close()
PY
```

Las tres páginas están enlazadas entre sí por una barra de navegación común, así que desde cualquiera se llega a las otras dos.

## Contenido cubierto

- **Clase 1** — Bioprocesos, tipos de producto (I, II, III y alto peso molecular), upstream y downstream, el biorreactor y su equipamiento, QbD y PAT, modelado, OUR / OTR / kLa, introducción al escalado.
- **Clase 2** — Fenómenos de transporte, reología, viscosidad, fluidos newtonianos y no newtonianos, número de Reynolds, viscosímetros, transporte de materia y números adimensionales.
- **Clase 3** — Mezclado, tanque agitado (partes, geometría, agitadores, patrones de flujo), airlift, fotobiorreactores, biorreactores de membrana y sistemas de control.
- **Clase 4** — Criterios de escalado, potencia y número de potencia, tip speed, mecanismos y tiempo de mezclado, kLa y su determinación experimental, scale-up vs scale-down.
- **TP 1** — Biorreactores: partes, dimensiones y funcionamiento.
- **TP 2** — Efecto de las propiedades físicas del medio sobre el tiempo de mezclado y la potencia.

## Lo que falta

El primer parcial incluye un bloque de **esterilización y filtración industrial** (parámetro D y z, filtración por lecho profundo, filtros en serie, HEPA, batch vs continua) que figura en el temario de la Clase 1 pero **no está entre los PDF de la cursada**. Esa parte del `parcial-resuelto.html` se resolvió con material de referencia estándar.
