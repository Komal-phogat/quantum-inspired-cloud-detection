# Quantum-Inspired Cloud Detection in Satellite Imagery

> **MSc Thesis Project** — Amity University, 2025  
> Comparing classical and quantum Support Vector Machine (SVM) kernels for cloud detection in multispectral satellite images using the 38-Cloud dataset.

---

## Overview

Cloud detection is a critical preprocessing step in satellite image analysis — misclassified clouds corrupt downstream tasks like land cover mapping, crop monitoring, and disaster response. This project investigates whether **Quantum Support Vector Machines (QSVM)** can offer a meaningful advantage over classical SVM for this binary classification task.

Using the **38-Cloud dataset** (multispectral Landsat-8 imagery), I compared:
- Classical SVM with RBF kernel (scikit-learn)
- Quantum SVM with a quantum kernel computed via **PennyLane** variational circuits

Preprocessing pipelines include **PCA-based dimensionality reduction**, **LAB colour transformation**, and **SLIC superpixel segmentation** to extract spatially meaningful features before kernel computation.

---

## Key Results

### Task 1: Cloud Detection (Multispectral Satellite Patches)

| Sample Size | Linear SVM | RBF SVM | QSVM |
|---|---|---|---|
| 20 | 87.5% | 92.5% | **92.5%** |
| 40 | 91.3% | 91.3% | **91.3%** |
| 60 | 91.7% | **92.5%** | 88.3% |
| 80 | 91.9% | **92.5%** | 88.8% |
| 160 | 91.9% | **92.8%** | 87.5% |
| 320 | 91.7% | **92.3%** | 85.9% |

### Task 2: Weather Classification (RGB Ground-Level Images)

| Sample Size | Linear SVM | RBF SVM | QSVM |
|---|---|---|---|
| 50 | 57.4% | **60.6%** | 18.4% |
| 100 | 58.8% | **61.6%** | 19.0% |
| 200 | 56.8% | **60.4%** | 20.0% |
| 300 | 58.0% | **59.0%** | 19.0% |

### Key Takeaway

RBF SVM was the strongest overall classifier (peak 92.8% on cloud detection). QSVM matched RBF at small sample sizes (n=20–40) but degraded as sample size increased — consistent with noise sensitivity in current quantum kernel simulations. QSVM showed limited suitability for multi-class tasks under these conditions.

---

## Repository Structure

```
quantum-inspired-cloud-detection/
│
├── cloud final code.ipynb          # Main notebook: preprocessing, training, evaluation
├── weather code.ipynb              # Weather classification experiments
├── Komal_Phogat_MSc_Thesis_2025.pdf  # Full thesis document
└── README.md
```

---

## Methodology

### 1. Dataset
- **38-Cloud Dataset**: Landsat-8 multispectral satellite patches (Red, Green, Blue, NIR bands)
- Binary labels: cloud vs. clear sky
- Publicly available via [Kaggle / 38-Cloud paper](https://github.com/SorourMo/38-Cloud-A-Cloud-Segmentation-Dataset)

### 2. Preprocessing Pipeline
- **LAB colour transformation** — decouples luminance from chroma for better spectral separation
- **SLIC superpixel segmentation** — groups spatially coherent pixels into meaningful regions
- **PCA** — reduces high-dimensional feature vectors to principal components before quantum encoding

### 3. Classical SVM
- Scikit-learn `SVC` with RBF kernel
- Hyperparameter tuning via grid search (C, gamma)

### 4. Quantum SVM (QSVM)
- Implemented using **PennyLane** variational quantum circuits
- Quantum feature map encodes classical data into quantum state space
- Quantum kernel matrix computed via inner products of quantum states
- Kernel passed to scikit-learn `SVC` for classification

---

## Requirements

```bash
pip install pennylane scikit-learn numpy pandas matplotlib seaborn scikit-image
```

Or with conda:

```bash
conda install numpy pandas matplotlib scikit-learn
pip install pennylane scikit-image
```

**Python version**: 3.8+

---

## How to Run

1. Clone the repository:
```bash
git clone https://github.com/Komal-phogat/quantum-inspired-cloud-detection.git
cd quantum-inspired-cloud-detection
```

2. Install dependencies (see above)

3. Open the main notebook:
```bash
jupyter notebook "cloud final code.ipynb"
```

4. Run cells sequentially — preprocessing → feature extraction → SVM training → QSVM training → evaluation

---

## Background & Motivation

Classical SVMs are well-established for remote sensing classification tasks. Quantum kernels, however, can implicitly map data into exponentially large Hilbert spaces — potentially capturing patterns that classical kernels miss. This project tests that hypothesis in the concrete, applied setting of satellite cloud detection, a task with real-world impact in Earth observation pipelines.

For the full research context, methodology, and literature review, see the [thesis PDF](./Komal_Phogat_MSc_Thesis_2025.pdf).

---

## Author

**Komal Phogat**  
MSc Data Science, Amity University (2023–2025), GPA: 8.27/10  
Research Intern — GGSIPU, New Delhi  
📧 komalphogat02@gmail.com  
🔗 [github.com/Komal-phogat](https://github.com/Komal-phogat)

---

## Related Work

- Schuld & Killoran (2019) — *Quantum Machine Learning in Feature Hilbert Spaces*
- Havlíček et al. (2019) — *Supervised learning with quantum-enhanced feature spaces* (Nature)
- Mohajerani & Saeedi (2019) — *38-Cloud Dataset*

---

## Tags

`quantum-machine-learning` `quantum-svm` `pennylane` `satellite-imagery` `cloud-detection` `remote-sensing` `scikit-learn` `python` `msc-thesis`
