# Dataset Preparation

This project uses a combined dataset created from **two sources**:

### 1. Yawn vs Safe Driving Dataset
- Folders: `yawn/` and `safe/`
- Uploaded to Google Cloud Storage:

gs://dms-yawdd-rajk/yawdd_images/


### 2. NTHU Driver Drowsiness Dataset
- Extracted frames from videos: `drowsy/` and `notdrowsy/`
- Uploaded to:

gs://dms-yawdd-rajk/nthu_images/


---

## CSV File Creation
Vertex AI requires a CSV file in this format:

GCS_IMAGE_PATH, label


Two CSV files were generated:
- `import.csv` (yawn/safe)
- `import_nthu.csv` (nthu images)

Both were merged into one:

#### copy import.csv + import_nthu.csv import_combined.csv

Label Standardization

All labels were mapped to two final classes:

| Original  | Final  |
| --------- | ------ |
| safe      | alert  |
| notdrowsy | alert  |
| yawn      | drowsy |
| drowsy    | drowsy |

A PowerShell script was used to rewrite labels into:

* alert

* drowsy

The output file used for training:

#### import_final.csv

Upload to Vertex AI

The final CSV was uploaded:

#### gsutil cp import_final.csv gs://dms-yawdd-rajk/

Vertex AI imported this CSV to create the final training dataset.






