# Graph Report - .  (2026-07-04)

## Corpus Check
- Corpus is ~3,300 words - fits in a single context window. You may not need a graph.

## Summary
- 29 nodes · 104 edges · 5 communities
- Extraction: 100% EXTRACTED · 0% INFERRED · 0% AMBIGUOUS
- Token cost: 0 input · 0 output

## Community Hubs (Navigation)
- [[_COMMUNITY_Ecosistema Microsoft (Trabajo)|Ecosistema Microsoft (Trabajo)]]
- [[_COMMUNITY_GitHub y Proyectos Personales|GitHub y Proyectos Personales]]
- [[_COMMUNITY_Stack Python y Datos|Stack Python y Datos]]
- [[_COMMUNITY_Metodología Segundo Cerebro|Metodología Segundo Cerebro]]
- [[_COMMUNITY_Carrera y Portafolio|Carrera y Portafolio]]

## God Nodes (most connected - your core abstractions)
1. `Home` - 20 edges
2. `Carrera Backend` - 16 edges
3. `ONESVIE` - 13 edges
4. `Stack Técnico` - 11 edges
5. `ASP.NET Core` - 10 edges
6. `API Gateway` - 9 edges
7. `Azure` - 9 edges
8. `Método PARA` - 9 edges
9. `Marca Personal y Contenido` - 8 edges
10. `Perfil GitHub` - 8 edges

## Surprising Connections (you probably didn't know these)
- `Home` --references--> `Cómo usar la bandeja`  [EXTRACTED]
  Home.md → 00 Inbox/Cómo usar la bandeja.md
- `Método PARA` --references--> `API Gateway`  [EXTRACTED]
  03 Recursos/Método PARA.md → 01 Proyectos/API Gateway.md
- `Home` --references--> `API Gateway`  [EXTRACTED]
  Home.md → 01 Proyectos/API Gateway.md
- `Home` --references--> `Automatización Power Platform`  [EXTRACTED]
  Home.md → 01 Proyectos/Automatización Power Platform.md
- `Pipeline de Datos ETL` --references--> `Carrera Backend`  [EXTRACTED]
  01 Proyectos/Pipeline de Datos ETL.md → 02 Areas/Carrera Backend.md

## Import Cycles
- None detected.

## Hyperedges (group relationships)
- **Ecosistema Microsoft** — 03_recursos_asp_net_core_asp_net_core, 03_recursos_sql_server_sql_server, 03_recursos_azure_azure, 03_recursos_power_platform_power_platform, 02_areas_onesvie_onesvie, 01_proyectos_api_gateway_api_gateway [INFERRED 0.85]
- **Stack Python open-source** — 03_recursos_python_python, 03_recursos_postgresql_postgresql, 01_proyectos_pipeline_de_datos_etl_pipeline_de_datos_etl, 04_archivo_no_country_no_country [INFERRED 0.85]
- **Flujo CODE + PARA** — 03_recursos_segundo_cerebro_segundo_cerebro, 03_recursos_metodo_para_metodo_para, 00_inbox_como_usar_la_bandeja_como_usar_la_bandeja [INFERRED 0.95]

## Communities (5 total, 0 thin omitted)

### Community 0 - "Ecosistema Microsoft (Trabajo)"
Cohesion: 0.72
Nodes (9): API Gateway, Automatización Power Platform, Aprendizaje Azure, ONESVIE, ASP.NET Core, Azure, Power Platform, SQL Server (+1 more)

### Community 1 - "GitHub y Proyectos Personales"
Cohesion: 0.57
Nodes (7): Hockjay OS, ZaunService, Marca Personal y Contenido, Perfil GitHub, Workstation, Plantilla de Proyecto, Home

### Community 2 - "Stack Python y Datos"
Cohesion: 0.70
Nodes (5): Pipeline de Datos ETL, PostgreSQL, Python, No Country, Proyectos de Aprendizaje GitHub

### Community 3 - "Metodología Segundo Cerebro"
Cohesion: 0.67
Nodes (4): Cómo usar la bandeja, Método PARA, Segundo Cerebro, Plantilla de Nota Diaria

### Community 4 - "Carrera y Portafolio"
Cohesion: 0.67
Nodes (4): Portafolio Web, Sys-PLA, Carrera Backend, Astro

## Knowledge Gaps
- **2 isolated node(s):** `Plantilla de Nota Diaria`, `Plantilla de Proyecto`
  These have ≤1 connection - possible missing edges or undocumented components.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `Home` connect `GitHub y Proyectos Personales` to `Ecosistema Microsoft (Trabajo)`, `Stack Python y Datos`, `Metodología Segundo Cerebro`, `Carrera y Portafolio`?**
  _High betweenness centrality (0.337) - this node is a cross-community bridge._
- **Why does `Carrera Backend` connect `Carrera y Portafolio` to `Ecosistema Microsoft (Trabajo)`, `GitHub y Proyectos Personales`, `Stack Python y Datos`, `Metodología Segundo Cerebro`?**
  _High betweenness centrality (0.135) - this node is a cross-community bridge._
- **Why does `Cómo usar la bandeja` connect `Metodología Segundo Cerebro` to `GitHub y Proyectos Personales`?**
  _High betweenness centrality (0.071) - this node is a cross-community bridge._
- **What connects `Plantilla de Nota Diaria`, `Plantilla de Proyecto` to the rest of the system?**
  _2 weakly-connected nodes found - possible documentation gaps or missing edges._