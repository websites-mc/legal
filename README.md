# legal

Per-client SMS **Terms & Conditions** and **Privacy Policy** pages for 10DLC / toll-free registrations, served by GitHub Pages (Jekyll, no plugins).

Base URL: `https://websites-mc.github.io/legal`

## Add a client (3 files, one commit)

| File | Purpose |
|---|---|
| `_data/clients/<slug>.yml` | All client details (copy `_templates/client.yml`) |
| `<slug>/terms.html` | Front matter only: `layout: terms`, `client: <slug>`, `permalink: /<slug>/terms/` |
| `<slug>/privacy.html` | Front matter only: `layout: privacy`, `client: <slug>`, `permalink: /<slug>/privacy/` |

Live about a minute after push:

- `https://websites-mc.github.io/legal/<slug>/terms/` → TCR **termsAndConditionsLink** (toll-free: termsAndConditionsUrl)
- `https://websites-mc.github.io/legal/<slug>/privacy/` → TCR **privacyPolicyLink** (toll-free: privacyPolicyUrl)

`<slug>` = lowercase, hyphens, e.g. `yossis-fish`.

## What every page includes (and why)

Terms: brand name, program description, message types, opt-in methods, frequency, "Message and data rates may apply", **HELP**/**STOP** in bold caps, carrier-liability disclaimer, link to the client's Privacy Policy, contact info.
Privacy: data collected and how it's used, no sharing of mobile opt-in data for marketing (Bandwidth wording), opt-out keywords, contact info.

Sources: BW – 10DLC vetting tips and tricks; BW – New requirements for 10DLC vetting; BW – New Toll-Free rule for Privacy Policy & T&Cs. Terms and Privacy are always two separate URLs (a combined page causes an 805 rejection).

## Rules

- `brand_name` must match the TCR brand name exactly.
- Pages render as static HTML at build time, so vetters and crawlers always see full content.
- Don't put anything on these pages that the client wouldn't put on their own site (SHAFT-C content gets the campaign rejected).
- Custom domain later: add a `CNAME` file and set `baseurl: ""` in `_config.yml`.
