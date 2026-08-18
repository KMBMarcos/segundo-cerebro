---
tags:
  - recurso
  - workspace
  - infraestructura
estado: en curso
ruta: C:\Users\XMK-PC03\Documents\Proyectos\Guia_Adaptacion_OpenCode_OmniRoute_Limpio.md
---
# OmniRoute (Gateway IA)

> **Guía completa**: `C:\Users\XMK-PC03\Documents\Proyectos\Guia_Adaptacion_OpenCode_OmniRoute_Limpio.md` (+ sección de uso y pasos)

## Resumen
Gateway local de IA multiproveedor (OmniRoute v3.8.48) con failover automático. Unifica proveedores en un único endpoint.

- **Dashboard**: `http://localhost:20128`
- **API OpenAI-compatible**: `http://localhost:20128/v1`

## Configuración actual (verificada)
- **Proveedores activos**: `gemini` y `openrouter` (key de OpenRouter válida, test passed)
- **Catálogo openrouter**: 400 modelos sincronizados, 14 variantes `:free`
- **Restricción free**: la API key `opencode-cli` tiene `allowedModels` con los 15 modelos free (cualquier modelo pago → 403; verificado con gpt-4o)
- **Modelo por defecto (opencode)**: `omniroute/openrouter/nvidia/nemotron-3-ultra-550b-a55b:free`
- **Env var**: `OMNIROUTE_API_KEY` (persistida a nivel usuario — la key `sk-eef1...` NO escribir en archivos)
- **Memoria transaccional**: activada (`settings.memoryEnabled=true`)

## MCP (herramientas) — ACTIVADO ✔
- **Estado**: `online` · transporte `sse` · **~109 herramientas** (health, memoria, providers, combos, usage…)
- **Endpoint**: `http://localhost:20128/api/mcp/sse`
- **Auth**: solo keys con scope `manage` (la `opencode-cli` da `AUTH_001`). Usar **`admin-local`** (scope `manage`, creada en setup; valor en `storage.sqlite` → tabla `api_keys`)
- **opencode**: bloque `mcp.omniroute` (type remote → SSE) ya añadido en `~/.config/opencode/opencode.json` — visible tras reiniciar opencode
- **Enable persistido** en `key_value` (namespace `settings`): `mcpEnabled=true`, `mcpTransport="sse"` — método completo en la guía, sección 8
- **Backup reversible**: `%TEMP%\opencode\storage-mcp-backup-*.sqlite`
- ✔ **Context Source Obsidian conectado** (2026-08-09): plugin Local REST API v5.1.0 en `http://127.0.0.1:27123` (puerto no cifrado 27123, token en Obsidian → Settings → Local REST API). Verificado: `GET /api/settings/obsidian → connected:true`. El servicio token está guardado en la BD del gateway (no escribir en notas)
- 💡 Bonus: el plugin Local REST API v5+ **incluye un MCP server propio** — se puede añadir como segundo MCP en opencode apuntando a su endpoint (opcional)

## Comandos útiles
```bash
omniroute serve                 # arrancar (tarda ~1 min en el sync de openrouter)
omniroute stop / status / health
omniroute providers list / test openrouter
omniroute models openrouter     # catálogo
```


## Relacionado
[[Index]]
[[Home]]
## Gotchas
- El servidor tarda ~1 min en arrancar cuando openrouter está activo (no asumir caído).
- Formato de IDs de modelo: `openrouter/<modelo>` (sin el prefijo da "No active credentials for provider: <vendor>").
- Si falla `better-sqlite3`: `omniroute runtime repair` o `npm rebuild better-sqlite3` (Node 24 requiere v137).
