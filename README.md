# ONLINEBOUTIQUE
Deployed E-commerce website on K8s with monitoring through  Prometheus &amp; Grafana

🛍️ ONLINEBOUTIQUE – Real-Time E-commerce Microservices Project
This repository documents the deployment of ONLINEBOUTIQUE, a real-time e-commerce application built using a microservices architecture. The project demonstrates scalable deployment on Google Kubernetes Engine (GKE) with integrated monitoring using Prometheus and Grafana.

🚀 Project Overview

Architecture: Microservices
Languages Used: Java / Python / Go / .NET
Deployment Platform: Google Kubernetes Engine (GKE)
Monitoring Stack: Prometheus + Grafana


🛠️ Deployment Process
1. 🔧 Cluster Creation on GKE
Steps to create a Kubernetes cluster:

Go to the Google Cloud Console
Navigate to Kubernetes Engine
Click Create → Select Standard Cluster
Configure with 3 nodes (1 per zone)
Set node size: 1 vCPU, 8GB RAM
Click Create


2. 📦 Code Download
   ```git clone https://github.com/GoogleCloudPlatform/microservices-demo.git
   cd microservices-demo/release```

3. 🚢 Deploy Microservices
Deploy all services using:
   'kubectl apply -f kubernetes-manifests.yaml'

This deploys:

Frontend Service
Cart Service
Payment Service
Email Service
Currency Service
Product Service
Ad Service
...and more


4. ✅ Verify Deployment
   'kubectl get pods
   kubectl get deploy
   kubectl get svc'

5. 🌐 Access the Application

Get the external IP of the frontend service:
   'kubectl get svc'

Copy the external IP of the frontend service
Open it in your browser (use http:// if https:// fails)

📊 Monitoring Setup (Prometheus + Grafana)
Create Monitoring Namespace
   'kubectl get ns
   kubectl create ns monitor
   kubectl get ns'

Install Prometheus Stack via Helm
   'helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
   helm repo update
   helm install kube-prometheus-stack prometheus-community/kube-prometheus-stack --namespace monitor'

Expose Grafana Dashboard
   'kubectl expose deployment kube-prometheus-stack-grafana \
   --port=3000 --target-port=3000 \
   --name=grafana --type=LoadBalancer -n monitor'

   'kubectl get svc -n monitor'

Get Grafana Admin Password
   'kubectl --namespace monitor get secrets kube-prometheus-stack-grafana \
  -o jsonpath="{.data.admin-password}" | base64 -d ; echo'

📎 References

GoogleCloudPlatform/microservices-demo
Prometheus Helm Chart

<img width="1360" height="688" alt="image" src="https://github.com/user-attachments/assets/021a64d8-4557-4f10-ba63-52cfeb906ba3" />

<img width="1360" height="693" alt="image" src="https://github.com/user-attachments/assets/341c27d9-66d7-45f0-a653-00c1e33db725" />

Thanks!
