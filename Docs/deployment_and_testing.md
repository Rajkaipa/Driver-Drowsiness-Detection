# Model Deployment & Testing

This document explains how the model was deployed to a Vertex AI endpoint and tested.

---

## 🚀 Deployment Steps

1. Go to **Vertex AI → Models**
2. Select:
alert_vs_drowsy_<timestamp>
3. Click **Deploy to Endpoint**
4. Create endpoint:
Driver Monitoring System (DMS)
5. Deployment complete:
- Status: **Active**
- Region: europe-west4

---

## 🖥️ Testing in Vertex Console

Uploaded images directly in **Test your model** panel.

Example prediction:

| Class   | Probability |
|---------|-------------|
| drowsy  | 0.793       |
| alert   | 0.207       |
