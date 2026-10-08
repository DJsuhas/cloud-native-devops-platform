# DevOpsX 2.0

A small Node.js service packaged with Docker and prepared for Kubernetes deployment. The repository also includes Terraform-managed Kubernetes objects, Prometheus Operator monitoring manifests, and a Jenkins pipeline example.

## Architecture

```text
Node.js app (port 3000)
  ├── HTTP response at /
  └── Prometheus metrics at /metrics
          │
          ▼
Kubernetes Deployment → ClusterIP Service → ServiceMonitor
                                                │
                              Prometheus Operator monitoring stack
                                                │
                                  Prometheus rules and Grafana dashboard
```

## Repository layout

```text
app/                 Node.js app, package metadata, and Dockerfile
infra/terraform/     Kubernetes namespace and ConfigMap resources
k8s/                 Deployment, Service, and ServiceMonitor manifests
monitoring/          Prometheus alert rules and Grafana dashboard JSON
Jenkinsfile          Jenkins pipeline example
```

## Prerequisites

- Node.js 18 or later and npm for local development
- Docker for building the application image
- A Kubernetes cluster and a working `kubectl` context for deployment
- Terraform 1.6 or later for the Terraform configuration
- For monitoring resources, a Prometheus Operator installation providing the `ServiceMonitor` and `PrometheusRule` custom resource definitions

The Terraform Kubernetes provider reads the local kubeconfig at `~/.kube/config`.

## Run locally

From the repository root:

```sh
cd app
npm install
node index.js
```

The service listens on port `3000`. Visit `http://localhost:3000/` for the application response and `http://localhost:3000/metrics` for Prometheus metrics.

## Build the Docker image

From the repository root:

```sh
docker build -t devopsx-app:latest ./app
docker run --rm -p 3000:3000 devopsx-app:latest
```

For a local Kubernetes cluster such as Minikube, make sure the cluster can access the image. One option is to build directly into Minikube's image store before applying the manifests:

```sh
minikube image build -t devopsx-app:1.2 ./app
```

The Kubernetes Deployment currently refers to `devopsx-app:1.2`; the Dockerfile does not prescribe an image tag.

## Deploy to Kubernetes

With the image available to the cluster:

```sh
kubectl apply -f k8s/
kubectl get deployment,service,pods
```

The Deployment requests two replicas and the Service exposes port `3000`. To access it from your machine:

```sh
kubectl port-forward svc/devopsx-service 3000:3000
```

Then open `http://localhost:3000/` or `http://localhost:3000/metrics`.

The manifests currently omit an explicit namespace and therefore deploy to the current namespace (normally `default`). The ServiceMonitor selects resources in `default`; keep these manifests aligned if deploying elsewhere.

## Provision Kubernetes configuration with Terraform

From `infra/terraform`:

```sh
terraform init
terraform plan
terraform apply
```

Terraform creates the `devopsx` namespace and a ConfigMap with `APP_MESSAGE=Hello from Terraform-managed ConfigMap!`. The variable defaults are `namespace=devopsx` and `environment=dev`.

Terraform currently does not deploy the application workload. Also note that the Kubernetes YAML manifests target the current namespace by default, while Terraform creates resources in `devopsx`; decide on one namespace and configure both paths consistently before combining them.

## Monitoring

- `k8s/servicemonitor.yaml` configures scraping of `/metrics` every 15 seconds and expects the Prometheus release label `monitoring`.
- `monitoring/monitoring-prometheus-rules.yaml` defines Prometheus alert rules.
- `monitoring/grafana-dashboard-devopsx.json` is a Grafana dashboard definition that can be imported into Grafana.

Apply the ServiceMonitor and Prometheus rules only after installing a compatible Prometheus Operator stack with the required CRDs and matching release label. This repository does not install Prometheus or Grafana, and does not include a Grafana Service to port-forward.

The request counter currently labels metrics by route, not HTTP status. As a result, the high-error-rate rule's `status` label filter does not currently measure 5xx responses as intended. The deployment availability alert is configured to wait two minutes before firing.

## Jenkins pipeline

The root `Jenkinsfile` demonstrates checkout and pipeline stage structure. It uses Windows `bat` steps. The Docker build and Kubernetes deploy commands are examples printed to the build log, not executed commands; configure the agent, credentials, and actual build/deploy commands before treating it as a working CI/CD pipeline.

## Current Kubernetes image and namespace settings

Before deploying, check `k8s/deployment.yaml` and update its image reference to the tag you built and made available to the cluster. If using a namespace other than `default`, set `metadata.namespace` consistently in the Deployment, Service, and ServiceMonitor and ensure Prometheus is configured to discover that namespace.

## Author

Furqan Mulla