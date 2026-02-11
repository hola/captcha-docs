---
layout: default
title: The Sessions Flow
parent: Documentation
nav_order: 2
---

# The Sessions Flow

The end-to-end lifecycle of a single CAPTCHA-solving attempt, from detection to final verification, is tracked and audited within the Sessions tab.

## The Complete Lifecycle

1. **Detection & Initialization**: The system identifies a CAPTCHA challenge on a target URL. A unique Session ID is generated, and the initial state of the page is captured as a screenshot.

2. **Visual Parsing (Step-by-Step)**: The solver breaks the interaction into discrete "Steps" (Step 0, Step 1, etc.).

3. **Screenshot Captures**: The system records the Initial state, any Cropped grids, and the final overlay.

4. **AI Reasoning**: For each step, the AI (e.g., GPT-5 Nano) processes the visual data to decide on a strategy.

5. **Action Execution**: The system sends a series of low-level commands to the browser, such as `Mouse_move`, `Click`, and specific `Timeout` delays.

6. **Verification & Completion**: Once the AI identifies the correct objects, it submits the result. The session status moves from Pending to Done if successful, or Error if it fails due to a timeout or blocked layout.

## Success Metrics in the Flow

A healthy session typically hits these benchmarks:

- **Step Count**: 2–5 steps for standard image grids.
- **AI Time**: Ideally under 10 seconds per step for solvers like GPT-5 Nano.
- **Status**: Successful transition to Done within 1–2 minutes total.

### Examples

**Example 1: Perfect Successful Run**
- **Duration**: 17 seconds
- **Steps**: 4 steps
- **Time per step**: ~2 seconds

**Example 2: Failed Run**
- **Duration**: 1 minute 20 seconds
- **Steps**: 4 steps
- **Time per step**: ~5 seconds
