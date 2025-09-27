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
- VM Instance created: 
  
