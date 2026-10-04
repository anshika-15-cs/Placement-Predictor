# DECISIONS

## 1. Impute missing values instead of dropping rows (meaningful change, tested)
**First approach:** drop every row with any missing value.
**Result:** only 781 of 1,000 rows survived (22% of the data lost). Logistic Regression F1 was 0.751 on that subset
versus 0.752 when imputing and keeping all 1,000 rows. Dropping rows bought no accuracy and threw away data.
**Decision:** impute inside the sklearn `Pipeline` (median for numeric, most-frequent for categorical).

## 2. Split first, impute/scale afterwards
Fitting the imputer/scaler on the full dataset would leak test-set statistics into training. Keeping them inside the
`Pipeline` means each CV fold and the final model fit them only on training data.

## 3. Cleaning rules
- CGPA values above 10 are treated as percentages and divided by 9.5 (common conversion), not discarded.
- Values outside valid ranges (e.g. aptitude = -1, negative backlogs) are set to missing, then imputed.
- Category spellings normalised via explicit maps so unseen spellings become missing instead of silently new categories.

## 4. Metrics
Precision, recall and F1 are reported (as required). Accuracy is not used for selection. `class_weight="balanced"` is used
so the minority class is not ignored.

## 5. Model choice
Logistic Regression (simple, interpretable baseline) vs Random Forest (captures non-linear effects).
Selection uses 5-fold CV F1 on the training set only. Random Forest wins by 0.006, which is within noise, so the honest conclusion
is "no clear winner on this data"; on the real dataset the choice may differ.

## 6. Limitation noticed
Permutation importance on the Random Forest shows only CGPA, backlogs and communication clearly above zero; the rest
hover around zero or slightly negative. That means the model barely uses them, or the test set is too small to detect their effect.


