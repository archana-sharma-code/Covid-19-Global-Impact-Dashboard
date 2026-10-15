# COVID-19 Global Impact Dashboard

A comprehensive data analysis project examining the global impact of COVID-19, with a focus on the relationship between vaccination rollout speed and mortality outcomes. This project demonstrates the full analytics pipeline from data cleaning to visualization and insight generation.

![COVID-19 Analysis](https://img.shields.io/badge/COVID--19-Data_Analysis-blue)
![Python](https://img.shields.io/badge/Python-3.8+-green)
![License](https://img.shields.io/badge/License-MIT-yellow)

## 📋 Project Overview

This internship project analyzes publicly available COVID-19 datasets from Our World in Data to uncover trends and build an interactive dashboard. The analysis covers cases, deaths, and vaccinations by country and date, with a focus on understanding whether vaccination rollout speed correlated with lower death rates.

### Key Features

- **Data Cleaning:** Handling missing values, filtering aggregates, and validating data quality
- **Metric Derivation:** 7-day rolling averages, case fatality rate, vaccination rate, doubling time
- **Exploratory Analysis:** Time-series trends, comparative analysis, correlation studies
- **Interactive Visualizations:** Charts and graphs using Matplotlib and Seaborn
- **Key Insights:** 5 major findings with data-driven conclusions

## 🎯 Project Objectives

- Practice the full analytics pipeline
- Clean and preprocess large-scale public health datasets
- Derive meaningful metrics from raw data
- Communicate findings visually through charts and dashboards
- Document assumptions and limitations transparently

## 🛠️ Tools & Technologies

- **Python 3.8+**
- **Pandas:** Data manipulation and analysis
- **NumPy:** Numerical computing
- **Matplotlib:** Data visualization
- **Seaborn:** Statistical data visualization
- **Jupyter Notebook:** Interactive analysis environment

## 📁 Project Structure

```
.
├── data/
│   ├── owid-covid-data.csv          # Original dataset from Our World in Data (98MB)
│   ├── covid_data_cleaned.csv      # Cleaned dataset with derived metrics
│   └── DATA_DOCUMENTATION.md        # Detailed data documentation
├── notebooks/
│   └── covid_analysis 1.ipynb       # Main analysis notebook
├── outputs/
│   ├── global_timeline.png          # Global cases and deaths timeline
│   ├── case_fatality_rate.png       # CFR comparison by country
│   ├── vaccination_vs_death_rate.png # Vaccination vs death rate correlation
│   ├── vaccination_timeline.png     # Vaccination rollout timeline
│   └── regional_distribution.png    # Regional impact distribution
├── scripts/
│   └── generate_pdf.py              # Script to generate PDF from Markdown
├── executive_summary.md             # 1-page executive summary (Markdown)
├── executive_summary.pdf            # 1-page executive summary (PDF)
├── requirements.txt                 # Python dependencies
├── .gitignore                       # Git ignore file
└── README.md                        # This file
```

## 🚀 Installation

### Prerequisites

- Python 3.8 or higher
- pip (Python package manager)

### Setup Instructions

1. **Clone the repository:**
   ```bash
   git clone <repository-url>
   cd <repository-directory>
   ```

2. **Create a virtual environment (recommended):**
   ```bash
   python -m venv venv
   
   # On Windows:
   venv\Scripts\activate
   
   # On macOS/Linux:
   source venv/bin/activate
   ```

3. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Download the dataset:**
   The dataset is already included in the `data/` directory. If you need to download it fresh:
   ```bash
   curl -o data/owid-covid-data.csv https://raw.githubusercontent.com/owid/covid-19-data/master/public/data/owid-covid-data.csv
   ```

## 📊 Usage

### Running the Analysis

1. **Start Jupyter Notebook:**
   ```bash
   jupyter notebook
   ```

2. **Open the analysis notebook:**
   Navigate to `notebooks/covid_analysis 1.ipynb` and open it

3. **Run the cells:**
   Execute the notebook cells sequentially (Kernel → Restart & Run All)

### Generating Visualizations

The notebook automatically generates the following visualizations in the `outputs/` directory:

- **global_timeline.png:** Global daily new cases and deaths (7-day rolling average)
- **case_fatality_rate.png:** Case fatality rate comparison by country
- **vaccination_vs_death_rate.png:** Correlation between vaccination rate and death rate
- **vaccination_timeline.png:** Vaccination rollout timeline for major countries
- **regional_distribution.png:** Regional distribution of cases and deaths

### Generating PDF Executive Summary

The notebook includes code to generate the PDF. After running the notebook, the PDF will be saved as `executive_summary.pdf` in the project root.

Alternatively, if you have a custom PDF generation script, run it according to its instructions.

## 📈 Key Insights

### 1. Deaths per Reported Case Fell Sharply
Global deaths peaked at 14,811/day (2021-01-24); cases peaked at 3.36 million/day during Omicron (2022-01-23). Deaths per 1,000 reported cases fell from 24.5 to 2.5 between the two peaks. This is consistent with vaccination, prior infection, and a milder variant, but testing and reporting also changed.

### 2. Reporting Artifacts Impact Data
The highest 7-day case value (6.3 million/day, Dec 2022) is not a global surge: China accounts for 86% of cases reported in that window, indicating a one-country reporting effect; China is also the largest contributor to the Feb 2023 death spike.

### 3. Case Fatality Rates Vary Widely
Among 129 countries with over 100K cases, CFR ranges from 0.05% (Brunei) to 4.88% (Peru). Lowest: Brunei, Singapore, Iceland, South Korea, China. Highest: Peru, Egypt, Mexico, Bosnia and Herzegovina, Afghanistan. CFR reflects how many cases were detected, not only how deadly the disease was.

### 4. Vaccination Rollout Speed Differs Significantly
87 countries (over 1M people) reached 50% fully vaccinated, from 97 days after the first dose (Israel) to 766 (Sierra Leone); median 257. Major countries: UK 176, Germany 211, US 221, France 223, Brazil 277, India 380 days.

### 5. Regional Impact Was Uneven
Asia reported 38.9% of cases and Europe 32.6%. Deaths per million: South America 3,104, Europe 2,815, North America 2,784, Oceania 731, Asia 347, Africa 182. Low figures in Asia and Africa likely partly reflect limited testing and reporting.

### 6. Early Spread Was Fast
The median doubling time of cumulative cases across countries was 9.6 days in March-April 2020.

### 7. No Detectable Vaccination Speed-Death Correlation
Across 57 countries (over 1M people and 1M cases) we found no statistically detectable relationship: Spearman correlation between days to 50% fully vaccinated and deaths per million = -0.17 (p = 0.20); +0.07 after controlling for median age (p = 0.62). This does not show vaccines were ineffective: cumulative deaths depend heavily on age structure, reporting quality and timing.

For detailed analysis, see the [Executive Summary](executive_summary.md).

## 📝 Data Source

**Dataset:** Our World in Data COVID-19 Dataset  
**URL:** https://github.com/owid/covid-19-data  
**Last Updated:** August 19, 2024 (dataset archived)  
**Size:** ~98MB  
**Coverage:** 200+ countries, January 2020 - August 2024

### Data Columns

The dataset includes the following key columns:
- `location`: Country/region name
- `date`: Date of observation
- `total_cases`: Cumulative confirmed cases
- `total_deaths`: Cumulative confirmed deaths
- `total_vaccinations`: Cumulative vaccinations administered
- `people_fully_vaccinated`: Number of people fully vaccinated
- `population`: Country population
- And 60+ additional indicators

## 🔬 Methodology

### Data Cleaning
- Removed continent aggregates (kept only countries)
- Converted date columns to datetime format
- Handled missing values appropriately
- Validated data quality (negative values, zero population, etc.)

### Metric Derivation
- **Case Fatality Rate:** `total_deaths / total_cases * 100` (percentage)
- **Vaccination Rate:** `people_fully_vaccinated / population * 100` (percentage)
- **7-day Rolling Average:** Moving average of new cases and deaths
- **Doubling Time:** Calculated from 7-day growth rates using cumulative cases
- **Days to 50% Vaccination:** Days from first recorded vaccination to reaching 50% population fully vaccinated

### Analysis Approach
- Time-series analysis of global trends
- Comparative analysis across countries and regions
- Spearman correlation analysis (days to 50% vaccination vs deaths per million) with median-age control
- Focus on countries with >1M people and >1M cases for statistical significance
- Forward-filled cumulative columns within each country to handle missing data

## ⚠️ Limitations

1. **Underreporting:** Many regions likely underreported cases and deaths
2. **Testing Variability:** Different testing strategies affect case detection
3. **Data Completeness:** Some countries had incomplete data
4. **Time Lags:** Reporting delays affect real-time accuracy
5. **Causality:** Country-level correlation is not causation
6. **Reporting Artifacts:** One-country batch reporting creates spikes (e.g., China in Dec 2022)
7. **Rollout Start Definition:** Based on first dose record in the data, which may not match actual campaign start

For a complete list of assumptions and limitations, see the analysis notebook and executive summary.

## 📦 Deliverables

- ✅ Cleaned dataset with documented assumptions (`data/covid_data_cleaned.csv`)
- ✅ Detailed data documentation (`data/DATA_DOCUMENTATION.md`)
- ✅ 3-5 key insights with data-driven conclusions
- ✅ Interactive Jupyter notebook with visualizations (`notebooks/covid_analysis.ipynb`)
- ✅ 1-page executive summary in Markdown (`outputs/executive_summary.md`)
- ✅ 1-page executive summary in PDF (`outputs/executive_summary.pdf`)
- ✅ 5 data visualizations (PNG format)
- ✅ Comprehensive README with setup instructions


## 🎓 Learning Outcomes

This project demonstrates:
- **Data Cleaning:** Handling real-world data quality issues
- **Feature Engineering:** Creating meaningful metrics from raw data
- **Exploratory Data Analysis:** Uncovering patterns and trends
- **Data Visualization:** Communicating findings effectively
- **Statistical Analysis:** Correlation and comparative studies
- **Documentation:** Transparent reporting of methods and limitations


## 📊 Project Statistics

- **Total Countries Analyzed:** 200+
- **Time Period:** January 2020 - August 2024
- **Data Points:** ~400,000 rows
- **Key Metrics Derived:** 4
- **Visualizations Generated:** 5
- **Key Insights Identified:** 5

---

