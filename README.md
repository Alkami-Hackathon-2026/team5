# Partnership Integration Portal — UI Demo

An interactive prototype of a **partnership integration dashboard configuration portal**,
plus a companion **unified log explorer**. Entirely static: two self-contained HTML files,
no backend, no dependencies, no real data.

## Live demo

<https://partnership-integration-portal-demo-fc06db.gitlab.io>

The log explorer is at `/logs.html`, or reachable from any **View Logs** button.
Pages is private to this project, so viewers need GitLab access to
`alkami-technology/MP/mskolnick`.

| Page | File | What it shows |
|---|---|---|
| Configuration portal | `index.html` | Per-partner configuration across eight tabs |
| Log explorer | `logs.html` | Every log line for a partner across all ten platform domains |

## Portal

Left rail switches between integrations; the top bar switches environment
(Sandbox / UAT / Production) and financial institution.

- **Flagged Issues** — a status panel above the tabs listing conditions that may break the
  integration, with severity, the exact config that triggered each one, impact, and jump-to-fix actions
- **Overview** — health stats, catalog metadata, promotion-readiness checklist, endpoint activity
- **Configuration Variables** — key/value table with type, scope resolution
  (Global → Partner → FI → Environment), override highlighting, and policy-locked rows
- **Connectivity** — endpoints, auth method, timeouts, retry and circuit breaker, TLS,
  IP allowlist, and an animated diagnostics console
- **Admin Credentials** — write-only vault-backed secrets and a rotation schedule
- **API Keys** — issue, revoke, scopes, expiry, and key policy
- **Entitlements** — per-feature toggles plus audience targeting and rollout percentage
- **Webhooks** — callback URL, HMAC signing secret, per-event subscriptions
- **Audit Log** — immutable change history

## Demo partners

| Partner | State | Illustrates |
|---|---|---|
| Glia | Live | A healthy, fully configured integration |
| Pop.io | Degraded | Elevated latency and error rate |
| Payrailz | **Outage** | Expired mTLS certificate — every call failing, breaker open |
| Plaid | Live | A second healthy integration |
| Zelle | **Blocked** | Never enabled: unsigned contract, no credentials, no keys |

Only Zelle carries entries in the Flagged Issues panel.

## Log explorer

Per-issue **Logs** buttons deep-link with `?issue=`.

Facet rail across all ten domains a partner request touches (web, mobile, orchestration,
gateway, identity, webhooks, vault, config, audit, CDN), a stacked severity histogram with
click-to-filter hours, a query bar understanding `status:401` and `latency>500`,
expandable JSON events, a cross-domain trace waterfall, and a live-tail toggle.

## Deploying

`.gitlab-ci.yml` copies both HTML files into `public/` on every push to
`main` — no build step. Edit the files, push, done.

## Note

All content is fabricated for demonstration — partner names are real vendors, but every
credential, key, endpoint, member, and financial institution shown is invented. Nothing
here reflects a real Alkami configuration.
