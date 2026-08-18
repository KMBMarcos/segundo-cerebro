Esta guía detalla los pasos para crear e implementar un sistema de memoria persistente local y segura para tus proyectos utilizando OmniRoute como pasarela inteligente y Obsidian como almacén estructurado de conocimiento.
1. Preparación del Entorno
Para que OmniRoute pueda gestionar la memoria de largo plazo en archivos locales, primero debes preparar la infraestructura de conexión:
Instala OmniRoute: Utiliza el comando npm install -g omniroute e inicia el servicio con omniroute.
Prepara Obsidian: Instala el plugin comunitario Obsidian Local REST API dentro de tu aplicación Obsidian.
Obtén la Clave de API: En la configuración del plugin en Obsidian, genera un token de acceso. Por defecto, el plugin escuchará en el puerto 27123.
2. Configuración de la Fuente de Contexto
Debes vincular tu "bóveda" (vault) de Obsidian con OmniRoute para que los agentes puedan leer y escribir en ella:
Accede al Dashboard de OmniRoute (http://localhost:20128).
Ve a la pestaña Context Sources y selecciona Obsidian.
Introduce el Token generado en Obsidian y la Base URL (típicamente http://127.0.0.1:27123).
Aislamiento por Proyecto: Si manejas varios proyectos, OmniRoute permite asignar vaults y rutas específicas de Obsidian por cada API Key generada. Esto evita que la memoria de un proyecto se mezcle con otro.
3. Activación de la Memoria Automática (Transaccional)
OmniRoute incluye un sistema nativo de dos fases que funciona de forma invisible para el agente:
Extracción (extraction.ts): OmniRoute intercepta las respuestas del LLM, aísla hechos críticos o decisiones de diseño y los persiste automáticamente en una base de datos local SQLite utilizando indexación FTS5 para búsquedas rápidas.
Inyección (injection.ts): Antes de enviar una nueva petición al modelo, el inyector busca recuerdos correlacionados en el almacén local y los añade dinámicamente al prompt de sistema, dotando al modelo de "recuerdos" de turnos previos.
Configuración: Asegúrate de que las variables extractionEnabled e injectionEnabled estén activas en los ajustes de persistencia del sistema.
4. Implementación de Memoria por Proyecto vía MCP
Para una memoria más proactiva donde el agente gestione su propio conocimiento, utiliza el protocolo MCP (Model Context Protocol):
Habilita el Servidor MCP: Ejecuta OmniRoute con la bandera omniroute --mcp para exponer las herramientas de gestión de memoria.
Herramientas Disponibles: El agente podrá utilizar herramientas como obsidian_write_note para guardar descubrimientos o obsidian_search_simple para recuperar información específica del proyecto.
Estrategia de Guardado: Se recomienda instruir al agente para que invoque obsidian_append_note al final de cada sesión para resumir cambios críticos o parches aplicados.
5. Continuidad con "Context Relay"
Si el agente debe cambiar de modelo de IA a mitad de una tarea (por ejemplo, si se agota la cuota de un proveedor), activa la estrategia Context Relay:
Cuando el consumo de cuota llega al 85%, OmniRoute genera un resumen técnico estructurado de la sesión actual.
Al conmutar al nuevo modelo, OmniRoute inyecta ese resumen como un mensaje de sistema prioritario, permitiendo que el agente continúe el trabajo sin perder el hilo del contexto anterior.
6. Seguridad y Auditoría
La gestión de memoria local requiere medidas preventivas para evitar corrupciones o ataques de inyección:
Control de Permisos (Scopes): Activa OMNIROUTE_MCP_ENFORCE_SCOPES=true para restringir qué agentes pueden escribir en tu memoria de Obsidian (permiso write:obsidian).
Uso de Git: Almacena tu bóveda de Obsidian como un repositorio Git. Esto permite auditar qué recuerdos ha guardado el agente y revertir cualquier cambio erróneo mediante un git revert.
Auditoría: Revisa regularmente la tabla mcp_tool_audit en el dashboard para supervisar qué herramientas de memoria han sido invocadas y por quién.