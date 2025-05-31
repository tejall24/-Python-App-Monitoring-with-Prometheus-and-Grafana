# Python App Monitoring with Prometheus and Grafana on AWS EC2

This project shows how to monitor a Python Flask application using **Prometheus** and **Grafana** on an **AWS EC2 instance**.
## 🧰 Prerequisites

- AWS account
- EC2 instance (Ubuntu)
- Security Group with open ports:
  - `9090` → Prometheus
  - `9100` → Node Exporter
  - `3000` → Grafana
  - `5000` → Python Flask App
  - `22` → SSh
## 🚀 Setup Steps

### ✅ 1. Launch EC2 Instance

- Launch an EC2 instance (Ubuntu)
- Name it `Prometheus`
- Open the required ports listed above
  
- ### ✅ 2. Install Prometheus & Node Exporter

  ![prometheus](https://github.com/tejall24/-Python-App-Monitoring-with-Prometheus-and-Grafana/blob/a03fc646b985c01896b93f6fe3af89b469776dad/images/prometheus.jpg).
