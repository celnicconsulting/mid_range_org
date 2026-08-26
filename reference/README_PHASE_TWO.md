# ====================MID_RANGE_ORG_PHASE_TWO====================

# Phase Two — Keyed Sources, Restored Maps and the Cross-Source Check

**Status:** Complete. All 18 validation checks pass.
**Built:** 24–26 August 2026
**Agencies:** seven — Internal Affairs, Customs, Stats NZ, Foreign Affairs and
Trade, Land Information, Environment, Health
**Mart:** `db/mid_range_org.duckdb` · **Extract:** `public/mid_range_org_public.duckdb` (43.8 MB)
**App:** [app/mid_range_org.py](app/mid_range_org.py)

```bash
python -m streamlit run app/mid_range_org.py --server.port 8520
```

---

# ====================WHAT_PHASE_TWO_WAS====================

Phase One built the platform from everything obtainable **without registering for
anything**. Three sources named in the work packets needed a free API key, and
were excluded at the outset rather than half-built:

- the **LINZ Data Service** — parcels, titles, addresses
- the **MfE Data Service** — river, lake, groundwater and air monitoring
- the **Stats NZ Aotearoa Data Explorer API**

Two map elements had to be marked `CUT` in `design/bridge_gaps.md` as a direct
consequence. Phase Two is what happened when the keys arrived.

| | Phase One | Phase Two |
|---|---|---|
| Sources | 32 registered, 215 files | + 3 keyed services, 12 layers |
| RAW | 814 tables, 31.4 M rows | 826 tables, 41.8 M rows |
| Staging | 22 tables | 30 tables |
| Mart | 46 `M_` + 1 `SYN_` | 54 `M_` + 1 `SYN_` |
| Validation | 15 checks | **18 checks** |
| Cut elements | 13 | **10** |
| Extract | 37.5 MB | 43.8 MB |

**The synthetic table did not grow.** Everything the keys bought is measured
data. Nothing was modelled to fill a gap a key could fill instead — which is the
whole argument for waiting for the keys rather than approximating.

---

# ====================THE_PLAN_FLIPPED_DRIVING_FROM_BUSINESS_OUTCOME====================

Same discipline as Phase One: the interface element came first, and the fetch was
designed to serve it. Each restored element was reduced to the question it has to
answer, and each question to the grain that answers it.

| Element | Question | Grain required | Fact built |
|---|---|---|---|
| 🗺️ Cadastre map | What does the land title fabric of a city actually look like? | one row per parcel, with its boundary ring | `M_LINZ_PARCEL` |
| 🗺️ Address density | Where do people actually live, as opposed to where the parcels are? | H3 cell × resolution | `M_LINZ_ADDRESS_H3` |
| 🌊 Freshwater map | How clean is the water, segment by segment? | river segment × measure | `M_MFE_RIVER_QUALITY` |
| 🌬️ Air trends | Is air quality improving, and where? | monitoring site × pollutant | `M_MFE_AIR_TREND` |
| 🏛️ Population | How many people live in each area, and is that figure trustworthy? | area × year | `M_ADE_POPULATION` |

**What that forced into the design**, working back from the questions:

1. A cadastre map needs **boundary geometry**, not centroids — so the fetch keeps
   the ring, and the extract's whole size problem becomes a geometry problem
   rather than a row-count problem.
2. Address *density* needs **aggregation, not points** — so the H3 cells are
   built in the mart from all 215,703 regional points, and the extract can then
   trim the point detail without touching the map.
3. River quality is a **categorical state class beside a modelled number** — so
   both travel, and the app never invents a numeric scale for the class.
4. A population figure the platform already had from another route is worth more
   as a **check** than as a number — so the ADE pull is wired into validation,
   not just into a chart.

---

# ====================THE_KEYS====================

## Two keys per Koordinates site, deliberately

LINZ and MfE both run on Koordinates. One login covers both, but **each site
issues its own key** — a LINZ key does not authenticate against the MfE service.

More importantly, Koordinates offers two kinds:

| Kind | Can do | Can it be re-read? |
|---|---|---|
| **Data access only** | fetch data through WFS and exports | yes, revealed on the site any time |
| **Manual scope** | the above **plus the catalogue API** | **no — shown once, at creation** |

The catalogue API is the difference between discovering layer ids at run time and
pinning them. The LINZ packet warns that layer ids are stable but should be
confirmed at run time; a data-access-only key returns **401** from the catalogue,
so a pipeline holding one has no choice but to pin.

Both kinds are kept in the environment file. The manually-scoped key cannot be
revealed again after creation, so if it is ever lost the build still runs against
the data-access key and pinned ids rather than stopping dead.

