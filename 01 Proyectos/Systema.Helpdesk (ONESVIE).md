---
tags:
  - proyecto
  - workspace
  - dotnet
estado: activo
ruta: C:\Users\XMK-PC03\Documents\Proyectos\project-void
---
> **Instrucciones**: `AGENTS.md` dentro del proyecto

## Resumen
Sistema de Helpdesk (Systema.Helpdesk) construido con ASP.NET Core MVC sobre .NET 9, con autenticación vía Entra ID, integración con Microsoft Graph/SharePoint y persistencia en Supabase. Esta plataforma de mesa de ayuda se está construyendo en para reemplazar la actual arquitectura en [[Mesa de Ayuda (ONESVIE)]].

## Stack
ASP.NET Core MVC (.NET 9) · Entra ID · Graph/SharePoint · Supabase (Npgsql)

## Comandos clave
```bash
# Ejecutar desde la raíz del proyecto
dotnet run --project "Systema.Helpdesk/Systema.Helpdesk.csproj"
```

## Gotchas / pitfalls
- **CRÍTICO**: la base de datos es **Postgres/Npgsql, NO SQL Server** — no asumir provider SQL.
- Secretos solo vía `dotnet user-secrets`.
- No incluir caracteres `< >` en los valores guardados (rompe el parseo).

## Secretos
- Cadenas de conexión Entra/Supabase: solo en `dotnet user-secrets` — never volcar al chat.

## Relacionado
- [[Index]]
- [[Home]]