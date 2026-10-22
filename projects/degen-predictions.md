# Degen Predictions

**Full-stack sports analytics | Python · Flask · SQL · Jinja2 · JavaScript**

[Live application](https://degenpredictions.com) · [Public source](https://github.com/karna012/degen-predictions) · [Back to profile](../README.md)

## Problem and application

Bring match information and model outputs into a browsable sports website,
alongside administrative tools and result analysis. The engineering work spans
data preparation, prediction artifacts, Python routes and a browser interface.

## Architecture

```text
Sports data → offline preparation / training → saved data and models
                                                   ↓
Browser ← Jinja2 / JavaScript ← Flask routes ← prediction modules
                                   ↕
                         SQLite analytics / feedback
```

The live website is hosted on a Linux server, with heavier processing
kept on a separate machine. The **public repository is an earlier snapshot**: it still
contains legacy investment modules, EC2 deployment scripts and DynamoDB account
storage. These are not a claim about the current live deployment.

## Code worth reviewing

| Area | Code | What it demonstrates |
| --- | --- | --- |
| Application integration | [webapp/app.py](https://github.com/karna012/degen-predictions/blob/master/webapp/app.py) | Flask routes, template rendering and feature integration |
| SQL reporting | [webapp/analytics.py](https://github.com/karna012/degen-predictions/blob/master/webapp/analytics.py) | Visit storage, aggregation and query-driven reports |
| Model evaluation | [scripts/backtest_pl.py](https://github.com/karna012/degen-predictions/blob/master/scripts/backtest_pl.py) | Chronological split and separate in-sample / holdout labels |
| Confidence analysis | [scripts/calibrate_sports_confidence.py](https://github.com/karna012/degen-predictions/blob/master/scripts/calibrate_sports_confidence.py) | Confidence-threshold evaluation against held-out results |
| Regression coverage | [webapp/tests](https://github.com/karna012/degen-predictions/tree/master/webapp/tests) | Route, sports-data, analytics and regression tests |

## Decisions and trade-offs

- Separate expensive training work from the web-serving machine.
- Reuse saved data and model artifacts in the application; freshness and upstream
  availability remain operational concerns.
- Keep model evaluation distinct from a guaranteed-outcome claim. Predictions
  are uncertain; this portfolio does not claim a betting return or accuracy rate.
- The large Flask application file is an obvious future refactoring target.

## Status and limitations

The public snapshot is inspectable but not a one-command reproduction of the
live service. Models, data, provider configuration and historical deployment
assumptions require review. See the repository's
[security boundary](https://github.com/karna012/degen-predictions/blob/master/SECURITY.md).
No production credentials or live account databases are included.
