# Inundata: Mapping Floods in South Africa

## In Collaboration With  
[@medAli-ai](https://github.com/medAli-ai) | [@ngoym](https://github.com/ngoym)

---

## Overview
This repository contains our solution for mapping floods in South Africa. All experiments were conducted on Kaggle, and we assume that users will run the notebooks in a Kaggle environment. If running in Google Colab, paths must be modified accordingly.

---

## Workflow
Our solution consists of four key stages:

### 1. Exploratory Data Analysis (EDA) & Data Preparation
We perform EDA on composite images to determine the optimal band combination for flood probability prediction. The best-performing band for this task was **Moisture Stress**.

#### Notebook:
- [first-stage-static-images-eda-data-preparation.ipynb](first-stage-static-images-eda-data-preparation.ipynb)

---

### 2. Image Classification
Using **Moisture Stress** images, we train an image classifier (**eva02_tiny_patch14_224**) to predict the probability of flooding at each location. This feature significantly improves the overall model performance.

#### Notebook:
- [second-stage-image-classifier.ipynb](second-stage-image-classifier.ipynb)

---

### 3. Modeling
We trained **nine different models** using a combination of flood probability, lagged precipitation values, rolling statistics, exponentially weighted moving averages (EWMA), and event time indicators.

#### Models & Notebooks:
1. **XGBoost** - [third_stage_xgb_modelling.ipynb](third_stage_xgb_modelling.ipynb)
2. **LightGBM** - [third_stage_lgb_modelling.ipynb](third_stage_lgb_modelling.ipynb)
3. **FastAI Tabular** - [third-stage-fastai-tabular-modelling.ipynb](third-stage-fastai-tabular-modelling.ipynb)
4. **FastAI GatedConv** - [third_stage_fastai_gatedconv_modelling.ipynb](third_stage_fastai_gatedconv_modelling.ipynb)
5. **FastAI 1DConv** - [third_stage_fastai_1dconv_modelling.ipynb](third_stage_fastai_1dconv_modelling.ipynb)
6. **FastAI TabTransformer** - [third_stage_fastai_tabtransformer_modelling.ipynb](third_stage_fastai_tabtransformer_modelling.ipynb)
7. **TabNet** - [third_stage_tabnet_modelling.ipynb](third_stage_tabnet_modelling.ipynb)
8. **Wavenet-GRU** (Inference recommended)  
   - Training: [third-stage-wavenet-gru-transformer-modelling.ipynb](third-stage-wavenet-gru-transformer-modelling.ipynb)  
   - Inference: [third-stage-wavenet-gru-transformer-inference-modelling.ipynb](third-stage-wavenet-gru-transformer-inference-modelling.ipynb)
9. **ResNet1D** (Inference recommended)  
   - Training: [third_stage_resnet1d_0_1_2_3_modelling.ipynb](third_stage_resnet1d_0_1_2_3_modelling.ipynb), [third_stage_resnet1d_4_5_6_modelling.ipynb](third_stage_resnet1d_4_5_6_modelling.ipynb), [third_stage_resnet1d_7_8_9_modelling.ipynb](third_stage_resnet1d_7_8_9_modelling.ipynb)  
   - Inference: [third-stage-resnet1d-inference-modelling.ipynb](third-stage-resnet1d-inference-modelling.ipynb)

---

### 4. Ensembling
We ensemble model predictions using **Nelder-Mead optimization** and apply flood probability normalization to improve generalization and predictive performance.

#### Notebook:
- [fourth-stage-models-ensemble.ipynb](fourth-stage-models-ensemble.ipynb)

---

## Justification for Normalization
- **Mathematical Validity**: Normalization aligns with log loss minimization while retaining ranking information.
- **Generalizability**: The approach is based on a predictive feature rather than dataset-specific artifacts.
- **Empirical Performance**: Both training and test scores improve after normalization, confirming its effectiveness.

---

## How to Use
1. Clone this repository:
   ```bash
   git clone https://github.com/yourusername/Inundata.git
   cd Inundata
   ```
2. Open the relevant notebook in a Kaggle/Colab environment.
3. Run the notebooks sequentially or execute specific models as needed.

---

## Acknowledgments
Special thanks to our team members, I could not ask for better teammates!

## Results
https://zindi.africa/competitions/inundata-mapping-floods-in-south-africa/leaderboard

* Public Leaderboard: 0.002105851
* Private Leaderboard: 0.002280238