## Scopes granted, and the ones refused

The manually-scoped keys were created with the narrowest set that does the job:

| Scope | Setting | Why |
|---|---|---|
| List datasets via admin API | **on** | run-time layer discovery — the entire point |
| Layer and table datasets | **read only** | layer metadata: WFS type names, schemas, licences |
| WFS and WFS changesets | **on** | how the data actually moves |
| Spatial query APIs | **on** | clipping to an extent |
| Exports API | **create** | server-side clipped exports for the large layers |
| Users and groups | **no access** | the pipeline never touches accounts |
| Sets, documents, sources, Kart repos | **no access** | not used |
| WMTS / XYZ tiles, Esri REST | **off** | the app draws vectors over a third-party basemap |

A key that lives in a configuration file should not be able to administer the
account it belongs to. Koordinates' own wording confirms tightening is free: a
scope *works in addition to* dataset permissions and can never widen them beyond
what the creating account already has.

## Where they live

An untracked environment file at the project root, listed in `.gitignore` at both
the project root and inside the publishable repository. **No key appears in the
published repository, in a manifest, in a log line, or in this document.** The
pipeline reads them at run time; a source whose key is absent is skipped with a
stated reason rather than failing halfway through a download.

---

# ====================FETCHING====================

## Three streams, three hosts, concurrent

`data.linz.govt.nz`, `data.mfe.govt.nz` and `apis.stats.govt.nz` are unrelated
services with unrelated rate limits, so there is no reason for one to wait on
another. Inside a stream the requests are serial and throttled, because paging a
WFS layer is one conversation with one server.

## The bounding box is silent about being wrong

This cost the most time of anything in Phase Two.

```
cql_filter=bbox(shape,174.6,-41.4,175.2,-40.8)   →  HTTP 200, 0 features
bbox=174.6,-41.4,175.2,-40.8,EPSG:4167           →  HTTP 200, correct features
```

Both are accepted. One returns nothing. There is no error, no warning, and no
indication that a filter was misunderstood — an empty map looks exactly like a
region with no data in it. The working form is the `bbox` parameter with an
explicit CRS, in longitude/latitude order, because EPSG:4167 (NZGD2000) is a
geographic system in degrees.

## Clipping is a decision, not an inference

The first version decided whether to clip from the layer's `feature_count`. The
Koordinates **list** endpoint does not return that field for the MfE service, so
it read as zero, and the run began pulling the entire national river network —
roughly 590,000 segments — for a map that opens on one city.

Clipping is now an explicit per-layer flag. *An explicit flag cannot be wrong
about a field that is absent.*

## What was fetched

| Layer | National | Held | Clipped |
|---|---|---|---|
| NZ Primary Parcels | 2,795,271 | 192,139 | Wellington region |
| NZ Property Titles | 2,451,640 | 199,392 | Wellington region |
| NZ Addresses | 2,424,285 | 215,703 | Wellington region |
| NZ Suburbs and Localities | 6,563 | 6,563 | whole |
| River quality — E. coli | — | 19,132 | Wellington region |
| River quality — Nitrogen | — | 28,698 | Wellington region |
| River quality — Phosphorus | — | 14,349 | Wellington region |
| River quality — Clarity and turbidity | — | 9,566 | Wellington region |
| River quality — Macroinvertebrate index | — | 4,783 | Wellington region |
| NZ Airsheds Gazetted | 74 | 74 | whole |
| Air quality annual trends | 66 | 66 | whole |
| Estimated resident population (ADE) | 6,520,500 obs | 14,490 | totals only |

The bounding box is a single constant in the download script. Widening the map is
a one-line change followed by a rebuild.

---

# ====================THE_SDMX_API====================

The Stats NZ Aotearoa Data Explorer is SDMX, and three of its behaviours are
worth writing down because none of them is what the documentation implies.

**The base URL is not the one the packets name.** It is
`apis.stats.govt.nz/ade-api/rest/v2/`, with the key in an
`Ocp-Apim-Subscription-Key` header. The `api.stats.govt.nz/opendata` path the
packet implies returns **502**.

**The key wildcard is `*`, not the dotted form.** An SDMX key is conventionally
one dot-separated position per dimension, with empty positions meaning "any".
This service validates the key against a no-empty-position pattern and rejects
`.....` outright. It also rejects the literal `all` with *"Not enough key values
in query, expecting 5 got 1"*, which is a helpful error pointing at an unhelpful
answer. `*` works.

**The metadata endpoints do not answer.** `structure/datastructure/…` and
`availability/…` both return **404**, so the dimension names cannot be read from
where they belong. They are read instead from the **data response's own structure
block**, which is the only place this service reliably publishes them.

## The label trap

