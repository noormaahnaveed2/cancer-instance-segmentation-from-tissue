
# 🧬 Cancer Instance Segmentation from Tissue

> **Repository**
> [https://github.com/noormaahnaveed2/cancer-instance-segmentation-from-tissue](https://github.com/noormaahnaveed2/cancer-instance-segmentation-from-tissue)

Deep learning–based instance segmentation and classification of cell nuclei from histopathology tissue images using state-of-the-art semantic segmentation architectures.

---

# 📊 Dataset

## PanNuke: Cancer Instance Segmentation & Classification

This project uses the **PanNuke dataset**, a large-scale nuclei instance segmentation dataset with exhaustive annotations across **19 tissue types**.

### 🔎 Dataset Overview

* **481 visual fields**

  * 312 randomly sampled from 20,000+ whole slide images
  * Multiple magnifications
  * Multiple data sources
* **205,343 labeled nuclei**
* Instance-level segmentation masks
* Unified nuclei category schema across all tissues
* Provided as **3 folds**
* Over **7,000+ training patches** (256×256) across folds

### 🧫 Tissue Types (19)

Breast, Colon, Bile-duct, Esophagus, Uterus, Lung, Cervix, Head & Neck, Skin, Adrenal Gland, Kidney, Stomach, Prostate, Testis, Liver, Thyroid, Pancreas, Ovary, Bladder.

---

## 📁 Data Format (per fold)

* `images.npy`
  → 256×256 RGB image patches

* `masks.npy`
  → 6-channel instance-wise masks

  ```
  0: Neoplastic cells  
  1: Inflammatory  
  2: Connective / Soft tissue cells  
  3: Dead cells  
  4: Epithelial  
  5: Background
  ```

* `types.npy`
  → Tissue type label per patch

---

## 🖼 Data Preview

![Preview](./assets/asset1.png)

---

## 📦 Dataset Source (Kaggle)

* Fold 1 – 12.53 GiB
* Fold 2 – 11.91 GiB
* Fold 3 – 12.84 GiB

Available on Kaggle:

* [https://www.kaggle.com/andrewmvd/cancer-inst-segmentation-and-classification](https://www.kaggle.com/andrewmvd/cancer-inst-segmentation-and-classification)
* [https://www.kaggle.com/andrewmvd/cancer-instance-segmentation-and-classification-2](https://www.kaggle.com/andrewmvd/cancer-instance-segmentation-and-classification-2)
* [https://www.kaggle.com/andrewmvd/cancer-instance-segmentation-and-classification-3](https://www.kaggle.com/andrewmvd/cancer-instance-segmentation-and-classification-3)

---

# 🏗 Model Architectures

We evaluated multiple state-of-the-art semantic segmentation architectures.

---

## 1️⃣ DeepLabV3 + ResNet101 (Baseline)

* Paper: [https://arxiv.org/abs/1706.05587](https://arxiv.org/abs/1706.05587)
* Implementation: PyTorch Vision
* Backbone: ResNet101
* Role: Baseline model

---

## 2️⃣ U-Net

* Paper: [https://arxiv.org/abs/1505.04597](https://arxiv.org/abs/1505.04597)
* Implementation: `models/unet.py`
* Encoder–decoder structure with skip connections
* Strong performance in biomedical segmentation

---

## 3️⃣ Inception U-Net

* Paper: [https://dl.acm.org/doi/10.1145/3376922](https://dl.acm.org/doi/10.1145/3376922)
* Implementation: `models/unet.py`
* Inception modules integrated into U-Net architecture
* Improved multi-scale feature extraction

---

## 4️⃣ RefineNet

* Paper: [https://arxiv.org/abs/1611.06612](https://arxiv.org/abs/1611.06612)
* Implementation: `models/refinenet.py`
* Multi-path refinement for high-resolution segmentation

---

# 📐 Training Strategy

## 🔥 Loss Function: Hybrid Loss

[
\text{Loss} = 2 \times \text{BCE} + 2 \times \text{Dice} + \text{IoU}
]

### Binary Cross Entropy (BCE)

[
\text{BCE} = - \sum_{i=1}^{N} y_i \log \hat{y}_i
]

### Dice Coefficient

[
\text{Dice} = \frac{2TP}{(TP + FP) + (TP + FN)}
]

### Intersection over Union (IoU)

[
\text{IoU} = \frac{\text{Dice}}{2 - \text{Dice}}
]

---

## ⚙ Optimization

* Optimizer: **Adam**
* Learning Rate Scheduling:
  **Cosine Annealing with Warm-up Restarts**

Reference implementation:
[https://github.com/katsura-jp/pytorch-cosine-annealing-with-warmup/](https://github.com/katsura-jp/pytorch-cosine-annealing-with-warmup/)

![Scheduler Graph](https://github.com/katsura-jp/pytorch-cosine-annealing-with-warmup/raw/master/src/plot002.png)

---

# 📈 Results

## Confusion Matrix

![Confusion Matrix](./assets/asset2.png)

---

## 🧪 Segmentation Examples

Qualitative predictions across different tissue types:

![Segmentation Example](./assets/asset6.png)
![Segmentation Example](./assets/asset7.png)
![Segmentation Example](./assets/asset8.png)
![Segmentation Example](./assets/asset9.png)
![Segmentation Example](./assets/asset10.png)
![Segmentation Example](./assets/asset11.png)
![Segmentation Example](./assets/asset12.png)
![Segmentation Example](./assets/asset13.png)
![Segmentation Example](./assets/asset14.png)
![Segmentation Example](./assets/asset15.png)

---

# 💻 Code Structure

* Modularized implementation
* Custom training pipeline
* Multiple architecture support
* Configurable loss functions and scheduler
* Fold-based dataset handling

Full source code available at:
[https://github.com/noormaahnaveed2/cancer-instance-segmentation-from-tissue](https://github.com/noormaahnaveed2/cancer-instance-segmentation-from-tissue)

-
