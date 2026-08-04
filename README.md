# Firefly Health

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
