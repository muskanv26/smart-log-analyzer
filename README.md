# Smart Log Analyzer

An AI-powered backend system that ingests application logs in real time, automatically detects anomalies, and lets users query logs in plain English using an LLM.

> 🚧 Currently in active development

---

## What it does

Most applications generate thousands of log lines every day. Reading through them manually to find errors is slow and painful. Smart Log Analyzer solves this by:

- **Ingesting logs** in real time through a REST API
- **Detecting anomalies** automatically using a machine learning model — no manual threshold-setting needed
- **Letting users ask questions** like *"show all errors from the last hour"* in plain English and getting structured results back

---

## Tech stack

| Layer | Technology |
|---|---|
| API | Python, FastAPI |
| Database | PostgreSQL |
| ML / Anomaly Detection | scikit-learn (Isolation Forest) |
| LLM Querying | LangChain, OpenAI API |
| Containerisation | Docker |

---

## Architecture

```
User query (plain English)
        │
        ▼
   LangChain + OpenAI API
   (converts to structured query)
        │
        ▼
   PostgreSQL
   (stores ingested logs)
        ▲
        │
   FastAPI backend
   (ingestion + anomaly detection)
        ▲
        │
   Incoming log events
```

---

## Project structure

```
smart-log-analyzer/
├── app/
│   ├── ingestion/       # Log ingestion endpoints
│   ├── detection/       # Anomaly detection pipeline
│   ├── querying/        # LangChain + OpenAI integration
│   └── main.py          # FastAPI app entry point
├── models/              # ML model training scripts
├── docker-compose.yml
├── Dockerfile
├── requirements.txt
└── .env.example
```

---

## Getting started

### Prerequisites
- Python 3.10+
- Docker & Docker Compose
- OpenAI API key

### Run locally

```bash
# Clone the repo
git clone https://github.com/muskanv26/smart-log-analyzer.git
cd smart-log-analyzer

# Copy environment variables
cp .env.example .env
# Add your OpenAI API key to .env

# Start with Docker
docker-compose up --build
```

The API will be available at `http://localhost:8000`

### API endpoints

| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/logs/ingest` | Ingest a new log event |
| `GET` | `/logs/anomalies` | Get detected anomalies |
| `POST` | `/logs/query` | Query logs in plain English |

---

## How anomaly detection works

Log events are scored using an **Isolation Forest** model from scikit-learn. Isolation Forest works by randomly partitioning data — anomalous points (unusual log patterns) are isolated faster and get a higher anomaly score.

The model is trained on normal log patterns and flags anything that deviates significantly as an anomaly.

---

## How natural language querying works

When a user sends a plain English question like *"show all critical errors from the last 24 hours"*:

1. LangChain sends the question + database schema to the OpenAI API
2. The LLM generates a SQL query
3. The query runs against PostgreSQL
4. Results are returned to the user

---

## What I learned building this

- How to structure a modular FastAPI project for real-world scalability
- How Isolation Forest works and when to use it for anomaly detection
- How LangChain connects LLMs to databases (text-to-SQL)
- How Docker simplifies running multi-service applications

---

## Status & roadmap

- [x] FastAPI backend with modular structure
- [x] Log ingestion pipeline
- [x] Isolation Forest anomaly detection
- [x] LangChain + OpenAI natural language querying
- [x] Docker setup
- [ ] TimescaleDB integration for time-series optimisation
- [ ] Dashboard UI for visualising anomalies
- [ ] Alerting system (email/Slack notifications)

---

## Author

**Muskan Varshney**  
B.Tech CS (Data Science) — ABES Engineering College, Ghaziabad  
[LinkedIn](https://linkedin.com/in/muskan-varshney-b2a9a5335) · [GitHub](https://github.com/muskanv26)
