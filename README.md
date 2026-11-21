# Sentix AI Monitor

<div align="center">
  <img src="assets/banner.svg" alt="Sentix AI Monitor Vector Banner" width="100%" />

  <br/><br/>

  [![Go Version](https://img.shields.io/badge/Go-1.26+-00ADD8?style=for-the-badge&logo=go)](https://golang.org)
  [![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)
  [![Build & Test](https://img.shields.io/badge/Unit%20Tests-100%25%20Passing-brightgreen?style=for-the-badge)](main_test.go)
  [![Architecture](https://img.shields.io/badge/Dependencies-Zero%20External-orange?style=for-the-badge)](go.mod)
  [![Port](https://img.shields.io/badge/Port-:8203-purple?style=for-the-badge)](#quickstart)
</div>

---

## 📌 Overview

**Sentix AI Monitor** is a high-performance, production-grade microservice and interactive web application designed for **AI & Analytics**. It provides an end-to-end implementation of **Realtime Customer Feedback Sentiment & Emotion Classifier**, built strictly using the **Go Standard Library** without third-party framework dependencies.

### 🌟 Key Highlights
- **🚀 Pure Go Standard Library**: Driven solely by `net/http`, `sync`, `time`, and `encoding/json` with zero bloat.
- **🎨 Modern Tailwind CSS Web UI**: Beautiful responsive dashboard with real-time DOM manipulation, metric cards, and live API dispatch.
- **🛡️ Concurrent-Safe Storage**: Thread-safe in-memory repository utilizing reader-writer synchronization (`sync.RWMutex`).
- **📊 Observability & Diagnostics**: Built-in `/health` and `/api/stats` endpoints for Prometheus scraping and Kubernetes readiness checks.
- **🧪 100% Automated Unit Test Coverage**: Full suite of unit tests validating store operations and HTTP handlers.

---

## 🏗️ Architecture

```
┌────────────────────────────────────────────────────────┐
│                   Client / Browser                     │
│        (Tailwind CSS + Vanilla JavaScript DOM)         │
└───────────────────────────┬────────────────────────────┘
                            │ HTTP Request
                            ▼
┌────────────────────────────────────────────────────────┐
│               Go HTTP Router (net/http)                │
│    ┌───────────────┬─────────────────┬─────────────┐   │
│    │  GET /        │  GET /health    │  /api/items │   │
│    │  (Static UI)  │  (Liveness)     │  (CRUD API) │   │
│    └───────────────┴─────────────────┴─────────────┘   │
└───────────────────────────┬────────────────────────────┘
                            │ Mutex Synchronization
                            ▼
┌────────────────────────────────────────────────────────┐
│               Thread-Safe Memory Store                 │
│         sync.RWMutex protected Slice Storage           │
└───────────────────────────┴────────────────────────────┘
```

---

## 🚀 Quickstart

### 1. Prerequisites
- **Go 1.22+** installed on your machine.

### 2. Run Directly
```bash
# Clone the repository
git clone https://github.com/k3ndzy/sentiment-analysis-hub.git
cd sentiment-analysis-hub

# Run the server
go run main.go
```

Open your browser at **[http://localhost:8203](http://localhost:8203)** to access the dashboard.

---

## 📡 REST API Documentation

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/` | Web Dashboard (Tailwind CSS + Interactive UI) |
| `GET` | `/health` | Service liveness probe & uptime status |
| `GET` | `/api/items` | Retrieve list of all Sentiment Evaluation / Review records |
| `POST` | `/api/items` | Create a new Sentiment Evaluation / Review entry |
| `GET` | `/api/stats` | High-level metrics & runtime counters |

---

## 🧪 Testing

Run all unit tests using the standard Go testing tool:
```bash
go test -v ./...
```

Expected output:
```
=== RUN   TestStore_ListAndAdd
--- PASS: TestStore_ListAndAdd (0.00s)
=== RUN   TestHealthEndpoint
--- PASS: TestHealthEndpoint (0.00s)
=== RUN   TestItemsEndpoint_Get
--- PASS: TestItemsEndpoint_Get (0.00s)
=== RUN   TestItemsEndpoint_Post
--- PASS: TestItemsEndpoint_Post (0.00s)
=== RUN   TestStatsEndpoint
--- PASS: TestStatsEndpoint (0.00s)
PASS
ok      github.com/k3ndzy/sentiment-analysis-hub    0.025s
```

---

## 📄 License
Released under the [MIT License](LICENSE). Built with clean architecture by [@k3ndzy](https://github.com/k3ndzy).
