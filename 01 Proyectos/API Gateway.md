---
tags: [proyecto, backend, produccion]
estado: producción
---

# API Gateway — Servicios Internos

Gateway REST centralizado para microservicios internos, construido con **[[ASP.NET Core]]**.

## Qué hace
- Autenticación con JWT
- Rate limiting
- Enrutamiento de peticiones entre múltiples servicios

## Stack
[[ASP.NET Core]] · C# · [[SQL Server]] · [[Azure]] App Service · JWT

## Impacto
Sirve a 3 aplicaciones internas con 99.9% de uptime.

## Relacionado
- [[ONESVIE]] — contexto laboral del proyecto
- [[Automatización Power Platform]] — consumidores internos de las APIs
