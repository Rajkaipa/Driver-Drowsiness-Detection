# Model Evaluation

This document summarizes the performance of the AutoML Vision model trained for driver drowsiness detection.

---

## 📊 1. Metrics (from Vertex AI)

- **Accuracy:** 85–90%
- **AUC ROC:** ~0.90
- **Precision (drowsy):** High
- **Recall (drowsy):** High → ideal for safety systems

---

## 📈 2. Confusion Matrix (conceptual)

|                | Predicted Drowsy | Predicted Alert |
|----------------|------------------|------------------|
| Actual Drowsy  | High             | Low              |
| Actual Alert   | Low              | High             |

The model is biased toward safety (better to classify drowsy even if borderline).

---

## 🧪 3. Sample Predictions
Actual testing inside Vertex AI UI showed:
- Closed-eye, yawning, slouching → **drowsy (0.79+)**
- Normal open eyes → **alert (0.85+)**

---

## 🧠 4. Strengths
- Works across multiple driver datasets  
- Learns both **eye closure** and **yawning**  
- Performs well in varied lighting conditions  
- Robust when combining datasets

---

## ⚠️ 5. Limitations
- Struggles with:
  - occlusions  
  - sunglasses  
  - very low light
- Better accuracy needs more diverse data

---
