## 🚗 Driver Drowsiness Detection using Google Vertex AI
A full end-to-end Computer Vision pipeline built using Google Cloud Storage + Vertex AI AutoML + Cloud Deployment to detect alert vs drowsy drivers using images from YawDD and NTHU-DDD datasets.

## 📌 Overview

This project builds a binary image classification model that detects whether a driver is alert or drowsy, using a combined dataset from two popular driver-monitoring datasets.

The entire ML workflow — from dataset preparation to deployment — is implemented on Google Cloud Vertex AI.


## ⭐ Key Features

✔️ Combined two real-world driver datasets (YawDD + NTHU-DDD)

✔️ Automated dataset labeling through CSV generation

✔️ End-to-end ML pipeline using Vertex AI AutoML Vision

✔️ Model deployed to an online Vertex AI Endpoint

✔️ Achieved high accuracy on drowsiness classification

✔️ Documentation included for reproducible GCP setup



## 🧠 Objective

Detect driver drowsiness from a single image frame.
Final classification labels:

* alert

* drowsy



## 📂 Dataset Summary

| Dataset                    | Original Labels   | Mapped Labels | Count                 |
| -------------------------- | ----------------- | ------------- | --------------------- |
| YawDD                      | safe, yawn        | alert, drowsy | ~109K                 |
| NTHU-DDD                   | notdrowsy, drowsy | alert, drowsy | ~66K                  |
| **Final combined dataset** | —                 | alert, drowsy | **175K total images** |

👉 The two datasets were merged and relabeled to unify the classification system.


## 🏗️ Project Architecture

Local Datasets (YawDD + NTHU)
        |
        v
Google Cloud Storage (bucket: dms-yawdd-rajk)
        |
        v
Vertex AI Dataset (Imported using CSV)
        |
        v
Vertex AI AutoML Vision Training
        |
        v
Trained Model (alert_vs_drowsy)
        |
        v
Vertex AI Endpoint (online predictions)
        |
        v
App / Notebook / UI usage


## 🔧 Tech Stack

* Google Cloud Platform (GCP)
   * Vertex AI
   * Cloud Storage
   * AutoML Vision
   * Endpoints
* Python / PowerShell / CMD for CSV generation

* Computer Vision + Image Classification

* Cloud Deployment

## ⚙️ Implementation Steps
##### 1️⃣ Upload Image Data to Cloud Storage

* Created bucket: dms-yawdd-rajk

* Uploaded 4 main folders:

   * yawdd_images/safe

   * yawdd_images/yawn

   * nthu_images/drowsy

   * nthu_images/notdrowsy

###### 2️⃣ Create Import CSVs

CSV contained rows of the form:

##### gs://bucket/path/to/image.jpg,label

CSV files were merged and normalized:

 * safe → alert

 * notdrowsy → alert

 * yawn → drowsy

 * drowsy → drowsy

###### Final CSV: import_final.csv

##### 3️⃣ Create Vertex AI Dataset

Imported import_final.csv to generate:

* 175,801 labeled images

* 2 classes: alert, drowsy

4️⃣ Train the AutoML Vision Model

* Training budget: 8 node hours

* Vertex AI handled:
  * Data split
  * Augmentation
  * Hyperparameter tuning

* Achieved strong accuracy on evaluation set.

5️⃣ Deploy the Model

* Deployed as an online prediction endpoint

* Tested using the Vertex AI “Deploy & Test” UI

* Model successfully predicted uploaded images with confidence scores (e.g., 0.79 drowsy)

## 🧪 Sample Prediction

Input image:
➡️ Driver with eyes closing, leaning forward.

Output:

* drowsy: 0.793
* alert : 0.207

### 📈 Results & Performance

* High classification accuracy

* Strong recall for the drowsy class (critical for safety applications)

* Consistent performance across datasets