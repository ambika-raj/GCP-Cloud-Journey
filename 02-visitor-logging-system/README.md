# Task 02: Visitor Logging System using Cloud Function + Pub/Sub

## Overview
Designed and deployed a cloud-native visitor logging system using Google Cloud services. When a user visits the webpage (Tic-Tac-Toe site hosted on a GCP VM), the system logs the visit using a Cloud Function triggered by HTTP, which then publishes a message to a Pub/Sub topic.

## Technologies Used
- Google Cloud Platform (GCP)
- Cloud Functions (Gen 2)
- Cloud Pub/Sub
- GCP Logging & Monitoring
- Python 3.10
- Compute Engine (VM) — used for website hosting
- gcloud CLI 

## What I Did: Phased Implementation 
### Phase 1: Hosting Tic-Tac-Toe Game on VM
- hosted a static website (Tic-Tac-Toe Game) on Apache server via a GCP VM
- Technologies: Compute Engine, Apache2, CLI

### Phase 2: Write & Deploy Cloud Function
- Created a Python Cloud Function to capture and publish visitor info.
- Code: main.py
  
`import functions_framework  
 from google.cloud import pubsub_v1  
 import json  
 @functions_framework.http  
 def publishVisitorLog(request):  
    publisher = pubsub_v1.PublisherClient()  
    topic_path = publisher.topic_path("tic-tac-toe-cloud-hosting", "visitor-logs")  
    visitor_data = {  
        "ip": request.remote_addr,  
        "user_agent": request.headers.get("User-Agent"),  
        "timestamp": request.headers.get("Date", "No Timestamp")  
    }  
    future = publisher.publish(topic_path, json.dumps(visitor_data).encode("utf-8"))  
    return "Message published to Pub/Sub!"`  
- Command Used for Deployment:
 `gcloud functions deploy publishVisitorLog --runtime python310 --trigger-http --allow-unauthenticated --region=asia-south1`

### Phase 3: Configure Pub/Sub
- Created a topic manually:
 `gcloud pubsub topics create visitor-logs`
- Verified logs in Logs Explorer.

### Phase 4: Integration Test
- Visited webpage (or triggered function from browser):
`https://asia-south1-tic-tac-toe-cloud-hosting.cloudfunctions.net/publishVisitorLog`
- Verified visitor entry in Logs:
  IP Address
  User Agent
  Timestamp

## Output
Web page hosted: http://34.100.136.157/

## Output Screenshots
- VM instance created: <img width="2880" height="1704" alt="VM-instances" src="https://github.com/user-attachments/assets/df471586-377d-4165-8b55-342aba5afa9d" />

- Topic created: <img width="2880" height="1704" alt="Topic-created" src="https://github.com/user-attachments/assets/6d759d40-c4c9-47ec-a583-c7180fad140f" />

- Function deployed successfully: <img width="2880" height="1704" alt="Function-deployed" src="https://github.com/user-attachments/assets/5a2afd0f-df06-4529-893c-1773aca35359" />

- Browser response: <img width="2880" height="1704" alt="Browser-response" src="https://github.com/user-attachments/assets/51ff6b55-199b-4970-bfd8-5ce2edf566f7" />

- Visitors records: <img width="2880" height="1704" alt="Visitor-records" src="https://github.com/user-attachments/assets/63e6ed4d-d70e-48be-bcfd-c83a2e36cca3" />

## What I Learned
- Hosting the Website Using VM
- Writing and deploying serverless Python functions
- Creating and triggering HTTP Cloud Functions
- Using Pub/Sub to log messages
- GCP Logs Explorer & debugging
- Logging Visitor Activity with Pub/Sub
