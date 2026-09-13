# Cesarean Section Rates in Poland (2010-2025)

This is a data analysis project I made while learning data analysis. I wanted to check how the cesarean section (C-section) rate changed in Poland over the last 15 years, if it's different between regions, and if hospital size has anything to do with it.

## Data

- Source: NFZ (Polish National Health Fund), public statistics - "Porody i opieka okołoporodowa 2010-2025" (births and perinatal care)
- About 70 000 rows - one row per hospital, per month, per year, from 2010 to 2025
- Columns: hospital id/name/address, province, year, month, total births, cesarean births, instrumental births, vaginal births (with/without episiotomy, with/without anesthesia)

The raw csv is in `data/`. It has a messy header (extra title rows) and extra spaces in the numbers, both handled in the notebook.

## What's in the notebook

1. Load and clean the data, rename the Polish columns to shorter English names
2. Check data quality (missing values, do the numbers add up)
3. National C-section rate trend, 2010-2025
4. Quick check for seasonality (births by year/month)
5. Differences between provinces
6. Hospitals with highest/lowest C-section rate (with a minimum births filter, so small hospitals with weird % don't mess things up)
7. Does hospital size matter for the rate?
8. Simple linear regression on the yearly trend, with a next-year prediction

## What I found

- National C-section rate went from about **34%** in 2010 to almost **48%** in 2025 (roughly +0.9 percentage points every year, R² = 0.89)
- Big gap between provinces: **Podkarpackie** (~51%) vs **Pomorskie** (~32%)
- Hospital size (average births per year) is **basically not correlated** with the C-section rate (correlation ~0.07) - I expected bigger hospitals to have a higher rate, but that's not really what the data shows
- A simple linear trend model fits the yearly data pretty well (R² = 0.89), and if the trend continued the same way next year could land around ~51% - I'm treating this as "how fast has it been growing", not a real forecast

## Tools used

Python, pandas, matplotlib, seaborn, scikit-learn (one simple LinearRegression model), Jupyter Notebook.

## How to run it

```bash
pip install -r requirements.txt
jupyter notebook notebooks/cesarean_analysis.ipynb
```

## Project structure

```
├── data/
│   └── porody_2010_2025.csv       # raw data (NFZ)
├── notebooks/
│   └── cesarean_analysis.ipynb    # the analysis
├── requirements.txt
└── README.md
```

## Ideas for later

- Use the KOC column (coordinated perinatal care) and check if those hospitals have a different rate
- Try predicting a hospital's C-section rate from a few features (region, size, year) instead of just looking at the national trend
- Compare with C-section rates in other EU countries, if I can find public data for that

---
Data source: NFZ (Polish National Health Fund), public statistics. This is a learning/portfolio project, not medical advice or a medical conclusion.
