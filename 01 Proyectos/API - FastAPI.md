---
tags:
  - proyecto
  - workspace
  - fastapi
  - mongodb
estado: activo
ruta: C:\Users\XMK-PC03\Documents\Proyectos\api-fastapi
---

# api-fastapi

> **Ruta**: `C:\Users\XMK-PC03\Documents\Proyectos\api-fastapi`
> **Instrucciones**: `CLAUDE.md` dentro del proyecto

## Resumen
API REST con FastAPI y MongoDB Atlas.

## Stack
FastAPI · Uvicorn · MongoDB Atlas (motor)

## Comandos clave
```bash
# Ejecutar SIEMPRE desde la carpeta FastApi/ (imports relativos + mount de static/)
uvicorn main:app --reload
```

## Gotchas / pitfalls
- Ejecutar **siempre desde `FastApi/`** — los imports relativos y el mount de `static/` dependen del working directory.
- Para entorno local usar `MongoClient().local`.

## Secretos
- Credenciales Atlas en `db/client.py` — no volcar al chat.

## Relacionado
- [[Index]]
- [[Home]]