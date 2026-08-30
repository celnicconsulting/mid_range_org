# Attribution

This repository demonstrates a data-platform build method. It is **not**
an official publication of any agency named below, and no agency has
endorsed it. Data has been **modified** (downloaded, staged, transformed,
and in places mixed with synthetic records) — treat every figure as
untrusted demonstration output.

Machine-readable provenance, including retrieval dates, upstream file globs and
the table each dataset feeds, is in [DATA_SOURCES.yaml](DATA_SOURCES.yaml).

**Attribution follows the publisher, not the work packet.** Six of the datasets
below were requested by the Customs, LINZ, MfE and Health work packets but are
published by Stats NZ; they are credited to Stats NZ and grouped there.

## Source datasets

### Stats NZ · Tatauranga Aotearoa

| Dataset | Publisher | Licence | Source |
|---|---|---|---|
| Bulk CSV files for download (85 pre-packaged release files) | Stats NZ | CC BY 4.0 | [stats.govt.nz](https://www.stats.govt.nz/large-datasets/csv-files-for-download/) |
| Information releases index | Stats NZ | CC BY 4.0 | [stats.govt.nz](https://www.stats.govt.nz/information-releases/) |
| Overseas merchandise trade (monthly release) | Stats NZ | CC BY 4.0 | [stats.govt.nz](https://www.stats.govt.nz/information-releases/overseas-merchandise-trade-july-2026/) |
| Property transfer statistics | Stats NZ | CC BY 4.0 | [stats.govt.nz](https://www.stats.govt.nz/large-datasets/csv-files-for-download/) |
| Greenhouse gas emissions by region, industry and household | Stats NZ | CC BY 4.0 | [stats.govt.nz](https://www.stats.govt.nz/information-releases/greenhouse-gas-emissions-by-region-industry-and-household-year-ended-2025/) |
| Environmental-economic accounts | Stats NZ | CC BY 4.0 | [stats.govt.nz](https://www.stats.govt.nz/large-datasets/csv-files-for-download/) |
| Period life tables, including health districts and NZDep | Stats NZ | CC BY 4.0 | [stats.govt.nz](https://www.stats.govt.nz/large-datasets/csv-files-for-download/) |
| Estimated resident population by SA2 (Aotearoa Data Explorer, `POPES_ERP_008`) | Stats NZ | ⚠️ **UNVERIFIED** — API-key source, see below | [apis.stats.govt.nz](https://portal.apis.stats.govt.nz/) |

### Department of Internal Affairs · Te Tari Taiwhenua

| Dataset | Publisher | Licence | Source |
|---|---|---|---|
| Quarterly gaming machine proceeds summary by territorial authority | Department of Internal Affairs | CC BY 4.0 | [dia.govt.nz](https://www.dia.govt.nz/diawebsite.nsf/wpg_URL/Resource-material-Information-We-Provide-Summary-of-Expenditure-by-Territorial-AuthorityDistrict) |
| Gaming machine proceeds dashboard data | Department of Internal Affairs | CC BY 4.0 | [dia.govt.nz](https://www.dia.govt.nz/gambling-statistics-gmp-dashboard) |
| Charities Register — all registered and previously registered charities | DIA, Charities Services · Ngā Ratonga Kaupapa Atawhai | ⚠️ **CC BY 3.0 NZ**, not 4.0 — see below | [odata.charities.govt.nz](https://www.odata.charities.govt.nz/Organisations) |
| Charities Register — annual return financials | DIA, Charities Services · Ngā Ratonga Kaupapa Atawhai | ⚠️ **CC BY 3.0 NZ**, not 4.0 — see below | [odata.charities.govt.nz](https://www.odata.charities.govt.nz/AnnualReturn) |
| Charities Register — sector, activity and beneficiary classifications | DIA, Charities Services · Ngā Ratonga Kaupapa Atawhai | ⚠️ **CC BY 3.0 NZ**, not 4.0 — see below | [odata.charities.govt.nz](https://www.odata.charities.govt.nz/MainSector) |

### Ministry of Foreign Affairs and Trade · Manatū Aorere

| Dataset | Publisher | Licence | Source |
|---|---|---|---|
| New Zealand Treaties Online register | Ministry of Foreign Affairs and Trade | ⚠️ **UNVERIFIED** — scraped register, see below | [treaties.mfat.govt.nz](https://www.treaties.mfat.govt.nz/search/results) |

### Land Information New Zealand · Toitū Te Whenua

| Dataset | Publisher | Licence | Source |
|---|---|---|---|
| New Zealand Gazetteer of place names | LINZ, for the New Zealand Geographic Board · Ngā Pou Taunaha o Aotearoa | ⚠️ CC BY 4.0 **to confirm** — see below | [gazetteer.linz.govt.nz](https://gazetteer.linz.govt.nz/) |
| LINZ Data Service — NZ Primary Parcels, NZ Property Titles, NZ Addresses, NZ Suburbs and Localities | Land Information New Zealand | ⚠️ **UNVERIFIED** — API-key source, see below | [data.linz.govt.nz](https://data.linz.govt.nz/) |

> Sourced from Toitū Te Whenua Land Information New Zealand data. Crown
> copyright reserved.

### Ministry for the Environment · Manatū Mō Te Taiao

| Dataset | Publisher | Licence | Source |
|---|---|---|---|
| New Zealand Greenhouse Gas Inventory 1990–2024 — time series and summary emissions data | Ministry for the Environment | CC BY 4.0 | [environment.govt.nz](https://environment.govt.nz/facts-and-science/climate-change/new-zealands-greenhouse-gas-inventory/) |
| Previous greenhouse gas inventory submissions (2003 onward) | Ministry for the Environment | CC BY 4.0 | [environment.govt.nz](https://environment.govt.nz/facts-and-science/climate-change/new-zealands-greenhouse-gas-inventory/previous-greenhouse-gas-inventories/) |
| MfE Data Service — modelled river water quality, gazetted airsheds, annual air quality trends | Ministry for the Environment | ⚠️ **UNVERIFIED** — API-key source, see below | [data.mfe.govt.nz](https://data.mfe.govt.nz/) |

### Ministry of Health · Manatū Hauora

| Dataset | Publisher | Licence | Source |
|---|---|---|---|
| New Zealand Health Survey regional data release — adult and child statistics, crude and age-standardised | Ministry of Health | CC BY 4.0 | [health.govt.nz](https://www.health.govt.nz/publications/regional-data-release-new-zealand-health-survey) |
| New Zealand Health Survey indicator reference guide 2024/25 | Ministry of Health | CC BY 4.0 | [health.govt.nz](https://www.health.govt.nz/publications/regional-data-release-new-zealand-health-survey) |

### New Zealand Customs Service · Te Mana Ārai o Aotearoa

The Customs work packet's quantitative sources are published by Stats NZ and are
credited above. Customs' own corporate publications were downloaded into the
private working tree but **no figure from them is published in this repository**,
so no Customs-published dataset appears here.

---

## Licence to confirm

Eight of the published datasets carry a licence question. Nothing has been
removed; each is flagged with `licence_issue: true` and a `licence_note` in
[DATA_SOURCES.yaml](DATA_SOURCES.yaml).

**Charities Register (three datasets).** This build's own registry records the
Charities Register as **CC BY 3.0 NZ**, a different instrument from CC BY 4.0.
It is attributed as 3.0 NZ above rather than swept into the repository's blanket
4.0 statement. *Recommendation: keep, with the 3.0 NZ attribution stated
separately.*

**Three API-key sources — LINZ Data Service, MfE Data Service, Stats NZ
Aotearoa Data Explorer.** These were fetched with personal API keys by
`scripts/10_keyed_download.py` and produce eleven published tables (the
cadastre, addresses, suburbs and title summary; river water quality, airsheds
and air trends; the SA2 population estimates). This build captured **no licence
for any of them**: they are recorded only as *excluded* sources needing a key,
and the work packets' CC BY claims about the two Koordinates services are marked
UNTESTABLE in `design/packet_assumptions.md`. An API portal's terms of use are a
separate instrument from the CC BY licence on an agency's published files and
may restrict redistribution. *Recommendation for each: confirm the terms per
layer or dataflow and record them, before the next release. If the Stats NZ ADE
terms do not permit redistribution, the population map can be rebuilt from the
CC BY subnational population estimates on the bulk CSV page instead.*

The app's own provenance registers still describe these three as *excluded*,
which is no longer true of their data. That inconsistency should be corrected in
`scripts/org_sources.py` at the next rebuild.

**New Zealand Gazetteer of place names.** The LINZ work packet's CC BY claim is
about the LINZ Data Service; the Gazetteer is served from a different host and
no licence statement for it is recorded here. The mandated LINZ attribution is
reproduced above. *Recommendation: keep with that attribution, and confirm the
Gazetteer's own terms.*

**New Zealand Treaties Online.** Not a published dataset — a server-rendered
HTML register, scraped over 330 pages. No licence or terms-of-use statement from
`treaties.mfat.govt.nz` is captured in this build, and a website's reuse terms
are a separate question from an agency's open-data policy. *Recommendation: keep
with special attribution — cite MFAT and New Zealand Treaties Online explicitly
as the register rather than as a CC BY dataset — and confirm the site's terms.*

A further four sources — the Customs annual report PDFs, the MFAT free trade
agreement portfolio, the LINZ overseas investment decision summaries, and the
Health New Zealand data pages — are also unverified, but **no data from any of
them reaches this repository**. They are listed under `upstream_only` in
[DATA_SOURCES.yaml](DATA_SOURCES.yaml) so the inventory is complete.

---

## Synthetic data

`SYN_VENUE_GMP` — venue-level gaming machine proceeds — is generated, not
sourced. The Department of Internal Affairs suppresses that grain by design.
Every row carries `IS_SYNTHETIC = TRUE`, no venue names are generated, and every
territorial authority in every quarter reconciles to the figure DIA published
for it. It carries no statistical meaning.

---

Source data © the named publishers, used under CC BY 4.0
(https://creativecommons.org/licenses/by/4.0/), except the Charities
Register, used under CC BY 3.0 NZ
(https://creativecommons.org/licenses/by/3.0/nz/), and the datasets
flagged above whose licence is still to be confirmed. Attribution does
not imply endorsement. Synthetic records are generated and carry no
statistical meaning.
