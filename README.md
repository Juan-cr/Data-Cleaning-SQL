# Data Cleaning Project: Nashville Housing Dataset (SQL)

##  Overview
This project focuses on cleaning and transforming a raw housing dataset using SQL.  
The goal is to improve data quality, consistency, and usability for further analysis.

The dataset contains property sales data with issues such as missing values, inconsistent formatting, and duplicate records.

---

##  Business Context

Real estate datasets are often messy and inconsistent, which makes accurate analysis difficult.  
This project simulates a real-world scenario where a data analyst must prepare housing data for:

- Market trend analysis
- Property valuation
- Investment decision-making
- Reporting and dashboarding

By cleaning and structuring the dataset, the data becomes reliable and ready for business insights, enabling stakeholders to make data-driven decisions.

---

##  Tools Used
- SQL Server
- T-SQL

---

##  Dataset
- Table: `NashvilleHousing`
- Database: `ProjectPortfolio`

---

##  Data Cleaning Steps

### 1. Standardizing Date Format
- Converted `SaleDate` from datetime to date format using `CONVERT`.

---

### 2. Handling Missing Property Address
- Identified missing `PropertyAddress` values.
- Used a self-join on `ParcelID` to populate null values from matching records.

---

### 3. Splitting Address Columns
#### Property Address:
- Extracted:
  - `PropertySplitAddress`
  - `PropertySplitCity`

#### Owner Address:
- Used `PARSENAME` with `REPLACE` to extract:
  - `OwnerSplitAddress`
  - `OwnerSplitCity`
  - `OwnerSplitState`

---

### 4. Standardizing Categorical Values
- Converted `SoldAsVacant` values:
  - `'Y' → 'Yes'`
  - `'N' → 'No'`

---

### 5. Removing Duplicates
- Used a CTE with `ROW_NUMBER()` to identify duplicate records based on:
  - ParcelID
  - PropertyAddress
  - SalePrice
  - SaleDate
  - LegalReference

---

### 6. Dropping Unused Columns
Removed unnecessary columns:
- `PropertyAddress`
- `OwnerAddress`
- `TaxDistrict`

---

##  Key Skills Demonstrated
- Data Cleaning & Transformation
- SQL Joins
- Common Table Expressions (CTEs)
- Window Functions (`ROW_NUMBER`)
- String Functions (`SUBSTRING`, `PARSENAME`, `REPLACE`)
- Data Standardization

---

##  Data Cleaning Impact (Metrics)

- Total records analyzed: **56,477**

- Missing Property Addresses:
  - Before: **29 null values**
  - After: **0 (populated using self-join)**

- Duplicate Records Identified:
  - **103 duplicate rows** based on key fields
  - (ParcelID, PropertyAddress, SalePrice, SaleDate, LegalReference)

- SoldAsVacant Standardization:
  - Standardized **451 records** (`Y` and `N` → `Yes` and `No`)

- Address Columns Created:
  - Added **5 new structured columns**:
    - PropertySplitAddress
    - PropertySplitCity
    - OwnerSplitAddress
    - OwnerSplitCity
    - OwnerSplitState

- Columns Removed:
  - Dropped **3 unused columns** to improve dataset usability

---

##  Future Improvements
- Create a cleaned dataset version instead of modifying raw data
- Add data validation checks
- Build dashboards using Power BI or Tableau
- Perform exploratory data analysis (EDA)

---

## How to Use
1. Import the dataset into SQL Server
2. Run the SQL script step by step
3. Verify transformations using SELECT statements

---

## Basic Data Analysis (After Cleaning)

After cleaning the dataset, a few quick insights can be observed:

- The majority of properties are marked as **"Not Sold as Vacant"**, indicating most transactions involve occupied or developed properties.

- A small portion of records required standardization (`Y/N → Yes/No`), highlighting inconsistencies in categorical data entry.

- Duplicate records (103 rows) suggest potential issues in data collection or system merging.

- Address splitting enables:
  - Geographic analysis by city/state
  - More efficient filtering and grouping in future analysis
 
-- Now We can Analize
-- Top cities by average sale price

SELECT PropertySplitCity, AVG(SalePrice) as AvgPrice
FROM ProjectPortfolio.dbo.NashvilleHousing
GROUP BY PropertySplitCity
ORDER BY AvgPrice DESC;

---

###  Analyze average sale price by city:
- Now We can Analize
- Top cities by average sale price
<img width="587" height="601" alt="image" src="https://github.com/user-attachments/assets/ea7cc77e-e276-483d-89a4-a7d27c37c550" />

###  Potential Next Steps:
- Identify trends over time using SaleDate
- Compare property value vs sale price
- Build a dashboard for real estate insights

---

##  Author
Juan Carlos  
Data Analyst | SQL | Data Cleaning | Data Visualization
