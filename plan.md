# Project Plan: Cost of Living in California vs. La Paz

## 1. Research Question & Hypothesis

**Question:** Where is it more affordable to live: California (US) or La Paz (Bolivia)?

**Hypothesis:** La Paz is cheaper in absolute (nominal USD) terms. Once adjusted for purchasing power parity (PPP) and local incomes, I expect it is *not* cheaper in relative terms.

## 2. Data Sources

- **Source:** World Bank Open Data (World Development Indicators)
- **Python tools:** `wbgapi` to pull the data, `pandas` to clean it, `matplotlib`/`seaborn` for charts
- **Candidate indicators:**

  | Code | Description |
  |------|-------------|
  | `PA.NUS.PPP` | PPP conversion factor, GDP (LCU per international $) |
  | `PA.NUS.PRVT.PP` | PPP conversion factor, private consumption |
  | `NY.GDP.PCAP.PP.CD` | GDP per capita, PPP (current international $) |
  | `NY.GNP.PCAP.PP.CD` | GNI per capita, PPP |
  | `NE.CON.PRVT.PC.KD` | Household final consumption expenditure per capita |
  | `FP.CPI.TOTL.ZG` | Inflation, consumer prices (annual %) |

- **Limitation:** The World Bank reports country-level data (US, BOL), not California or La Paz. Supplementary sources for state/city-level detail:
  - **California:** BEA Regional Price Parities and per-capita personal income; BLS wage data
  - **La Paz:** INE Bolivia (Instituto Nacional de Estadística)
  - **Rent and daily costs:** a cost-of-living dataset such as Numbeo (cited, and noted as crowd-sourced)

## 3. Cleaning Steps

- **Date range:** the most recent 5 years with data for both countries
- **Merge:** combine indicators into one tidy DataFrame keyed on `country` and `year`
- **Missing values:** interpolate linearly within each country's time series; if a value is missing at the start or end of the range, forward- or back-fill it and flag it. Record every imputed value.
- **Transformations:** convert local-currency values to USD and to PPP-adjusted international $; compute ratios such as income ÷ cost of living and disposable income (income − essential expenses)

## 4. Charts & Analysis

1. **PPP comparison:** price levels in the US vs. Bolivia over the 5-year window (line chart)
2. **PPP-adjusted income vs. cost of living:** relative purchasing power in each place (grouped bar chart)
3. **Lifestyle / daily cost comparison:** a basket of everyday costs including rent, food, and transport (stacked bar chart)

**Analysis:** compare the gap between income and essential costs in each location, as a percentage and in PPP dollars, and check whether it holds across all 5 years.

## 5. Interpreting the Results

- **Supports the hypothesis:** California has higher costs but leaves *more* PPP-adjusted disposable income at the end of the month, so moving to California would be the rational choice.
- **Neutral result:** higher income in California is roughly cancelled out by higher costs, so disposable income is similar in both places and location doesn't matter financially.
- **Contradicts the hypothesis:** La Paz leaves more PPP-adjusted disposable income, meaning it is cheaper in both absolute and relative terms.
