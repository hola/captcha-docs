---
layout: default
title: scrape_test / sbr_test Scripts
parent: Documentation
nav_order: 5
---

# scrape_test / sbr_test Scripts

`scrape_test` and `sbr_test` are two internal scripts used to stress-test and improve the CAPTCHA solver by mass-collecting image data when SR is low.

---

## 1. scrape_test (The Mass Requester)

This is a straightforward tool designed to "hammer" a site with requests to trigger CAPTCHA challenges.

**When to Use**: CAPTCHA appears immediately on URL.

### Function
It allows for high-volume automated requests without complex user logic.

### Workflow

**Step 1**: Download a list of target URLs (e.g., product pages).

```bash
scrape_test urls -l 10000 -d homedepot.com -g pdp --days 1 > homedepot_pdp.txt
```

**Step 2**: Use the run command to send requests (e.g., 10 times) to those URLs.

```bash
scrape_test run -u './homedepot_pdp.txt' -g scrape_r.js -t -B 'output' --clear -n 10
```
