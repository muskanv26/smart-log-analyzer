# 🔍 Smart Log Analyzer

> AI-powered real-time log analysis with ML anomaly detection
> and natural language querying via LLM.

## 🏗️ Architecture
[ Logs ] → [ Ingestion ] → [ PostgreSQL ] → [ ML Model ] → [ LLM Layer ] → [ Dashboard ]

## 🛠️ Tech Stack
- **Backend:** FastAPI, SQLAlchemy, Python
- **ML:** scikit-learn, PyTorch
- **LLM:** LangChain, OpenAI
- **Database:** PostgreSQL + TimescaleDB
- **DevOps:** Docker, GitHub Actions, Render

## 🚀 Getting Started
```bash
git clone https://github.com/muskanv26/smart-log-analyzer.git
cd smart-log-analyzer
python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt
cp .env.example .env
```

## 📌 Project Status
🔨 Phase 1 — Foundation ✅