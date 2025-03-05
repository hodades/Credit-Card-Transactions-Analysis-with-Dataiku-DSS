# Credit Card Transactions Analysis with Dataiku DSS
![image](https://github.com/user-attachments/assets/6a3f49d9-1b6b-47cd-80bd-435802aaaafb)


## Project Overview
This project focuses on **analyzing credit card transactions** using **Dataiku DSS**. The workflow includes **data integration, enrichment, and preparation** to build a structured dataset for analysis and modeling.

## Workflow Summary

### 1. Stacking Transactions
- Merged `transactions_2021` and `transactions_2022` into a single dataset using a **Stack recipe**.
- Output dataset: `transactions_stacked`.

### 2. Data Enrichment
- **Joined transactions with cardholder data** (`cardholder_info`) using `card_id = internal_card_mapping`.
- **Joined transactions with merchant data** (`merchant_info`) using `merchant_id = merchant_id`.
- Output dataset: `transactions_stacked_joined`.

### 3. Data Preparation
Using a **Prepare recipe**, the following transformations were applied:
- **Filtering**: Removed invalid rows where `signature_provided` contained errors.
- **Geolocation Processing**:
  - Created **geopoints** from merchant and cardholder latitude/longitude.
  - Applied **reverse geocoding** to extract state-level location details.
- **Categorization**:
  - Created `spending_type` based on `merchant_subsector_description`.
  - Categories include `essential`, `discretionary`, and `standard`.
- **Date Processing**:
  - Parsed `first_active_month`.
  - Computed the time difference between `purchase_date` and `first_active_month`.
- Output dataset: `transactions_stacked_joined_prepared`.
