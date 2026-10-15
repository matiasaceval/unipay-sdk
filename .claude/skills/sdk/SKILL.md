---
name: sdk
description: Diseñar, implementar, probar y publicar el SDK TypeScript @unipay/sdk - tipos generados desde OpenAPI, cliente, errores tipados, reintentos, idempotencia, ejemplos y versionado semántico. Usar ante cualquier cambio en packages/sdk o al actualizar el contrato.
---

# SDK `@unipay/sdk`

## Principios
- Cliente fino: refleja la API, no la reimplementa. Ninguna regla de negocio, autorización ni licencia en el SDK.
- Solo servidor (Node.js LTS). No documentar uso en navegador: expondría la credencial.

## Al actualizar el contrato
1. Copiar el nuevo `unipay.v1.yaml` publicado por la API a `openapi/`.
2. Regenerar tipos (`src/generated/`, no editar a mano).
3. Ajustar la capa ergonómica (`unipay.payments.create`, etc.) solo para endpoints nuevos.
4. Tests contra el mock generado del OpenAPI (Prism) + suite de humo en sandbox (`@sandbox`, requiere credencial `upk_test_…`).
5. Changeset con el tipo de versión: `patch` (fix), `minor` (endpoint/campo nuevo), `major` (cambio incompatible del SDK).

## Comportamiento obligatorio
- `Idempotency-Key` automática en `payments.create` y `refunds.create`, reutilizada en reintentos.
- Reintentos solo en red/429/5xx idempotentes; respetar `Retry-After`; máximo configurable.
- Errores por `code`: `AuthenticationError` (`invalid_credential`, `credential_revoked`, `credential_expired`), `SubscriptionInactiveError`, `PermissionError` (`insufficient_scope`, `feature_not_in_plan`), `RateLimitError` (`retryAfter`), `OperationNotSupportedError` (`capability`, `reason`), `ConflictError`, `ValidationError`, `ProviderError`. Todos con `requestId` y `status`.
- Tolerar campos y enums desconocidos (test explícito).
- `webhooks.verify(payload, headers, secret)` con Standard Webhooks.
- Nunca loguear la credencial.

## Publicación
CI con npm provenance, ESM + CJS, `exports` explícitos, README con ejemplos ejecutables contra sandbox, CHANGELOG generado.
