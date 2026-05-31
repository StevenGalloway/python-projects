# Python Projects

A collection of Python applications demonstrating end-to-end engineering across conversational AI, recommendation systems, algorithmic trading, and data automation. Projects are built with production considerations in mind — clean separation of concerns, testable design, and operational readiness.

---

## What This Repository Demonstrates

- Full-stack Python application development (FastAPI, LangGraph, Streamlit)
- Applied ML integration: intent classification, NLP, content-based recommendation
- Production patterns: circuit breakers, rate limiting, retry logic, structured logging
- Data automation: bulk file processing, enrichment pipelines, scoring engines
- API design and real-time model serving
- Algorithmic signal generation and financial data analysis

---

## Focus Areas

- Conversational AI and agent-based workflows
- Content-based recommendation systems
- Algorithmic trading and financial signal scoring
- Data enrichment and automation pipelines
- API development and real-time model serving
- Structured logging, observability, and operational readiness

---

## Repository Structure

- `spa-booking-chatbot/` — AURA: LangGraph-based conversational AI for spa and wellness booking
- `recommendation-engine/` — ANIMATCH: TF-IDF content-based anime recommendation engine
- `TradeBot/` — Pre-market stock screener with VWAP, gap, and volume scoring
- `AddStateToLeads-Project/` — Bulk lead enrichment and regional distribution automation

---

## Featured Projects

### [AURA - Spa Booking Chatbot](https://github.com/StevenGalloway/spa-booking-chatbot)
Conversational AI platform for wellness service booking built on a **LangGraph** state machine with three sequential nodes: `intent_analysis → data_retrieval → appointment_trigger`. Intent classification uses a two-tier strategy: a **DistilBERT** model fine-tuned on 240 labeled wellness-booking examples, backed by keyword override rules for safety-critical intents (cancel, reschedule) that must never be misrouted. Supports booking, rescheduling, cancellation, pricing inquiry, and appointment status with full multi-turn conversation state.

**Stack:** Python, FastAPI, LangGraph, DistilBERT (HuggingFace), Streamlit\
**Production patterns:** JWT auth, request ID tracking, structured JSON logging, CORS configuration, environment-based settings, health probes

---

### [ANIMATCH — Anime Recommendation Engine](https://github.com/StevenGalloway/recommendation-engine)
Content-based recommendation engine using TF-IDF vectorization and cosine similarity across a dataset of anime titles. Implements a three-tier search strategy: exact title match → genre/type similarity fallback → external Jikan API integration with circuit breaker protection. The cosine similarity matrix is computed once at startup and held in memory for low-latency serving.

**Stack:** Python, FastAPI, scikit-learn, Next.js (TypeScript)\
**Production patterns:** Circuit breaker (3-failure threshold, 60s reset), tenacity retry with exponential backoff, per-IP rate limiting, Prometheus metrics, Docker Compose

---

### [Stock Trade Bot](https://github.com/StevenGalloway/TradeBot)
Pre-market stock screening system that generates ranked buy signals by combining three weighted scoring signals: VWAP proximity (50%), premarket gap analysis (25%), and volume surge detection (25%). Each signal is computed independently, merged into a unified scored and ranked output, and delivered via email alert.

**Stack:** Python, Pandas, yfinance\
**Capabilities:** VWAP calculation and scoring, premarket gap analysis, volume surge detection, weighted signal combination, ranked CSV output, email notification

---

### [Leads Enrichment & Distribution](https://github.com/StevenGalloway/AddStateToLeads-Project)
Bulk data enrichment automation for sales lead spreadsheets. Processes batches of XLSX files, enriches each lead record with state data via city-to-state lookup against the SimpleMaps US cities dataset, and supports regional sorting and distribution for downstream use.

**Stack:** Python, openpyxl, csv\
**Capabilities:** Bulk XLSX batch processing, city-to-state lookup, state enrichment, regional organization and sorting

---

## Tools & Stack

| Capability | Tools |
|---|---|
| Web Frameworks | FastAPI, Streamlit |
| AI / NLP | LangGraph, DistilBERT (HuggingFace), scikit-learn (TF-IDF, cosine similarity) |
| Data Processing | Pandas, NumPy, openpyxl |
| Financial Data | yfinance |
| API Clients | httpx, tenacity (retry + backoff), circuit breaker patterns |
| Observability | Structured JSON logging, Prometheus, request ID tracking |
| Auth & Security | JWT, API key validation, CORS |
| Testing | pytest, httpx (API tests), conftest fixtures |
| Frontend | Next.js (TypeScript), Streamlit |
| Infrastructure | Docker, Docker Compose |

---

## Design Principles

- **Production-oriented:** structured logging, health probes, environment-based configuration, and graceful degradation are standard across projects — not afterthoughts
- **Testable by design:** pytest suites with synthetic in-memory data and mocked external dependencies keep tests fast and environment-independent
- **Separation of concerns:** tools, workflows, API routing, and configuration are clearly layered and independently testable
- **Operational readiness:** circuit breakers, rate limiting, and retry logic are applied wherever external dependencies are involved
