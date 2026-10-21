# Smart Mini-Dairy Dashboard

**Full-stack operations dashboard | Python · FastAPI · SQLAlchemy · SQLite · Jinja2**

[Source and setup](https://github.com/karna012/SmartMiniDairyDashboard) · [Back to profile](../README.md)

## Problem and application

Connect herd profiles, milking activity, station status and feed inventory so
operators can review them in one interface. Beyond displaying rows, the app
enforces rules around milking cycles and station conflicts and supports bulk
CSV/XLSX imports.

## Architecture

```text
Forms / station payloads / imports
                ↓
        FastAPI validation
                ↓
   Domain rules + SQLAlchemy models ↔ SQLite
                ↓
       Jinja2 reports / dashboard
```

## Code worth reviewing

| Area | Code | What it demonstrates |
| --- | --- | --- |
| Request validation | [app.py](https://github.com/karna012/SmartMiniDairyDashboard/blob/main/app.py) | Normalization, imports, form processing and report routes |
| Domain logic | [models.py](https://github.com/karna012/SmartMiniDairyDashboard/blob/main/models.py) | `record_station_session`, milking-cycle checks, relational models and inventory queries |
| Business-rule tests | [test_business_rules.py](https://github.com/karna012/SmartMiniDairyDashboard/blob/main/tests/test_business_rules.py) | Duplicate-cycle rejection, conflicting stations and feed calculations |
| Frontend | [templates](https://github.com/karna012/SmartMiniDairyDashboard/tree/main/templates) · [theme assets](https://github.com/karna012/SmartMiniDairyDashboard/tree/main/static) | Server-rendered UI and responsive dark/light styling |
| Example imports | [static/samples](https://github.com/karna012/SmartMiniDairyDashboard/tree/main/static/samples) | Sample CSV/XLSX input contracts |

## Decisions and trade-offs

- Put operational checks in the data/domain layer rather than relying on form
  validation alone.
- Keep the lightweight deployment server-rendered with SQLite persistence.
- Support both individual entry and file-based import workflows.
- Use temporary or disposable data when testing; the existing test suite writes
  sample records and must not be run against a production database.

## Status and next engineering steps

The application has known authentication and API-protection limitations,
documented in its [security notes](https://github.com/karna012/SmartMiniDairyDashboard#security-status).
Harden those boundaries before unrestricted production access. The public export
excludes live records, uploaded photos and production configuration.
