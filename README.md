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
- sudo apt update
  -sudo apt install prometheus -y
  -sudo apt install prometheus-node-exporter -y
  

  ![prometheus](https://github.com/tejall24/-Python-App-Monitoring-with-Prometheus-and-Grafana/blob/e914c09b02ae4ba974c18cd169f7e2dcd216ae68/images/metrics_console.jpg).


  
  Visit Prometheus: http://<EC2-IP>:9090

  Visit Node Exporter: http://<EC2-IP>:9100

#set alterts for that we need rules.yml file :
so create that file :

![rules.yml](https://github.com/tejall24/-Python-App-Monitoring-with-Prometheus-and-Grafana/blob/e914c09b02ae4ba974c18cd169f7e2dcd216ae68/rules.jpg)


add on rules section in the prometheus.yml:



![alerts](https://github.com/tejall24/-Python-App-Monitoring-with-Prometheus-and-Grafana/blob/e914c09b02ae4ba974c18cd169f7e2dcd216ae68/images/alerts.jpg)

✅ 3. Create Python Flask App with Prometheus Metrics

-sudo apt install python3-pip -y

-sudo apt install python3.12-venv -y

-python3 -m venv prometheus-env

-source prometheus-env/bin/activate

-pip install flask prometheus_client

#Create app.py:


![app.py](https://github.com/tejall24/-Python-App-Monitoring-with-Prometheus-and-Grafana/blob/e914c09b02ae4ba974c18cd169f7e2dcd216ae68/app.py.txt)


Run the app:


-python app.py

![pythonapp_output](https://github.com/tejall24/-Python-App-Monitoring-with-Prometheus-and-Grafana/blob/e914c09b02ae4ba974c18cd169f7e2dcd216ae68/images/app.jpg)


Visit App: http://<EC2-IP>:5000

Metrics: http://<EC2-IP>:5000/metrics

✅ 4. Configure Prometheus to Monitor the Flask App

-sudo nano /etc/prometheus/prometheus.yml

#add on prometheus.yml:

  - job_name: 'python_app'
    static_configs:
      - targets: ['localhost:5000']
   
#Reload Prometheus:

-sudo service prometheus reload

agian run python app.py ...(refersh again and again)

#go to the prometheus Dashborad :

![graph](https://github.com/tejall24/-Python-App-Monitoring-with-Prometheus-and-Grafana/blob/e914c09b02ae4ba974c18cd169f7e2dcd216ae68/images/prometheus_graph.jpg).



![console ](https://github.com/tejall24/-Python-App-Monitoring-with-Prometheus-and-Grafana/blob/e914c09b02ae4ba974c18cd169f7e2dcd216ae68/images/prometheus.jpg).



![target](https://github.com/tejall24/-Python-App-Monitoring-with-Prometheus-and-Grafana/blob/e914c09b02ae4ba974c18cd169f7e2dcd216ae68/images/terget.jpg)



✅ 5. Install and Start Grafana

-sudo mkdir -p /usr/share/keyrings
-curl -fsSL https://apt.grafana.com/gpg.key | sudo gpg --dearmor -o /usr/share/keyrings/grafana.gpg
-echo "deb [signed-by=/usr/share/keyrings/grafana.gpg] https://apt.grafana.com stable main" | sudo tee /etc/apt/sources.list.d/grafana.list
-sudo apt update
-sudo apt install grafana -y

#start grafnana :

-sudo systemctl start grafana-server
-sudo systemctl enable grafana-server


Access Grafana at: http://<EC2-IP>:3000


#Login with:

Username: admin

Password: admin


 ![Image Alt](https://github.com/tejall24/-Python-App-Monitoring-with-Prometheus-and-Grafana/blob/e914c09b02ae4ba974c18cd169f7e2dcd216ae68/images/grafana_login.jpg)




 this is dashboard i created through grafana :

  ![Image Alt](https://github.com/tejall24/-Python-App-Monitoring-with-Prometheus-and-Grafana/blob/e914c09b02ae4ba974c18cd169f7e2dcd216ae68/images/grafana_dashborad.jpg)


🙋‍♀️ Author
Tejal Mogal
GitHub: @tejall24
