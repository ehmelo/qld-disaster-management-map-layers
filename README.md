# Queensland disaster management map layers

Boundary files for Queensland's disaster management geography, prepared for the Power BI
**Azure Maps** visual (GeoJSON reference layer) and the **Shape Map** visual (TopoJSON).
Every layer is simplified, cleaned of overlaps between neighbouring shapes, and served from
GitHub Pages so it can be referenced by URL.

**Preview the layers:** https://ehmelo.github.io/qld-disaster-management-map-layers/

Generated 13/09/2026. Layer metadata, including sources and
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

| Disaster Management Region | Code | Short name | Disaster districts (DDMG) |
|---|---|---|---|
| Brisbane Region | `BR` | Brisbane | Brisbane, Moreton |
| Central Region | `CR` | Central | Gladstone, Longreach, Mackay, Rockhampton |
| Far Northern Region | `FNR` | Far North | Cairns, Innisfail, Mareeba |
| North Coast Region | `NCR` | North Coast | Bundaberg, Gympie, Maryborough, Sunshine Coast |
| Northern Region | `NR` | Northern | Mount Isa, Townsville |
| South Eastern Region | `SER` | South East | Gold Coast, Logan |
| Southern Region | `SR` | Southern | Charleville, Dalby, Ipswich, Roma, Toowoomba, Warwick |

Local government areas take the region of the disaster district they sit in.

## Layers

All coordinates are longitude / latitude in degrees. `simp20` and `simp10` mean the shapes
were simplified to 20 % or 10 % of the source vertex count, which is ample for statewide and
regional maps and keeps files small. Coordinates are rounded to 5 decimal places (about 1 m).

The disaster district and council polygons extend over Queensland's coastal waters, as the
source datasets draw them: disaster management areas cover the state's maritime territory,
so a coastal council or district is larger than its land area. One repair was needed: the
Cook Shire polygon in the source pipeline had lost its western coastal land when a Gulf of
Carpentaria extension was removed; that land is restored here from the raw shapefile, clipped
to the Australian Bureau of Statistics 2021 coastline.

### Statewide

| Layer | Features | GeoJSON | TopoJSON | Match field | Coordinates |
|---|---|---|---|---|---|
| `qld_ddmg_boundaries_gda2020_simp20` | 23 | 643 KB | 154 KB | `DDMG Name` | GDA2020 (EPSG:7844) |
| `qld_ldmg_boundaries_gda2020_simp20` | 78 | 1595 KB | 357 KB | `LDMG Name` | GDA2020 (EPSG:7844) |

### Disaster Management Regions

| Layer | Features | GeoJSON | TopoJSON | Match field | Coordinates |
|---|---|---|---|---|---|
| `qld_dm_region_boundaries_gda2020_simp20` | 7 | 373 KB | 102 KB | `Police Region Short Name` | GDA2020 (EPSG:7844) |

### Per region

One district file and one council file for each Disaster Management Region. Subsets of the
statewide layers; each feature also carries `Police Region Name`, `Police Region Code` and
`Police Region Short Name` (the property names the consuming reports use for the region).

