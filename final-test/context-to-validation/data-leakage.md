"Preventing data leakage means that we need to ensure that no information from the validation or test set influences the model training."

"Data leakage was prevented by encapsulating all preprocessing steps within a pipeline, ensuring that transformations were learned exclusively from training data and applied consistently during validation and testing." 

## Where data leakage “hides” in practice.
| Stage | Risk |
| ------------------- | ----------------------------------- |
| Scaling | Use the entire dataset before splitting |
| Encoding | Adjust the encoder with future data |
| Feature engineering | Use the target directly or indirectly |
| Outlier treatment | Calculate limits with the entire dataset |
| Imputation | Average calculated with test data |
| CV | Use the test set within the CV |


### How experts prevent data leakage
Golden rules

- Split first, always
- Everything that “learns” → inside the pipeline
- fit() only in training
- transform() in testing
- Test set is sacred (use only once)
- Single pipeline saved with joblib