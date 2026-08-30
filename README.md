# Mid-Range Organisations — New Zealand Public Data

> **Data & licence.** Built on open data used under CC BY 4.0 and CC BY 3.0 NZ
> — every licence verified at source, 30 August 2026. See
> [ATTRIBUTION.md](ATTRIBUTION.md) and [DATA_SOURCES.yaml](DATA_SOURCES.yaml)
> for every source, licence, evidence URL, and modification. Demonstration of
> method only:
> the data is modified and partly synthetic, and must not be relied on for
> operational, policy, or reporting purposes.

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
licences: CC BY 4.0 for most of it, and **CC BY 3.0 NZ** for the Charities
Register, the DIA quarterly gaming machine proceeds summary, and the New Zealand
Treaties Online register.

Every licence was **verified online at source on 30 August 2026** against the
publisher's own page or the dataset's own `data.govt.nz` catalogue record.
[DATA_SOURCES.yaml](DATA_SOURCES.yaml) records, dataset by dataset, the licence,
where it was read (`licence_basis`) and the URL it was read at
(`licence_evidence`); [ATTRIBUTION.md](ATTRIBUTION.md) gives the attribution
each licence requires and reproduces the wording LINZ mandates. No published
dataset is `unverified`. Rows marked † inherit an agency-wide statement because
no dataset-specific one exists — that is a note about the evidence, not a doubt
about the licence.

The three API-key sources (LINZ Data Service, MfE Data Service, Stats NZ
Aotearoa Data Explorer) were checked twice over: the licence on each layer or
dataflow, and separately whether the portal's terms of use permit redistribution
of derived extracts. All are CC BY 4.0 and all permit it. The key gates access,
not reuse.

LINZ mandates its attribution wording, and because this data is modified the
adapted form applies:

> This work is based on/includes Toitū Te Whenua Land Information New Zealand
> data which are licensed by Toitū Te Whenua Land Information New Zealand for
> re-use under the Creative Commons Attribution 4.0 International licence.

No person is named anywhere in this platform: the Charities Register's Officers
entity was never downloaded, and direct contact details were dropped at staging.

---

## Licence

Two licences apply, to two different things.

| | Covers | File |
|---|---|---|
| **MIT** | the code in this repository — the app, its configuration, and the documentation written for this build | [`LICENSE`](LICENSE) |
| **Publishers' own licences** | the data — CC BY 4.0 for most of it, CC BY 3.0 NZ for the Charities Register, the DIA gaming machine proceeds summary and the treaties register; all verified at source | [`LICENSE-DATA`](LICENSE-DATA) |

The MIT licence grants you nothing in the source data. Per-dataset provenance is
in [DATA_SOURCES.yaml](DATA_SOURCES.yaml); the required attribution is in
[ATTRIBUTION.md](ATTRIBUTION.md).

Built by Celnic Consulting.
