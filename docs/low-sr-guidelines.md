---
layout: default
title: Low Success Rate Guidelines
parent: Documentation
nav_order: 4
---

# CAPTCHA Low SR (Success Rate) Guidelines

Solvers cannot improve on their own; they require fresh data (images) to handle new or changing CAPTCHA variations.

## Why SR Might Drop

- **Inherent AI Error**: Neural networks will occasionally make mistakes.
- **New Variations**: CAPTCHA providers frequently update puzzles; if not "taught" the variation, SR will plummet.
- **Environmental Blocks**: Success rates may drop due to network-level "Rate Limiting" unrelated to AI accuracy.

## Before Opening a Ticket

{: .warning }
> Do not open tickets simply because the SR is low; ensure enough data exists to fix the problem first.

### The Data Collection Process

- **Data Collection (The 200-300 Rule)**: Approximately 200 to 300 samples of the failing challenge are needed before a solver can be improved.

- **Identifying the Challenge**: Locate the task in the Challenges tab. A high Unsolved count confirms the model needs retraining.

- **Escalation**: Once 300+ samples are collected, open a ticket in Monday.com. Developers will use the Create Dataset feature to retrain the model and push it to 100% success rate.

### Key Takeaway

{: .important }
> Always collect sufficient data (200-300 samples) before escalating SR issues. Without enough training data, the AI cannot improve.
