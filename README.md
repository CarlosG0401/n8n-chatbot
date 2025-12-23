🧠 n8n + Ollama Chatbot (Huawei Cloud Pricing Demo)

This project is a **local chatbot** built with **n8n** (workflow orchestration) and **Ollama** (local LLM runtime).  
It is designed to query and analyze **Huawei Cloud ECS pricing** from a local **CSV file**, without sending data to external services.

Example questions you can ask:
- “Show me the most expensive machines”
- “What is the monthly price for an ECS c6.large in Santiago?”
- “Return only the final monthly price for this flavor”

Everything runs **locally using Docker**.

---

## ✅ What’s included

- **n8n** workflow (Webhook → Read CSV → Process → LLM → Response)
- Docker Compose to run:
  - `n8n` (UI + workflow engine)
  - `ollama` (LLM server)
- A sample pricing CSV file (`precios_hwc_v1.csv`)
- Exported n8n workflow JSON file

---

## 📁 Project structure

```text
n8n-chatbot/
├── n8n-local/
│   ├── docker-compose.yml
│   ├── data/
│   │   └── precios_hwc_v1.csv
│   └── workflows/
│       └── workflow_localhost_huaweiprices.json
├── .gitignore
└── README.md

⚠️ Important
Do NOT commit ollama_data/ (models can be several GB).
GitHub will reject large model files (and it’s not recommended to version them anyway).

🤖 Install Ollama model

After installing Ollama, download the model used by this project:

ollama pull deepseek-r1:7b


Verify the model is available:

ollama list

🚀 Run the stack with Docker Compose

Go into the n8n-local folder:

cd n8n-local
docker-compose up -d


Services:

n8n UI → http://localhost:5678

Ollama API → http://localhost:11434

🔁 Import the workflow into n8n

Open n8n:
http://localhost:5678

In n8n, go to:
Import → From File

Select the workflow file:

n8n-local/workflows/workflow_localhost_huaweiprices.json


Save the workflow and activate it.

🔐 Configure Ollama credentials in n8n

In n8n:

Open Credentials

Create a new credential for Ollama

Set the Base URL to:

http://ollama:11434


Leave API Key empty (unless you are using a proxy like Open WebUI with auth)

Save and test connection