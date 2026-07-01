# Online Retail II E-Commerce Customer Behavior Analysis

## Student
- Name: Ömer Faruk İşcanlı
- ID: 1306220071

## Project Goal
This project analyzes customer purchasing behavior in the UCI Online Retail II dataset. The workflow cleans historical transaction data, explores sales and product patterns, creates RFM customer features, and segments customers with a simple K-Means clustering model.

## Dataset
- Dataset name: UCI Online Retail II
- Dataset source: UCI Machine Learning Repository (https://archive.ics.uci.edu/dataset/502/online+retail+ii)
- Dataset license: CC BY 4.0

## Data Setup
The raw dataset is not committed to the repository because of its size (~90 MB).
To run the notebook end-to-end:

1. Download the Online Retail II dataset from the UCI link above.
2. Save it as `data/raw/online_retail_ii.csv` (the loader also accepts the original
   `.xlsx`; if you use it, update `DATA_PATH` at the top of the loading cell).

The cleaned dataset (`data/processed/online_retail_cleaned.csv`) is produced automatically
when the notebook runs, so it is not committed either. All figures and summary tables under
`outputs/` are committed, so the results can be reviewed without re-running the notebook.

## Folder Structure
```text
data/
  raw/              Raw dataset copy
  processed/        Cleaned dataset and customer segment outputs
notebooks/          Main analysis notebook
outputs/
  figures/          EDA and clustering visualizations
  tables/           Summary, KPI, RFM, and interpretation tables
prompts/            Prompt log and per-step prompt records
reports/            Report draft
```

## Installation
Install the required Python libraries from the project root:

```bash
python -m pip install -r requirements.txt
```

## How to Run the Notebook
Open and run the notebook from top to bottom:

```bash
jupyter notebook notebooks/online_retail_project.ipynb
```

The notebook uses the raw data, creates the cleaned processed dataset, produces EDA outputs, builds RFM features, trains the K-Means segmentation model, and consolidates findings.

## Main Libraries Used
- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn
- openpyxl
- jupyter

## Main Outputs Produced
- `data/processed/online_retail_cleaned.csv`
- `data/processed/customer_segments.csv`
- `outputs/tables/project_kpi_summary.csv`
- `outputs/tables/research_question_summary.csv`
- `outputs/tables/segment_interpretation.csv`
- `outputs/tables/cluster_summary.csv`
- EDA and clustering figures in `outputs/figures/`
- Turkish report draft: `reports/final_report_draft.md`
- Turkish prompt log deliverable: `prompts/prompt_gunlugu.md`

## Known Limitations
- The analysis is based on historical transaction data and does not prove future behavior.
- Cancellations, non-positive quantities/prices, and missing CustomerID rows were removed during cleaning.
- Removing missing CustomerID records may affect customer-level conclusions.
- Product descriptions may contain noise or service-like entries.
- K-Means clustering is exploratory and does not prove causality.
