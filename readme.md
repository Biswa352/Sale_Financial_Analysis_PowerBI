# Credit Risk Dashboard — Power BI

## Author
**Biswarup Das**

## Project Overview

This project uses Microsoft Power BI to explore customer financial profiles and associated card records. The report combines customer-level attributes—such as credit score, income, debt, age and gender—with card-level attributes including brand, type, chip status and credit limit.

The dashboard is designed for **descriptive financial-health and card-portfolio analysis**. It is not a predictive credit-scoring model and does not estimate default probability or detect fraudulent transactions.

## Project Objectives

- Summarize customers' credit scores, debt and income.
- Compare average debt across gender groups and show the customer distribution by gender.
- Examine card-brand composition, chip prevalence and average recorded credit limits by card type.
- Explore customer credit scores against total debt and summarize card-record counts across credit-score bands.
- Provide interactive filtering by gender, chip status and card brand.

## Tools and Technologies

- **Microsoft Power BI Desktop** — report development and visual analytics
- **DAX** — measures and calculated categories
- **CSV** — source tables for customer and card data

## Data and Model

| File | Records | Columns | Description |
|---|---:|---:|---|
| `users_data.csv` | 2,000 | 14 | Customer profile, age, gender, location fields, income, debt, credit score and reported card count |
| `cards_data.csv` | 6,146 | 13 | Card identifier and client key, brand, type, chip status, credit limit, issue-count field, account dates and dark-web indicator |

The model uses a **one-to-many relationship** from `users_data[id]` to `cards_data[client_id]`, with single-direction filtering. The provided CSVs contain no blank cells in the fields examined, all 2,000 customer IDs appear in the card table, and no unmatched card client IDs were found.

## Dashboard Pages

### 1. Customer Financial Health Overview

- KPI cards for average credit score, average total debt and average yearly income
- Average total debt by gender
- Customer count by gender
- Average credit score by birth year
- Average credit score by credit-limit band

### 2. Card Risk Analysis

- Dark-web card count and overall percentage with a chip
- Percentage of cards with a chip by brand
- Average recorded credit limit by card type
- Card-brand composition chart

### 3. Client Credit Risk Dashboard

- Scatter plot of credit score against total debt, identified by customer ID
- Table combining selected customer and card attributes
- Card-record counts by customer credit-score band
- Slicers for gender, chip status and card brand

## Selected Findings

- The average customer credit score is **709.73**; scores range from **480 to 850**.
- Average total debt is approximately **$63.71K**, and average yearly income is approximately **$45.72K** in the dollar-denominated fields supplied.
- Average total debt is approximately **$64.11K for male customers** and **$63.32K for female customers**.
- **89.49%** of card records have `has_chip = YES`.
- Mastercard represents **52.21%** of card records and Visa **37.85%**. These percentages describe record share in the current visual, not the sum of `num_cards_issued`.
- The `card_on_dark_web` field is `No` for all **6,146** card records, so the current dataset does not provide positive examples of dark-web exposure.

More detailed calculations, caveats and interpretation notes are in [`Credit Risk Analysis Insights.txt`](Credit%20Risk%20Analysis%20Insights.txt).

## Dashboard Screenshots

**Customer Financial Health Overview**

![Customer Financial Health Overview](Customer%20Financial%20Health%20Overview.png)

Additional pages: [Card Risk Analysis](Card%20Risk%20Analysis.png) · [Client Credit Risk Dashboard](Client%20Credit%20Risk%20Dashboard.png)

## Repository Files

- `Sales_Financial.pbix` — Power BI report
- `users_data.csv` — customer-level source data
- `cards_data.csv` — card-level source data
- `Customer Financial Health Overview.png` — Page 1 screenshot
- `Card Risk Analysis.png` — Page 2 screenshot
- `Client Credit Risk Dashboard.png` — Page 3 screenshot
- `Credit-Risk-Dashboard .pptx` — accompanying presentation (current filename includes a space before `.pptx`)
- `Credit Risk Analysis Insights.txt` — findings and interpretation notes
- `LICENSE` — repository license

## How to View the Report

1. Download `Sales_Financial.pbix` and the two CSV files from this repository.
2. Open the PBIX file in Power BI Desktop.
3. If Power BI requests updated data-source paths, point the queries to the downloaded CSV files.
4. Use the tabs at the bottom of the report to navigate between the three pages. On Page 3, test the gender, chip-status and card-brand slicers.

## Interpretation and Data Notes

- The score threshold of **below 600**, when used for a simple segment, is a descriptive rule for this project—not an official lending standard or a validated risk model.
- The Page 1 chart *Average Credit Score by Credit Limit Band* currently displays the same rounded average (about 710) across all four bands. Given the model's single-direction relationship from customers to cards, the card-level band may not be filtering the customer-level score measure as intended. That chart is therefore **not used as evidence of differences between credit-limit bands**.
- The card-brand pie visual's current `Count of num_cards_issued` aggregation shows each brand's share of card records. If the intended measure is the number of cards issued, the aggregation and title should be aligned.
- The card table includes card-number and CVV fields, while the customer table contains address and coordinates. Confirm the dataset's provenance, synthetic status and redistribution terms before publishing; remove or mask fields that are not necessary for the analysis.

## License and Data Provenance

The repository includes a `LICENSE` file. The supplied files do not identify the original dataset source or establish separate redistribution rights for the CSV data. Confirm the source attribution and dataset terms before sharing or redistributing the source tables publicly.

## Contact

**Biswarup Das** — connect via GitHub for feedback or collaboration.
