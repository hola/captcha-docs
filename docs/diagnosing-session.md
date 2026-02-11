---
layout: default
title: Diagnosing a Session
parent: Documentation
nav_order: 3
---

# Diagnosing a Session

Follow these instructions to audit failed CAPTCHA attempts through the Sessions tab.

## 1. Accessing and Filtering Sessions

- **Locate the Dashboard**: Open the Sessions tab to view the live audit trail of all CAPTCHA attempts.
- **Filter for the Client**: Use the Hostname or URL filter (e.g., `www.reddit.com`) or the Session ID to find specific instances.
- **Identify the Failed Run**: Look for sessions marked with a yellow Pending or red Error status.

## 2. Expanding the Debug Info

- **Drill Down**: Click the "+" icon next to the Session ID to reveal detailed DEBUG INFO.
- **Review Sequential Steps**: Chronologically examine the interaction from Step 0 through the final step.
- **Time Audit**: Each step records the exact duration spent by the AI versus the system interaction time.

## 3. Visual Verification

- **Check the Initial State**: Review the Initial screenshot to ensure the grid rendered correctly. Blank screens suggest network errors or blocked pop-ups.
- **Analyze AI Intent**: Open the final screenshot of a step that overlays the AI's intended click points and movements.
- **Confirm Accuracy**: Compare clicked points against the Actions list. If the AI clicked correctly but failed, the issue is likely client IP Reputation.

## 4. Analyzing Error Categories

- **Environmental Blockers**: Notify the client if "Cookie Consent" banners or broken layouts are blocking the grid.
- **Timeouts**: Hard Timeouts or Resolve Failed errors usually mean the provider stopped responding or suspected bot behavior.
- **Unrecognized Tasks**: Complex tasks the system hasn't seen before may require new dataset collection and model training.

## 5. Taking Action

- **Manual Validation**: Use the Manual button to solve the CAPTCHA in real-time to check if the AI is failing. If even a human cannot pass it, the issue is a blacklisted IP.
- **Escalation**: For recurring technical bugs, create a ticket in Monday.com with the Session ID and reasoning log screenshots.
