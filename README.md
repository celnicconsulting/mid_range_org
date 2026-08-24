# Mid-Range Organisations — New Zealand Public Data

A Streamlit application over seven New Zealand government agencies' open data,
built end to end from public sources: discovery, download, a faithful landing
layer, staging, a design-driven mart, and one clearly labelled synthetic table.

**Not an official product of any New Zealand government agency.**

---

## The seven

| Code | Agency | What it contributes here |
|---|---|---|
| `DIA` | Department of Internal Affairs · Te Tari Taiwhenua | Quarterly gaming machine proceeds by territorial authority; the full Charities Register with annual return financials |
| `CUS` | New Zealand Customs Service · Te Mana Ārai o Aotearoa | Merchandise trade by partner country and commodity chapter; annual report tables |
| `SNZ` | Stats NZ · Tatauranga Aotearoa | GDP, CPI, labour market, migration, building consents, life tables — the economic backbone |
| `MFT` | Ministry of Foreign Affairs and Trade · Manatū Aorere | The New Zealand treaty register; the free trade agreement portfolio |
| `LNZ` | Land Information New Zealand · Toitū Te Whenua | The New Zealand Gazetteer of place names; property transfer statistics |
| `MFE` | Ministry for the Environment · Manatū Mō Te Taiao | The greenhouse gas inventory back to 1990, across every submission since 2003 |
| `MOH` | Ministry of Health · Manatū Hauora | New Zealand Health Survey indicators with confidence intervals, by region, ethnicity and deprivation |

---

## The eight tabs

| # | Tab | Provenance |
|---|---|---|
| 1 | 🏛️ Overview | real |
| 2 | 💹 Economy | real |
| 3 | 🌏 Trade & Treaties | real |
| 4 | 🎲 Civic & Charitable | **part synthetic** |
| 5 | 🩺 Health | real — survey estimates with confidence intervals |
| 6 | 🌡️ Environment | real |
| 7 | 🗺️ Places & Property | real |
| 8 | 🔎 Data & Provenance | real |

Only tab 4 carries synthetic content, and only in two of its eleven elements.

---

## How to read the colours

| | Means |
|---|---|
| **Blue** `#2a78d6` | REAL — a figure an agency published |
| **Orange** `#eb6834` | DERIVED — computed here from published figures, method stated in the chart |
| **Aqua** `#1baf7a` | COMPARE — a second agency's measure of the same thing, drawn as its own line and never averaged with the first |
| **Magenta** 🔶 | SYNTHETIC — modelled, not measured |
| ◍ | A survey estimate, always drawn with its 95% confidence interval |

**Suppressed values are drawn as a gap, never as zero.** Reading a suppression
symbol as zero understates every total it touches, and the understatement is
invisible because the visible parts still sum to the visible total.

---

## The one synthetic table

`SYN_VENUE_GMP` — venue-level gaming machine proceeds.

The grain does not exist in the public record and cannot: DIA suppresses
venue-level proceeds **by design**, clustering areas with fewer than three venues
into a neighbour precisely so individual venues cannot be identified.

It is safe to publish because:

- **Every territorial authority in every quarter reconciles exactly** to the
  figure DIA published for it — district by district, not merely in national
  total. Any one council area can be checked against DIA's own quarterly summary.
- `IS_SYNTHETIC = TRUE` on every row, and 🔶 appears on the metric label, the
  chart title, the legend entry and the detail-table heading.
- **No venue names are generated at all.** A venue is an id, a type and a
  district. A plausible-looking venue name attached to a modelled figure is
  exactly the artefact that gets screenshotted out of context.
- Fixed seed 42, so the build reproduces byte for byte.
- Machine counts respect the Gambling Act 2003 caps (9 per venue, 18
  grandfathered).

---

## Running it

```bash
pip install -r requirements.txt
python -m streamlit run app/mid_range_org.py
```

The app reads `data/mid_range_org_public.duckdb`, which is in this repository.
Nothing else is needed — no keys, no network calls.

---

## Sources and licence

Every source URL, its download date, its MD5 and its byte count are in the app's
**Data & Provenance** tab, along with the coverage register, the reconciliation
results, and the list of RAW tables staging did not consume with a reason for
each.

Data is New Zealand government open data under Creative Commons Attribution
licences (CC-BY 4.0; CC-BY 3.0 NZ for the Charities Register). Code is MIT — see
`LICENSE`.

> Sourced from Toitū Te Whenua Land Information New Zealand data. Crown copyright
> reserved.

No person is named anywhere in this platform: the Charities Register's Officers
entity was never downloaded, and direct contact details were dropped at staging.

Built by [Celnic Consulting](mailto:consult@celnic.nz).
