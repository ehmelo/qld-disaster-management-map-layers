# Queensland disaster management map layers

Boundary files for Queensland's disaster management geography, prepared for the Power BI
**Azure Maps** visual (GeoJSON reference layer) and the **Shape Map** visual (TopoJSON).
Every layer is served from GitHub Pages so it can be referenced by URL.

> **Reduced size and precision, on purpose.** These files are compacted for state-level and
> regional views: shapes are simplified with a 200 m tolerance, meaning boundary detail
> finer than about 200 m (small inlets, headlands and bends) is removed while every
> island and enclave larger than 0.01 km² is kept; coordinates are rounded to 4 decimal places
> (about 11 m). Boundaries are right at the scale of a Queensland dashboard, where one screen
> pixel is about 2 km, and neighbours share edges with no gaps or overlaps. They are **not** for
> pinpoint locations, address lookups, property-level or legal boundary work: use the source
> datasets listed below for those.

**Preview the layers:** https://ehmelo.github.io/qld-disaster-management-map-layers/

Generated 14/09/2026. Layer metadata, including sources and
licences per file, is in [`layers.json`](layers.json).

## What is in here

Queensland's disaster management arrangements run at three levels. This repository holds
boundaries for the two geographic ones, plus a reporting grouping and, for comparison, the
Queensland Police Service's own operational boundaries.

- **Disaster districts (DDMG)** - 23 districts, each coordinated by a District Disaster
  Management Group. The boundaries are the QPS Disaster Districts dataset.
- **Local government areas (LDMG)** - 78 council polygons covered by the 77 Local Disaster
  Management Groups. Torres Strait has two councils (Torres Shire and Torres Strait Island
  Regional) under one group name.
- **Disaster Management Regions** - the 23 districts merged into 7 regions. This grouping is
  a reporting convention used by the dashboards these files serve (see the table below).
  **It is not the QPS operational region boundary.** The official QPS regions carry the
  same seven names but follow the current 15 police districts and differ from this grouping
  in several places, most visibly around Brisbane, Moreton and Gympie.
- **QPS operational regions and districts** - the official Queensland Police Service
  boundaries, included so that the difference is visible.

### Disaster Management Region grouping

| Disaster Management Region | Code | Short name | Region slug (file name) | Disaster districts (DDMG) |
|---|---|---|---|---|
| Brisbane Region | `BR` | Brisbane | `brisbane` | Brisbane, Moreton |
| Central Region | `CR` | Central | `central` | Gladstone, Longreach, Mackay, Rockhampton |
| Far Northern Region | `FNR` | Far North | `far_north` | Cairns, Innisfail, Mareeba |
| North Coast Region | `NCR` | North Coast | `north_coast` | Bundaberg, Gympie, Maryborough, Sunshine Coast |
| Northern Region | `NR` | Northern | `northern` | Mount Isa, Townsville |
| South Eastern Region | `SER` | South East | `south_east` | Gold Coast, Logan |
| Southern Region | `SR` | Southern | `southern` | Charleville, Dalby, Ipswich, Roma, Toowoomba, Warwick |

Local government areas take the region of the disaster district they sit in. The **region slug**
is the short name in lower case with spaces as underscores; it is the `<region>` part of every
per-region file name, so a report can build the URL from the region it is showing without a
lookup table: `layers/qld_<slug>_ldmg_boundaries_gda2020_simp200m.geojson`.

## Layers

All coordinates are longitude / latitude in degrees. `simp200m` in a file name is the
simplification tolerance described above: boundary detail finer than about 200 m is
removed while every island and enclave larger than 0.01 km² is kept. All polygons of a layer are
simplified together with shared edges, so every district and council keeps its area to within
about 3 % of the source (the smallest councils, around 10 km², move the most) and the coastline
is drawn the same way on every layer.

The disaster district and council polygons extend over Queensland's coastal waters, as the
source datasets draw them: disaster management areas cover the state's maritime territory,
so a coastal council or district is larger than its land area. One repair was needed: the
Cook Shire polygon carried a Gulf of Carpentaria water box that, when removed upstream, took
the shire's western coastal land with it; here the box is removed and the land kept, using
the Australian Bureau of Statistics 2021 coastline.

### Statewide

| Layer | Features | GeoJSON | TopoJSON | Match field | Coordinates |
|---|---|---|---|---|---|
| `qld_ddmg_boundaries_gda2020_simp200m` | 23 | 438 KB | 178 KB | `DDMG Name` | GDA2020 (EPSG:7844) |
| `qld_ldmg_boundaries_gda2020_simp200m` | 78 | 858 KB | 365 KB | `LDMG Name` | GDA2020 (EPSG:7844) |

The council match field `LDMG Name` is not unique: Torres Strait covers two councils (LGA codes
6950 and 6960); bind on `LGA Code` when a one-to-one key is needed.

