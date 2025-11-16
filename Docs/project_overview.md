# Driver Drowsiness Detection – Project Overview

## 📌 Introduction
Driver fatigue is a major cause of road accidents worldwide. This project builds an AI-based solution to classify driver state as:

- **Alert**
- **Drowsy**

The system analyzes driver facial features, eye patterns, yawning behavior, and blinking frequency using computer vision.

This project was developed using **Google Cloud Vertex AI**, combining two datasets:
1. **Yawning vs Safe Driving Dataset**
2. **NTHU Driver Drowsiness Dataset**

The final model is deployed as an online prediction endpoint on Vertex AI.

---

## 🎯 Problem Statement
Fatigue-related accidents occur due to:
- Prolonged blinking
- Slow or no eye closure
- Frequent yawning
- Reduced attention

The goal is to **automatically detect driver drowsiness from images** and enable real-time alerting systems.

---

## 🚀 Solution Overview
We built a hybrid dataset combining yawning, eye-blink, and driver-alert/safe images, then trained an **AutoML Image Classification** model on Vertex AI.

**Pipeline:**
1. Collected two datasets
2. Preprocessed & uploaded to Google Cloud Storage
3. Created a combined CSV for training
4. Imported into Vertex AI Datasets
5. Trained custom AutoML Vision model
6. Evaluated performance (accuracy, confusion matrix)
7. Deployed online prediction endpoint
8. Tested with real unseen driver images

---

## 🧠 Model Capabilities
The final model predicts:
- **drowsy** – eye closure, yawning, sleepy posture
- **alert** – normal driving posture, open eyes

Average performance:
- **Accuracy:** ~85–90% (varies based on training budget)
- **Strong recall for drowsy class**

---

## 🧰 Technologies Used
- **Google Cloud Vertex AI (AutoML Vision)**
- Google Cloud Storage (GCS)
- Python for dataset preprocessing
- PowerShell for CSV transformation
- NTHU Drowsiness Dataset
- Custom Yawn vs Safe dataset
- GitHub for version control

---

## 📂 Repository Structure
```bash
Driver-Drowsiness-Detection/
├── README.md
├── LICENSE
├── .gitignore
├── docs/
│   ├── project_overview.md
│   ├── dataset_preparation.md
│   ├── vertex_ai_pipeline.md
│   ├── model_evaluation.md
│   └── deployment_and_testing.md
└── assets/