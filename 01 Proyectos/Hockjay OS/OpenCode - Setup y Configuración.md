---
tags: [opencode, configuracion, replicacion, herramienta, linux]
estado: vigente
fecha: 2026-08-09
origen: C:\Users\XMK-PC03\.config\opencode (Windows)
destino: Linux Mint (Hockjay OS)
---

# OpenCode — Setup y Configuración

> Configuración **real** del opencode en esta máquina, documentada para levantar el mismo entorno en la otra PC (Linux Mint / Hockjay OS). Origen verificado el 2026-08-09.

## Resumen del stack

| Componente | Detalle |
|---|---|
| **CLI** | opencode (config global en `~/.config/opencode/`) |
| **Plugin** | `@bluelovers/opencode-arise` **v0.1.40** — Shadow Army (agentes sombra: beru, igris, bellion, tusk, tank, shadow-sovereign, esil-radiru, monarch) |
| **Proveedor por defecto** | `omniroute` → gateway local `http://localhost:20128/v1` (OpenAI-compatible) |
| **Modelo por defecto** | `omniroute/openrouter/nvidia/nemotron-3-ultra-550b-a55b:free` |
| **MCP** | `omniroute` (remote SSE): `http://localhost:20128/api/mcp/sse` — ~99-109 herramientas del gateway · `obsidian` (remote): `http://127.0.0.1:27123/mcp` — **16 herramientas del vault** (vault_read, vault_write, search_query…) vía plugin Local REST API v5.1.0 |
| **Skills** | `customize-opencode` (built-in) · `graphify` (Claude, en `~/.claude/skills/`) |
| **Memoria** | Vault de Obsidian (`Documents/Obsidian Vault/`) + `AGENTS.md` del workspace apuntando al vault |

---

## 1. Archivos a copiar (inventario)

| Archivo | Ruta (origen Windows) | Propósito |
|---|---|---|
| `opencode.json` | `~/.config/opencode/opencode.json` | Provider `omniroute` + MCP server + modelo por defecto |
| `opencode.jsonc` | `~/.config/opencode/opencode.jsonc` | Registro del plugin arise |
| `opencode-arise.json` | `~/.config/opencode/opencode-arise.json` | Config del plugin arise (modelos por agente) |
| `package.json` (+ `package-lock.json`) | `~/.config/opencode/` | Dependencias locales del plugin (`@opencode-ai/plugin 1.15.13`) |
| `~/.omniroute/` (entera) | `C:\Users\XMK-PC03\.omniroute\` | Gateway OmniRoute: `storage.sqlite` (contiene **keys con scope manage**), `.env`, logs |
| `~/.claude/CLAUDE.md` + `~/.claude/skills/graphify/` | — | Skill graphify (Claude Code) |
| `AGENTS.md` del workspace + vault Obsidian | `Documents/Proyectos/` | Memoria persistente de proyectos |

> ⚠️ **NO copiar** `opencode.json.bak-*` (solo referencia). El `node_modules/` de `~/.config/opencode` se regenera automáticamente con `npm install`.

---

## 2. Contenido de los archivos de configuración

### `opencode.json`

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "omniroute": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "OmniRoute Gateway",
      "options": {
        "baseURL": "http://localhost:20128/v1",
        "apiKey": "{env:OMNIROUTE_API_KEY}"
      },
      "models": {
        "oc/deepseek-v4-flash-free": { "name": "DeepSeek V4 Flash (free)" },
        "openrouter/deepseek/deepseek-v4-flash": { "name": "DeepSeek V4 Flash" },
        "free": { "name": "Free (todos + fallback auto)" },
        "free/coding": { "name": "Free Coding" },
        "free/reasoning": { "name": "Free Reasoning" },
        "free/vision": { "name": "Free Vision" },
        "gemini/gemini-3.5-flash": { "name": "Gemini 3.5 Flash" },
        "gemini/gemini-3.1-pro-preview": { "name": "Gemini 3.1 Pro Preview" },
        "gemini/gemini-2.5-pro": { "name": "Gemini 2.5 Pro" },
        "gemini/gemini-2.5-flash": { "name": "Gemini 2.5 Flash" },
        "openrouter/nvidia/nemotron-3-ultra-550b-a55b:free": { "name": "Nemotron 3 Ultra 550B (free, 1M ctx)" },
        "openrouter/nvidia/nemotron-3-super-120b-a12b:free": { "name": "Nemotron 3 Super 120B (free)" },
        "openrouter/nvidia/nemotron-3-nano-omni-30b-a3b-reasoning:free": { "name": "Nemotron 3 Nano Omni 30B (free, omni)" },
        "openrouter/nvidia/nemotron-3-nano-30b-a3b:free": { "name": "Nemotron 3 Nano 30B (free)" },
        "openrouter/nvidia/nemotron-3.5-content-safety:free": { "name": "Nemotron 3.5 Content Safety (free)" },
        "openrouter/nvidia/nemotron-nano-12b-v2-vl:free": { "name": "Nemotron Nano 12B VL (free)" },
        "openrouter/nvidia/nemotron-nano-9b-v2:free": { "name": "Nemotron Nano 9B (free)" },
        "openrouter/google/gemma-4-31b-it:free": { "name": "Gemma 4 31B (free, visión)" },
        "openrouter/google/gemma-4-26b-a4b-it:free": { "name": "Gemma 4 26B (free)" },
        "openrouter/cohere/north-mini-code:free": { "name": "Cohere North Mini Code (free)" },
        "openrouter/poolside/laguna-xs-2.1:free": { "name": "Poolside Laguna XS 2.1 (free)" },
        "openrouter/poolside/laguna-s-2.1:free": { "name": "Poolside Laguna S 2.1 (free)" },
        "openrouter/inclusionai/ling-3.0-tiny:free": { "name": "InclusionAI Ling 3.0 Tiny (free)" },
        "openrouter/openai/gpt-oss-20b:free": { "name": "OpenAI GPT-OSS 20B (free)" },
        "openrouter/free": { "name": "Auto-router free (OpenRouter)" }
      }
    }
  },
  "mcp": {
    "omniroute": {
      "type": "remote",
      "url": "http://localhost:20128/api/mcp/sse",
      "headers": { "Authorization": "Bearer <KEY_SCOPE_MANAGE>" },
      "enabled": true
    },
    "obsidian": {
      "type": "remote",
      "url": "http://127.0.0.1:27123/mcp",
      "headers": { "Authorization": "Bearer <TOKEN_LOCAL_REST_API>" },
      "enabled": true
    }
  },
  "model": "omniroute/openrouter/nvidia/nemotron-3-ultra-550b-a55b:free"
}
```

