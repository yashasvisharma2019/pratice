# Mini Data Center (Mini-DC) – LLM + Automation + Monitoring

A fully containerized simulation of an on-premises LLM infrastructure built using Docker.  
This project demonstrates LLM API hosting, API Gateway routing, workflow automation,  
S3-compatible object storage, and full observability.

---

## How to Run This Project

### 1️⃣ Install Requirements
- **Docker Desktop**
- **Git** (optional)

---

### 2️⃣ Clone or Download the Project

#### Clone:
```bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPO.git
cd YOUR_REPO
```

#### Or download ZIP:
- Click **Code → Download ZIP**
- Extract the ZIP  
- Open the extracted folder

---

### 3️⃣ Start All Services

Open **Command Prompt** or **PowerShell** inside the project folder:

```bash
docker compose up -d
```

This starts all components:

- API Gateway (Nginx)  
- FastAPI LLM service  
- n8n workflow automation  
- S3-compatible object storage  
- Prometheus metrics  
- Grafana dashboards  

---

### 4️⃣ Verify Running Containers

```bash
docker compose ps
```

All services should show **Up**.

---

## 🌐 Accessing the Services

| Service | URL |
|--------|-----|
| **LLM via API Gateway** | http://localhost:8080/llm/ |
| **LLM Direct Port** | http://localhost:11434 |
| **n8n Workflow UI** | http://localhost:5678 |
| **Object Storage (S3 UI)** | http://localhost:9000 |
| **Prometheus** | http://localhost:9090 |
| **Grafana Dashboard** | http://localhost:3000 |

(No credentials are shown for security.)

---

## 🔄 Using the n8n Workflow

The repository includes a ready-to-use workflow:

```
workflow.json
```

### Webhook Endpoint:
```
POST http://localhost:5678/webhook/generate
```

### Example request (CMD):
```cmd
curl.exe -X POST "http://localhost:5678/webhook/generate" ^
  -H "Content-Type: application/json" ^
  -d "{ "prompt": "hello" }"
```

### Example request (PowerShell):
```powershell
Invoke-RestMethod -Uri "http://localhost:5678/webhook/generate" `
  -Method Post `
  -Headers @{ "Content-Type" = "application/json" } `
  -Body '{ "prompt": "hello" }'
```

The workflow will:
- Receive the input  
- Send it to the LLM API  
- Upload the output to object storage  

---

## 📊 Monitoring Stack

### **Prometheus**
Collects metrics from:
- LLM service  
- n8n  
- API Gateway  
- Storage service  

### **Grafana**
Displays:
- LLM response latency  
- Workflow executions  
- System resource metrics  
- Gateway activity  

You can create custom dashboards or import community dashboards.

---

##  Project Structure

```
.
├── app.py                 # FastAPI LLM service
├── docker-compose.yml     # Orchestration file
├── nginx.conf             # API Gateway routing rules
├── prometheus.yml         # Metrics scraping configuration
├── requirements.txt       # Python dependencies
├── workflow.json          # Pre-configured n8n workflow
└── README.md              # Project documentation
```

---

##  Stopping the System

```bash
docker compose down
```

To remove containers + volumes:

```bash
docker compose down -v
```

---

##  Summary

This Mini-DC project simulates a real on-premises AI environment:

- API Gateway controlled access  
- LLM microservice  
- Automation pipelines  
- S3 object storage  
- Full monitoring  
- Secure, isolated Docker network  



