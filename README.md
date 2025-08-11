
# Data Analysis Workflow – Plant Growth Experiments

## 1. Collect Data
- **Data Collection Sheet** (paper or digital):
  - Prepare a clearly labeled template for each measurement day.
  - Include metadata columns: `Date`, `Time`, `Location`, `Treatment`, `Plant_ID`, `Observer`.
  - Use standard units (e.g., cm for height, g for biomass).
  - Example columns:
    ```
    Date | Plant_variety | Treatment | Height| No_flowers | Fruit_weight | Soil_water_% | Soil_EC
    ```
- **Best Practices**:
  - Use consistent naming conventions for treatments and plant IDs.
  - Record data immediately to reduce transcription errors.
  - Calibrate instruments before taking measurements.


## 2. Organise Data
- Enter data into Excel in a **tidy format**:
  - One row per observation.
  - One column per variable.
  - Avoid merged cells or multiple header rows.
- **Advantages**:
  - Easy summarisation with Excel Pivot Tables.
  - Directly compatible with Python `pandas` DataFrames.
- **File Management**:
  - Keep **raw data** separate from **cleaned data**.
  - Use versioned filenames:
    ```
    plant_growth_2025-08-11_raw.xlsx
    ```


## 3. Explore Data

### In Excel
- Use Pivot Tables to quickly summarise:
  - Mean and standard deviation of height by treatment.
  - Biomass by treatment and date.
- Apply conditional formatting to spot possible outliers.

### In Python (`pandas`)
**Numeric data**:
```python
df.shape        # number of rows and columns
df.info()       # column data types, missing values
df.columns      # list of column names
df.describe()   # summary statistics
```
**Categorical data**:
```python
df['Treatment'].unique()  # check treatment names
```
* Look for inconsistencies (case sensitivity, trailing spaces, typos).


## 4. Clean Data
**Numeric Data**
* Identify and handle:
  * Outliers (e.g., values far outside the expected range).
  * Incorrect decimal placement.
  * Check for missing values and decide on:
  * Removal, interpolation, or imputation.

**Categorical Data**
* Standardise category names:
```python
df['Treatment'] = df['Treatment'].str.strip().str.lower()
```
* Verify categories match planned treatment groups.

> **Tip – Spotting Data Errors with Quick Graphs:**  
> * You can often detect data issues by making quick visualisations, either in Excel Pivot Tables, Prism GraphPad, or Python (`matplotlib`).  
> * For example, when plotting means with error bars (based on at least 3–4 replicates per measurement), unusually large error bars can signal problems.  
> * This is often caused by missing values or incorrect entries — in my experience, a common reason is a missing decimal point in the raw data.  
> * If you spot this, revisit the original data sheet to confirm and correct errors.


## 5. Save Cleaned Data
* Save cleaned data separately:
```python
plant_growth_2025-08-11_clean.csv
```
* Keep raw and cleaned versions for traceability.


## 6. Visual Quick Check
```
import matplotlib.pyplot as plt
df.boxplot(column='Height_cm', by='Treatment')
plt.show()
```
* Plot distributions to confirm data quality before statistical analysis.


## 7. Next Steps
* Run statistical tests (e.g., ANOVA) to compare treatments.

* Build growth curves over time.

* Prepare publication-ready plots and summary tables.