Having got the cube, it had to be filtered to the total-of-every-breakdown cell —
one number per area, rather than every combination of ethnicity, age and sex.

Stats NZ labels its totals:

```
Total people, sex
Total people, ethnic group
Total people, age
```

Not `Total`, not `All`, not a `_T` code. A generic `startswith("total")` test
matches **none** of them. The first version of that filter kept zero rows and
fell back to an arbitrary 200,000-row slice — a plausible-looking table that was
simply the first fifth of a cube in whatever order it arrived.

The filter now matches the labels exactly, and if it ever matches nothing it
**returns an error rather than substituting a slice**. That is the difference
between a build that fails loudly and one that ships a quiet lie.

---

# ====================GEOMETRY_IS_THE_COST====================

31,238 parcels came to 20.7 MB. The rows are not the problem; the rings are.

Three reductions, none of which removes anything the map shows:

1. **Exterior ring only.** A parcel's interior rings are easements and exclusions,
   invisible at city zoom.
2. **Coordinates rounded to five decimal places** — about 1.1 m at this latitude.
   Finer than a parcel is surveyed to for a web map, and far finer than a screen
   pixel at the zoom this layer draws at.
3. **A flat `[[lon,lat], …]` array** rather than nested GeoJSON, because that is
   the shape a polygon layer wants. Keeping the GeoJSON wrapper means storing
   punctuation.

A fourth applies to a small tail: the median parcel ring has **seven** points, the
mean eleven, and the largest **2,342** — reserves and road corridors. Those are
evenly sampled to 24 points, which keeps the shape recognisable and stops six
thousand outliers dominating the extract.

Result: 20.7 MB → 13.4 MB, **without dropping a single parcel**. That constraint
was deliberate. Dropping parcels makes a map quietly incomplete; rounding them
does not.

---

# ====================MART====================

## New tables

| Table | Grain | Rows | Note |
|---|---|---|---|
| `M_LINZ_PARCEL` | parcel | 106,680 | ring stored as `RING_JSON` + `RING_POINTS` |
| `M_LINZ_ADDRESS` | address point | 215,703 | |
| `M_LINZ_ADDRESS_H3` | H3 cell × resolution | 21,446 | resolutions 7–10 |
| `M_LINZ_TITLE_SUMMARY` | estate type × status | 16 | ownership names never downloaded |
| `M_LINZ_SUBURB` | suburb | 6,563 | name and centroid only |
| `M_MFE_RIVER_QUALITY` | segment × measure | 76,528 | five indicators |
| `M_MFE_AIR_TREND` | site × pollutant | 66 | MfE's own published slopes |
| `M_MFE_AIRSHED` | airshed | 74 | |
| `M_ADE_POPULATION` | area × year | 14,490 | totals only |

## Resolutions 7–10, not the packet's 8–12

The packet asks for H3 resolutions 8 through 12. At 11 and 12 a cell is a few
metres across, and 215,703 address points produce **more cells than points** — a
slower map showing less. The slider offers what a city-scale map can actually
render.

## What was deliberately not kept

- **Suburb polygons.** 124 MB of boundary geometry for 6,563 rows, and no element
  draws them — the parcels are the polygon layer. Name and centroid only.
- **Title geometry.** The title footprint duplicates the parcel footprint for most
  titles; the summary carries composition instead.
- **Ownership names.** The LINZ titles layer that includes owner details is a
  separate, licence-gated dataset. This build uses the titles-*without*-owners
  layer, by design and in line with the packet's own instruction. **No person is
  named anywhere in this platform.**

---

# ====================VALIDATION====================

Three checks were added, taking the suite from 15 to 18. All pass.

## X4 — the check the key actually bought

```
ADE population  vs  bulk-CSV subnational estimates      diff 0.0026
```

The same Stats NZ estimate reached two entirely different ways: through the SDMX
API, and through the bulk CSV download page — different endpoints, different
formats, different parsers, different code paths. For the areas and years both
cover they agree to well within the 2% tolerance.

**Before the key there was exactly one route to this figure and nothing to check
it against.** That is the strongest argument for the keyed build, and it is worth
more than either map.

## X5 — territorial authority labels across three agencies

LINZ names territorial authorities in its address points, Internal Affairs names
them in the gambling series, and Stats NZ names them in the population estimates.
The check counts LINZ labels that match neither of the others. Tolerance is three,
because the Wellington clip crosses into areas the agencies genuinely label
differently.

## I9 — cadastre geometry is drawable

No tolerance. A ring of fewer than three points is not a polygon, and a parcel
outside the clip window means the bounding box was applied in the wrong axis
order — the exact failure that returns zero features without an error.

---

# ====================APPLICATION====================

