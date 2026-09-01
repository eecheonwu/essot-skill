# EIP SSOT Sync Orchestrator Skill

This skill is an orchestrator designed to maintain parity between your local codebase's Single Source of Truth (SSOT) and the Engineering Intelligence Platform (EIP).

## Overview

The `eip-ssot` skill acts as an intelligent bridge, ensuring that documentation, architecture changes, and artifacts within your local repository are seamlessly synchronized with the centralized EIP Web App. It enforces a strict, two-step synchronization workflow to guarantee data integrity.

## Connection to EIP and `eip-mcp-server`

This skill relies on the **Model Context Protocol (MCP)** to interact with the Engineering Intelligence Platform.

*   **Engineering Intelligence Platform (EIP):** The centralized web application that tracks your project's architecture, documentation, and engineering artifacts.
*   **`eip-mcp-server`:** A specialized MCP server running locally that securely connects the AI agent to the EIP Web App. It exposes tools like `synchronize_ssot` to handle the actual data transfer and API communication.
*   **The Skill (`eip-ssot`):** Defines the workflow and rules for the AI agent. It instructs the agent on *what* data to collect locally, *how* to organize it, and *when* to invoke the `eip-mcp-server` to push the data to EIP. 

## Workflow

When triggered (e.g., by asking the agent to "update SSOT" or "synchronize SSOT"), the skill executes the following process:

1.  **Verification:** Checks for the existence of a local `ssot/` directory. (If missing, it will halt and notify you).
2.  **Local Update:** Analyzes recent codebase changes and updates the relevant artifacts within the local `ssot/` directory. It critically ensures the `ssot.yaml` tracking file is kept up to date.
3.  **Synchronization:** After local updates are complete, the skill calls the `synchronize_ssot` tool provided by the `eip-mcp-server` to push the local state to the EIP Web App.
4.  **Reporting:** Generates a structured summary report detailing the updated files and the status of the EIP synchronization.

## Prerequisites

To use this skill successfully, ensure:

1.  Your workspace contains a local `ssot/` directory.
2.  The `eip-mcp-server` is properly configured and active in your MCP environment.
