# Attribution

This repository demonstrates a data-platform build method. It is **not**
an official publication of any agency named below, and no agency has
endorsed it. Data has been **modified** (downloaded, staged, transformed,
and in places mixed with synthetic records) — treat every figure as
untrusted demonstration output.

Machine-readable provenance, including retrieval dates, upstream file globs and
the table each dataset feeds, is in [DATA_SOURCES.yaml](DATA_SOURCES.yaml).

**Every licence below was verified online at source on 30 August 2026** against
the publisher's own pages and, where one exists, the dataset's own
`data.govt.nz` catalogue record. Nothing is inherited from the build's internal
registry. Each row records where the claim was read:

| Mark | Basis | Meaning |
|---|---|---|
| *(none)* | `dataset_page` | read from this dataset's own page or its own catalogue record |
| † | `agency_record` | only an agency-wide or site-wide statement exists; no dataset-specific one could be read |
| ⚠ | `unverified` | no licence could be established |

**Attribution follows the publisher, not the work packet.** Six of the datasets
below were requested by the Customs, LINZ, MfE and Health work packets but are
published by Stats NZ; they are credited to Stats NZ and grouped there.

## Source datasets

### Stats NZ · Tatauranga Aotearoa

| Dataset | Publisher | Licence | Evidence read at |
|---|---|---|---|
| Bulk CSV files for download (85 pre-packaged release files) | Stats NZ | CC BY 4.0 † | [stats.govt.nz/about-us/copyright](https://www.stats.govt.nz/about-us/copyright/) |
| Information releases index | Stats NZ | CC BY 4.0 † | [stats.govt.nz/about-us/copyright](https://www.stats.govt.nz/about-us/copyright/) |
| Overseas merchandise trade (monthly release) | Stats NZ | CC BY 4.0 † | [stats.govt.nz/about-us/copyright](https://www.stats.govt.nz/about-us/copyright/) |
| Property transfer statistics | Stats NZ | CC BY 4.0 † | [stats.govt.nz/about-us/copyright](https://www.stats.govt.nz/about-us/copyright/) |
| Greenhouse gas emissions by region, industry and household | Stats NZ | CC BY 4.0 † | [stats.govt.nz/about-us/copyright](https://www.stats.govt.nz/about-us/copyright/) |
| Environmental-economic accounts | Stats NZ | CC BY 4.0 † | [stats.govt.nz/about-us/copyright](https://www.stats.govt.nz/about-us/copyright/) |
| Period life tables, including health districts and NZDep | Stats NZ | CC BY 4.0 † | [stats.govt.nz/about-us/copyright](https://www.stats.govt.nz/about-us/copyright/) |
| Estimated resident population by SA2 (Aotearoa Data Explorer, `POPES_ERP_008`) | Stats NZ | CC BY 4.0 † | [portal.apis.stats.govt.nz/terms](https://portal.apis.stats.govt.nz/terms) |

> This work is licensed under the Creative Commons Attribution 4.0
> International licence. You are free to copy, distribute, and adapt the work,
> as long as you attribute the work to Statistics NZ and abide by the other
> licence terms. Use the wording 'Statistics New Zealand' in your attribution,
> not the Statistics NZ logo.

### Department of Internal Affairs · Te Tari Taiwhenua

| Dataset | Publisher | Licence | Evidence read at |
|---|---|---|---|
| Quarterly gaming machine proceeds summary by territorial authority | Department of Internal Affairs | **CC BY 3.0 NZ** | [dia.govt.nz — the download page itself](https://www.dia.govt.nz/diawebsite.nsf/wpg_URL/Resource-material-Information-We-Provide-Summary-of-Expenditure-by-Territorial-AuthorityDistrict) |
| Gaming machine proceeds dashboard data | Department of Internal Affairs | CC BY 4.0 | [catalogue.data.govt.nz](https://catalogue.data.govt.nz/dataset/gaming-machine-profits-gmp-dashboard) |
| Charities Register — all registered and previously registered charities | DIA, Charities Services · Ngā Ratonga Kaupapa Atawhai | **CC BY 3.0 NZ** | [catalogue.data.govt.nz](https://catalogue.data.govt.nz/dataset/charities-register-open-data) |
| Charities Register — annual return financials | DIA, Charities Services · Ngā Ratonga Kaupapa Atawhai | **CC BY 3.0 NZ** | [catalogue.data.govt.nz](https://catalogue.data.govt.nz/dataset/charities-register-open-data) |
| Charities Register — sector, activity and beneficiary classifications | DIA, Charities Services · Ngā Ratonga Kaupapa Atawhai | **CC BY 3.0 NZ** | [catalogue.data.govt.nz](https://catalogue.data.govt.nz/dataset/charities-register-open-data) |

The gaming machine proceeds page states its own licence, and it is **3.0 NZ,
not 4.0**:

> Gaming machine and gambling expenditure statistics owned and administered by
> the New Zealand Public Sector by Department of Internal Affairs is licensed
> under a Creative Commons Attribute 3.0 New Zealand Licence.

The Charities Register's catalogue record carries `licence_id: CC-BY-NZ-3.0`,
`licence_title: Creative Commons Attribution 3.0 New Zealand` — confirming the
version difference the build had recorded but never checked.

### Ministry of Foreign Affairs and Trade · Manatū Aorere

| Dataset | Publisher | Licence | Evidence read at |
|---|---|---|---|
| New Zealand Treaties Online register | Ministry of Foreign Affairs and Trade | **CC BY 3.0 NZ** | [treaties.mfat.govt.nz/about](https://www.treaties.mfat.govt.nz/about) |

New Zealand Treaties Online is a published register rather than a packaged open
dataset — server-rendered HTML with no file, API or catalogue record behind it —
but its content is openly licensed, under its own statement:

> Unless otherwise specified, the content on this site is licensed under the
> Creative Commons Attribution 3.0 New Zealand licence.

This is a different instrument from the CC BY 4.0 on mfat.govt.nz proper. The
rows here are credited to the Ministry of Foreign Affairs and Trade and to **New
Zealand Treaties Online** as the register they were read from.

### Land Information New Zealand · Toitū Te Whenua

| Dataset | Publisher | Licence | Evidence read at |
|---|---|---|---|
| New Zealand Gazetteer of place names | LINZ, for the New Zealand Geographic Board · Ngā Pou Taunaha o Aotearoa | CC BY 4.0 † | [linz.govt.nz/copyright](https://www.linz.govt.nz/copyright) |
| LINZ Data Service — NZ Primary Parcels | Land Information New Zealand | CC BY 4.0 | [catalogue.data.govt.nz](https://catalogue.data.govt.nz/dataset/nz-primary-parcels) |
| LINZ Data Service — NZ Property Titles | Land Information New Zealand | CC BY 4.0 | [catalogue.data.govt.nz](https://catalogue.data.govt.nz/dataset/nz-property-titles) |
| LINZ Data Service — NZ Addresses | Land Information New Zealand | CC BY 4.0 | [catalogue.data.govt.nz](https://catalogue.data.govt.nz/dataset/nz-addresses) |
| LINZ Data Service — NZ Suburbs and Localities | Land Information New Zealand | CC BY 4.0 | [catalogue.data.govt.nz](https://catalogue.data.govt.nz/dataset/nz-suburbs-and-localities) |

LINZ mandates its attribution wording. Because the data here has been modified,
the adapted form applies. For LINZ material generally, including the Gazetteer:

> This work is based on/includes Toitū Te Whenua Land Information New Zealand
> data which are licensed by Toitū Te Whenua Land Information New Zealand for
> re-use under the Creative Commons Attribution 4.0 International licence.

For the four LINZ Data Service layers specifically:

> Contains data sourced from the LINZ Data Service licensed for reuse under
> CC BY 4.0

No owners-names layer was fetched and no person is named in any published table.
LINZ states that NZ Property Titles is property data without owner information
and needs no separate data licence; the restrictive *LINZ Licence for Personal
Data*, which bars public republication, does not apply to anything here.

### Ministry for the Environment · Manatū Mō Te Taiao

| Dataset | Publisher | Licence | Evidence read at |
|---|---|---|---|
| New Zealand Greenhouse Gas Inventory 1990–2024 — time series and summary emissions data | Ministry for the Environment | CC BY 4.0 † | [environment.govt.nz copyright](https://environment.govt.nz/about-this-site/copyright/) |
| Previous greenhouse gas inventory submissions (2003 onward) | Ministry for the Environment | CC BY 4.0 † | [environment.govt.nz copyright](https://environment.govt.nz/about-this-site/copyright/) |
| MfE Data Service — NZ Airsheds Gazetted | Ministry for the Environment | CC BY 4.0 | [catalogue.data.govt.nz](https://catalogue.data.govt.nz/dataset/nz-airsheds-gazetted) |
| MfE Data Service — modelled river water quality | Ministry for the Environment | CC BY 4.0 | [catalogue.data.govt.nz](https://catalogue.data.govt.nz/dataset/river-water-quality-escherichia-coli-modelled-2016-2020) |
| MfE Data Service — annual air quality trends, 2011–2020 | Ministry for the Environment | CC BY 4.0 | [catalogue.data.govt.nz](https://catalogue.data.govt.nz/dataset/annual-trends-particulate-matter-10-pm10-particulate-matter-2-5-pm2-5-nitrogen-dioxid-2011-2020) |

> Unless indicated otherwise for specific items or collections of content …
> this copyright material is licensed for re-use under the Creative Commons
> Attribution 4.0 International licence.

Attribute to the Ministry for the Environment. The licence excludes logos,
emblems, trademarks, photography and imagery; none is used here.

### Ministry of Health · Manatū Hauora

| Dataset | Publisher | Licence | Evidence read at |
|---|---|---|---|
| New Zealand Health Survey regional data release — adult and child statistics, crude and age-standardised | Ministry of Health | CC BY 4.0 | [catalogue.data.govt.nz](https://catalogue.data.govt.nz/dataset/regional-data-release-new-zealand-health-survey) |
| New Zealand Health Survey indicator reference guide 2024/25 | Ministry of Health | CC BY 4.0 † | [health.govt.nz copyright](https://www.health.govt.nz/about-this-site/copyright) |

`health.govt.nz` refuses non-browser clients (HTTP 403), so the survey's
licence was read from its own `data.govt.nz` catalogue record — whose four
resources are exactly the four files this build staged.

### New Zealand Customs Service · Te Mana Ārai o Aotearoa

The Customs work packet's quantitative sources are published by Stats NZ and are
credited above. Customs' own corporate publications were downloaded into the
private working tree but **no figure from them is published in this repository**,
so no Customs-published dataset appears here.

---

## What verification changed

Three questions the previous pass left open are now closed, and one licence the
build had asserted turned out to be wrong.

**The three API-key sources are clear to publish.** A portal's terms of use are
a separate instrument from the licence on the data, so both were checked
separately for each portal.

| Portal | Per-layer / per-dataflow licence | Do the portal terms permit redistribution? |
|---|---|---|
| **LINZ Data Service** (`data.linz.govt.nz`, Koordinates) | CC BY 4.0 on all four layers used, each confirmed on its own catalogue record | **Yes.** Koordinates terms defer to the publisher's licence: where the publisher "had openly published the data", a user "may likewise openly publish" their copy while complying with the publisher's licensing terms. |
| **MfE Data Service** (`data.mfe.govt.nz`, Koordinates) | CC BY 4.0 on airsheds, modelled river water quality and the annual air trends, each confirmed on its own catalogue record | **Yes.** Same Koordinates terms, same result. |
| **Stats NZ Aotearoa Data Explorer** (`apis.stats.govt.nz`) | CC BY 4.0 — the API Portal terms state it directly | **Yes.** "You may use, share, and adapt the data, including for commercial purposes, provided you give appropriate credit to Stats NZ, indicate if changes were made, and do not imply endorsement by Stats NZ." The only stated restriction is not attempting to re-identify individuals; `POPES_ERP_008` is area-level population estimates. |

In every case the API key gates *access*, not *reuse*. **`M_ADE_POPULATION` does
not need replacing** — the recorded fallback of dropping it and rebuilding from
the CC BY subnational population estimates is not required.

**The gaming machine proceeds data is CC BY 3.0 NZ, not 4.0.** This was not
previously flagged. The DIA page the quarterly files are downloaded from states
its own licence and it is the 3.0 NZ instrument. Its `data.govt.nz` catalogue
record for the same series says CC BY 4.0; the narrower statement, on the page
the data actually came from, is the one recorded and attributed.

**The Charities Register 3.0 NZ position is confirmed**, from the register's own
catalogue record rather than from the build's registry.

**New Zealand Treaties Online is openly licensed after all** — CC BY 3.0 NZ
under the register site's own terms — though it remains a published register
rather than a packaged dataset.

### Still marked †

Twelve of the twenty-one published datasets carry `licence_issue: true` in
[DATA_SOURCES.yaml](DATA_SOURCES.yaml) purely because the strongest statement
that exists for them is agency-wide: the Stats NZ releases (which are not
individually catalogued and whose pages render client-side), the MfE greenhouse
gas publications, the Stats NZ ADE dataflow, the LINZ Gazetteer, and the MoH
indicator reference guide. **That flag is about the strength of the evidence,
not a doubt about the licence.** Every one of those publishers states CC BY 4.0
site-wide, and each statement was read at its own URL, recorded in
`licence_evidence`.

Nothing in this repository is `unverified`.

Four upstream-only sources — the Customs annual report PDFs, the MFAT free trade
agreement portfolio, the LINZ overseas investment decision summaries, and the
Health New Zealand data pages — are listed under `upstream_only` in
[DATA_SOURCES.yaml](DATA_SOURCES.yaml) so the inventory is complete. **No data
from any of them reaches this repository.** Of the four, only the Customs annual
reports remain `unverified`: no copyright page for `customs.govt.nz` could be
reached, and each report states its own terms internally.

The app's own provenance registers still describe the three keyed sources as
*excluded*, which is no longer true of their data. That inconsistency is tracked
as a separate task against `scripts/org_sources.py`.

---

## Synthetic data

`SYN_VENUE_GMP` — venue-level gaming machine proceeds — is generated, not
sourced. The Department of Internal Affairs suppresses that grain by design.
Every row carries `IS_SYNTHETIC = TRUE`, no venue names are generated, and every
territorial authority in every quarter reconciles to the figure DIA published
for it. It carries no statistical meaning.

---

Source data © the named publishers. Most is used under CC BY 4.0
(https://creativecommons.org/licenses/by/4.0/); the Charities Register,
the DIA quarterly gaming machine proceeds summary, and the New Zealand
Treaties Online register are used under CC BY 3.0 NZ
(https://creativecommons.org/licenses/by/3.0/nz/). Attribution does not
imply endorsement. Synthetic records are generated and carry no
statistical meaning.
