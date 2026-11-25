## ETO5513_Assessment_2: Team Project

This repository contains a collaborative report for the ETO5513 group assessment. The project explores poverty, inequality and economic wellbeing across countries using World Bank data.

### Data Source

Data is obtained from the World Bank, the Poverty and Inequality Platform (https://pip.worldbank.org/) and the World Bank poverty topic page (https://data.worldbank.org/topic/poverty), using the WDI package in R.

### Analysis Sections

1. Levels and Trends: Changes in extreme poverty over time and differences between poverty measures.
2. Growth and the Poor: Income growth among the bottom 40% compared with the overall population.
3. Inequality: Relationships between inequality, poverty and income distribution.
4. Poverty and Wellbeing: Relationships between extreme poverty, life expectancy and GDP per capita.

### Reproducibility

1. Clone this GitHub repository.
2. Open the project in RStudio.
3. Install the required R packages, starting with `install.packages("pacman")`.
4. Ensure the saved datasets are available in the `data` folder.
5. Knit the `Assessment2.Rmd` file to reproduce the HTML report.
6. Print or export the HTML report to PDF if required.

An internet connection may be required to install packages and retrieve data for sections that access the World Bank API directly.

### Collaboration

Each team member works on an individual Git branch. Completed sections are merged into the master branch.

### License

Original project code is released under the MIT License. World Bank data is subject to its original licensing terms.

### Section 1 details: Levels and Trends

**Research questions**

1. How has extreme poverty changed over time, and which regions have progressed fastest?
2. How do international and national poverty lines differ for the same countries?

**Data.** World Bank World Development Indicators, accessed using the WDI package in R. Indicators retrieved:

| Variable | Indicator | Code |
|---|---|---|
| `poverty` | International poverty headcount ratio ($3/day, 2021 PPP) | `SI.POV.DDAY` |
| `national_poverty` | National poverty headcount ratio | `SI.POV.NAHC` |
| `poverty_gap` | Poverty gap at the international poverty line | `SI.POV.GAPS` |
| `gdp_pc` | GDP per capita (current US$) | `NY.GDP.PCAP.CD` |
| `population` | Total population | `SP.POP.TOTL` |

The dataset contains 6,916 observations and 17 variables covering the period 2000–2025. It is saved in `data/wdi_section1.rds`.

**Methodology.**

- Regional extreme poverty trends are examined between 2002 and 2024.
- Poverty reductions are calculated in percentage points.
- Regional aggregates are excluded from country-level comparisons.
- International and national poverty rates are compared using the latest available matched observation for each country.
- The ten countries with the largest absolute differences are selected for visualisation.

**Packages.** WDI, dplyr, tidyr, ggplot2 and knitr.

**Reproducibility.** The data retrieval procedure is documented in the `s1-data-source` chunk (`eval = FALSE`) in `Assessment2.Rmd`. The saved RDS file allows Section 1 to be reproduced without downloading the data again. Fresh downloads may differ due to World Bank data revisions.

**Notes.** Missing observations, incomplete regional coverage, different survey years and differences in national poverty definitions limit comparability and generalisability.

### Section 2 details: Growth and the Poor

**Data.** World Bank World Development Indicators, downloaded with the `WDI` package on 15 November 2026. Indicators used:

| Variable | Indicator | Code |
|---|---|---|
| `g_b40` | Annualised growth in survey mean consumption or income, bottom 40% (%) | `SI.SPR.PC40.ZG` |
| `g_all` | Annualised growth in survey mean consumption or income, total population (%) | `SI.SPR.PCAP.ZG` |
| `b40` | Survey mean consumption or income per capita, bottom 40% (2021 PPP $ per day) | `SI.SPR.PC40` |
| `gdp_pc` | GDP per capita (current US$) | `NY.GDP.PCAP.CD` |

The cleaned data are saved in `data/wdi_section2.rds` and committed to the repository, so Section 2 knits without downloading the dataset again. The code that created the file is in the `s2_data_source` chunk (`eval = FALSE`) at the end of Section 2 in `Assessment2.Rmd`. If you rebuild it, retry if the World Bank API times out.

**Packages.** The setup chunk uses `pacman`, so install it first with `install.packages("pacman")`. `pacman::p_load()` then installs and loads the rest. Knitting directly to PDF also needs LaTeX, for example `install.packages("tinytex")` then `tinytex::install_tinytex()`.

**Notes.** For each country the analysis uses the most recent survey year with data, so years differ between countries.

### Section 4 details: Poverty and Wellbeing

**Research questions**

1. Do countries with higher extreme poverty rates have lower life expectancy?
2. Does the relationship between poverty and life expectancy remain after accounting for GDP per capita?

**Data:** World Bank World Development Indicators, accessed using the `WDI` package in R. Indicators retrieved:

| Variable | Indicator | Code |
|---|---|---|
| `poverty` | International poverty headcount ratio ($3/day, 2021 PPP) | `SI.POV.DDAY` |
| `life_expectancy` | Life expectancy at birth, total (years) | `SP.DYN.LE00.IN` |
| `gdp_per_capita` | GDP per capita (current US$) | `NY.GDP.PCAP.CD` |

The dataset covers 2015–2023. After excluding regional aggregates and observations with missing values, the analysis includes 702 country-year observations from 150 countries. The original World Bank data are saved in `data/wdi_section4.rds`.

**Methodology:**

- Regional aggregates and observations with missing values are excluded.
- GDP per capita is categorised into three groups: low (below US$5,000), middle (US$5,000–19,999) and high (US$20,000 or above).
- Scatterplots and boxplots are used to examine the relationship between poverty, life expectancy and GDP per capita.
- Two linear regression models are compared: Model 1 examines the relationship between poverty and life expectancy, while Model 2 adding variable for log GDP per capita.
- Regression coefficients, statistical significance and adjusted R² are compared to assess the relationships between variables.

**Packages:** WDI, dplyr, ggplot2, kableExtra and knitr.

**Reproducibility:** The data retrieval procedure is included in the `s4-data-source` chunk (`eval = FALSE`) at the end of Section 4 in `Assessment2.Rmd`. The dataset is saved into `data` folder to allows Section 4 to be reproduced without downloading the data again. Results from new downloads may vary due to World bank data updates.

**Notes:** Missing data and uneven country coverage may affect the results. The analysis also excludes other factors influencing life expectancy, such as healthcare and education. The findings represent statistical associations rather than causal relationships.