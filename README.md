# Penguin Species Classification Pipeline

A simple, reproducible machine-learning pipeline that predicts a penguin's species from physical measurements and sex. This repository was created for the AIPI 510 Week 12.

## Project overview

The notebook downloads the public [Palmer Penguins](https://github.com/allisonhorst/palmerpenguins) dataset, cleans it, splits it into training and test sets, trains an AdaBoost classifier, and evaluates the final model.

**Prediction target:** `species` (`Adelie`, `Chinstrap`, or `Gentoo`)

**Input features:**

- Bill length and depth
- Flipper length
- Body mass
- Sex, encoded as a binary feature

## Pipeline

1. Download `penguins.csv` from the Palmer Penguins GitHub repository.
2. Remove rows with missing values.
3. Remove `island` and `year`, then one-hot encode `sex`.
4. Create a stratified 80/20 train/test split using `random_state=42`.
5. Fit a scikit-learn `Pipeline` with:
   - `StandardScaler`
   - `AdaBoostClassifier` using 200 decision stumps (`max_depth=1`)
6. Evaluate with 5-fold stratified cross-validation on the training set and once on the held-out test set.

## Results

Using the fixed preprocessing and random seed in `penguins_ml_pipeline.ipynb`:

| Evaluation | Result |
| --- | --- |
| Cleaned dataset | 333 rows, 6 features |
| Training set | 266 rows |
| Test set | 67 rows |
| 5-fold CV accuracy | 95.1% ± 3.1% |
| **Test accuracy** | **95.5%** |

The held-out test result is based on 64 correct predictions out of 67 observations.

## How to run

### 1. Clone the repository

```bash
git clone <your-repository-url>
cd AIPI510_week12_ML-pipeline
```

### 2. Create and activate a virtual environment (optional but recommended)

```bash
python3 -m venv .venv
source .venv/bin/activate
```

On Windows:

```powershell
.venv\Scripts\Activate.ps1
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Run the notebook

```bash
jupyter notebook penguins_ml_pipeline.ipynb
```

Run the cells from top to bottom. The notebook downloads the dataset automatically, so an internet connection is required on the first step.

## Repository contents

| File | Purpose |
| --- | --- |
| `penguins_ml_pipeline.ipynb` | End-to-end data download, preprocessing, training, cross-validation, test evaluation, and confusion matrix |
| `requirements.txt` | Python package dependencies |

## Notes

- The test set is held out during cross-validation and model fitting, so the 95.5% test accuracy is the final evaluation reported for this run.
- Results may change if the data source, preprocessing, split, model settings, or random seed changes.
