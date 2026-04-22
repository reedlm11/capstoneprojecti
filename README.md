# capstoneprojecti
Capstone Project: The Agentic Career Coach (ACC)

# Multi-Agent MCP Internship Pipeline System

## Overview
This project implements a **multi-agent system** for managing internship and job searches using **MCP (Model Context Protocol) concepts**.

The system consists of:
- A **Supervisor Agent (Lead Orchestrator)** – user-facing, interprets requests
- A **Career Specialist Agent (Worker Agent)** – performs backend operations
- MCP-style tools deployed via a **FastAPI backend on Cloud Run**

---

## System Architecture

User → Supervisor Agent → Career Specialist → MCP Tools → Cloud Run API → Job Data

### Key Concepts:
- **Prompt-based routing**: Supervisor interprets user intent
- **A2A (Agent-to-Agent) handoff**: Supervisor delegates tasks to Specialist
- **Tool-based execution**: Specialist calls backend APIs
- **MCP simulation**: JSON-RPC + SSE concepts modeled using REST

---

## MCP Tools (Backend API)

### 1. fetch_jobs
- **Method:** GET  
- **Endpoint:** `/fetch_jobs`  
- **Description:** Retrieves job/internship listings  
- **Supports filters:** role, location, keyword  

---

### 2. sync_pipeline
- **Method:** POST  
- **Endpoint:** `/sync_pipeline`  
- **Description:** Adds a new job to the pipeline  

---

## Agent Design

### Supervisor Agent (Lead Orchestrator)
- Handles user input  
- Determines user intent  
- Delegates tasks to Career Specialist  
- Returns final response  

### Career Specialist (Worker Agent)
- Executes backend tasks  
- Calls MCP tools:
  - `fetch_jobs`
  - `sync_pipeline`

---


---

## Running the Project

### 1. Install Dependencies

```bash
pip install -r requirements.txt
----

uvicorn main:app --reload

-------------------------------------------

gcloud run deploy acc-mcp-server \
  --source . \
  --region us-east1 \
  --allow-unauthenticated
------------------------------------------------------------------

python3 agent_orchestration.py

------------------------------------------------------------------

https://acc-mcp-server-420216438094.us-east1.run.app/

---------------------------------------------------------------
###API Usage

GET /fetch_jobs

POST /sync_pipeline

{
  "title": "AI Intern",
  "location": "Remote",
  "company": "OpenAI",
  "keywords": "ml, python"
}



