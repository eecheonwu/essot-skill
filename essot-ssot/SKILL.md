---
name: essot-ssot
description: Specialized orchestrator to synchronize the local ssot/ directory with the codebase and update the Engineering Intelligence Platform (ESSOT) Web App via the essot-mcp-server. Use when asked to update SSOT or synchronize SSOT.
---

# ESSOT SSOT Sync Orchestrator

This skill orchestrates the synchronization of the Single Source of Truth (SSOT). It ensures that the local `ssot/` directory is updated first, and subsequently updates the ESSOT Web App using the `essot-mcp-server`.

## Pre-requisites

Before starting any synchronization or update task, you **MUST** verify the existence of the local `ssot/` directory in the current workspace. 
If the `ssot/` directory is not found, you must halt execution and explicitly flag a message to the user exactly as follows:
**"local SSOT is not found. Local SSOT required to continue"**

## Workflow

When asked to update SSOT or synchronize SSOT, strictly follow these steps in order:

### 1. Update the Local SSOT Directory
- Gather updates from the codebase (e.g., source code changes, architecture changes).
- Apply these updates to the artifacts and documentation within the local `ssot/` directory.
- **IMPORTANT**: You must also update the `ssot.yaml` file in the `ssot/` directory accordingly to track any of these updates.
- **Rule**: The local `ssot/` directory MUST be updated **first** before making any external calls to the ESSOT Web App.

### 2. Synchronize with the ESSOT Web App
- Once the local `ssot/` directory is updated and accurate, call the `essot-mcp-server`.
- Use the `synchronize_ssot` tool within the `essot-mcp-server` to push the content from the local `ssot/` directory to the ESSOT Web App.

### 3. Generate a Report
- At the end of the task, always generate a structured report detailing what was done.
- The report should include:
  - What specific files or contents were updated in the local `ssot/` directory.
  - The status/result of the `synchronize_ssot` tool call.
  - A brief summary for the user to review.
