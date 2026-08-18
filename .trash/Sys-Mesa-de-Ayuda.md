---
tags:
  - proyecto
  - workspace
  - dotnet
  - efcore
estado: activo
ruta: C:\Users\XMK-PC03\Documents\Proyectos\Sys-Mesa-de-Ayuda
---
> **Solución**: `Sys Mesa de Ayuda.sln`

## Resumen
Sistema de Mesa de Ayuda en .NET. La solución contiene varios proyectos; solo tres tienen código real.

## Stack
.NET (solución `Sys Mesa de Ayuda.sln`) · EF Core + Migrations

## Proyectos con código
- **API** — servicios REST
- **DB** — EF Core + Migrations
- **Journey** — MVC (frontend)

## Gotchas / pitfalls
- **CRÍTICO**: `APIApp/` y `Frontend.App/` contienen **solo bin/obj/node_modules** (sin .csproj ni código fuente) — no intentar compilarlos.
- El árbol del README está desactualizado; no guiarse por él.
- No confundir con [[Mesa de Ayuda]] (Power Platform/ONESVIE, stack distinto).

## Relacionado
- [[Index]]
- [[Home]]