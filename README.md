# Anymoly 

[![Docker](https://img.shields.io/badge/docker-not_ready-blue)]()
[![License](https://img.shields.io/badge/license-Custom_Business-green)]()

A minimal yet powerful backend system for **automated anomaly detection** in bank statements using **Spring Boot + Python + LLMs**. Designed for clean ingestion, structured analysis, and compliance — with zero frontend. Ready to plug into internal platforms or sell as a backend product.

---

## 🧩 What It Does

- Accepts `.csv` bank statements via API
- Parses file metadata and row-level values
- Detects inconsistencies (e.g., wrong dates, malformed entries)
- Uses **LLM (OpenAI or local)** to suggest intelligent corrections
- Returns clean JSON to integrate with your tools or expose to clients

---

## ⚙️ Core Features

✅ Java Spring Boot ingestion API  
✅ FastAPI microservice for anomaly detection via Local LLMs and AWS Bedrock LLMs  
✅ File metadata and schema validation  
✅ Structured JSON anomaly reports  
✅ Confidence scoring and fix suggestions  
✅ Dockerized, CI-ready, and auditable  
✅ REST API for B2B/partner integrations  

---

## 💡 Example Use Case

Upload a file named `April_2025.csv` with rows containing June dates:

1. Spring Boot handles file upload and CSV parsing  
2. Sends filename + content to Python LLM microservice  
3. LLM detects mismatches, malformed rows  
4. Returns structured JSON with corrections  
5. Optional: Serve through secure partner-facing REST API

---

## 🛠️ Tech Stack

| Layer         | Tech Stack                              |
|---------------|------------------------------------------|
| Ingestion API | Java 17, Spring Boot, Apache Commons CSV |
| AI/LLM Engine | Python 3.10, FastAPI, OpenAI API, Mistral, Ollama |
| DevOps        | Docker, Docker Compose, GitHub Actions   |
| Monitoring    | Prometheus (optional), JSON logs         |
| Compliance    | Auto-delete, audit logging, GDPR-light   |

---

## 🚦 Project Phases & Checklist

### 🟢 Phase 0 — Core MVP
- [ ] Spring Boot file upload API
- [ ] Parse filename + CSV rows
- [ ] REST call to Python microservice
- [ ] LLM response with structured JSON
- [ ] Docker Compose setup
- [ ] S3 integration

---

### 🟡 Phase 1 — Hardening
- [ ] Limit file size, support `.csv` only
- [ ] Validate header schema and null rows
- [ ] Track token usage (Local models and cloud models)
- [ ] Add audit logs (file hash, IP, timestamp)
- [ ] Handle LLM timeout/failure gracefully

---

### 🔵 Phase 2 — AI Enhancements
- [ ] Prompt template with filename, row sample
- [ ] Anomaly types (date mismatch, malformed, missing fields)
- [ ] Confidence score and type in response
- [ ] JSON schema validation before return

---

### 🟣 Phase 3 — Partner Integration API
- [ ] Secure API for partners to POST/upload files
- [ ] Rate limits and token auth (JWT or API key)
- [ ] Optional: Multi-tenant tagging per request
- [ ] Standard OpenAPI docs (Swagger/Postman) with vuepress

---

### 🟤 Phase 4 — Compliance & Deployment
- [ ] Auto-delete files after processing
- [ ] Mask PII in logs (account numbers, IFSC)
- [ ] GDPR: Audit logs only, no file retention
- [ ] Configurable retention and audit logging
- [ ] CI pipeline with test/build/deploy

---

## 📄 LLM JSON Output Sample

```json
{
  "anomalies": [
    {
      "row": 4,
      "type": "Date Mismatch",
      "confidence_score": 0.92,
      "issue": "Row date is '2025-06-01' while filename is 'April_2025.csv'",
      "suggested_fix": "Change date to '2025-04-01' or move row to correct file"
    },
    {
      "row": 12,
      "type": "Malformed Row",
      "confidence_score": 0.87,
      "issue": "Amount column missing",
      "suggested_fix": "Insert missing amount or remove row"
    }
  ],
  "meta": {
    "filename": "April_2025.csv",
    "rows_checked": 120,
    "anomaly_count": 2,
    "llm_model": "gpt-3.5-turbo",
    "tokens_used": 154
  }
}
```

### Folder Structure
```
bank-analyzer/
├── springboot-app/              # Java ingestion service
│   ├── controller/
│   ├── service/
│   └── resources/
│
├── python-llm-api/              # Python LLM detection 
│   ├── app.py
│   ├── llm_engine.py
│   ├── prompts/
│   └── model_fallback/
│
├── audit-logs/
├── docker-compose.yml
└── README.md
```