# Vertex AI Pipeline (No-Code)

This project uses **Google Cloud Vertex AI** to train and deploy an image-classification model for **driver drowsiness detection**.

The whole pipeline was built using the **Vertex AI Console (UI)**, not custom training code.

---

## 1. Prerequisites

- Google Cloud project: `dms-capstone-ai`
- Region: `europe-west4`
- Services enabled:
  - Vertex AI API  
  - Cloud Storage
- Cloud Storage bucket:
  - `gs://dms-yawdd-rajk/`
  - Folders:
    - `yawdd_images/` – yawn vs safe images  
    - `nthu_images/` – drowsy vs notdrowsy images  
- Combined CSV manifest:
  - `gs://dms-yawdd-rajk/import_final.csv`  
  - Format:  
    `gs://dms-yawdd-rajk/<path_to_image>,alert|drowsy`

---

## 2. Create the Combined Dataset

1. Go to **Vertex AI → Datasets → Create dataset**.
2. Type: **Image**  
3. Objective: **Single-label classification**
4. Dataset name: e.g. `combined_drowsiness_dataset`
5. Region: `europe-west4`

### Import data from Cloud Storage

1. In the dataset, open the **Import** tab.
2. Choose **Import files** → **Select import files from Cloud Storage**.
3. File path:  
   `gs://dms-yawdd-rajk/import_final.csv`
4. Click **Continue** and wait for import to finish.
5. You should see two labels in **Browse**:
   - `alert`
   - `drowsy`

---

## 3. Train an AutoML Image Classification Model

1. In the dataset view, click **Train new model**.
2. Method: **AutoML**.
3. Model name example: `alert_vs_drowsy_YYYYMMDD`.
4. Training options:
   - No class weighting initially.
   - No incremental training (fresh model).
5. Compute & pricing:
   - Budget: e.g. **8 node hours** (used less in practice).
6. Click **Start training** and wait until the status is **Succeeded**.

> Vertex AI automatically performs data split (train/validation/test) and hyper-parameter search for the AutoML model.

---

## 4. Evaluate the Model

1. Open **Vertex AI → Models**.
2. Click the trained model (e.g. `alert_vs_drowsy_YYYYMMDD`).
3. Under **Evaluate**, note:
   - Overall metrics (AUC PR, Log loss, Accuracy).
   - Per-class Precision/Recall for `alert` and `drowsy`.
4. Optionally adjust the **score threshold** to balance false positives vs false negatives.

---

## 5. Deploy to an Endpoint (Online Prediction)

1. In the model page, go to **Deploy & test**.
2. Click **Deploy to endpoint**.
3. Create new endpoint, e.g. `driver_drowsiness_endpoint`.
4. Traffic split: **100%** to this model.
5. Number of nodes: **1** (sufficient for demo).
6. Wait until deployment status is **Deployed**.

### Quick manual test

1. In **Deploy & test**, use **Upload image**.
2. Upload a sample driver image.
3. Check the predicted probabilities for:
   - `drowsy`
   - `alert`

---

## 6. Cost Control (Clean-up)

To avoid charges after experiments:

1. **Undeploy** the model from the endpoint:
   - Vertex AI → **Endpoints** → select endpoint → **Undeploy**.
2. Optionally **delete**:
   - Endpoint
   - Model versions
   - Temporary datasets (if no longer needed)

Cloud Storage objects (images and CSVs) are kept for future experiments.

---

## 7. Next Steps

- Re-train with class weighting or filtered data.
- Export the model for on-device inference.
- Build a **custom-training** version (Keras / PyTorch) in **Google Colab** and integrate with this dataset and pipeline.
