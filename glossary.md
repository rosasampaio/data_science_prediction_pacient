"The preprocessing steps were fully integrated into a unified pipeline using ColumnTransformer and Pipeline, ensuring consistent transformations across training, validation, testing, and inference phases, and preventing data leakage."

## Ensuring complete preprocessing

- It means ensuring that all data, in training, validation, testing, and production, goes through exactly the same rules, in the same order, without exceptions.
- In ML, incomplete preprocessing is one of the main causes of models that work on the laptop but fail in real-world scenarios.

### Steps

#### Pillar 1 — A Single Source of Truth
- How to guarantee this? Using Pipeline + ColumnTransformer.

##### Pillar 2 — Explicit separation by variable type
- Experts never treat everything the same.

| Variable Type | Correct Handling |
| ------------------ | ------------------------------------ |
| Continuous Numeric | Scaling / RobustScaler |
| Binary Numeric | Hold or Cast |
| Nominal Categorical | OneHotEncoder |
| Ordinal Categorical | OrdinalEncoder |
| Dates | Feature Engineering (Year, Month, etc.) |

#### Pillar 3 — Preventing data leakage
- Classic error: Calculating mean, standard deviation, IQR, or encoding before the split.
- Correct approach:
> fit() → only in training

> transform() → training, validation, testing, production

> Pipeline ensures this automatically.

#### Pillar 4 — Tolerance for “new” (production) data
Experts assume that data never comes perfect.
Best practices:

- handle_unknown="ignore" in the encoder.
- Explicit imputation strategies.
- Outlier flags.
- Schema validation (number and names of columns).

#### Pillar 5 — Preprocessing as part of the model
If preprocessing is not versioned along with the model, it does not exist.

The Pipeline ensures:
- Single save (joblib)
- Reproducibility
- Auditability
- Secure deployment

#### Pillar 6 — Consistent Evaluation
Experts evaluate the entire pipeline, not the isolated model:

1. Cross-validation
2. Test set
3. Confusion matrix
4. Classification report

**Everything done after the pipeline, never before.**


##### Practical checklist for a professional ML
- ColumnTransformer
- Pipeline
- Correct Train/Test split
- CV before Test
- Prediction of new patient with best_model.predict()
- No manual preprocessing outside the pipeline