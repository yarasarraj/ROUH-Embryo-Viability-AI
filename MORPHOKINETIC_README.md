# ROUH — Morphokinetic Modeling & Late Fusion

A research notebook comparing **LSTM and GRU** models for embryo developmental-timing annotations and demonstrating **decision-level late fusion** with image-model probabilities. This is a component of the ROUH graduation project.

## What is included

- Conversion of annotation CSVs into developmental-timing feature tables
- Exploratory analysis and preprocessing of 13 timing features
- LSTM and GRU training and evaluation
- SHAP feature analysis of a **separate random-forest model** (not a direct LSTM explanation)
- A weighted late-fusion function: **0.60 × image probability + 0.40 × morphokinetic probability**
- **Illustrative** fusion examples, not matched image-and-timing test cases

## Results recorded in the original notebook

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
| --- | ---: | ---: | ---: | ---: | ---: |
| LSTM | 0.8865 | 0.8611 | 0.9894 | 0.9208 | 0.8556 |

These figures are saved outputs from an earlier run, **not independently revalidated**. GRU's original comparison table contained hard-coded numbers; the cleaned notebook calculates its comparison table from actual predictions when rerun.

## Important methodological limitations

1. The training target is **presence/absence of a recorded blastocyst-stage timing (`tB`)**, a developmental proxy rather than a validated clinical viability outcome.
2. In the original notebook `MinMaxScaler` is fitted on all rows **before** the train/test split, potentially inflating test performance. A rigorous reproduction should split first, fit on training only, then reevaluate.
3. The image and morphokinetic datasets are **not paired embryo-by-embryo**. Fusion code is a decision-level **demonstration** using sample probabilities; no measured held-out fusion performance is claimed.
4. SHAP explains a separate random forest trained on the morphokinetic features; it should not be described as directly explaining the LSTM.
5. Dataset CSVs, patient/embryo identifiers, model weights and saved outputs are excluded from the public repository.

## Running the notebook

1. Install dependencies: `pip install numpy pandas matplotlib seaborn scikit-learn tensorflow joblib shap jupyter`
2. Obtain the annotation CSVs through an authorized source. Do not upload sensitive/private records.
3. Set `ROUH_ANNOTATIONS_DIR` to the folder containing annotation CSVs; optionally set `ROUH_PROJECT_DIR` for output files.
4. Run `morphokinetic_lstm_late_fusion.ipynb` sequentially. TensorFlow/SHAP package versions may need adjustment for your environment.

**Disclaimer:** Educational/research prototype only; not intended for clinical decision-making.
