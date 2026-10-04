# Placement-Predictor

A machine learning model that predicts whether a student is likely to be placed, based on their academic and skill profile. It is a **binary classification** problem (placed / not placed).

---

##  Dataset

- About 1,000 students with 10 features: `branch`, `cgpa`, `internships`, `projects`, `certifications`, `aptitude_score`, `coding_score`, `communication_skill`, `backlogs`, `extracurricular`
- Target column: `placed` (1 = placed, 0 = not placed)

> **Note:** the results below come from a synthetic practice dataset. Update them after running on the official GDG-USAR dataset.

---

##  How it works

1. **Clean the data:** remove duplicates, standardize spellings (`cse` and `Computer Science` become `CSE`), convert percentages entered as CGPA, and treat impossible values as missing.
2. **Split the data:** 80% train and 20% test, stratified so both keep the same placed ratio.
3. **Preprocess inside a scikit-learn `Pipeline`:** impute missing values, scale numeric columns, and one-hot encode categorical columns. This happens after the split to avoid data leakage.
4. **Train and compare two models:** Logistic Regression and Random Forest, selected using 5-fold cross-validation on the training data.
5. **Evaluate:** precision, recall, F1-score and confusion matrices on the test set.
6. **Explain:** permutation feature importance and a what-if analysis for one example student.

---

##  Results

| Model | Precision | Recall | F1-score |
|-------|-----------|--------|----------|
| Logistic Regression | 0.70 | 0.82 | 0.75 |
| Random Forest | 0.70 | 0.76 | 0.73 |

The two models perform almost the same, so neither is clearly better on this data.

**Example prediction:** a student with a CGPA of 7.2, 1 backlog and 2 certifications got about a **40%** chance of placement. The backlog lowered it by roughly 17 percentage points, and the certifications raised it by about 6.

---

##  How to run

```bash
# 1. Clone the repository
git clone <your-repo-url>
cd <your-repo-name>

# 2. Install dependencies
pip install pandas numpy scikit-learn matplotlib seaborn

# 3. Place the dataset at data/placement_data.csv, then run the code
```

You can run the code in **Google Colab**, **Jupyter Notebook**, or as a Python script. To use a different dataset, edit the column names at the top of the code.

---

##  Key decisions

- **F1, precision and recall instead of accuracy:** they show both kinds of mistakes.
- **Impute instead of drop:** dropping incomplete rows lost 22% of the data and did not improve the score.
- **Pipeline:** keeps the test data separate and prevents data leakage.

See [DECISIONS.md](DECISIONS.md) for details.

---

## Limitations

- Results come from synthetic data and may differ on the real dataset.
- A single train/test split on 1,000 rows gives only a rough estimate.
- Some features add very little to the prediction.

---

##  Project structure

```
├── README.md
├── DECISIONS.md
├── AI_USAGE.md
├── data/
│   └── placement_data.csv
└── placement_predictor.ipynb
```

Change the notebook or script name in this tree to match your actual files.

---

## 🤖 AI usage

AI tools (Claude) helped write the code and documentation. I reviewed every step and can explain it. See [AI_USAGE.md](AI_USAGE.md).
