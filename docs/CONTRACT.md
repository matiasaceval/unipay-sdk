# Contrato con la API

- Fuente: `openapi/unipay.v1.yaml` del repositorio privado `platform`, publicado como artefacto de cada release de la API.
- Este repo guarda una copia en `openapi/unipay.v1.yaml` con la versión de la API en el nombre del commit que la actualiza.
- Los tipos se generan (`openapi-typescript`) en `packages/sdk/src/generated/` y no se editan a mano.
- Reglas de compatibilidad de la API: cambios aditivos en v1; el SDK debe tolerar campos y valores de enum desconocidos.
- Errores: `application/problem+json` con `code` estable. El SDK los mapea a clases tipadas (ver skill `sdk`).

Diseño completo (interno): `platform/docs/SDK_AND_MCP.md` y `platform/docs/API_DESIGN.md`.