### Disaster Management Regions

| Layer | Features | GeoJSON | TopoJSON | Match field | Coordinates |
|---|---|---|---|---|---|
| `qld_dm_region_boundaries_gda2020_simp200m` | 7 | 254 KB | 112 KB | `Police Region Short Name` | GDA2020 (EPSG:7844) |

### Per region

One district file and one council file for each Disaster Management Region. Subsets of the
statewide layers; each feature also carries `Police Region Name`, `Police Region Code` and
`Police Region Short Name` (the property names the consuming reports use for the region).

| Layer | Features | GeoJSON | TopoJSON | Match field | Coordinates |
|---|---|---|---|---|---|
| `qld_brisbane_ddmg_boundaries_gda2020_simp200m` | 2 | 16 KB | 12 KB | `DDMG Name` | GDA2020 (EPSG:7844) |
| `qld_brisbane_ldmg_boundaries_gda2020_simp200m` | 3 | 19 KB | 14 KB | `LDMG Name` | GDA2020 (EPSG:7844) |
| `qld_central_ddmg_boundaries_gda2020_simp200m` | 4 | 114 KB | 55 KB | `DDMG Name` | GDA2020 (EPSG:7844) |
| `qld_central_ldmg_boundaries_gda2020_simp200m` | 14 | 197 KB | 89 KB | `LDMG Name` | GDA2020 (EPSG:7844) |
| `qld_far_north_ddmg_boundaries_gda2020_simp200m` | 3 | 82 KB | 44 KB | `DDMG Name` | GDA2020 (EPSG:7844) |
| `qld_far_north_ldmg_boundaries_gda2020_simp200m` | 21 | 256 KB | 125 KB | `LDMG Name` | GDA2020 (EPSG:7844) |
| `qld_north_coast_ddmg_boundaries_gda2020_simp200m` | 4 | 52 KB | 30 KB | `DDMG Name` | GDA2020 (EPSG:7844) |
| `qld_north_coast_ldmg_boundaries_gda2020_simp200m` | 8 | 77 KB | 41 KB | `LDMG Name` | GDA2020 (EPSG:7844) |
| `qld_northern_ddmg_boundaries_gda2020_simp200m` | 2 | 59 KB | 39 KB | `DDMG Name` | GDA2020 (EPSG:7844) |
| `qld_northern_ldmg_boundaries_gda2020_simp200m` | 16 | 151 KB | 79 KB | `LDMG Name` | GDA2020 (EPSG:7844) |
| `qld_south_east_ddmg_boundaries_gda2020_simp200m` | 2 | 14 KB | 10 KB | `DDMG Name` | GDA2020 (EPSG:7844) |
| `qld_south_east_ldmg_boundaries_gda2020_simp200m` | 3 | 20 KB | 13 KB | `LDMG Name` | GDA2020 (EPSG:7844) |
| `qld_southern_ddmg_boundaries_gda2020_simp200m` | 6 | 101 KB | 55 KB | `DDMG Name` | GDA2020 (EPSG:7844) |
| `qld_southern_ldmg_boundaries_gda2020_simp200m` | 13 | 140 KB | 74 KB | `LDMG Name` | GDA2020 (EPSG:7844) |

### Official QPS boundaries (for comparison)

| Layer | Features | GeoJSON | TopoJSON | Match field | Coordinates |
|---|---|---|---|---|---|
| `qld_qps_regions_gda94_simp200m` | 7 | 236 KB | 101 KB | `QPS Region` | GDA94 (EPSG:4283) |
| `qld_qps_districts_gda94_simp200m` | 15 | 314 KB | 129 KB | `QPS District` | GDA94 (EPSG:4283) |

## Metadata in the files

Every feature in every layer carries, besides its own attributes (district or council names and
codes), the same set of metadata properties so a file can be used, filtered and cited on its own:
`Layer Id`, `Layer Group`, `Layer Kind`, `Source`, `Source URL`, `Licence`, `Licence URL`,
`Dataset Date`, `Simplification Tolerance M`, `Coordinate Precision Decimals`, `CRS`, `Modified`.
Disaster district, council and region features also carry `Police Region Name`,
`Police Region Code`, `Police Region Short Name` and `Region Slug`, so the statewide files can be
filtered to a region without the per-region files. Every feature has a stable `id`: the district
name, the council's LGA code, the region code, the QPS region name or the QPS district id.

[`layers.json`](layers.json) is the machine-readable catalogue: for each layer its ids, URLs,
sizes, SHA-256 hashes, feature count, bounding box, property list, match field, source, licence
and dataset date; plus the region list with slugs and layer names, the district-to-region
grouping, the source datasets, and the URL pattern.

## Using a layer in Power BI

