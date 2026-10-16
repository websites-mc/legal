# legal

Per-client SMS **Terms & Conditions** and **Privacy Policy** pages for 10DLC / toll-free registrations, served by GitHub Pages (Jekyll, no plugins).

Base URL: `https://legal.interline.chat`

## Add a client (3 files, one commit)

| File | Purpose |
|---|---|
| `_data/clients/<slug>.yml` | All client details (copy `_templates/client.yml`) |
| `<slug>/terms.html` | Front matter only: `layout: terms`, `client: <slug>`, `permalink: /<slug>/terms/` |
| `<slug>/privacy.html` | Front matter only: `layout: privacy`, `client: <slug>`, `permalink: /<slug>/privacy/` |

Live about a minute after push:

- `https://legal.interline.chat/<slug>/terms/` → TCR **termsAndConditionsLink** (toll-free: termsAndConditionsUrl)
- `https://legal.interline.chat/<slug>/privacy/` → TCR **privacyPolicyLink** (toll-free: privacyPolicyUrl)

`<slug>` = lowercase, hyphens, e.g. `yossis-fish`.

## What every page includes (and why)

Terms: brand name, program description, message types, opt-in methods, frequency, "Message and data rates may apply", **HELP**/**STOP** in bold caps, carrier-liability disclaimer, link to the client's Privacy Policy, contact info.
Privacy: data collected and how it's used, no sharing of mobile opt-in data for marketing (Bandwidth wording), opt-out keywords, contact info.

Sources: BW – 10DLC vetting tips and tricks; BW – New requirements for 10DLC vetting; BW – New Toll-Free rule for Privacy Policy & T&Cs. Terms and Privacy are always two separate URLs (a combined page causes an 805 rejection).

## Rules

- `brand_name` must match the TCR brand name exactly.
- Pages render as static HTML at build time, so vetters and crawlers always see full content.
- Don't put anything on these pages that the client wouldn't put on their own site (SHAFT-C content gets the campaign rejected).

## Keyword opt-in pages (optional, for clients with no website or no opt-in form)

Set `keyword`, `sms_number` and `keyword_summary` in the client's data file, then add two front-matter-only files:

| File | Front matter | Live at |
|---|---|---|
| `<slug>/sms.html` | `layout: sms`, `client: <slug>`, `permalink: /<slug>/sms/` | `https://legal.interline.chat/<slug>/sms/`: public keyword page with the full disclosure. Use it as the CTA link in TCR and in the client's posts. |
| `<slug>/sign.html` | `layout: sign`, `client: <slug>`, `permalink: /<slug>/sign/` | `https://legal.interline.chat/<slug>/sign/`: printable letter-size sign for the counter or window. |

The client must actually post the sign or share the page. The CTA screenshot uploaded to TCR is a photo or screenshot of the real, published ad, never a mock-up. See `playbooks/keyword-cta-playbook.md` in the compliance knowledge repo.
