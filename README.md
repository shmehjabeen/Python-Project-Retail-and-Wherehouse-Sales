# Retail & Warehouse Sales Analysis

An exploratory analysis of 2020 retail and warehouse sales activity using Python, pandas, NumPy, Matplotlib, and Seaborn. The notebook covers data quality, channel and category performance, monthly patterns, SKU performance, transaction anomalies, and exports summary tables to Excel.

<img width="1206" height="613" alt="Retail and wherehouse Sale" src="https://github.com/user-attachments/assets/097859ec-dc09-4ebd-a8e9-085bae9fea01" />

- <a href="C:\Users\Mehjabeen Shaikh\Desktop\Mehjabeen\Personal\Mehjabeen Documents\Data Science - IIM Skills\3. Advanced Python\Project\Retail_Sales_Data_Analysis.pdf">View Dashboard</a>

## Project files

- `Retail_Sales_Data_Analysis.ipynb` — complete analysis notebook.
- <a href="https://github.com/shmehjabeen/Python-Project-Retail-and-Wherehouse-Sales/blob/main/Retail%20and%20wherehouse%20Sale.csv">Dataset</a> — source dataset (30,000 rows).
- `Retail_Sales_Data_Analysis.xlsx` — generated workbook, created when the notebook is run.

Place the CSV in the same folder as the notebook, or update `file_path` in the first code cell. The notebook currently uses a Google Colab path (`/content/Retail and wherehouse Sale.csv`).

## Dataset

The input contains 30,000 monthly item records across nine columns: `YEAR`, `MONTH`, `SUPPLIER`, `ITEM CODE`, `ITEM DESCRIPTION`, `ITEM TYPE`, `RETAIL SALES`, `RETAIL TRANSFERS`, and `WAREHOUSE SALES`. The data covers 2020 and contains records for January, March, July, and September. It includes 15,668 distinct item codes and eight item types.

The dataset has 33 missing supplier values and one missing retail-sales value. The notebook fills the missing retail-sales amount with zero. It reports no duplicate rows.

## Analysis workflow

1. Load and inspect the data types, shape, summary statistics, and missing values.
2. Clean column names and prepare numeric measures and a month date field.
3. Calculate total activity as retail sales + retail transfers + warehouse sales.
4. Compare channel totals and contributions; analyze activity by month and item type.
5. Rank suppliers and SKUs, review concentration and product performance, and calculate correlations.
6. Examine zero activity, negative transactions, adjustment categories, outliers, and distributions.
7. Build an executive summary and export cleaned data and analysis tables to an Excel workbook.

## Key findings in the notebook

| Measure | Notebook result |
| --- | ---: |
| Total retail sales | 208,186.94 |
| Total retail transfers | 197,821.74 |
| Total warehouse sales | 822,930.93 |
| Total activity | 1,228,939.61 |
| Warehouse share of channel activity | 66.96% |
| Retail sales share | 16.94% |
| Retail transfers share | 16.10% |
| Largest item type | BEER — 66.12% of activity |
| Highest activity SKU | CORONA EXTRA LOOSE NR - 12OZ — 49,109.50 |
| Highest month in the supplied records | July — 595,339.95 |
| Lowest month in the supplied records | September — 16,834.62 |
| Retail sales / retail transfers correlation | 0.84 |

Amounts are reported in the dataset’s activity units; the source does not document a currency or unit. “Total activity” is the sum of the three channel measures, so it is an operational aggregate rather than a separately defined financial metric. The monthly comparisons describe only the four months present in this file. The notebook’s month-over-month percentages compare consecutive available months (January → March → July → September), not adjacent calendar months.

## Data quality note: supplier results need correction

The notebook’s cleaning section mistakenly treats `SUPPLIER` as numeric and applies `pd.to_numeric(..., errors="coerce").fillna(0)`. This replaces supplier names with `0`. As a result, the notebook’s reported unique supplier count, supplier rankings, concentration, risk level, and automated supplier insight are not valid. The source CSV has 290 distinct nonblank supplier names, plus 33 blank supplier values. Remove `SUPPLIER` from the numeric cleaning list and rerun the notebook before using supplier-level outputs.

## Run the notebook

Install the required packages:

```bash
python -m pip install pandas numpy matplotlib seaborn jupyter openpyxl
```

Start Jupyter and open the notebook:

```bash
jupyter notebook Retail_Sales_Data_Analysis.ipynb
```

The final notebook section writes `Retail_Sales_Data_Analysis.xlsx` with sheets for cleaned data, executive KPIs, monthly, category, supplier, SKU, zero-activity, and negative-transaction analyses.

## Limitations

- Only four months from 2020 are present, so the results do not represent a complete year.
- The source does not define measurement units or currency.
- Negative and unusually large values are present; they may represent returns, corrections, or other adjustments and should be reviewed before interpreting them as ordinary sales.
- Supplier-level conclusions are compromised by the conversion bug described above.
