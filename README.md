# Tarav1
# TARA AI — Multi-Signal Image Forensics System (v1)

## Overview
TARA is a multi-modal image forensics system designed to detect AI-generated or manipulated images using a combination of deep learning, anomaly detection, and forensic signal analysis.

Instead of relying on a single model, TARA integrates multiple independent signals into a unified decision engine, improving robustness under real-world conditions.

---

## Problem
AI-generated images are increasingly used in fraud, impersonation, and misinformation. Traditional single-model classifiers often fail under distribution shifts or adversarial manipulation.

TARA addresses this by combining:
- learned features (CNN)
- statistical anomalies
- frequency-domain artifacts
- compression inconsistencies

---

## System Architecture


Input Image
↓
Preprocessing
↓
Feature Extraction (CNN)
↓
Multi-Signal Analysis
├── CNN Probability
├── Anomaly Score
├── FFT Frequency Score
├── Noise / ELA Score
↓
Fusion Engine
↓
Risk Classification + Confidence


---

## Core Components

### 1. CNN Model (EfficientNet)
- Binary classification (REAL vs FAKE)
- Implemented using PyTorch
- Outputs probability scores for both classes

---

### 2. Anomaly Detection
- Embeddings extracted from CNN
- Isolation-based anomaly scoring
- Detects out-of-distribution inputs

---

### 3. Frequency Analysis (FFT)
- Detects unnatural high-frequency artifacts
- Uses ring-based masking for signal extraction

---

### 4. Noise / Compression Analysis (ELA)
- Measures compression inconsistencies
- Highlights manipulated regions

---

### 5. Image Fingerprinting
- SHA256 hashing for integrity
- Perceptual hashing (pHash) for similarity detection

---

### 6. Fusion Decision Engine
- Combines all signals using weighted scoring
- Handles uncertain predictions explicitly
- Outputs:
  - predicted label (REAL / FAKE / UNCERTAIN)
  - confidence score
  - risk level

---

## Evaluation

### ROC Curve
- AUC Score: ~0.96
- Indicates strong classification performance

### Additional Metrics
- Confusion Matrix
- Classification Report
- Balanced Accuracy

### Real-World Testing
- Evaluated on:
  - clean real images
  - noisy / compressed real images
  - AI-generated images
- Includes uncertainty handling

---

## Training

- Model: EfficientNet-B0
- Framework: PyTorch
- Techniques:
  - data augmentation (rotation, blur, color jitter)
  - mixed dataset training (base + custom)
- Optimizer: Adam
- Loss: CrossEntropyLoss

---

## API (FastAPI)

### Endpoint: `/analyze`

**Input**
- Image file

**Output**
```json
{
  "predicted_label": "FAKE",
  "confidence_percent": 87.3,
  "risk_level": "High Risk",
  "signals": {
    "fft_score": 0.42,
    "noise_score": 0.31,
    "anomaly_score": 0.55
  }
}
How to Run
1. Install dependencies
pip install -r requirements.txt
2. Run API server
python -m uvicorn main:app --reload
3. Open in browser
http://127.0.0.1:8000
Project Structure
tara-ai/
├── main.py              # FastAPI + core pipeline
├── model.py             # CNN + Grad-CAM
├── anomaly.py           # anomaly scoring
├── frequency.py         # FFT analysis
├── noise.py             # ELA analysis
├── fingerprint.py       # hashing
├── train.py             # training pipeline
├── evaluate.py          # evaluation
├── real_world_eval.py   # real-world testing
├── roc_analysis.py      # ROC curve generation
├── benchmark.py         # performance testing
├── tara_classifier.pth  # trained model
├── README.md
Key Design Decisions
Multi-signal fusion instead of single-model reliance
Explicit uncertainty handling
Bias-aware threshold tuning
Modular architecture for extensibility
Limitations
Dataset bias may affect generalization
Fusion weights are heuristic (not learned)
Limited adversarial robustness testing
No distributed deployment
Future Improvements
Ensemble models (ResNet + EfficientNet)
Learned fusion mechanism
Larger and more diverse datasets
Cloud deployment and scaling
Adversarial robustness evaluation
Key Learnings
Model accuracy alone is insufficient for real-world systems
Combining multiple signals improves reliability
Data bias can significantly impact performance
Explainability (Grad-CAM) is essential for trust
Summary

TARA demonstrates the transition from a single-model classifier to a complete AI system that integrates:

machine learning
signal processing
decision engineering

It reflects practical system design considerations required for deploying AI in real-world environments.


---

If you want next:
I can upgrade this into a **“top 1% GitHub README (with diagrams + demo + badges)”** or review your repo structure brutally.
its too long , and the canvas broke in the middle a lot of time 

Good catch. Your instinct is right—short + sharp > long + noisy.

Here’s a clean, compact README (no break issues, recruiter-friendly):

# TARA AI — Multi-Signal Image Forensics System

## Overview
TARA is a multi-modal system for detecting AI-generated or manipulated images by combining deep learning with forensic signal analysis.

---

## Key Idea
Instead of relying on a single model, TARA fuses multiple signals:
- CNN prediction (EfficientNet)
- Anomaly detection (embedding-based)
- Frequency analysis (FFT)
- Compression artifacts (ELA)

---

## Pipeline

Image → CNN → Signals (FFT + Noise + Anomaly) → Fusion → Output


---

## Features
- Multi-signal decision engine (not single-model)
- Handles uncertainty (REAL / FAKE / UNCERTAIN)
- Risk scoring with confidence calibration
- Grad-CAM explainability

---

## Performance
- ROC-AUC: ~0.96
- Evaluated on real + AI-generated datasets
- Includes real-world testing (clean vs noisy inputs)

---

## API
**POST /analyze**

Returns:
```json
{
  "predicted_label": "FAKE",
  "confidence_percent": 87.3,
  "risk_level": "High Risk"
}
Run Locally
pip install -r requirements.txt
uvicorn main:app --reload
Tech Stack
Python, FastAPI
PyTorch (EfficientNet)
OpenCV, NumPy
FAISS / Isolation (anomaly)
Limitations
Dataset bias affects generalization
Fusion weights are heuristic
Not tested for adversarial attacks
Summary

TARA moves beyond a single ML model into a system that combines multiple signals to improve robustness in real-world AI detection scenarios.
