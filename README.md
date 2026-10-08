DevOpsX 2.0 – End-to-End CI/CD with Kubernetes, Terraform & Monitoring
📌 Project Overview
DevOpsX 2.0 is a full-stack DevOps implementation that automates source code management, containerization, CI/CD, Kubernetes deployment, infrastructure provisioning, and monitoring.
This project demonstrates modern DevOps practices with a focus on automation, scalability, reliability, and observability.
🏗️ Objective
The objective of this project is to design and implement a complete DevOps pipeline integrating:
- Git-based version control
- Automated CI/CD using Jenkins
- Containerization with Docker
- Deployment on Kubernetes
- Infrastructure provisioning using Terraform
- Monitoring and alerting using Prometheus and Grafana
🏛️ Architecture
                    Developer
                        |
                        v
                     GitHub
                        |
                        v
                Jenkins CI/CD Pipeline
                        |
             +----------+----------+
             |                     |
             v                     v
       Build Docker Image    Deploy to Kubernetes
                                   |
                                   v
                           Kubernetes Cluster
                                   |
                                   v
                            Running Application
                                   |
                                   v
                         Prometheus Monitoring
                                   |
                                   v
                              Grafana
                                   |
                                   v
                         Dashboards & Alerts
🧩 Tools & Technologies
Component	Technology
Source Code Management	Git, GitHub
CI/CD	Jenkins
Containerization	Docker
Deployment & Orchestration	Kubernetes
Infrastructure as Code	Terraform
Monitoring & Alerting	Prometheus, Grafana
Application	Node.js, Express
Metrics	/metrics endpoint
Operating Environment	Linux


📁 Project Structure
Capstone_project/
│
├── app/
│   ├── index.js
│   └── Dockerfile
│
├── k8s/
│   ├── deployment.yaml
│   ├── service.yaml
│   └── servicemonitor.yaml
│
├── infra/
│   └── terraform/
│       ├── main.tf
│       ├── outputs.tf
│       ├── providers.tf
│       └── variables.tf
│
├── monitoring/
│   ├── grafana-dashboard-devopsx.json
│   └── monitoring-prometheus-rules.yaml
│
├── Jenkinsfile
└── README.md
🐳 Containerization with Docker
The application is containerized using Docker.
For a Minikube-based environment:
eval $(minikube docker-env)
Build the Docker image:
docker build -t devopsx-app:latest ./app
☸️ Kubernetes Deployment
Kubernetes manifests are available in the k8s/ directory.
Apply the Kubernetes configuration:
kubectl apply -f k8s/
Check the running pods:
kubectl get pods
The Kubernetes deployment manages the application containers and exposes the application through a Kubernetes Service.
🚀 CI/CD Pipeline with Jenkins
The CI/CD pipeline is defined in the Jenkinsfile located in the project root.
Pipeline Flow
Checkout Source Code
        ↓
Build Docker Image
        ↓
Deploy to Kubernetes
        ↓
Restart Deployment
        ↓
Post-Build Status
Pipeline Trigger
The pipeline can be triggered through:
- Git push webhook
- Jenkins SCM scan/polling
The Jenkins pipeline automates the application build and deployment workflow.
🛠️ Infrastructure as Code with Terraform
Terraform is used for infrastructure provisioning.
Navigate to the Terraform directory:
cd infra/terraform
Initialize Terraform:
terraform init
Apply the Terraform configuration:
terraform apply
Check Kubernetes namespaces:
kubectl get namespaces
The Terraform configuration creates the required Kubernetes namespace:
devopsx
📈 Monitoring with Prometheus & Grafana
The project implements monitoring and observability using Prometheus and Grafana.
Monitoring Components
- Kubernetes ServiceMonitor
- Prometheus metrics scraping
- Prometheus alert rules
- Grafana dashboard
- Application /metrics endpoint
The application exposes metrics through:
/metrics
📊 Grafana Dashboard
Grafana is used to visualize application and infrastructure metrics.
Access Grafana using Kubernetes port forwarding:
kubectl port-forward svc/monitoring-grafana 3100:80
Open:
http://localhost:3100
🔔 Alerts
The project implements monitoring alerts for application availability and traffic.
Alert 1: Deployment Down
The alert is triggered when:
kube_deployment_status_replicas_available < 1
This helps identify when the application deployment has no available replicas.
Alert 2: High Request Rate
The request rate is monitored using:
rate(devopsx_http_requests_total[5m])
This helps identify unusually high application traffic.
🧪 Running the Application
The application can be accessed using Kubernetes port forwarding:
kubectl port-forward svc/devopsx-service 3000:3000
Application
http://localhost:3000
Metrics
http://localhost:3000/metrics
🧪 Testing Alerts
To test the deployment availability alert, scale the application down to zero replicas:
kubectl scale deployment devopsx-deploy --replicas=0
Prometheus should detect the deployment failure and report the:
DevOpsXAppDown
alert.
🎯 Deliverables
The project implements:
- ✔ GitHub-based source code management
- ✔ Jenkins CI/CD pipeline
- ✔ Dockerized application
- ✔ Kubernetes deployment
- ✔ Terraform-based infrastructure provisioning
- ✔ Prometheus monitoring
- ✔ Grafana dashboards
- ✔ Prometheus alert rules
- ✔ Kubernetes ServiceMonitor
- ✔ Automated DevOps workflow
📝 Conclusion
DevOpsX 2.0 demonstrates an end-to-end DevOps lifecycle integrating infrastructure automation, continuous integration and delivery, containerized applications, cloud-native deployment, and real-time observability.
The project focuses on modern DevOps practices including:
- Automation
- Scalability
- Reliability
- Performance
- Monitoring
- Infrastructure as Code
- Continuous Delivery
👨‍💻 Author
Suhas D J
Information Science and Engineering
Siddaganga Institute of Technology, Tumkur
