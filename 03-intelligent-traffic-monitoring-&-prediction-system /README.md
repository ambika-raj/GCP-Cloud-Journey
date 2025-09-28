# Task 03: Intelligent Traffic Monitoring & Prediction System

## Overview
This project simulates, monitors, logs, and predicts traffic congestion using Google Cloud Platform (GCP) services.
It integrates VM-based traffic data generation, logging, monitoring, BigQuery analytics, and machine learning predictions to create an intelligent traffic monitoring and prediction system.

## Technologies Used
- Google Cloud Platform (GCP)
- Compute Engine (VM)
- Cloud Logging & Monitoring (Ops Agent)
- Pub/Sub
- BigQuery ML
- Cloud Storage
- gcloud cli (for VM setup & log simulation)
- SQL (BigQuery queries for analysis & ML)

## What I Did: Phased Implementation
### Phase 1: Setup Traffic Simulation VM
- Created VM instance on GCP to simulate vehicle traffic logs.
  `gcloud compute instances create traffic-sim-vm --zone=asia-south1-a --machine-type=e2-micro`
- Installed and configured web server + test logs for traffic simulation.
- Configured firewall rules for HTTP & SSH access.
  `gcloud compute ssh traffic-sim-vm --zone=asia-south1-a
   sudo apt update && sudo apt install apache2 -y`

### Phase 2: Logging & Monitoring Setup
- Installed and configured Google Cloud Ops Agent.
- Connected VM logs to Cloud Logging for real-time monitoring.
- Tested with custom log entries:
  `logger "Test log - Ambika $(date)"`
- Verified logs in Cloud Logging Explorer.

### Phase 3: Data Pipeline & BigQuery ML
- Exported traffic logs to Cloud Storage as CSV.
- Created BigQuery dataset & loaded logs.
- Built ML model in BigQuery to predict traffic congestion based on:
    Vehicle count
    Weather conditions
- Model Training Query:
  `CREATE OR REPLACE MODEL ``traffic_ml.traffic_congestion_model``
   OPTIONS(model_type='logistic_reg', input_label_cols=['traffic_status']) AS
   SELECT vehicle_count, weather, traffic_status
   FROM ``traffic_ml.traffic_logs``
   WHERE traffic_status IS NOT NULL;`
- Prediction Query:
  `SELECT vehicle_count, weather,
   ML.PREDICT(MODEL ``traffic_ml.traffic_congestion_model``,
    (SELECT 60 AS vehicle_count, 'Rainy' AS weather)) AS prediction;`

### Phase 4: Visualization Dashboard
- Built interactive BigQuery Dashboard.
- Visualized:
    Traffic congestion by vehicle count
    Weather impact on congestion
- Added filters (weather, status) for real-time analysis.

## Output Screenshots
### Phase: Logging & Data Capture (GCP Cloud Logging)
- VM Instance created: <img width="2880" height="1704" alt="03VM-instance" src="https://github.com/user-attachments/assets/c9f8b940-5e6c-4193-952f-c8f8ed1a2313" />

- Logs Explorer: <img width="2880" height="1704" alt="03logExplorer" src="https://github.com/user-attachments/assets/c10d168d-2b9f-44ea-a95f-2de383990509" />

### Phase: BigQuery Setup & Data Transformation
- Traffic logs Dataset: <img width="2880" height="1704" alt="03TrafficlogDataset" src="https://github.com/user-attachments/assets/dad8a7f8-b8f4-4f66-a8ce-ddc86edd1a00" />

- Traffic logs Schema: <img width="2880" height="1704" alt="03TrafficLogSchema" src="https://github.com/user-attachments/assets/8513d3a1-d911-46db-977c-d8f47c0d4a7c" />

- Data Preview: <img width="2880" height="1704" alt="03Trafficlogpreview" src="https://github.com/user-attachments/assets/37285ff7-f25e-4263-a462-d618a182dcbc" />

- Traffic Prediction Schema: <img width="2880" height="1704" alt="03TrafficPredictionSchema" src="https://github.com/user-attachments/assets/e2f898e5-0e4c-4a5f-a797-7d4fc8d7bdf8" />

- Traffic Prediction Preview: <img width="2880" height="1704" alt="03TrafficpredictionPreview" src="https://github.com/user-attachments/assets/8251dd6a-87db-4364-af86-8e3a3b3c2d47" />

### Phase: Machine Learning Model (BigQuery ML)
- Model Overview: <img width="2880" height="1704" alt="03ModelOverview" src="https://github.com/user-attachments/assets/53eb9523-afa9-4f35-8022-9256f341821d" />

- Evaluation Metrics: <img width="2880" height="1704" alt="03ModelEvaluationMetrics" src="https://github.com/user-attachments/assets/d26b5634-5510-41d7-bea6-62be73582e6c" />

- Predictions Table: <img width="2880" height="1704" alt="03MLPredictionTable" src="https://github.com/user-attachments/assets/83c20185-477f-4ed3-ab4c-0d943cc88c67" />

### Phase: Dashboard Visualization (Looker Studio)
- Full Dashboard Overview: <img width="2880" height="1704" alt="03Dashboard" src="https://github.com/user-attachments/assets/3fac2337-40ff-47c7-b83a-05ca140502d0" />

## What I Learned
- VM creation & firewall configuration on GCP
- Setting up Ops Agent for log collection
- Exporting and analyzing logs with BigQuery
- Building ML model with BigQuery ML
- Creating a dashboard for real-time predictions
- End-to-end cloud integration from data generation → monitoring → ML prediction → visualization

 



  
