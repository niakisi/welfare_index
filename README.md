# Multidimensional Welfare Index for Russian Regions (2020–2023)

This project constructs an **Integrated Welfare Index** for 84 Russian federal subjects using official Rosstat data. The index captures four dimensions of welfare — material wellbeing, property endowment, human capital, and digitalization — and is used to compare regions, identify typological clusters, and test hypotheses about the structure of regional inequality.

---

## Motivation

Existing welfare measurement tools have critical limitations for regional analysis in Russia:
- **International indices** (HDI, OECD BLI) were designed for cross-country comparisons and are not available at the regional level
- **Single Rosstat indicators** (income, poverty rate) capture only the monetary dimension
- **Commercial Russian ratings** lack transparent, reproducible methodology

This project fills that gap by building a statistically justified, reproducible, and multidimensional index adapted to Russian regional statistics.

---

## Methodology

The index is built in three sequential steps:

### 1. Min-Max Normalisation
All indicators are scaled to [0, 1]. Indicators where *lower is better* (poverty rate, infant mortality, share of dilapidated housing) are inverted before normalisation, so that a higher normalised value always means better welfare.

### 2. Principal Component Analysis (PCA) Within Blocks
Within each of the four thematic blocks, PCA is applied to the normalised indicators. The **first principal component (PC1)** score serves as the block score. Block weights in the final aggregation are set equal to the **explained variance ratio** of PC1 — a data-driven approach that requires no subjective expert judgement.

### 3. Weighted Aggregation
The four block scores are combined into a final index using a weighted sum. The index is rescaled to [0, 100] for interpretability.

Robustness is tested by recalculating the index with equal weights (0.25 per block). The correlation between weighted and equal-weight rankings is **r = 0.977**, confirming the results are stable to the weighting scheme.

---

## Indicator System

| Block | Indicator | Direction |
|---|---|---|
| **Material Wellbeing** | Per capita monetary income, RUB/month | + |
| | Poverty rate, % of population | − |
| | Real disposable income index, % of prev. year | + |
| **Property Endowment** | Housing area per capita, sq.m | + |
| | Cars per 1,000 persons | + |
| **Human Capital** | Life expectancy at birth, years | + |
| | Infant mortality per 1,000 live births | − |
| | Preschool education coverage, % | + |
| | University students per 10,000 persons | + |
| **Digitalization** | Households with internet access, % | + |
| | Internet users among population, % | + |
| | Organizations using internet, % | + |

---

## Key Results (2023, 84 regions)

| Metric | Value |
|---|---|
| Median index | 46.1 |
| Standard deviation | 21.1 |
| Top region | Moscow (100.0) |
| Bottom region | Republic of Ingushetia (0.0) |
| Sensitivity (r, weighted vs equal weights) | 0.977 |
| Correlation with per capita income | 0.513 |

### Four Regional Clusters

| Cluster | Regions | Mean index | Profile |
|---|---|---|---|
| 1 — High welfare | 17 | 69.3 ± 12.0 | Balanced high scores across all blocks |
| 2 — Above average | 25 | 59.5 ± 18.8 | High material block, moderate digitalization |
| 3 — Specific profile | 11 | 38.0 ± 19.2 | Low material block, relatively high human capital |
| 4 — Below average | 30 | 34.2 ± 11.9 | Uniformly low scores across all dimensions |

### Research Hypotheses

- **H1** ✅ Regions differ in welfare *structure*, not only income level (e.g. Kamchatsky Krai ranks 2nd in the index but is not in the income top-10)
- **H2** ✅ Stable geographical and typological patterns confirmed (cluster composition follows known regional typologies)
- **H3** ✅ Human capital and digitalization contribute independently of income (index–income correlation r = 0.513, not 1.0)

---

## Repository Structure

```
├── welfare_index_russia.ipynb   # Main notebook: full pipeline from data to figures
├── data_rosstat.xlsx            # Dataset: 84 regions × 12 indicators × 4 years
├── welfare_index_paper_EN.docx  # Full research paper (English)
└── README.md
```

---

## Data Source

**Federal State Statistics Service of Russia (Rosstat)**  
*Regions of Russia. Socio-Economic Indicators* — editions 2021, 2022, 2023, 2024  
URL: https://rosstat.gov.ru

Data cover **84 federal subjects** over **2020–2023**. Excluded from analysis:
- Yamalo-Nenets and Nenets Autonomous Okrugs — extreme income values (oil & gas rent distortion)
- Chukotka Autonomous Okrug — systematic data gaps
- Four new federal subjects (added 2022) — incomplete statistical series

---


## References

- Aivazyan S.A., Afanasyev M.Yu., Kudrov A.V. (2023). Integral indicator of quality of living conditions in Russian regions. *Economy of Region*, 19(1), 17–32.
- Zubarevich N.V. (2019). *Socio-economic development of Russian regions: inequality and growth factors*. Moscow: NISP.
- Sen A. (1999). *Development as Freedom*. New York: Oxford University Press.
- Stiglitz J.E., Sen A., Fitoussi J.-P. (2010). *Mismeasuring Our Lives*. New York: The New Press.
- OECD (2008). *Handbook on Constructing Composite Indicators*. Paris: OECD Publishing.
- UNDP (2024). *Human Development Report 2023/2024*. New York: UNDP.
- Litvintseva G.P. et al. (2020). Digital inequality of Russian regions. *Problems of Forecasting*, 5, 97–107.
