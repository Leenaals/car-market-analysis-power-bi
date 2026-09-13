# Car Market Analysis Dashboard

An interactive **Power BI** dashboard analyzing the automotive market — combining vehicle specifications and used-car auction pricing data to help users compare brands, examine prices, and identify the factors that affect a car's value.

This project supports **Sustainable Development Goal 9: Industry, Innovation and Infrastructure**, by using data analytics and interactive visualization to support smarter, data-driven market analysis in the automotive industry.

## Overview

Understanding car prices is difficult because many factors — brand, model, year, mileage, condition — influence value, and raw data is often messy and inconsistent. This project turns two raw Kaggle datasets into a clean, connected data model and an interactive Power BI dashboard that surfaces pricing patterns, performance metrics, and market trends across manufacturers.

## Data

- **Car Prices** (fact table) — 558,837 records, 17 features (year, condition, selling price, state, seller, transmission type, etc.) — [Used Car Auction Prices, Kaggle](https://www.kaggle.com/datasets/tunguz/used-car-auction-prices?select=car_prices.csv)
- **Car Specifications** (dimension table) — 1,500 records, 13 features (model, seating capacity, rating, max power, fuel tank capacity, etc.) — [Cars 2022 Dataset, Kaggle](https://www.kaggle.com/datasets/tr1gg3rtrash/cars-2022-dataset)

## Data Preparation

Both tables were cleaned prior to modeling:

- Missing values in critical columns (`make`, `model`) were dropped; other missing categorical values were imputed with the mode, and missing numeric values with the median.
- Unnecessary columns (e.g. `Unnamed`, `saledate`) were removed.
- Text columns were standardized (lowercased, whitespace trimmed) for consistency.
- Numeric columns were cast to the correct type.
- Outliers (e.g. in `sellingprice`) were detected and removed using the **IQR method**.
- A dedicated `Car_Key` field was engineered to link the two tables — the original key contained duplicates, which initially caused many-to-many relationship issues in the data model.

## Data Model

Three connected tables built around a unique `Car_Key`:

- **car_prices_BI** — fact table with transactional/market data (pricing, condition, odometer, state, seller, transmission).
- **car_Specifications_BI** — dimension table with technical specs (horsepower, RPM, torque, fuel tank capacity, rating).
- A supporting lookup table with unique `Car_Key` values, added to resolve the many-to-many relationship issue.

## Dashboard Features

- **Filters & Slicers** — dynamic filtering by car make and body type.
- **KPI Cards** — min/max selling price, max horsepower (BHP), engine speed at max power (RPM).
- **Charts & Visuals** — clustered column charts (average mileage, rating, horsepower by make) and a donut chart (brand distribution).
- **Map Visualization** — car distribution by state.
- **Data Modeling** — relationships across the three tables for accurate cross-filtering.

Two dashboard pages: *Pricing and Market Distribution* and *Specifications and Performance*.

## Key Insights

- Brands like BMW, Nissan, and Infiniti show higher average horsepower than others.
- Customer ratings are relatively high and similar across most manufacturers.
- Mileage vs. price shows varied patterns — some brands sustain higher prices despite higher mileage.
- Ford, Chevrolet, and Nissan represent the largest share of the dataset by volume.

## Repository Structure

```
├── Power_BI project.pbix          # Power BI dashboard file
├── project BI_Report.docx         # Full written report (data prep, model, dashboard, findings)
├── BI Presentation.pptx           # Slide deck presentation
├── car_prices_BI.csv              # Cleaned car prices dataset
├── Car_Specifications_BI.csv      # Cleaned car specifications dataset
└── README.md
```

## How to Open

1. Install [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (Windows only).
2. Open `Power_BI project.pbix`.
3. If prompted to refresh data sources, point Power BI to `car_prices_BI.csv` and `Car_Specifications_BI.csv` in this repo.

## Limitations

- Some brands have limited record counts, which may affect comparison accuracy.
- The datasets lack features like fuel efficiency, accident history, and maintenance records.
- Analysis quality depends entirely on the completeness of the source datasets.

## Future Work

- Integrate additional datasets (fuel efficiency, maintenance history, accident records, customer reviews).
- Apply predictive analytics / machine learning to forecast car prices and market trends.
- Add real-time data updates and more advanced filtering.

## About This Project

This is a **group project for the DS322 (Business Intelligence) course**.

## References

- United Nations, "Goal 9: Industry, Innovation and Infrastructure," Sustainable Development Goals, 2023. [Online]. Available: https://sdgs.un.org/goals/goal9
- B. Tunguz, "Used Car Auction Prices Dataset," Kaggle, 2022.
- T. Tr1gg3rtrash, "Cars 2022 Dataset," Kaggle, 2022.
