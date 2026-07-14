---
tags: [proyecto, data, activo]
estado: activo
---

# Pipeline de Datos — ETL

Pipeline ETL construido con **[[Python]]** que extrae datos de múltiples fuentes, los transforma y los carga en un warehouse [[PostgreSQL]].

## Qué hace
- Extracción desde múltiples fuentes de datos
- Transformación con Pandas
- Carga en PostgreSQL vía SQLAlchemy
- Jobs programados con Cron, con logging y alertas

## Stack
[[Python]] · [[PostgreSQL]] · Pandas · SQLAlchemy · Cron

## Impacto
Procesa más de 50K registros diarios con reportes automatizados.

## Relacionado
- [[Carrera Backend]] — data engineering como especialidad
- [[Pipeline de Datos ETL]] y [[Mesa de Ayuda]] comparten la meta de eliminar trabajo manual