**Azure Maps visual.** Format pane > Reference layer > paste the GeoJSON URL
(for example `https://ehmelo.github.io/qld-disaster-management-map-layers/layers/qld_ddmg_boundaries_gda2020_simp200m.geojson`), or upload the file.
Put the data column that matches the layer's *match field* in the **Location** well; values
must match the property exactly, including case. Colour the shapes with a measure in the
**Color** well or through conditional formatting on the polygon fill.

**Shape Map visual.** Format pane > Map settings > Type > **URL**, then paste the TopoJSON
or GeoJSON URL, or press **Fx** and point it at a measure that returns the URL. The measure
route lets one visual switch maps with the report's filters, for example loading the
per-region council file for whichever Disaster Management Region is selected. Uploading the
`.topojson` file also works. Bind the matching column to **Location**.

Files are served with permissive cross-origin headers, so a URL reference works from the
Power BI service as well as Desktop. The layer URLs are stable; the viewer page has a
copy button beside each layer.

**Dated releases, stable URLs.** `layers/` always holds the latest published set; each publish
also freezes a copy under `releases/<date>/`, for example
`https://ehmelo.github.io/qld-disaster-management-map-layers/releases/2026-09-14/`. Bind a report to `layers/` to follow
future corrections, or to a dated `releases/<date>/` copy to freeze the boundary a report uses.
[`layers.json`](layers.json) records the current release under `release_url`.

The Power BI service caches URL layers for some time after a change; re-enter the URL or reopen
the report if a correction does not appear straight away.

## Sources and licences

| Dataset | Publisher | Licence | Dataset date |
|---|---|---|---|
| [QPS Disaster Districts](https://www.data.qld.gov.au/dataset/qps-disaster-districts) | Queensland Police Service, via the Queensland Government Open Data Portal | [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) | 19/05/2025 |
| [Local government area boundaries - Queensland](https://www.data.qld.gov.au/dataset/local-government-area-boundaries-queensland) | Department of Natural Resources and Mines, Manufacturing and Regional and Rural Development | [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) | extract of 11/05/2026 |
| [ASGS Edition 3 (2021) Local Government Areas](https://www.abs.gov.au/statistics/standards/australian-statistical-geography-standard-asgs-edition-3/jul2021-jun2026/access-and-downloads/digital-boundary-files) - Cook Shire coastline only | Australian Bureau of Statistics | [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) | 2021 |
| [QPS Regions](https://www.data.qld.gov.au/dataset/qps-regions) | Queensland Police Service | [CC BY 3.0 AU](https://creativecommons.org/licenses/by/3.0/au/) | 09/03/2022 |
| [QPS Districts](https://www.data.qld.gov.au/dataset/qps-districts) | Queensland Police Service | [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) | 09/03/2022 |

The derived layers keep the licence of their sources. Attribute the source dataset and
publisher when you reuse them; a link to this repository is welcome but not required.
The viewer page and any code in this repository are under the MIT licence (`LICENSE`).
The layers are modified from their sources (simplified, repackaged, Cook Shire repaired); this
statement and the per-feature `Modified` property are the change indication CC BY requires.

## Caveats

- **Disaster Management Regions are a grouping, not a gazetted boundary.** Use the official
  QPS layers if you need police regions.
- **Dataset dates.** The QPS Regions and Districts files are dated March 2022; check the
  source pages before relying on any boundary for an operational decision.
- **Simplification.** Shapes are generalised to a 200 m tolerance and 11 m coordinate
  rounding. Right for thematic maps at state and regional scale; wrong for anything that needs
  a precise line, including whether a given address falls inside a boundary.
- **Tolerances between shapes.** Within one layer, neighbouring shapes share their edges and
  agree to within the coordinate rounding (about 11 m); residual hairline overlaps left by the
  validity repair total about 0.0024 km² (2,400 m²) statewide, all on Cook Shire's seams with
  Aurukun, Pormpuraaw and Torres Shire; the district layer has none. Between layers, district and council boundaries come from two
  different government datasets and disagree by up to about 200 m in places (about 7 km² of
  council area falls outside any district statewide). None of this is visible at the intended
  scale; do not use these files to decide which side of a boundary a location falls on.
- **Datums.** Disaster district and council layers are GDA2020; the QPS layers are GDA94.
  The difference is under 2 m and irrelevant at these scales. The `crs` member inside the
  GeoJSON files records the source datum for reference only: Power BI, Azure Maps and Leaflet
  ignore it and read the coordinates as WGS84, which is the same thing at this precision.
- **Same names, different boundaries.** The Disaster Management Region layer and the official
  QPS regions layer use the same seven region names as their match values (Brisbane, Central,
  Far North, ...). Binding a region slicer to the wrong layer produces a plausible map with the
  wrong boundary and no error. Check the layer id in the visual before trusting a region map.

## Reporting a problem

Open an issue in this repository with the layer name and, if possible, the feature involved.
