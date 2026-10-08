# DevOpsX 2.0 – End-to-End CI/CD with Kubernetes, Terraform & Monitoring

## 📌 Project Overview

**DevOpsX 2.0** is a full-stack DevOps implementation that automates source code management, containerization, CI/CD, Kubernetes deployment, infrastructure provisioning, and monitoring.

This project demonstrates modern DevOps practices used in enterprise environments, with a focus on automation, scalability, reliability, and observability.

---

## 🏗️ Objective

Design and implement a complete DevOps pipeline integrating:

- Git-based version control
- Automated CI/CD using Jenkins
- Containerization with Docker
- Application deployment on Kubernetes
- Infrastructure provisioning using Terraform
- Monitoring and observability using Prometheus and Grafana

---

## 🏛️ Architecture

```text
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
