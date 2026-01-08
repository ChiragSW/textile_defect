**Overview**
- **Script**: `trainer.ipynb` trains a defect classifier using Local Binary Patterns (LBP) features and an SVM.

**Data & Preprocessing**
- **Input folders**: `captured`, `hole`, `horizontal`, `verticle`.
- **Preprocessing**: images converted to grayscale, LBP computed per image, histograms extracted as feature vectors.

**Model & Training**
- **Model**: `SVC` with RBF kernel.
- **Hyperparameter search**: `GridSearchCV` over `C` and `gamma` with 5-fold CV; repeated train-test splits (70-30, 80-20, 90-10) and multiple runs to measure variance.
- **Output**: best model saved per run as `best_fabric_defect_model_{split}_run{n}.pkl`.

**Metrics**
## Classification Report

| Class        | Precision | Recall | F1-Score | Support |
|--------------|-----------|--------|----------|---------|
| Hole         | 0.73      | 0.90   | 0.81     | 21      |
| Horizontal   | 0.56      | 0.82   | 0.67     | 11      |
| Vertical     | 0.00      | 0.00   | 0.00     | 10      |
| **Accuracy** |           |        | **0.67** | **42**  |
| **Macro Avg** | 0.43     | 0.57   | 0.49     | 42      |
| **Weighted Avg** | 0.51 | 0.67   | 0.58     | 42      |

**Overall Accuracy**
**66.67%**

**Example Prediction (hole_image.jpg)**
- **Image**: `hole_image.jpg`
- **Model used**: `best_fabric_defect_model_80-20_run3.pkl`
- **Result**:
  - Defect Type: `hole`
  - Confidence Scores: `{'hole': 0.9928, 'horizontal': 0.0022, 'vertical': 0.0049}`
  - Defect Center: `(137, 91)`
  - Severity: `High`

**Quick Usage**
- To reproduce training or run predictions, open `trainer.ipynb` and run the cells in order. Use `predict_defect_from_path(image_path, classifier)` to classify a single image.