## Tabs

| Tab | Provenance | Phase Two change |
|---|---|---|
| 🏛️ Overview | real | **+ estimated resident population from the ADE API** |
| 💹 Economy | real | — |
| 🌏 Trade & Treaties | real | — |
| 🎲 Civic & Charitable | part synthetic | — |
| 🩺 Health | real (survey) | — |
| 🌡️ Environment | real | **+ freshwater map, + air-quality trends** |
| 🗺️ Places & Property | real | **+ cadastre map with address density** |
| 🔎 Data & Provenance | real | 18 checks rather than 15 |
| 📐 Method | real | **new — this document** |

## Honesty built into the interface

- The map layer selector on Places names both options rather than silently
  swapping one for the other: the Gazetteer map is national, the cadastre is one
  city. Neither replaced the other.
- The cadastre caption states **how many polygons are drawn against how many are
  held**, so a bounded render is never mistaken for the whole extract.
- The freshwater caption says the modelling is **the ministry's, not this
  pipeline's** — these are published figures, not derived ones. That distinction
  is left to words rather than to the colour key.
- The river colour ramp is a **single hue, light to dark**, not red-to-green. A
  diverging good/bad ramp would assert a judgement the state classes make
  categorically and this numeric value does not.
- Air-quality trends say **negative is improving**, because a falling line on a
  pollutant chart is good news and nothing about the axis says so.

---

# ====================DECISIONS_AND_DEPARTURES====================

**Layer ids are discovered, not pinned.** The catalogue API is queried at run
time and layers matched by title. A renumbered layer is still found.

**The Census topic explorer stays cut.** The ADE key works and the 2023 Census
dataflows are visible, but each topic is a separate cube with its own dimensions.
That is a build of its own, not a tail-end of this one. Ten of the original
thirteen cuts remain — three fewer than Phase One, and the reasons for the rest
are unchanged.

**Two extents on one tab, stated.** Parcels cover Wellington City inner suburbs
because a browser will not draw more rings than that. Address density covers the
whole Wellington region, because an H3 cell costs the same whatever it aggregates.
Both are named in the caption rather than left to be discovered.

**The extract gate did its job three times.** 71 MB, then 62.9 MB, then 43.8 MB.
Each reduction removed a whole nameable slice — an abolished geography, older
editions of the same years, a coordinate precision finer than a pixel — and every
one is recorded in `M_EXTRACT_NOTES` so the app can state what it cannot answer.
**Nothing was sampled.** Sampling produces a chart that is quietly wrong.

---

# ====================RUNNING_IT====================

```bash
# everything, from source
python scripts/run_all.py

# just the keyed sources
python scripts/10_keyed_download.py

# resume from staging
python scripts/run_all.py --from 05
```

| Step | Script | What it does |
|---|---|---|
| 01 | `01_discover.py` | crawl registered pages, cache every one, emit the manifest |
| 02 | `02_download.py` | fetch to `raw/`, keyed on a URL hash, sniffing content |
| 02b | `02b_scrape_registers.py` | the three registers that publish no file |
| 02c | `02c_fetch_odata.py` | page the charity annual returns whose export faults |
| **02d** | **`10_keyed_download.py`** | **the three keyed services, three concurrent streams** |
| 03 | `03_extract.py` | faithful cell grids to parquet |
| 04 | `04_load_duckdb.py` | land RAW, plus catalog, gaps and aliases |
| 05 | `05_stage.py` | resolve grids into tidy long facts |
| 07 | `07_mart.py` | build exactly the contract |
| 08 | `08_synthetic.py` | the one modelled table, reconciled |
| 06 | `06_validate.py` | 18 cross-source and shape checks |
| 09 | `09_build_public.py` | the compact extract the app reads |

The keyed step needs the environment file present. Without it, it reports which
key is missing and exits without partial output — it does not fetch what it can
and leave the rest silently absent.

---

# ====================WHAT_PHASE_THREE_WOULD_BE====================

1. **Census 2023 topic tables** — the population map at SA2 grain, and the topic
   explorer the Stats NZ packet asked for.
2. **Widen the cadastre** — one constant, then a rebuild. The question is what a
   national cadastre costs in an extract that must stay under 50 MB, and the
   answer is probably vector tiles rather than rings in a database.
3. **LINZ Basemaps** — a separate free key for aerial and topo tiles. The parcels
   read considerably better over aerial imagery than over a generic basemap.
4. **The changeset APIs** — both Koordinates services publish changesets, so a
   refresh could fetch what changed rather than re-clipping the whole extent.

---

Built independently by Celnic Consulting from publicly published New Zealand open
data. **Not an official product of any New Zealand government agency.**
