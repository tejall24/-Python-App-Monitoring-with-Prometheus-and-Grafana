# -Python-App-Monitoring-with-Prometheus-and-Grafana
 Python App Monitoring with Prometheus and Grafana

 This project shows how to monitor a Python Flask application using **Prometheus** and **Grafana** on an **AWS EC2 instance**.

![Setup Overview](https://github.com/tejall24/-Python-App-Monitoring-with-Prometheus-and-Grafana/blob/main/images/setup-overview.png)

---

## 🧰 Prerequisites

- AWS account
- EC2 instance (Ubuntu)
- Security Group with open ports:
  - `9090` → Prometheus
  - `9100` → Node Exporter
  - `3000` → Grafana
  - `5000` → Python Flask App
  - `22` → SSH

---

## 🚀 Setup Steps

### ✅ 1. Launch EC2 Instance

- Launch an EC2 instance (Ubuntu)
- Name it `Prometheus`
- Open the required ports listed above

---

### ✅ 2. Install Prometheus & Node Exporter

```bash
sudo apt update
sudo apt install prometheus -y
sudo apt install prometheus-node-exporter -y
Visit Prometheus: http://<EC2-IP>:9090

Visit Node Exporter: http://<EC2-IP>:9100

✅ 3. Create Python Flask App with Prometheus Metrics
bash
Copy
Edit
sudo apt install python3-pip -y
sudo apt install python3.12-venv -y
python3 -m venv prometheus-env
source prometheus-env/bin/activate
pip install flask prometheus_client
Create app.py:
![app.py](https://github.com/tejall24/-Python-App-Monitoring-with-Prometheus-and-Grafana/blob/93254ac7383ce25f7031440e829ff7d7b89be80a/app.py.txt)

python
Copy
Edit
from flask import Flask
from prometheus_client import Counter, generate_latest

app = Flask(__name__)
REQUEST_COUNT = Counter('http_requests_total', 'Total HTTP Requests')

@app.route("/")
def home():
    REQUEST_COUNT.inc()
    return "Hello from Flask App!"

@app.route("/metrics")
def metrics():
    return generate_latest(), 200, {'Content-Type': 'text/plain'}

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
Run the app:

bash
Copy
Edit
python app.py
Visit App: http://<EC2-IP>:5000

Metrics: http://<EC2-IP>:5000/metrics

✅ 4. Configure Prometheus to Monitor the Flask App
Edit the Prometheus config:

bash
Copy
Edit
sudo nano /etc/prometheus/prometheus.yml
Add:

yaml
Copy
Edit
  - job_name: 'python_app'
    static_configs:
      - targets: ['localhost:5000']
Reload Prometheus:

bash
Copy
Edit
sudo service prometheus reload
✅ 5. Install and Start Grafana
bash
Copy
Edit
sudo mkdir -p /usr/share/keyrings
curl -fsSL https://apt.grafana.com/gpg.key | sudo gpg --dearmor -o /usr/share/keyrings/grafana.gpg
echo "deb [signed-by=/usr/share/keyrings/grafana.gpg] https://apt.grafana.com stable main" | sudo tee /etc/apt/sources.list.d/grafana.list
sudo apt update
sudo apt install grafana -y
Start Grafana:

bash
Copy
Edit
sudo systemctl start grafana-server
sudo systemctl enable grafana-server
Access Grafana at: http://<EC2-IP>:3000
Login with:

Username: admin

Password: admin

📊 Visuals
🧩 Prometheus Dashboard


📈 Grafana Dashboard


🔧 Python Flask App


📈 What You Can Monitor
Total HTTP requests to the app

System-level metrics from Node Exporter (CPU, memory, disk)

Real-time app metrics via Prometheus

📝 License
This project is licensed under the MIT License.

🙋‍♀️ Author
Tejal Mogal
GitHub: @tejall24
