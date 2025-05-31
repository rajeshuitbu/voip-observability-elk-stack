
# 📞 VoIP Observability with ELK Stack

A complete end-to-end DevOps project to collect, parse, and visualize logs from an Asterisk VoIP system using the **ELK Stack** (Elasticsearch, Logstash, Kibana) and **Filebeat**.

---

## 🚀 Project Description

This project sets up centralized log monitoring and analytics for **VoIP infrastructure** (using Asterisk). It enables **real-time visibility** into call logs, SIP response patterns, errors, and system events using dashboards and structured log pipelines.

It is a great portfolio project to showcase **DevOps, observability, and VoIP integration** skills.

---

## 📊 Architecture
+-------------------+ +---------------------+
| Asterisk PBX | | SIPp Tool |
| (VoIP Server) | | (Generates traffic) |
+--------+----------+ +----------+----------+
| |
| /var/log/asterisk/ |
| |
v v
+---------------------------------------------+
| Filebeat Agent |
| Ships logs to Logstash (port 5044) |
+--------------------------+------------------+
|
v
+------------------+
| Logstash |
| Parses and maps |
+--------+---------+
|
v
+------------------+
| Elasticsearch |
| (Data Storage) |
+--------+---------+
|
v
+------------------+
| Kibana |
| Dashboards/Alerts|
+------------------+


---

## 🔧 Technologies Used

|Tool            | Purpose                            |
|-----------------|------------------------------------|
| **Asterisk**    | VoIP Server (SIP)                  |
| **SIPp**        | SIP traffic generator              |
| **Filebeat**    | Log shipper                        |
| **Logstash**    | Log parsing and transformation     |
| **Elasticsearch** | Searchable log storage engine    |
| **Kibana**      | Visualization and dashboards       |
| **Docker Compose** | Stack orchestration             |

---

## 🛠️ Setup Instructions

### 1. Clone Repository

```bash
git clone https://github.com/rajeshuitbu/voip-observability-elk-stack.git
cd voip-observability-elk-stack

2. Install Asterisk
sudo apt update
sudo apt install asterisk -y
Ensure logs are enabled in /etc/asterisk/logger.conf:
[logfiles]
messages => notice,warning,error,verbose
Restart : sudo systemctl restart asterisk

3) Deploy ELK Stack
cd elasticsearch
docker-compose up -d

4. Install Filebeat on Host
curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-8.12.0-amd64.deb
sudo dpkg -i filebeat-8.12.0-amd64.deb
sudo cp ../filebeat/filebeat.yml /etc/filebeat/filebeat.yml
sudo systemctl start filebeat

5) Parse Logs with Logstash
Logstash config is in log-parsing/logstash.conf and parses Asterisk logs using Grok patterns.

To restart logstash inside Docker:
docker restart elasticsearch-logstash-1

6) Access Kibana
Go to:
📍 http://localhost:5601

Create an index pattern: asterisk-logs*

Explore logs in Discover tab

Import dashboards from /dashboards/kibana-export.ndjson

7) 📚 Use Cases
Real-time SIP traffic monitoring

VoIP call troubleshooting

Alerting on SIP errors or drops

Call volume analytics

Asterisk failure diagnostics


