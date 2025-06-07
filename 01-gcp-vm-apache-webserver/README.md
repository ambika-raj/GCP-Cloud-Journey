# Task 01: gcp-vm-apache-web server

## Overview
Created and configured a Virtual Machine (VM) on Google Cloud Platform using the CLI, installed Apache, and hosted a simple HTML webpage.

## Technologies Used
- Google Cloud Platform (GCP)
- Compute Engine
- gcloud CLI
- cloud shell
- Apache2

## What I did: Steps Followed 
1. Created VM instance using (Created a VM instance via 'gcloud' CLI):
   `gcloud compute instances create vm-cli-1 --machine-type=e2-micro --zone=asia-south1-a`

2. SSH into the VM (Learned how to SSH into a VM and manage files):
   `gcloud compute ssh vm-cli-1 --zone=asia-south1-a`

3. Installed Apache (Installed Apache server):
   `sudo apt update
   sudo apt install apache2 -y
   exit`

4. Created cutom webpage (Deployed a basic HTML page):
   `echo "<h1>Hello from Ambika's Cloud Server</h1>" | sudo tee /var/www/html/index.html`

5. Allow HTTP traffic (Configured firewall rules to allow HTTP traffic (port 80)):
   `gcloud compute firewall-rules create allow-http --allow tcp:80 --target-tags=http-server --description="Allow HTTP traffic"
   gcloud compute instances add-tags vm-cli-1 --tags=http-server --zone=asia-south1-a`

6. Visit the VM's External IP:
   `gcloud compute instances list`

## Output:
   Web page hosted at: http://35.244.63.149

## What I Learned:
 - VM creation on Google cloud shell (CLI)
 - SSH and remote commands
 - Basic server setup
 - Firewall rules and networking
 - Understanding zone, machine-type and external IP
 - Real-world feel of cloud deployment

## Output Screenshot:
 - VM webpage: (./screenshots/Screenshot 2025-06-07 092438.png)
 - GCP VM creation: (./screenshots/Screenshot 2025-06-07 092527.png)
