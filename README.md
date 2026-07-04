# 🧠 Segundo Cerebro

Vault personal de conocimiento de **Marcos Mateo Tiburcio** (KMBMarcos), organizado con la metodología [PARA](https://fortelabs.com/blog/para/) + [CODE](https://fortelabs.com/blog/basboverview/) (Building a Second Brain, Tiago Forte) y visualizado como grafo de conocimiento con [graphify](https://github.com/safishamsi/graphify).

## Estructura

| Carpeta | Qué contiene |
|---|---|
| `00 Inbox` | Bandeja de captura — todo lo nuevo entra aquí primero |
| `01 Proyectos` | Esfuerzos con fecha y resultado concreto |
| `02 Areas` | Responsabilidades continuas sin fecha final |
| `03 Recursos` | Temas de interés y material de referencia |
| `04 Archivo` | Todo lo inactivo de las otras tres |
| `05 Plantillas` | Plantillas reutilizables |

Empieza por [`Home.md`](Home.md) — es el dashboard central.

## Grafo de conocimiento

La carpeta `graphify-out/` contiene el grafo generado:

- **`graph.html`** — grafo interactivo, ábrelo en cualquier navegador
- **`GRAPH_REPORT.md`** — reporte de auditoría (nodos centrales, conexiones, preguntas)
- **`graph.json`** — datos del grafo para consultas

Para regenerarlo tras añadir notas, desde la raíz del vault:

```bash
python -m graphify . --update
```

## Uso

1. Abre esta carpeta como vault en [Obsidian](https://obsidian.md/).
2. Captura ideas en `00 Inbox` sin organizar.
3. Procesa la bandeja 1–2 veces por semana moviendo cada nota según PARA.
