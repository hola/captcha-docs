---
layout: default
title: Navigation & Terminology
parent: Documentation
nav_order: 1
---

# Navigation & Terminology

The following core components represent the infrastructure used to manage and monitor the CAPTCHA solving ecosystem.

- **Datasets**: Collections of images used to "teach" the system to solve challenges.
- **Models**: The trained files that recognize objects (e.g., finding a bicycle in a grid).
- **Solvers**: The code-based logic built on top of models to execute the final solution.
- **Simulation**: A way to "debug" or test how the system will react to a specific image before it goes live or test if production is working properly.
- **Sessions**: A real-time audit trail and history of all CAPTCHA solving attempts, storing historical data for the last 4 days only.
- **Manual**: A tool used to prove if an issue is caused by the AI or the client's IP reputation. If a human cannot solve it manually on the dashboard, the problem is likely that the client's IP is blacklisted by Google or hCaptcha.

## Quick Reference Table

| Term | Functional Description |
| :--- | :--- |
| **Datasets** | Collections of images for system training. |
| **Models** | Recognition files for object identification. |
| **Solvers** | Execution logic built on models. |
| **Simulation** | Pre-deployment debugging and production testing. |
| **Sessions** | Live audit trail with 4-day data retention. |
| **Manual** | Diagnostic tool for AI vs. IP reputation testing. |
