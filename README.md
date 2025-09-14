# ONLINEBOUTIQUE
Deployed E-commerce website on K8s with monitoring through  Prometheus &amp; Grafana

working on a Real-Time Project 'ONLINEBOUTIQUE', which involves:

Developing an e-commerce application using a microservices architecture
Microservices built with Java / Python / Go / .NET
Deployment target: Google Kubernetes Engine (GKE)
Monitoring: Prometheus & Grafana

A detailed overview of the project deployment and commands used:
Project Deployment Process

Cluster Creation
First, a Kubernetes cluster was created on Google Cloud:
	1	Go to Google Cloud console
	2	Navigate to Kubernetes Engine
	3	Click Create, select Standard cluster
	4	Configure with 3 nodes (1 node per zone)
	5	Set node size (1 core, 8GB RAM was used)
	6	Click Create

Code Download
git clone https://github.com/GoogleCloudPlatform/microservices-demo.git
cd microservices-demo
cd release

Deployment Command
The entire microservice application was deployed with a single command:
kubectl apply -f kubernetes-manifests.yaml
This command deployed all microservices including:
	•	Frontend service
	•	Cart service
	•	Payment service
	•	Email service
	•	Currency service
	•	Product service
	•	Ad service
	•	And others

Verification Commands
To verify deployment:
kubectl get pods
kubectl get deploy
kubectl get svc
Testing the Application
To access the application:
	1	Get the external IP from the frontend service:kubectl get svc
	2	Copy the external IP of the frontend service
	3	Access it in a browser (remove 'https://' and use 'http://' if needed)

Monitoring

kubectl get ns
kubectl create ns monitor
kubectl get ns
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
kubectl get po -n monitor
helm install kube-prometheus-stack prometheus-community/kube-prometheus-stack --namespace monitor
kubectl get po -n monitor
kubectl expose deployment kube-prometheus-stack-grafana --port=3000 --target-port=3000 --name=grafana --type=LoadBalancer -n monitor
kubectl get svc -n monitor
kubectl --namespace monitor get secrets kube-prometheus-stack-grafana -o jsonpath="{.data.admin-password}" | base64 -d ; echo