> El `<KEY_SCOPE_MANAGE>` es la API key con scope `manage` (en esta instalación: `admin-local`, guardada en `~/.omniroute/storage.sqlite` → tabla `api_keys`). La key de modelos (`opencode-cli`, env `OMNIROUTE_API_KEY`) **no** vale para el transporte MCP (da `AUTH_001 Invalid management token`).

### `opencode.jsonc` (plugin)

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "plugin": [
    "@bluelovers/opencode-arise"
  ]
}
```

### `opencode-arise.json` (agentes sombra → modelos)

```json
{
  "show_banner": true,
  "disabled_shadows": [],
  "disabled_hooks": [],
  "agents": {
    "monarch":          { "model": "anthropic/claude-opus-4-5" },
    "beru":             { "model": "anthropic/claude-haiku-4-5" },
    "igris":            { "model": "zai-coding-plan/glm-4.7" },
    "bellion":          { "model": "openai/gpt-5.2" },
    "tusk":             { "model": "google/gemini-3-pro-preview" },
    "tank":             { "model": "zai-coding-plan/glm-4.7" },
    "shadow-sovereign": { "model": "openai/gpt-5.2" },
    "esil-radiru":      { "model": "x-ai/grok-4" }
  }
}
```

---

## 3. Plugins instalados

| Plugin | Versión | Rol |
|---|---|---|
| `@bluelovers/opencode-arise` | **0.1.40** | Shadow Army: summon de agentes (arise_summon, arise_background, arise_collaborate…). Se autoinstala en `~/.cache/opencode/packages/` al arrancar opencode |
| `@opencode-ai/plugin` | 1.15.13 | SDK de plugins (dependencia local) |

> El plugin **no** va en `~/.config/opencode/node_modules` de forma persistente: opencode lo instala por su cuenta desde el registro npm al leer `plugin` del `opencode.jsonc`. Solo hay que copiar el `.jsonc`.

---

## 4. Skills disponibles

- **`customize-opencode`** (built-in de opencode): se activa al editar `opencode.json`/`.opencode/` del proyecto o la config global. No requiere instalación.
- **`graphify`** (`~/.claude/skills/graphify/SKILL.md`): convierte cualquier input en knowledge graph persistente (`/graphify` — usado desde Claude Code). Copiar la carpeta `skills/graphify` + el `~/.claude/CLAUDE.md`.

---

## 5. Proveedores y autenticación

| Proveedor | Cómo se autentica | Estado en origen |
|---|---|---|
| `google` | `opencode auth login` → Google / Gemini | ✅ en `auth.json` |
| `anthropic` | `opencode auth login` → Anthropic | ✅ en `auth.json` |
| `openai` | `opencode auth login` o `OPENAI_API_KEY` | ⚠️ no autenticado (arise lo referencia: gpt-5.2) |
| `x-ai` | `opencode auth login` o `XAI_API_KEY` | ⚠️ no autenticado (arise: grok-4) |
| `zai-coding-plan` | `opencode auth login` | ⚠️ no autenticado (arise: glm-4.7) |
| `omniroute` | env var nivel usuario `OMNIROUTE_API_KEY` | ✅ (env User) |

> En la otra PC conviene hacer `opencode auth login` para todos los proveedores que usan los agentes arise, o los sombras caerán al modelo por defecto.

---

## 6. Gateway OmniRoute (requisito del provider y del MCP)

- **Docs completas**: `Guia_Adaptacion_OpenCode_OmniRoute_Limpio.md` (instalación `npm i -g omniroute`, providers, keys, free models).
- **Activación MCP**: se persiste en la BD `~/.omniroute/storage.sqlite` (`key_value` namespace `settings`: `mcpEnabled=true`, `mcpTransport="sse"`) + invalidar caché con `PUT /api/settings/memory {"enabled":true}`. Detalle completo en la **sección 8** de la guía.
- **Keys**: `opencode-cli` (modelos, restringida a los 15 `:free`) · `admin-local` (scope `manage`, usada por el MCP de opencode).
- **Requiere**: Node ≥ 22, `better-sqlite3` nativo (`omniroute runtime repair` si falla).

---

## 7. Pasos para levantar en Linux Mint (orden)

1. **Instalar Node 22+** (nvm o apt) y npm.
2. **Instalar opencode y el gateway**:
   ```bash
   npm i -g opencode-ai omniroute
   ```
3. **Copiar la config**:
   ```bash
   mkdir -p ~/.config/opencode
   # copiar desde el origen: opencode.json, opencode.jsonc, opencode-arise.json
   cd ~/.config/opencode && npm install   # instala @opencode-ai/plugin local
   ```
4. **Copiar OmniRoute**: mover `~/.omniroute/` completo (trae `storage.sqlite` con las keys incl. `admin-local`, y `.env`). Alternativa limpia: reinstalar y reconfigurar desde la guía.
5. **Env var**: `export OMNIROUTE_API_KEY="<key opencode-cli>"` en `~/.bashrc` (persistente).
6. **Arrancar y verificar el gateway**:
   ```bash
   omniroute serve   # ~1 min (sync openrouter)
   omniroute health
   curl http://localhost:20128/api/mcp/status   # → "enabled":true,"transport":"sse"
   ```
7. **Verificar auth**: `opencode auth login` para google, anthropic, openai, x-ai, zai-coding-plan (si se quieren los modelos de arise).
8. **MCP en opencode**: ya viene en el `opencode.json` copiado; al iniciar opencode debe aparecer el server `omniroute` (`/mcp` en el TUI). Las ~109 herramientas quedan disponibles.
9. **(Opcional) Skills**: copiar `~/.claude/skills/graphify/` + `~/.claude/CLAUDE.md` (Claude Code); el vault de Obsidian (memoria de proyectos) y el `AGENTS.md` del workspace.

---

## 8. Secretos — dónde viven (NO versionar ni compartir)

| Secreto | Ubicación |
|---|---|
| Key `opencode-cli` (modelos, free) | env `OMNIROUTE_API_KEY` (User) |
| Key `admin-local` (scope manage → MCP) | `~/.omniroute/storage.sqlite` → tabla `api_keys` |
| Credenciales proveedores | `~/.local/share/opencode/auth.json` |
| Secrets del gateway (JWT, INITIAL_PASSWORD, encryption) | `~/.omniroute/.env` y `.env` del paquete npm |
| Token/plugin Obsidian Local REST API | Obsidian (por instalar) |

---

## 9. Checklist de verificación tras el despliegue

- [ ] `opencode --version` y arise banner visible
- [ ] `omniroute health` → healthy
- [ ] `GET /api/mcp/status` → `"status":"online","enabled":true,"transport":"sse"`
- [ ] En opencode: `/mcp` muestra `omniroute` conectado (~99-109 tools) y `obsidian` conectado (16 tools del vault)
- [ ] `opencode -m omniroute/openrouter/nvidia/nemotron-3-ultra-550b-a55b:free "hola"` responde
- [ ] `opencode auth login` completado para los proveedores deseados
- [ ] Obsidian con plugin **Local REST API** v5.1.0 activo (puerto inseguro 27123, mismo token en `opencode.json` y en el Context Source del gateway: `GET /api/settings/obsidian → connected:true`)

---

## Relacionado
- [[Hockjay OS - Mint Variant]] · [[Hockjay OS - Parrot Variant]]
- [[OmniRoute (Gateway IA)]] + guía técnica en `Documents/Proyectos/Guia_Adaptacion_OpenCode_OmniRoute_Limpio.md`
- [[Index]]