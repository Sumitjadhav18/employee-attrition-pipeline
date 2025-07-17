# Employee Attrition Prediction Pipeline

This project builds a complete ETL + ML pipeline for predicting employee attrition using the WA_Fn-UseC_-HR-Employee-Attrition dataset. It follows the Medallion Architecture (Bronze → Silver → Gold) on Azure Databricks and is triggered via Azure DevOps CI/CD pipeline.

## 🔧 Tech Stack

- Azure Databricks (Notebooks, Delta Lake)
- Azure Blob Storage (mounted as `/mnt/attrition`)
- Azure DevOps (Repo + Pipeline)
- Databricks CLI
- Python (PySpark)
- MLflow (for model tracking)
- Logistic Regression / XGBoost (for classification)

## 📁 Project Structure

employee-attrition-pipeline/
├── 1_mount_storage.py # Mounts ADLS Gen2 to /mnt/attrition
├── 2_bronze_ingestion.py # Reads raw CSV and writes Delta to Bronze
├── 3_silver_cleaning.py # Cleans, drops nulls, formats columns
├── 4_gold_feature_engineering.py # Adds features, encodes, normalizes
├── 5_ml_model_training.py # Trains and logs model using MLflow
├── azure-pipelines.yml # Azure DevOps CI/CD YAML trigger
├── README.md # Project documentation
└── .gitignore # Ignore system and notebook clutter


## 🚀 Pipeline Flow

1. Notebooks run sequentially via a Databricks Job (ID: `836396086717676`)
2. Triggered from Azure DevOps pipeline using `databricks-cli`
3. End-to-end run from Bronze to ML training with model tracking

## 🧪 Setup Instructions

1. Mount the data using `1_mount_storage.py` (run once)
2. Create Databricks multi-task job linking all `.py` notebooks
3. Push code and pipeline to Azure DevOps
4. Pipeline runs `databricks jobs run-now` to start execution

---

## 📊 Dataset

- File: `WA_Fn-UseC_-HR-Employee-Attrition.csv`
- Format: Tabular, HR employee details with target column `Attrition`

---

## ✅ Output

- Cleaned Delta Tables: `/mnt/attrition/silver`, `/mnt/attrition/gold`
- Trained ML model in MLflow
- Attrition prediction insights
