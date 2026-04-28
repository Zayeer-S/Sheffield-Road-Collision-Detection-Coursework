# Sheffield Road Collision Data Analysis and Prediction

End-to-end machine learning workflow for the Sheffield Road Collision dataset (STATS19). Covers data preprocessing, supervised learning (classification), regression, unsupervised learning (clustering), and consolidated model evaluation.

---

## Dependencies

Python 3.12 is required. Install all dependencies with:

```bash
pip install -r requirements.txt
```

Core libraries used:

- `pandas`, `numpy` - data manipulation
- `scikit-learn` - preprocessing, classification, regression, clustering, evaluation
- `xgboost` - gradient boosting classifier and regressor
- `imbalanced-learn` - SMOTE oversampling
- `scipy` - statistical tests (trend analysis)
- `matplotlib`, `seaborn` - visualisation
- `pyyaml` - config loading

---

## File Organisation

```
Sheffield-Road-Collision-Detection-Coursework/
├── notebooks/
|   ├── notebook-config.yml           # Display-only config (plot styles, label mappings)
|   ├── stage_outputs/                # Persisted .pkl files passed between notebook stages
|   |
|   ├── 01_preprocessing.ipynb        # Data cleaning, imputation, feature engineering
|   |
|   ├── 02_supervised_stage1.ipynb    # Feature selection, leakage removal, train/test split
|   ├── 02_supervised_stage2.ipynb    # SMOTE / class imbalance handling (all three tasks)
|   ├── 02_supervised_stage3.ipynb    # Multiclass classification (collision_severity)
|   ├── 02_supervised_stage4.ipynb    # Binary classification (urban_or_rural_area)
|   ├── 02_supervised_stage5.ipynb    # Categorical classification (junction_detail)
|   |
|   ├── 03_regression.ipynb           # Regression: casualty prediction, trend analysis, spatial
|   ├── 04_unsupervised.ipynb         # Clustering: risk profiles and geospatial hotspots
|   └── 05_evaluation.ipynb           # Consolidated evaluation, responsible AI, error analysis
|
├── storage/
|   ├── raw/
|   |   └── Filtered_Sheffield_Traffic_Data.csv   # Raw STATS19 Sheffield dataset
|   └── processed/
|       └── Sheffield_Traffic_Data_Processed.csv  # Output of preprocessing notebook
|
├── config.yml                        # Single source of truth for all pipeline parameters
├── requirements.txt
└── README.md
```

---

## Usage

Notebooks must be run **in order**. Each stage persists its outputs as `.pkl` files in `notebooks/stage_outputs/` which downstream notebooks load directly.

### Recommended run order

```
01_preprocessing.ipynb
    => 02_supervised_stage1.ipynb
    => 02_supervised_stage2.ipynb
        => 02_supervised_stage3.ipynb
        => 02_supervised_stage4.ipynb
        => 02_supervised_stage5.ipynb
    => 03_regression.ipynb
    => 04_unsupervised.ipynb

05_evaluation.ipynb   (run last -- depends on stages 3, 4, 5, regression, and unsupervised)
```

### Running a notebook

Open any notebook from the project root so that `find_project_root()` can locate
`config.yml` by walking up the directory tree:

```bash
cd Sheffield-Road-Collision-Detection-Coursework
jupyter notebook notebooks/01_preprocessing.ipynb
```

Note: You will likely need to select the kernel on the first launch of each notebook

---

## Configuration

All pipeline-critical parameters live in `config.yml` at the project root.
This is the single source of truth for:

- Raw data and output paths
- Sentinel value treatment and imputation settings
- Feature lists per classification task
- Train/test split parameters and random seeds
- Model hyperparameter search grids
- Regression and unsupervised learning settings

Display-only parameters (plot sizes, colour palettes, label mappings) live in
`notebooks/notebook-config.yml` and do not affect pipeline outputs.

---

## Dataset

The dataset is the STATS19 road collision dataset filtered to Sheffield city
(local_authority_district = 215), provided as `Filtered_Sheffield_Traffic_Data.csv`.

Original source: Department for Transport, UK
https://www.gov.uk/government/statistical-data-sets/road-safety-open-data

---

## Installation (step-by-step)

```bash
# 1. Clone the repository
git clone https://github.com/Zayeer-S/Sheffield-Road-Collision-Detection-Coursework
cd Sheffield-Road-Collision-Detection-Coursework

# 2. Create and activate a virtual environment (recommended)
python -m venv venv
source venv/bin/activate        # macOS / Linux
venv\Scripts\activate           # Windows

# 3. Install dependencies
pip install -r requirements.txt

# 4. Launch Jupyter (alternatively, run them by clicking "Run All" inside the notebooks)
jupyter notebook
```

# AI Transparency Scale Declaration
No AI used