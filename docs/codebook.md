# Codebook

Full description of every file in this dataset. All files use UTF-8 encoding. CSV files use comma separators; plain-text frequency files use tab separators as exported from Web of Science.

---

## `data/raw/`

### `Plaintext623.txt`

The complete Web of Science Core Collection export for the 623 articles in the sample, in WoS plaintext format (field tags such as `AU`, `TI`, `AB`, `C1`, `CR`, `DE`, `ID`, `PY`, `TC`). Each record is delimited by `ER`. This is the primary input file for VOSviewer and the authoritative source of all derived files in this repository.

- **Encoding**: UTF-8 with BOM
- **Records**: 623 articles
- **Size**: 3.7 MB
- **Export date**: 2024-04-12

### `Plaintext623-02.txt`

A supplementary WoS export block containing an additional slice of the sample (used for consistency checking during preprocessing).

---

## `data/processed/`

### `CitationReport_623.xlsx`

Web of Science's Citation Report for the sample, showing total citations, h-index, average citations per item and the annual citation distribution. Columns follow the standard WoS Citation Report layout.

### `Authors_623.txt`

Author publication frequency within the sample.

| Column | Description |
|---|---|
| `Authors` | Author name as recorded by WoS (last name + initials) |
| `Record Count` | Number of articles in the sample with this author |
| `% of 623` | Percentage of the 623-article sample |

### `Affiliations_623.txt`

Institutional affiliation frequencies. Same column structure as `Authors_623.txt`.

### `Department_623.txt`

Departmental affiliation frequencies (one level deeper than institution). Same column structure.

### `Countries623.xlsx`

Country-level publication and citation counts, with two panels:
- **Panel A** — ordered by number of papers
- **Panel B** — ordered by number of citations

Columns include country name, number of papers, number of citations.

### `countries623.txt`

Plain-text country publication-frequency table.

| Column | Description |
|---|---|
| `Countries/Regions` | Country name as recorded by WoS |
| `Record Count` | Number of articles with at least one author from this country |
| `% of 623` | Percentage of the 623-article sample |

### `Publications_year_623.txt`

Annual publication counts across the full sample window.

| Column | Description |
|---|---|
| `Publication Years` | Year |
| `Record Count` | Number of articles published that year |
| `% of 625` | Percentage of the sample (minor rounding to 625 reflects WoS internal tallying) |

### `Research_Area_623.txt`

Distribution of the sample across Web of Science research areas (one article may be assigned to multiple areas).

| Column | Description |
|---|---|
| `Research Areas` | WoS research area label |
| `Record Count` | Number of articles tagged with this area |
| `% of 625` | Percentage of the sample |

---

## `data/networks/keyword_cooccurrence/`

Keyword co-occurrence network of 71 Keywords Plus terms, generated with VOSviewer 1.6.20 (minimum occurrences = 5, normalisation = association strength, modularity-based clustering, resolution = 1.00, minimum cluster size = 5). Yields 5 thematic clusters.

### `Nodes623.csv`

VOSviewer node export for the keyword network.

| Column | Description |
|---|---|
| `id` | Internal keyword identifier |
| `label` | Keyword |
| `x`, `y` | 2-D map coordinates assigned by VOSviewer |
| `cluster` | Cluster membership (1–5) |
| `weight<Links>` | Number of other keywords it co-occurs with |
| `weight<Total link strength>` | Sum of co-occurrence weights |
| `weight<Occurrences>` | Number of articles the keyword appears in |
| `score<Avg. pub. year>` | Mean publication year of articles using the keyword |
| `score<Avg. citations>` | Mean citations of articles using the keyword |
| `score<Avg. norm. citations>` | Mean normalised citations |
| `Cluster`, `No. of Occurences` | Cluster-level aggregate columns (first few rows only) |

### `Edges623.csv`

Keyword co-occurrence edges.

| Column | Description |
|---|---|
| `source` | Source keyword id (matches `id` in `Nodes623.csv`) |
| `target` | Target keyword id |
| `weight` | Co-occurrence frequency |

### `Comprehensive_Node_Attributes.csv`

Extended node-level network metrics computed in Python (NetworkX) for every keyword.

| Column | Description |
|---|---|
| `id`, `label`, `x`, `y`, `cluster` | As in `Nodes623.csv` |
| `total_link_strength`, `occurrences` | As in `Nodes623.csv` |
| `degree_centrality` | Normalised degree |
| `betweenness_centrality` | Normalised betweenness |
| `closeness_centrality` | Normalised closeness |
| `eigenvector_centrality` | Eigenvector centrality |
| `pagerank` | PageRank |
| `clustering_coefficient` | Local clustering coefficient |
| `core_number` | k-core assignment |
| `load_centrality` | Load centrality |
| `eccentricity` | Node eccentricity |
| `average_path_length` | Mean shortest-path length from the node |
| `radiality` | Radiality |
| `participation_coefficient` | Participation coefficient (across clusters) |
| `modularity_class` | Modularity class assignment |
| `assortativity` | Node assortativity contribution |

### `Comprehensive_Edge_Attributes.csv`

Edge-level attributes with co-occurrence weight and additional metrics used in the Python analysis.

---

## `data/networks/country_collaboration/`

Country co-authorship network of 38 countries meeting the ≥ 5 documents threshold (87 countries in the raw sample).

### `Node_countries_623.csv`

VOSviewer country-node export.

| Column | Description |
|---|---|
| `id` | Internal country identifier |
| `label` | Country name (lowercase) |
| `x`, `y` | 2-D map coordinates |
| `cluster` | Cluster membership (1–4) |
| `weight<Links>` | Number of co-authorship partners |
| `weight<Total link strength>` | Sum of co-authorship weights |
| `weight<Documents>` | Number of articles with this country |
| `weight<Citations>` | Total citations received |
| `weight<Norm. citations>` | Total normalised citations |
| `score<Avg. pub. year>` | Mean publication year |
| `score<Avg. citations>` | Mean citations per article |
| `score<Avg. norm. citations>` | Mean normalised citations per article |

### `Edge_countries_623.csv`

Country co-authorship edges, three columns without a header row:

| Column | Description |
|---|---|
| col 1 | Source country id |
| col 2 | Target country id |
| col 3 | Co-authorship weight |

---

## `figures/`

Pre-rendered PNG figures that appear in the article or support its interpretation.

| File | Description |
|---|---|
| `NetworkGraph623-71key.png` | 71-keyword co-occurrence map — this is the publication figure (Appendix B of the article) |
| `Keyword_Cooccurrence_Network.png` | High-resolution export of the same keyword network with enlarged labels |
| `Countries-Graph.png` | Country co-authorship network — Figure 2 of the article |
| `Education-central-link-623.png` | Education-centred link visualisation of the keyword network |
| `Graph_python_623.png` | Python/NetworkX rendering of the keyword network with centrality highlighting |

All PNG files are at publication-ready resolution. Source VOSviewer `.net` and `.vos` files can be regenerated from the raw export (see Replication in the README).

---

## Known inconsistencies

- `% of 625` vs `% of 623` appearing in some WoS exports reflects WoS's internal counting of article variants and does not change the sample size (623 unique articles).
- The country file `countries623.txt` lists 87 countries in total; the network file `Node_countries_623.csv` lists only the 38 countries meeting the ≥ 5 documents threshold.
- `Nodes623.csv` has 71 keyword rows but the trailing cluster-aggregate columns (`Cluster`, `No. of Occurences`) are populated only for the first five rows — these are VOSviewer summary artefacts and can be ignored for most analyses.
