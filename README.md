## ETO5513_Assessment_2: Team project

This repository contains a collaborative report for ETO5513 group assessment. The project explores poverty, inequality and economic wellbeing across countries using World Bank Data.

### Data Source:
Data is obtained from the World Bank and the Poverty and Inequality Platform(https://pip.worldbank.org/) and the World Bank poverty topic page (https://data.worldbank.org/topic/poverty), using the WDI package in R.

### Analysis Sections
1. Levels and Trends: Changes in extreme poverty over time and differences between poverty measures.
2. Growth and the Poor: Income growth among the bottom 40% compared with the overall population.
3. Inequality: Relationships between inequality, poverty and income distribution.
4. Poverty and Wellbeing: Relationships between extreme poverty, life expectancy and GDP per capita.

### Reproducibility
1. Clone this GitHub repository.
2. Open the project in RStudio.
3. Install the required R packages.
4. Knit the Assessment1.Rmd Markdown file to reproduce the HTML file, print the HTML to PDF.

### Collaboration
Each team member works on an individual Git branch, completed sections are merged into the master branch

### License
Original project code is released under the MIT License. World bank data is subject to its original licensing terms.

### Section 2 details: Growth and the Poor
**Data.** World Bank World Development Indicators, downloaded with the `WDI` package on 15 November 2026. Indicators used:

| Variable | Indicator | Code |
|---|---|---|
| `g_b40` | Annualised growth in survey mean consumption or income, bottom 40% (%) | `SI.SPR.PC40.ZG` |
| `g_all` | Annualised growth in survey mean consumption or income, total population (%) | `SI.SPR.PCAP.ZG` |
| `b40` | Survey mean consumption or income per capita, bottom 40% (2021 PPP $ per day) | `SI.SPR.PC40` |
| `gdp_pc` | GDP per capita (current US$) | `NY.GDP.PCAP.CD` |

The cleaned data are saved in `data/wdi_section2.rds` and committed to the repository, so the report knits without an internet connection. The code that created the file is in the `s2_data_source` chunk (`eval = FALSE`) at the end of Section 2 in `Assessment2.Rmd`. If you rebuild it, retry if the World Bank API times out.

**Packages.** The setup chunk uses `pacman`, so install it first with `install.packages("pacman")`. `pacman::p_load()` then installs and loads the rest. Knitting to PDF also needs LaTeX, for example `install.packages("tinytex")` then `tinytex::install_tinytex()`.

**Notes.** For each country the analysis uses the most recent survey year with data, so years differ between countries.
