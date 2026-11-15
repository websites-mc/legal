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

Optional extras:

| Field / file | Effect |
|---|---|
| `logo`, `brand_color`, `perks` | Optional branding on the sign and card: logo path in the repo, accent color, up to 3 benefit tiles on the sign. QR codes use vendored `assets/qrcode.js` (MIT). |
| `hosted_sms: true` | Client texts from their own hosted number: do NOT add `<slug>/sms.html` (a CTA on our domain is not accepted for hosted SMS; the opt-in must be on the client's own page or printed materials). Sign and card then show Terms + Privacy URLs instead of the SMS page. |
| `conversational: true` | Adds "Questions? Just text us" + the consumer-initiated disclosure (replies only, no marketing unless they text the keyword) to the sms, sign and card pages. |
| `<slug>/card.html` (`layout: card`, `permalink: /<slug>/card/`) + optional `card_headline`, `card_message` | `https://legal.interline.chat/<slug>/card/`: printable delivery/receipt insert, 4 per letter page (4.25 × 5.5 in), with QR code that opens a text with the keyword. |

The client must actually post the sign or share the page. The CTA screenshot uploaded to TCR is a photo or screenshot of the real, published ad, never a mock-up. See `playbooks/keyword-cta-playbook.md` in the compliance knowledge repo.

## Printed pieces (placements)

Clients onboarded through the Interline back office list **placements**: where the keyword opt-in is advertised. Each printed placement gets one printable page, a "piece", built by `_layouts/piece.html`. **A slug whose data file has `org_id` is written only by the back office.** Don't edit its files by hand: every publish rewrites the data file and deletes any `<slug>/*.html` or `<slug>/logo.*` it didn't write in that commit.

What the back office commits, in one commit per publish:

| File | Content |
|---|---|
| `_data/clients/<slug>.yml` | The data file: the template's fields, the extras below, `org_id`, and `revision` as the last line |
| `<slug>/terms.html`, `<slug>/privacy.html` | Front matter only, as above |
| `<slug>/<id>.html`, one per printed placement | Front matter only: `layout: piece`, `client: <slug>`, `piece: <id>`, `permalink: /<slug>/<id>/` |
| `<slug>/logo.<png\|jpg\|webp\|svg>` | The client's logo, taken from their own site (scripted SVGs are refused before they get here) |

Web placements (on the client's own site) get no page here. Piece ids are lowercase words joined by hyphens and are never `terms`, `privacy`, `sms`, `sign`, `card`, `logo` or `assets`. A client has at most 6 placements.

Data-file fields the pieces read:

| Field | Shape | Effect |
|---|---|---|
| `placements` | list of `{ id, name, where, size, headline?, message? }` (printed ones only) | The page for stub `piece: <id>` renders the entry with that `id`. `headline` (else the brand name) and `message` are printed. `name` and `where` are staff words: they appear only in the screen-only print hint, never on the piece. |
| `size` | `letter` \| `half` \| `quarter` \| `tent` | `letter`: one 8.5 × 11 in sign. `half`: two 5.5 × 8.5 in pieces on a landscape letter sheet, dashed cut line. `quarter`: four 4.25 × 5.5 in cards on a portrait sheet, like `card`. `tent`: a portrait letter sheet folded in half on the dashed line; the top panel is printed upside down so both faces stand upright. |
| `disclosure` | one string | Printed **word for word** under the call to action. It already includes the HELP/STOP, conversational and age wording and the Terms and Privacy URLs, so the layout never rebuilds it from other fields. HELP and STOP are bolded without changing the text. |
| `logo` | `/<slug>/logo.<ext>` | Shown on the piece. Without it, the brand name is printed. |
| `brand_color` | `"#rrggbb"` | Main colour (keyword chip, headline, footer), default `#111111`. |
| `accent_color` | `"#rrggbb"`, placements only | Second colour (rule under the logo, QR caption, "Questions?", footer edge), default `brand_color`. |
| `revision` | 12 lowercase hex chars, last line | Printed as `<meta name="legal-revision" content="<revision>">` in the `<head>` of every piece and every page built from `base.html` (terms, privacy). The back office counts a publish as live only when each page serves that revision, so it can tell this commit's build apart from the previous one. It is only printed when set, so clients without placements are unchanged. |

Pieces never link to `/<slug>/sms/`. A data file with a keyword from the back office always has `hosted_sms: true`, and the back office's live check requires `/<slug>/sms/` to answer **404**: don't add a catch-all, redirect or generated sms page.

Note: the `keyword` comment in `_templates/client.yml` ("Turns on /<slug>/sms/ and /<slug>/sign/") is out of date for back-office clients, which get pieces instead. The template's field list and order are left as they are, because the back office checks them. The errands-nyc pages are hand-made `layout: null` HTML and carry no revision meta. That is fine, because errands-nyc has no `org_id` and the back office never publishes it.
