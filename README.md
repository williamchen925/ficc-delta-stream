# FICC Delta-Stream: Real-Time Options Analytics Engine

**FICC Delta-Stream** is a high-throughput, low-latency data pipeline engineered to ingest multi-exchange derivatives order books, compute intense numerical options operations (Implied Volatility and Option Greeks) in real-time, and deliver structured volatility surfaces to proprietary trading desks and quantitative funds.

* **Course:** Big Data Systems (Spring 2026) — Final Project
* **University:** National Taiwan University (NTU)
* **Student ID:** B12703102
* **Author Name:** 陳泓宇
* **Live Demo URL:** https://ficc-delta-stream.streamlit.app

---

## 🏗️ Architecture Overview

The pipeline is structured using decoupled, horizontally scalable big data paradigms:
1. **Ingestion Layer:** Asynchronous WebSocket handlers connection pooling to derivatives exchanges (e.g., Deribit API).
2. **Processing Layer:** Vectorized Black-Scholes-Merton mathematical processing engine running a localized root-finding Newton-Raphson optimization loop to calculate Implied Volatility, Delta, and Gamma.
3. **Storage Layer:** Dual-storage topology featuring an in-memory transactional cache (Redis) for immediate sub-millisecond state updates and a structured historical time-series ledger (PostgreSQL via TimescaleDB).
4. **Delivery Layer:** High-frequency RESTful JSON APIs structured through FastAPI coupled with a cloud-hosted frontend Streamlit diagnostic dashboard interface.

---

## 🚀 Quick Start (Local Execution)

Ensure you have **Docker**, **Docker Compose**, and **Python 3.10+** installed.

### Step 1: Spin Up Infrastructure Services (Database & Cache Containers)
```bash
docker compose up -d
