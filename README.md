# UniPay SDK y MCP

Clientes oficiales de la API de UniPay. Este repositorio está pensado para poder publicarse como código abierto: no contiene lógica de negocio ni secretos.

> Estado: **sin código** (2026-10-15). Se implementa en la Fase 5 (SDK) y 6 (MCP), cuando la API v1 sea estable.

## Paquetes previstos
| Paquete | Qué es |
|---|---|
| `@unipay/sdk` | Cliente TypeScript/JavaScript para Node.js: pagos, devoluciones, terminales, capacidades, verificación de webhooks, errores tipados |
| `@unipay/mcp` | Servidor MCP local (stdio) para que agentes de IA consulten terminales y pagos e inicien cobros con confirmación |

## Requisito de uso
Ambos necesitan una **credencial de plataforma** (`upk_test_…` o `upk_live_…`). Las claves de prueba (`upk_test_…`) son gratis y no vencen; las reales (`upk_live_…`) necesitan un cliente con **suscripción vigente**. El control lo hace la API: el SDK y el MCP no pueden saltearlo.

## Contrato
Los tipos se generan desde el OpenAPI publicado por la API (`unipay.v1.yaml`). Ver [docs/CONTRACT.md](docs/CONTRACT.md).
