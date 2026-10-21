# Xstreem Car Care

**Full-stack business application | Python · FastAPI · SQL / SQLite · JavaScript · Ollama**

[Source and setup](https://github.com/karna012/Xstreem_car_care) · [Back to profile](../README.md)

## Problem and application

A car-care business needs a customer-facing website and an administrative view
of bookings, vehicles, services, memberships and payment records. This project
connects those workflows to a Python API and relational storage, with a local AI
chatbot for business questions.

## Architecture

```text
Customer / admin interface → FastAPI → SQLite
                               ├── HTTP client → local Ollama
                               └── WhatsApp integration
```

## Code worth reviewing

| Area | Code | What it demonstrates |
| --- | --- | --- |
| API and UI boundary | [main.py](https://github.com/karna012/Xstreem_car_care/blob/main/main.py) | Pydantic request models, CRUD routes and template rendering |
| Relational operations | [database.py](https://github.com/karna012/Xstreem_car_care/blob/main/database.py) | Customers, vehicles, bookings and payments; joins and schema maintenance |
| AI integration | [ai_service.py](https://github.com/karna012/Xstreem_car_care/blob/main/ai_service.py) | Reusable async HTTP client, timeouts, local model configuration and business context |
| Browser interface | [templates](https://github.com/karna012/Xstreem_car_care/tree/main/templates) | Customer and admin views |
| External messaging | [whatsapp_service.py](https://github.com/karna012/Xstreem_car_care/blob/main/whatsapp_service.py) | Provider integration configured through environment variables |

## Decisions and trade-offs

- SQLite keeps the local application simple; higher write concurrency would
  require measurement and a database deployment decision.
- A locally hosted model avoids making an external AI API a prerequisite, but
  adds local model setup, resource usage and response-time concerns.
- Business records and configuration are separate from the public source.

## Status and next engineering steps

The repository contains application code, not a security-hardened release.
Before untrusted deployment, review authorization across all routes, replace
development defaults, protect customer data and verify webhook requests.
Automated API tests and reproducible dependency management would strengthen the
project; no test-pass or production-readiness claim is made here.
