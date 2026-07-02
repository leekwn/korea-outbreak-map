# HPAI Korea Outbreak Map

A single-file HTML tool that visualizes Korean HPAI (Highly Pathogenic Avian
Influenza) case data on an interactive map, entirely in the browser. No
server or build step — open the `.html` file directly, or serve it as a
static file. No data ever leaves the browser.

## Tool

**`HPAI_korea_publication_map.html`** — simplified, publication-friendly map.
Minimal controls, choice of colorblind-safe (Okabe-Ito) or high-contrast
palette, clean basemap. Records with no genotype value (blank, `N/A`,
`n.a.`, `unknown`, etc.) are hidden from the map by default — toggle "Hide
records with no genotype data" to show them. Class and subtype checkbox
filters (auto-populated from whatever values are in the loaded data, with
"All"/"None" shortcuts) let you show only defined categories. Intended for
figures in reports/papers. Sample data: `hpai_korea_publication_sample.csv`.

## CSV schema

| column      | meaning                                   | example values                  |
|-------------|--------------------------------------------|----------------------------------|
| `class`     | host type                                   | `Poultry`, `Wild bird`           |
| `institute` | reporting/diagnostic institute              | `APQA`, `NIWDC`                  |
| `date`      | sample collection date                      | `2024-11-05`                     |
| `species`   | species/breed                               | `Chicken`, `Mandarin Duck`       |
| `sample`    | sample type                                 | `Feces`, `Dead`, `Live captured` |
| `subtype`   | virus subtype                               | `H5N1`, `H5N6`, `H5N8`, `H7N9`   |
| `genotype`  | genotype/clade label                        | `2.3.4.4b-G1`                    |
| `lat`, `lon`| decimal latitude / longitude                | `36.3`, `127.6`                  |

Column names are auto-detected (English and Korean variants); use the
mapping table in step 2 of the page if a column isn't picked up. Only `lat`
and `lon` are required — everything else is optional.

The sample CSV and the sample embedded in the HTML are **synthetic data**
generated for demo purposes, not real outbreak records.

## Notes

- All CSV parsing, filtering, and rendering happens client-side; nothing is
  uploaded anywhere.
- Basemap tiles (CARTO) and Leaflet.js are loaded from public CDNs, so an
  internet connection is needed for the map tiles/library even though your
  data stays local.
