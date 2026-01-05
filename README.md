# Transaction Ledger Service

A **production-grade backend service** written in **Go** that implements a **financial transaction ledger**
using **double-entry accounting principles**.  
This project is designed to follow **real-world fintech backend practices**, focusing on correctness,
consistency, and scalability rather than UI.

> 🚀 Backend-only project (Frontend can be generated later using Swagger / AI tools)

---

## 📌 Why This Project

This project is built as a **learning + portfolio project** to:
- Learn Go in a **real production context**
- Understand how **financial systems** are built
- Practice **clean architecture**
- Build something that **backend interviewers respect**

---

## 🧠 Core Concepts Implemented

- Double-entry accounting (Debit & Credit)
- Immutable ledger (append-only)
- ACID-compliant database transactions
- Idempotent APIs (planned)
- Clean architecture (API → Service → Repository)
- Event-driven design (RabbitMQ – planned)

---

## 🏗️ High-Level Architecture

Client / Swagger UI / AI-generated Frontend
|
REST API (chi)
|
Service Layer (Business Logic)
|
Repository Layer (SQL / pgx)
|
PostgreSQL
|
Message Broker (RabbitMQ)



### Architecture Principles

- **Ledger writes are synchronous** and handled inside a single DB transaction
- **PostgreSQL is the source of truth**
- Message broker is used only for **secondary concerns**
  - Audit logs
  - Notifications
  - Analytics
- Ledger correctness **never depends on messaging**

---

## 🛠️ Tech Stack

| Layer | Technology |
|-----|-----------|
| Language | Go (1.22+) |
| HTTP Framework | chi |
| Database | PostgreSQL |
| DB Driver | pgx |
| Migrations | golang-migrate |
| Messaging | RabbitMQ (planned) |
| API Docs | OpenAPI / Swagger |
| Logging | Zap |
| Containerization | Docker |
| CI/CD | GitHub Actions (planned) |

---

## 📂 Folder Structure

ledger-service/
│
├── cmd/
│ └── server/
│ └── main.go
│ # Application entry point
│
├── internal/
│ ├── api/
│ │ # HTTP handlers (request/response layer)
│ │
│ ├── service/
│ │ # Business logic (transaction rules, validations)
│ │
│ ├── repository/
│ │ # Database access layer (SQL queries, transactions)
│ │
│ ├── model/
│ │ # Domain models (Account, LedgerEntry, Transaction)
│ │
│ ├── middleware/
│ │ # Custom HTTP middleware
│ │
│ └── config/
│ # Configuration loading (env, flags)
│
├── migrations/
│ # Database migration files (planned)
│
├── docker-compose.yml
│ # Local infrastructure setup (planned)
│
├── Dockerfile
│ # Container build (planned)
│
├── go.mod
└── README.md


### Folder Design Philosophy

- `cmd/` → Application entry points
- `internal/` → Enforces **clean boundaries**
- `service/` → No HTTP or DB logic
- `repository/` → No business rules
- Each layer has **one responsibility**

This structure matches **real production Go services**.

---

## ▶️ Running the Service Locally

### Prerequisites
- Go 1.22+
- Git

### Start the server
```bash
go run cmd/server/main.go
