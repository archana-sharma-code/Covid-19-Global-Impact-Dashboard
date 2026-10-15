# Data Documentation

## Original Dataset

**Source:** Our World in Data COVID-19 Dataset  
**URL:** https://github.com/owid/covid-19-data  
**Download Date:** October 14, 2026  
**File:** `owid-covid-data.csv`  
**Size:** 98.4 MB  
**Rows:** ~400,000  
**Columns:** 67  

### Data Coverage

- **Time Period:** January 22, 2020 - August 19, 2024
- **Geographic Coverage:** 200+ countries and territories
- **Update Frequency:** Daily (until archive in August 2024)

### Key Columns

| Column Name | Description | Data Type |
|-------------|-------------|-----------|
| iso_code | ISO 3166-1 alpha-3 country code | String |
| continent | Continent name | String |
| location | Country/territory name | String |
| date | Date of observation | Date |
| total_cases | Cumulative confirmed cases | Numeric |
| new_cases | New confirmed cases | Numeric |
| total_deaths | Cumulative confirmed deaths | Numeric |
| new_deaths | New confirmed deaths | Numeric |
| total_vaccinations | Cumulative vaccinations administered | Numeric |
| people_vaccinated | Number of people who received at least one dose | Numeric |
| people_fully_vaccinated | Number of people fully vaccinated | Numeric |
| population | Country population | Numeric |
| reproduction_rate | Estimated reproduction rate (R) | Numeric |

## Cleaned Dataset

**File:** `covid_data_cleaned.csv`  
**Derived Columns:** 4  

### Cleaning Process

1. **Date Conversion**
   - Converted `date` column from string to datetime format
   - Format: YYYY-MM-DD

2. **Filtering**
   - Removed continent aggregates (rows where `continent` is null)
   - Kept only country-level data
   - Result: Reduced from ~400,000 to ~380,000 rows

3. **Missing Value Handling**
   - No imputation performed for key metrics
   - Missing values preserved as NaN for transparency
   - Derived metrics only calculated when sufficient data available

4. **Data Quality Checks**
   - Checked for negative values in `new_cases` and `new_deaths`
   - Verified no zero or negative population values
   - Identified data quality issues but did not remove data

### Derived Metrics

#### 1. Case Fatality Rate (CFR)
```
CFR = total_deaths / total_cases
```
- **Units:** Percentage (0-100)
- **Calculation:** Per row, per country
- **Assumptions:** 
  - All cases and deaths are reported accurately
  - Total deaths and cases are from the same population
- **Limitations:** 
  - Underreporting of cases and deaths affects accuracy
  - Different testing strategies across countries
  - Time lag between case confirmation and death

#### 2. Vaccination Rate
```
Vaccination Rate = (people_fully_vaccinated / population) * 100
```
- **Units:** Percentage (0-100)
- **Calculation:** Per row, per country
- **Assumptions:**
  - Population estimates are accurate
  - Vaccination data reflects actual coverage
- **Limitations:**
  - Reporting delays in vaccination data
  - Different definitions of "fully vaccinated" over time
  - Booster doses not included in this metric

#### 3. 7-Day Rolling Average (New Cases)
```
new_cases_7day_avg = rolling_mean(new_cases, window=7)
```
- **Units:** Cases per day
- **Calculation:** Per country, sorted by date
- **Purpose:** Smooth daily fluctuations
- **Method:** Pandas rolling mean with min_periods=1

#### 4. 7-Day Rolling Average (New Deaths)
```
new_deaths_7day_avg = rolling_mean(new_deaths, window=7)
```
- **Units:** Deaths per day
- **Calculation:** Per country, sorted by date
- **Purpose:** Smooth daily fluctuations
- **Method:** Pandas rolling mean with min_periods=1

#### 5. Doubling Time
```
Doubling Time = ln(2) / growth_rate
growth_rate = (new_cases_7day_avg[t] - new_cases_7day_avg[t-7]) / new_cases_7day_avg[t-7]
```
- **Units:** Days
- **Calculation:** Per country, based on 7-day growth rates
- **Purpose:** Estimate how fast cases are doubling
- **Limitations:**
  - Based on 7-day window, may not capture rapid changes
  - Returns infinity when growth rate is zero or negative
  - Sensitive to reporting fluctuations

## Data Quality Issues

### Known Issues

1. **Negative Values**
   - Some rows have negative `new_cases` or `new_deaths`
   - Likely due to data corrections or reclassification
   - Not removed to preserve data integrity

2. **Missing Data**
   - Vaccination data missing for early pandemic period (before vaccines available)
   - Some countries have incomplete demographic data
   - Testing data sparsely reported

3. **Reporting Delays**
   - Some countries reported with significant delays
   - Weekend effects in reporting
   - Backfilling of historical data

4. **Inconsistent Definitions**
   - "Confirmed cases" definition varied by country
   - "Fully vaccinated" definition changed over time
   - Death attribution criteria varied

## Assumptions

### General Assumptions

1. **Reporting Consistency**
   - Countries reported data consistently throughout the period
   - No systematic bias in reporting over time

2. **Data Accuracy**
   - Population estimates are reasonably accurate
   - Vaccination numbers reflect actual doses administered
   - Case and death counts are not manipulated

3. **Representativeness**
   - Sample countries represent global patterns
   - Countries with >1M cases provide statistically significant samples

### Analysis-Specific Assumptions

1. **Correlation Analysis**
   - Assumes linear relationship between vaccination rate and death rate
   - Assumes other factors (healthcare quality, demographics) are either:
     - Controlled for, or
     - Acknowledged as confounding variables

2. **Rolling Averages**
   - 7-day window sufficiently smooths noise while preserving trends
   - No significant seasonal patterns within 7-day window

3. **Regional Analysis**
   - Continent groupings are meaningful for comparison
   - Sufficient within-continent homogeneity for analysis

## Limitations

### Data Limitations

1. **Underreporting**
   - Many countries underreported cases, especially early in pandemic
   - Death reporting varies significantly by country
   - Asymptomatic cases often not captured

2. **Testing Variability**
   - Different testing strategies affect case detection
   - Testing capacity varied over time and by country
   - Positive rate not consistently reported

3. **Temporal Lag**
   - Reporting delays of days to weeks
   - Some data backfilled retroactively
   - Real-time analysis affected by these lags

### Analysis Limitations

1. **Correlation vs Causation**
   - Correlation between vaccination and death rates does not prove causation
   - Confounding variables not fully controlled
   - Ecological fallacy risk (country-level vs individual-level)

2. **Metric Limitations**
   - CFR does not account for age structure
   - Vaccination rate doesn't measure effectiveness over time
   - Doubling time sensitive to reporting fluctuations

3. **Generalizability**
   - Patterns may not apply to future pandemics
   - COVID-19-specific characteristics may limit generalization
   - Healthcare system evolution over time

## Data Sources and Citations

### Primary Source

- **Our World in Data COVID-19 Dataset**
  - URL: https://github.com/owid/covid-19-data
  - Citation: Hasell, J., Mathieu, E., Beltekian, D. et al. A cross-country database of COVID-19 testing. Sci Data 7, 390 (2020). https://doi.org/10.1038/s41597-020-00688-8

### Secondary Sources

- **World Health Organization (WHO)**
  - COVID-19 situation reports
  - Vaccination data

- **National Health Ministries**
  - Country-specific reporting
  - Official statistics




