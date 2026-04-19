# TARA AI v2 — Learned Image Forensics System

## Overview
TARA v2 is an upgraded image forensics system that replaces rule-based decision logic with a learned fusion model.

It combines deep learning features and forensic signals into a unified feature vector and learns how to classify images as REAL or FAKE.

---

## Dataset
- AI vs Real Images Dataset (Kaggle)  
  https://www.kaggle.com/datasets/tristanzhang32/ai-generated-images-vs-real-images  

---

## Key Idea
Instead of manually combining signals, TARA v2 learns how to fuse them.

Features used:
- CNN embeddings (ResNet50)
- Frequency features (FFT)
- Noise statistics (residual-based)

---

## Pipeline
Image → Feature Extraction → Feature Vector → FusionNet → Output

---

## Model (FusionNet)
- Separate branches for:
  - CNN features (2048)
  - FFT features (32)
  - Noise features
- Features are processed independently and fused
- Outputs:
  - classification (REAL / FAKE)
  - manipulation score

---

## Training
- Precompute features → stored as `.npz`
- Normalize using mean/std
- Balanced sampling for class imbalance
- Loss:
  - Binary classification (BCE)
  - Score regression (MSE)
- Optimizer: Adam
- Early stopping enabled

---

## Inference
Run locally:

pip install -r requirements.txt  
streamlit run app.py  

Upload an image to get:
- Label (REAL / FAKE)
- Confidence
- Manipulation score

---

## Project Structure
v2/
- app.py
- train.py
- model.py
- dataset.py
- extract_features.py
- utils.py

---

## Improvements Over v1
- Replaced heuristic fusion with learned model
- Better generalization across datasets
- Structured feature pipeline
- End-to-end training system

---

## Limitations
- Depends on feature extraction quality
- Requires preprocessing pipeline
- Not optimized for real-time deployment

---

## Summary
TARA v2 moves from rule-based detection to a learned fusion system, improving robustness and making the pipeline more scalable and adaptable.