| Layer | Features | GeoJSON | TopoJSON | Match field | Coordinates |
|---|---|---|---|---|---|
| `qld_brisbane_ddmg_boundaries_gda2020_simp20` | 2 | 28 KB | 12 KB | `DDMG Name` | GDA2020 (EPSG:7844) |
| `qld_brisbane_ldmg_boundaries_gda2020_simp20` | 3 | 40 KB | 17 KB | `LDMG Name` | GDA2020 (EPSG:7844) |
| `qld_central_ddmg_boundaries_gda2020_simp20` | 4 | 161 KB | 48 KB | `DDMG Name` | GDA2020 (EPSG:7844) |
| `qld_central_ldmg_boundaries_gda2020_simp20` | 14 | 317 KB | 83 KB | `LDMG Name` | GDA2020 (EPSG:7844) |
| `qld_far_north_ddmg_boundaries_gda2020_simp20` | 3 | 120 KB | 39 KB | `DDMG Name` | GDA2020 (EPSG:7844) |
| `qld_far_north_ldmg_boundaries_gda2020_simp20` | 21 | 603 KB | 151 KB | `LDMG Name` | GDA2020 (EPSG:7844) |
| `qld_north_coast_ddmg_boundaries_gda2020_simp20` | 4 | 80 KB | 28 KB | `DDMG Name` | GDA2020 (EPSG:7844) |
| `qld_north_coast_ldmg_boundaries_gda2020_simp20` | 8 | 139 KB | 44 KB | `LDMG Name` | GDA2020 (EPSG:7844) |
| `qld_northern_ddmg_boundaries_gda2020_simp20` | 2 | 76 KB | 32 KB | `DDMG Name` | GDA2020 (EPSG:7844) |
| `qld_northern_ldmg_boundaries_gda2020_simp20` | 16 | 228 KB | 69 KB | `LDMG Name` | GDA2020 (EPSG:7844) |
| `qld_south_east_ddmg_boundaries_gda2020_simp20` | 2 | 23 KB | 10 KB | `DDMG Name` | GDA2020 (EPSG:7844) |
| `qld_south_east_ldmg_boundaries_gda2020_simp20` | 3 | 39 KB | 15 KB | `LDMG Name` | GDA2020 (EPSG:7844) |
| `qld_southern_ddmg_boundaries_gda2020_simp20` | 6 | 158 KB | 55 KB | `DDMG Name` | GDA2020 (EPSG:7844) |
| `qld_southern_ldmg_boundaries_gda2020_simp20` | 13 | 238 KB | 77 KB | `LDMG Name` | GDA2020 (EPSG:7844) |

### Official QPS boundaries (for comparison)

| Layer | Features | GeoJSON | TopoJSON | Match field | Coordinates |
|---|---|---|---|---|---|
| `qld_qps_regions_gda94_simp10` | 7 | 142 KB | 42 KB | `QPS Region` | GDA94 (EPSG:4283) |
| `qld_qps_districts_gda94_simp10` | 15 | 204 KB | 57 KB | `QPS District` | GDA94 (EPSG:4283) |

## Using a layer in Power BI

**Azure Maps visual.** Format pane > Reference layer > paste the GeoJSON URL
(for example `https://ehmelo.github.io/qld-disaster-management-map-layers/layers/qld_ddmg_boundaries_gda2020_simp20.geojson`), or upload the file.
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

## Sources and licences

| Dataset | Publisher | Licence | Dataset date |
|---|---|---|---|
| [QPS Disaster Districts](https://www.data.qld.gov.au/dataset/qps-disaster-districts) | Queensland Police Service, via the Queensland Government Open Data Portal | [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) | 19/05/2025 |
| [Local government area boundaries - Queensland](https://www.data.qld.gov.au/dataset/local-government-area-boundaries-queensland) | Department of Natural Resources and Mines, Manufacturing and Regional and Rural Development | [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) | extract of 11/05/2026 |
| [ASGS Edition 3 (2021) Local Government Areas](https://www.abs.gov.au/statistics/standards/australian-statistical-geography-standard-asgs-edition-3/jul2021-jun2026/access-and-downloads/digital-boundary-files) - Cook Shire coastline only | Australian Bureau of Statistics | [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) | 2021 |
| [QPS Regions](https://www.data.qld.gov.au/dataset/qps-regions) | Queensland Police Service | [CC BY 3.0](https://creativecommons.org/licenses/by/3.0/au/) | 09/03/2022 |
| [QPS Districts](https://www.data.qld.gov.au/dataset/qps-districts) | Queensland Police Service | [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) | 09/03/2022 |

The derived layers keep the licence of their sources. Attribute the source dataset and
publisher when you reuse them; a link to this repository is welcome but not required.
The viewer page and any code in this repository are under the MIT licence (`LICENSE`).

## Caveats

- **Disaster Management Regions are a grouping, not a gazetted boundary.** Use the official
  QPS layers if you need police regions.
- **Dataset dates.** The QPS Regions and Districts files are dated March 2022; check the
  source pages before relying on any boundary for an operational decision.
- **Simplification.** Shapes are generalised. They are right for thematic maps at state and
  regional scale, not for property-level work.
- **Datums.** Disaster district and council layers are GDA2020; the QPS layers are GDA94.
  The difference is under 2 m and irrelevant at these scales.

## Reporting a problem

Open an issue in this repository with the layer name and, if possible, the feature involved.
