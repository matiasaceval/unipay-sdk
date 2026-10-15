# Instrucciones para Claude — repo `sdk`

- Este repo puede ser **público**: nunca agregar secretos, URLs internas, detalles de proveedores no públicos ni lógica de negocio de la API.
- SDK y MCP son clientes finos de la API. No duplicar validaciones de negocio, autorización, suscripción ni rate limiting: todo eso lo aplica la API.
- Antes de trabajar: leer `docs/CONTRACT.md` y la skill que corresponda (`sdk` o `mcp`). Si tenés acceso a `../platform`, su `docs/SESSION_CONTEXT.md` describe el estado general.
- Documentación en español. Todo lo relacionado con código va en inglés: identificadores, comentarios, mensajes, nombres de tests, commits, ramas y PR.
