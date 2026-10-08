DevOpsX 2.0 – End-to-End CI/CD with Kubernetes, Terraform & Monitoring
📌 Project Overview
DevOpsX 2.0 is a full-stack DevOps implementation that automates:

source code management,
containerization,
CI/CD,
Kubernetes deployment,
infrastructure provisioning,
and monitoring.
This project demonstrates modern industry standards used in enterprise DevOps environments.

🏗️ Objective
Design and implement a complete DevOps pipeline integrating:

Git-based version control
Automated CI/CD using Jenkins
Containerization with Docker
Deployment on Kubernetes
Infrastructure provisioning with Terraform
Monitoring using Prometheus & Grafana
🧱 Architecture
Developer → GitHub → Jenkins (CI/CD Pipeline)
      |                 |
      |                 → Builds Docker Image
      |                 → Deploys to Kubernetes
      |
Kubernetes Cluster → Running Application
      |
Monitoring Stack (Prometheus + Grafana)
      |
Dashboards & Alerts
🧩 Tools & Technologies
Component	Technology
Source Code Management	Git, GitHub
CI/CD	Jenkins (Pipeline as Code)
Build & Packaging	Docker
Deployment & Orchestration	Kubernetes
Infrastructure Provisioning	Terraform
Monitoring & Alerts	Prometheus, Grafana
Metrics	Node.js Express /metrics endpoint
📁 Project Structure
Capstone_project/
│
├── app/                     # Node.js application + Dockerfile
│   ├── index.js
│   └── Dockerfile
│
├── k8s/                     # Kubernetes manifests
│   ├── deployment.yaml
│   ├── service.yaml
│   └── servicemonitor.yaml
│
├── infra/terraform/         # Terraform IaC resources
│   └── main.tf
│
├── monitoring/              # Monitoring & Alert Rules
│   ├── prometheus-rules-devopsx.yaml
│   └── grafana-devopsx-dashboard.json
│
├── Jenkinsfile              # CI/CD pipeline
└── README.md
🐳 Containerization (Docker)
eval $(minikube docker-env)
docker build -t devopsx-app:latest ./app
☸️ Kubernetes Deployment
kubectl apply -f k8s/
kubectl get pods
🚀 CI/CD Pipeline (Jenkins)
Defined using Jenkinsfile in repo root.

Pipeline Flow:
Checkout Source Code
Build Docker Image
Deploy to Kubernetes
Restart Deployment
Post-Build Status
Triggered:

via Git push (webhook or SCM scan)
🛠️ Infrastructure as Code (Terraform)
cd infra/terraform
terraform init
terraform apply
kubectl get namespaces
Creates namespace:

devopsx
📈 Monitoring (Prometheus & Grafana)
Implemented:

ServiceMonitor for scraping /metrics
Prometheus alert rules
Grafana dashboard
Files:

monitoring/prometheus-rules-devopsx.yaml
monitoring/grafana-devopsx-dashboard.json
📊 Accessing Grafana
kubectl port-forward svc/monitoring-grafana 3100:80
Open:

http://localhost:3100
🔔 Alerts Implemented
Alert 1: Deployment down
Triggers when:

kube_deployment_status_replicas_available < 1
Alert 2: High request rate
Based on:

rate(devopsx_http_requests_total[5m])
🧪 Running the Application
kubectl port-forward svc/devopsx-service 3000:3000
App:

http://localhost:3000
Metrics:

http://localhost:3000/metrics
🧪 Test Alerts
kubectl scale deployment devopsx-deploy --replicas=0
Prometheus should report:

DevOpsXAppDown
🎯 Deliverables Completed
✔ Fully functional CI/CD pipeline
✔ Terraform-based Infra provisioning
✔ Dockerized application
✔ Kubernetes deployment
✔ Monitoring dashboards + alerts
✔ DevOps workflow with GitHub integration
✔ Jenkinsfile-driven build automation

📝 Conclusion
DevOpsX 2.0 represents an enterprise-grade DevOps lifecycle, integrating:

infrastructure automation,
continuous delivery pipelines,
cloud-native deployments,
and real-time observability.
This project aligns with modern DevOps practices focused on: automation, performance, scalability, and resilience.
