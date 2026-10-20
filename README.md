# ROUH — Embryo Image Classification

Research component of **ROUH**, an AI system that uses late fusion exploring non-invasive embryo viability assessment using image analysis and morphokinetic data.

## Notebook

[`image_classification_clean.ipynb`](image_classification_clean.ipynb) compares a baseline convolutional neural network, ResNet50, and EfficientNetB0 on binary embryo-image classification. It includes transfer learning, class-weighting, evaluation, fine-tuning, threshold analysis, and Grad-CAM visualization.

## Recorded results

The following are from the saved run of the original notebook, **not independently reproduced here**:

| Model | Test accuracy | Viable-class F1 | AUC |
|---|---:|---:|---:|
| Baseline CNN | 85.12% | 0.000 | 0.491 |
| ResNet50 | 80.95% | 0.500 | 0.774 |
| EfficientNetB0 | 88.10% | 0.615 | 0.790 |

The held-out test split contained **168 images** (143 labeled non-viable and 25 viable). The baseline CNN failed to identify viable cases despite its high overall accuracy, illustrating the impact of class imbalance.

## Dataset and reproducibility

**Embryo images and trained model weights are not included.** Only use data you are permitted to access and redistribute. The notebook expects the following folder structure, with class subfolders under each split:

```text
data/embryo_images_raw/
  train/
    0/
    1/
  test/
    0/
    1/
```

Set `ROUH_DATASET_DIR` to the dataset root, `ROUH_OUTPUT_DIR` to the desired output directory, and optionally `ROUH_SAMPLE_IMAGE` to an authorized sample image for Grad-CAM. In Colab, mount Drive and set these environment variables before executing the notebook. Required Python packages include TensorFlow, NumPy, Pandas, Matplotlib, Pillow, scikit-learn, and OpenCV (`opencv-python`). Version compatibility and full reproducibility have **not yet been verified**.

## Responsible use

This is an **academic research prototype**, not a clinically validated diagnostic system. Predictions should not be used for clinical decisions. Do not publicly commit patient-identifiable data, confidential embryo images, credentials, or restricted model artifacts.

