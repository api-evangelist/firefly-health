# Firefly Health

Firefly Health is a virtual-first primary care practice and clinically integrated health plan founded in 2016 and headquartered in Watertown, Massachusetts. Members get a dedicated care team — a primary care physician, nurse practitioner, health guide and behavioral health specialist — reachable by chat and video through the Firefly Health app, backed by the Firefly Nearby network for in-person, at-home and specialty care. Firefly sells an employer-sponsored alternative health plan alongside its virtual primary care service, and in 2025 became the first national primary care practice to earn NCQA Virtual Care Accreditation.

- Website: https://www.fireflyhealth.com/
- Member portal: https://members.firefly.health/
- GitHub: https://github.com/fireflyhealth
- Secondary market listing: https://forgeglobal.com/firefly-health_stock/

## API surface

**Firefly Health publishes no public API.** There is no developer portal, no documentation, no API reference, no SDK, no CLI, no Postman collection and no machine-readable specification of any kind.

The member web and mobile apps are served by a **private** first-party API observed at `https://api-prod.firefly.health/api/v2/` (referenced from the `members.firefly.health` application bundle). It answers from a gunicorn origin with HSTS preload, a CSP, `X-Frame-Options: DENY` and `X-Content-Type-Options: nosniff`, and varies on `Cookie` — session-based authentication. Every discovery path probed on 2026-08-01 returned 404: `/openapi.json`, `/openapi.yaml`, `/swagger.json`, `/v1/openapi.json`, `/api-docs`, `/docs`, `/redoc`, `/graphql`, `/metadata`, `/fhir/metadata`, and every `/.well-known/*` path.

`members.firefly.health` is a single-page app whose catch-all route answers **HTTP 200 with the same HTML shell for every path**, including `/.well-known/agent-card.json`. Those 200s are false positives and are recorded as rejected — no agent card, no OpenAPI, no OIDC metadata exists there.

## Artifacts

| Artifact | Method | Result |
|---|---|---|
| `conformance/firefly-health-conformance.yml` | searched | HIPAA Notice of Privacy Practices, NCQA Virtual Care Accreditation, CMS Transparency in Coverage; no FHIR / SMART / OAuth / OpenAPI posture |
| `lifecycle/firefly-health-lifecycle.yml` | probed | `/api/v2/` URI-path versioning; **no** status page, SLA, changelog or deprecation policy; acquisition by Included Health announced 2026-07-28 |
| `security/firefly-health-domain-security.yml` | probed | TLS 1.3 on the web hosts, TLS 1.2 on the API host; HSTS preload on `api-prod.firefly.health` only; DNSSEC on both domains; CAA on `firefly.health` only; SPF + DMARC on both (`p=none` on `fireflyhealth.com`) |
| `well-known/firefly-health-well-known.yml` | probed | **none** — no security.txt, OIDC, OAuth, api-catalog, ai-plugin or agent card on any host |
| `llms/firefly-health-llms.txt` | generated | Catalog-derived llms.txt (Firefly publishes no `/llms.txt`) |

Not written, because nothing real was found to write: `openapi/`, `graphql/`, `asyncapi/`, `mcp/`, `a2a/`, `skills/`, `packages/`, `cli/`, `sandbox/`, `changelog/`, `components/`, `errors/`, `data-model/`, `conventions/`, `overlays/`, `scopes/`, `authentication/`, `grpc/`. No agent card was authored — that artifact is search-only.

## Corporate

Included Health signed a definitive agreement to acquire Firefly Health on 2026-07-28, expected to close in Q3 2026. Re-probe these hosts after the close; the `members.firefly.health` and `api-prod.firefly.health` surfaces may move or retire.
