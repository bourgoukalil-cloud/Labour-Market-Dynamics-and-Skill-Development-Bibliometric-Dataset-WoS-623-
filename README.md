# Labour Market Dynamics and Skill Development — Bibliometric Dataset (WoS 623)

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.XXXXXXX.svg)](https://doi.org/10.5281/zenodo.XXXXXXX)
[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

This repository provides the complete bibliometric dataset underlying the article:

> Bourgou, K., Abdi Khalife, M., Dunay, A., & Illés, C. B. (2026). **Labour market dynamics and skill development: Bibliometric and scientometric analysis.** *Prosperitas*. https://prosperitas.uni-bge.hu/

The dataset covers **623 Web of Science–indexed articles** published between **1975 and 2024** at the intersection of labour-market dynamics and skill development, extracted on **12 April 2024** from the Web of Science Core Collection.

---

## Scope and purpose

The dataset supports full replicability of the bibliometric and scientometric analyses reported in the article. It is published to:

- enable independent verification of the article's figures, tables and cluster structure;
- support follow-on studies that extend the sample to other databases (Scopus, Dimensions) or more recent years;
- provide a reference corpus for teaching bibliometric methods on labour-market and skill-development research.

---

## Search strategy

The full Web of Science query that generated the sample is:

```
TS = ("labor market" OR "employment market" OR "job market" OR "workforce market"
      OR "occupational market" OR "human capital market" OR "employment sector")
AND
TS = ("skill gap*" OR "reskilling" OR "upskilling" OR "in-demand skill*"
      OR "workforce skill*" OR "soft skill*" OR "technical skill*"
      OR "future skill*" OR "industry 4.0 skill*" OR "industry 4.0 competencies"
      OR "workplace skill*" OR "emerging skill*")

Timespan        : 1975-01-01 to 2024-04-12
Document types  : Article, Review, Proceedings Paper
Language        : All
Date of export  : 2024-04-12
Records         : 623
```

---

## Repository structure

```
.
├── README.md                                   this file
├── LICENSE                                     Creative Commons Attribution 4.0 International
├── CITATION.cff                                how to cite this dataset
├── docs/
│   └── codebook.md                             description of every data file
├── data/
│   ├── raw/
│   │   ├── Plaintext623.txt                    full Web of Science export (WoS plaintext format)
│   │   └── Plaintext623-02.txt                 supplementary WoS export block
│   ├── processed/
│   │   ├── CitationReport_623.xlsx             WoS citation report for the sample
│   │   ├── Authors_623.txt                     author frequency counts
│   │   ├── Affiliations_623.txt                institutional affiliation frequency counts
│   │   ├── Department_623.txt                  departmental affiliation frequency counts
│   │   ├── Countries623.xlsx                   country publication and citation counts (full)
│   │   ├── countries623.txt                    country publication frequency (plain text)
│   │   ├── Publications_year_623.txt           annual publication counts
│   │   └── Research_Area_623.txt               WoS research area distribution
│   └── networks/
│       ├── keyword_cooccurrence/
│       │   ├── Nodes623.csv                    VOSviewer keyword nodes (71 keywords, 5 clusters)
│       │   ├── Edges623.csv                    keyword co-occurrence edges with weights
│       │   ├── Comprehensive_Node_Attributes.csv  extended node metrics (centralities, etc.)
│       │   └── Comprehensive_Edge_Attributes.csv  extended edge-level attributes
│       └── country_collaboration/
│           ├── Node_countries_623.csv          VOSviewer country nodes (38 countries, 4 clusters)
│           └── Edge_countries_623.csv          country co-authorship edges
└── figures/
    ├── Countries-Graph.png                     country collaboration network (export)
    ├── Education-central-link-623.png          education-centred keyword visualisation
    ├── Graph_python_623.png                    Python-generated network graph
    ├── Keyword_Cooccurrence_Network.png        full keyword co-occurrence map (high resolution)
    └── NetworkGraph623-71key.png               71-keyword VOSviewer map (publication figure)
```

A detailed description of every column in every file is in [`docs/codebook.md`](docs/codebook.md).

---

## Software used

- **Web of Science Core Collection** — bibliographic data source (requires institutional subscription)
- **VOSviewer 1.6.20** — co-occurrence mapping and clustering ([vosviewer.com](https://www.vosviewer.com/))
- **Python 3.11** with `networkx`, `pandas`, `matplotlib` — network metrics and auxiliary analysis
- **Microsoft Excel** — descriptive tables

---

## Replication

To reproduce the main results:

1. **Raw records**: open `data/raw/Plaintext623.txt` in VOSviewer (Create → Create a map based on bibliographic data → Read data from bibliographic database files → WoS tab).
2. **Keyword co-occurrence network**: set keyword type to *Keywords Plus*, minimum occurrences = 5, normalisation = association strength, clustering = modularity-based (default resolution = 1.00), minimum cluster size = 5. This reproduces the 71-keyword, 5-cluster structure reported in Table 4 of the article.
3. **Country co-authorship network**: set unit of analysis to country, minimum documents per country = 5, which yields the 38-country network reported in Figure 2.

The processed outputs under `data/networks/` can be imported directly into VOSviewer or Gephi for further analysis.

---

## Citation

If you use this dataset, please cite both the article and the dataset:

**Article**
> Bourgou, K., Abdi Khalife, M., Dunay, A., & Illés, C. B. (2026). Labour market dynamics and skill development: Bibliometric and scientometric analysis. *Prosperitas*.

**Dataset**
> Bourgou, K. (2026). *Labour market dynamics and skill development — Bibliometric dataset (WoS 623)* [Data set]. GitHub. [https://github.com/Bourgou/labour-market-bibliometric-wos623](https://github.com/bourgoukalil-cloud/Labour-Market-Dynamics-and-Skill-Development-Bibliometric-Dataset-WoS-623-)

A machine-readable citation is provided in [`CITATION.cff`](CITATION.cff).

---

## Licence

The dataset is released under the **Creative Commons Attribution 4.0 International Licence (CC BY 4.0)** — see [`LICENSE`](LICENSE).

You are free to share and adapt the material for any purpose, including commercially, provided you give appropriate credit, link to the licence and indicate if changes were made.

**Note on the underlying bibliographic metadata**: individual bibliographic records are extracted from the Web of Science Core Collection and remain subject to Clarivate's terms of use. Redistribution is limited to the aggregated and derived form provided here, as permitted for scholarly replication purposes.

---

## Known limitations

Users should be aware of the limitations documented in Section 3.5 of the article:

- **Database bias** — Web of Science under-represents non-English venues, applied-training journals, and Global-South publishers.
- **Language bias** — English-language publications dominate the sample.
- **Journal-coverage bias** — the 2015 ESCI expansion creates a discontinuity in the annual series.
- **First-author affiliation** — multi-affiliated authors are attributed only to their first listed affiliation.
- **Citation lag** — papers published after 2020 have had less time to accumulate citations.

---

## Contact

For questions about the dataset or replication issues, please open an issue on the repository or contact:

**Khalil Bourgou**  
Doctoral School of Management and Business Administration  
John von Neumann University, Kecskemét, Hungary  
📧 bourgoukalil@gmail.com

---

## Acknowledgements

We thank the Editor-in-Chief and reviewers of *Prosperitas* for the careful editorial process that strengthened this work.
