# atlas-fleetpanda-api-docs

Partner-facing API documentation for the FleetPanda integration. Rendered with Swagger UI
at **https://agriland-fs.github.io/atlas-fleetpanda-api-docs/** (GitHub Pages, `main` root).

Two independent APIs, selectable from the picker at the top of the page:

| Spec | API | Direction | Auth |
|---|---|---|---|
| `openapi.yaml` | `API-100-Panda-IngestEvents` | FleetPanda → ATLAS | Cognito bearer token |
| `openapi-pricing.yaml` | `API-018-AxxisPricesOPIS` | ATLAS → FleetPanda | API key (`x-api-key`) |

They are separate documents rather than one because Swagger 2.0 permits a single `host`
per spec, and these differ in host, base path, and authentication scheme.

## Fuel Pricing (API-018)

Two read-only endpoints, refreshed on every Axxis drop:

- `GET /v1/index` — OPIS rack benchmark prices, keyed by **market**
- `GET /v1/supplier` — individual supplier quotes, keyed by **terminal**

Source: [repo-105-atlas-daily-fuel-prices](https://github.com/AGRILAND-FS/repo-105-atlas-daily-fuel-prices)
(`LFN-130-AxxisPriceSplit` writes, `LFN-131-AxxisPricesApi` serves).

`GET /v1/prices` also exists on API-018 and is **deliberately undocumented** — it is the
superseded predecessor, has never been called by any consumer, and silently truncates
results past ~1000 rows. Do not point anyone at it.

## Editing

Both specs are hand-maintained; neither is exported from API Gateway. After editing,
check the rendered page rather than trusting the YAML — Swagger UI is the contract our
partners actually read.
