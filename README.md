# Fraud Detection — PaySim (Synthetic) Analysis

Project
- Exploratory Data Analysis (EDA) and initial investigation to support fraud detection modeling on the PaySim synthetic mobile-money transaction dataset.
- Notebook: [Code.ipynb](Code.ipynb) — runs the full analysis and contains the code referenced below.
- Dataset: [Dataset.csv](Dataset.csv)

Quick links to workspace symbols
- Notebook DataFrame: [`df`](Code.ipynb)  
- Target variable detection: [`target`](Code.ipynb)  
- Visualization sample features: [`selected_features`](Code.ipynb)  
- Time feature created from step: [`df['hour']`](Code.ipynb)  
- Hourly aggregated fraud rate series: [`fraud_by_hour`](Code.ipynb)

Environment / Dependencies
- Python 3.8+ (recommended)
- pandas, numpy, matplotlib, seaborn, jupyterlab/notebook
- Install with:
  ```
  pip install pandas numpy matplotlib seaborn jupyterlab
  ```

How to run
1. Open the repository folder and start Jupyter:
   ```
   jupyter lab
   ```
2. Open [Code.ipynb](Code.ipynb) and run cells top-to-bottom.
3. Confirm [Dataset.csv](Dataset.csv) is in the same directory as the notebook.

Notebook walkthrough (what I did, step-by-step)
1. Imports and setup
   - Imported standard EDA libraries (os, zipfile, Path, numpy, pandas, matplotlib, seaborn, Counter) in the first cell.

2. Load dataset
   - Read the CSV into the DataFrame [`df`](Code.ipynb] via `pd.read_csv('Dataset.csv')`.

3. Initial inspection
   - Viewed first rows (`df.head(5)`), shape (`df.shape`), and `df.info()` for column types and non-null counts.
   - Computed basic summary statistics with `df.describe()`.

4. Identify features and target
   - Determined `target = 'isFraud'` if present and built lists of categorical and numerical columns. See [`target`](Code.ipynb).

5. Missing values
   - Checked missing value counts: `df.isnull().sum()` and printed any columns with missing data.

6. Class imbalance check
   - Computed counts and percentages for the target and plotted class distribution with `sns.countplot`. Observed heavy imbalance (frauds are rare).

7. Numeric summary and distributions
   - Displayed descriptive stats for numeric columns.
   - Plotted histograms of numeric features to inspect skew and scale.
   - Plotted boxplots for numeric features to highlight outliers.

8. Correlation analysis
   - Computed `corr = df[num_features].corr()` and plotted a heatmap with `sns.heatmap` to inspect pairwise relationships.

9. Categorical EDA
   - For each categorical column (detected as object/category), printed value counts and percentages. Displayed observations of dominant categories.

10. Transaction type vs fraud
    - If `type` exists, grouped by `type` and computed fraud rate: `type_fraud = df.groupby("type")["isFraud"].mean()`. Plotted a bar chart to highlight which transaction types have the highest fraud rates.

11. Amount distribution vs fraud
    - Used `sns.boxplot` to compare `amount` distribution across `isFraud` classes and set `plt.yscale("log")` to reveal differences across scales.

12. Pairwise relationships (sample)
    - Defined `selected_features` (see [`selected_features`](Code.ipynb)) and sampled 5,000 rows for performance. Created pairplots with `sns.pairplot(..., hue="isFraud")` to visualize multi-dimensional separation.

13. Temporal analysis
    - Converted simulation `step` (hours) to datetime: created [`df['hour']`](Code.ipynb) using `pd.to_datetime(df['step'], unit='h')`.
    - Aggregated hourly fraud rate: [`fraud_by_hour`](Code.ipynb) = `df.groupby('hour')['isFraud'].mean()` and plotted the result to inspect when fraud occurs most.

Key observations
- The dataset is highly imbalanced — frauds are a tiny fraction of transactions.
- Fraud rate differs by transaction `type` (e.g., `TRANSFER`, `CASH_OUT` typically higher).
- Fraudulent transactions show different patterns in `amount` and balance change (use log scale to visualize).
- Temporal aggregation (`fraud_by_hour`) can reveal hours with elevated fraud activity.
