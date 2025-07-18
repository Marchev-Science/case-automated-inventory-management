# Project Brief: Demand Forecasting for Optimized Inventory Planning

## Objective

Develop a machine learning model to forecast the 14-day demand for each product listed in `items.csv`, starting from **June 30, 2018**, using real anonymized retail data. The goal is to **maximize the monetary value** for a retailer by accurately predicting sales while avoiding overstocking.

## Data Sources

You are provided with three structured CSV files:

1. **`items.csv`** – Master data with descriptive features for each item (categorical/numerical).  
2. **`orders.csv`** – Detailed historical transactions over 6 months, including timestamps (not pre-aggregated).  
3. **`infos.csv`** – Item prices and promotion dates for the simulation (forecast) period.

> **Note:** Column details and value ranges are available in the accompanying `features.pdf` document. Fields are separated by `|`.

## Task Requirements

- **Aggregate** historical demand per item (e.g., daily or weekly) from `orders.csv`.  
- **Create features** from all three files (`items.csv`, `orders.csv`, `infos.csv`).  
- **Build** a machine learning model to predict total demand for each item for the 14-day period starting June 30, 2018.  
- **Incorporate promotions** (explicitly flagged in `infos.csv`) into your model.  
- **Assume prices are fixed** during the forecast period (no need to model price effects).

## Output File Format

Submit predictions in a CSV file with the following structure:

```text
itemID|demandPrediction
995539|34
1000002|42
995554|10
````

* `itemID`: string – unique identifier (as in `items.csv`)
* `demandPrediction`: integer – total forecasted demand for the 14 days
* **Separator**: `|`
* **Filename**: `<TeamName>.csv` (e.g., `TU_Chemnitz_1.csv`)

## Evaluation Metric

Submissions will be evaluated based on their **monetary value** to the retailer:

* If **forecast ≤ actual demand**:

  ```
  Value = price × forecasted_demand
  ```
* If **forecast > actual demand**:

  ```
  Value = price × actual_demand 
        – 0.6 × price × (forecast – actual)
  ```

The goal is to maximize total monetary value over all items by balancing revenue and overstock penalties.

## Additional Requirement

Propose a model or approach in which the retailer can explicitly define the following constraints:

* **Maximum acceptable overstock** (waste).
* **Maximum acceptable lost sales** (missed revenue opportunities).
* **Maximum acceptable locked capital in inventory**, assuming a 30% markup over the product’s purchase cost.

