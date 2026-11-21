## Setup & Data

### 1. Environment

```bash
python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

The pinned versions were tested with Python 3.13. If a pin cannot be installed, relax it to the closest release.

### 2. Download the data

The data is **not included** in this repository: it belongs to the course and to the original Kaggle competition.

- **To reproduce the reported results**, use the files of the GCI Global 2026 in-class competition (`competition.zip`): `train.csv`, `test.csv` and `sample_submission.csv`.
- The original Kaggle competition (<https://www.kaggle.com/c/home-credit-default-risk/data>) uses `application_train.csv` and `application_test.csv`. The notebook accepts those names too, but the in-class files are a subset with different row counts, so the numbers will not match.

### 3. Place the files

```
<repo>/
└── data/
    ├── input/                 <- put the downloaded files here
    │   ├── train.csv
    │   ├── test.csv
    │   └── sample_submission.csv
    ├── output/                created by the notebook (feature cache, submission)
    └── checkpoints/           created by the notebook (model checkpoints)
```

Everything inside `data/` except its README is ignored by git.

### 4. Run

Open `notebooks/home_credit_default_risk_pipeline.ipynb` in VS Code or Jupyter and run all cells. It works the same from the repository root and from `notebooks/`: the notebook finds the repository root and uses `<repo_root>/data` automatically.

- **Another data folder:** set `HC_COMPETITION_DIR` before starting Jupyter (it must contain `input/`).
  PowerShell: `$env:HC_COMPETITION_DIR = "D:\data\home_credit"` · bash: `export HC_COMPETITION_DIR=/path/to/home_credit`
- **Google Colab:** `!git clone <repo-url>`, then `%cd <repo>/notebooks`, upload the three CSV files into `<repo>/data/input/` and run the notebook. Nothing is read from Google Drive, and checkpoints are lost when the runtime resets.
- **Outputs:** the submission is written to `data/output/submission_v5_rank.csv`, and the aggregated tables for the dashboard to `reports/tableau/`.
- **Time:** a full run takes about an hour on a laptop. Results are checkpointed in `data/checkpoints/`, so an interrupted run resumes where it stopped. Delete that folder to retrain from scratch.
