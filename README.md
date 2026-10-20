# Creation of Intelligent Bug Diagnosis Platform with Fix Recommendation Assistance

## Overview

The **Creation of Intelligent Bug Diagnosis Platform with Fix Recommendation Assistance** is an AI-powered application designed to help developers understand software defects, identify potential root causes, detect similar historical issues, and generate actionable fix recommendations.

Built with Streamlit and a multi-agent analysis pipeline, the application accepts bug reports and stack traces as text or uploaded log files. It combines AI-based analysis with semantic retrieval from a historical defect knowledge base to provide structured diagnostic results.


## Core Features

### 1. Bug Submission and Analysis
- Accepts pasted bug reports, error messages, stack traces, and uploaded `.txt` or `.log` files.
- Generates a structured analysis of the submitted defect.
- Displays key findings, including severity, priority, affected component, error type, and failure location.

### 2. Multi-Agent Bug Diagnosis
The application uses five specialized agents:

- **Triage Agent:** Assesses defect severity, priority, and component.
- **Log Analysis Agent:** Examines error information and identifies relevant failure details.
- **Root Cause Agent:** Produces a root-cause hypothesis using available evidence and retrieved historical bugs.
- **Duplicate Detection Agent:** Checks for potentially similar previous submissions.
- **Remediation Agent:** Generates recommended fixes, implementation steps, code examples where available, validation steps, and prevention guidance.

### 3. Historical Defect Knowledge Base
- Uses the `all-MiniLM-L6-v2` sentence-transformer model to represent text as embeddings.
- Retrieves semantically similar historical defects using cosine similarity over saved embeddings.
- Uses retrieved records to support root-cause analysis and fix recommendations.
- Allows the retrieval depth to be adjusted when analyzing a submission.

### 4. Analytics Dashboard
- Presents defect-related statistics and submission activity.
- Supports analysis of stored submissions and remediation records.
- Includes monthly activity filtering and visual summaries of defect trends.

### 5. Knowledge Base and Resolution Tracking
- Displays historical knowledge base records and summary statistics.
- Tracks remediation records and their resolution status.
- Supports adding confirmed fixes to the knowledge base through the implemented knowledge-growth workflow.

### 6. User Interface and Authentication
- Provides a Streamlit interface with separate Dashboard, Submit Bug, Analytics Dashboard, Knowledge Base, About the App, and User Guide pages.
- Includes user registration and login functionality.
- Records submission metadata and analysis results using the application's configured storage.

## How the Application Works

1. **Input:** The user pastes a bug report or uploads a log file.
2. **Triage and log analysis:** The application identifies important defect characteristics.
3. **Historical retrieval:** The system searches for semantically similar historical bugs.
4. **Root-cause analysis:** The root-cause agent uses the analysis results and retrieved evidence.
5. **Duplicate detection:** The application checks for potentially similar submissions.
6. **Remediation:** The remediation agent generates a suggested solution and validation guidance.
7. **Storage and display:** The results are saved and presented in the interface, subject to successful execution of the relevant storage operations.

## Technology Stack

| Area | Technology |
|---|---|
| Programming language | Python |
| User interface | Streamlit |
| Embedding model | Sentence Transformers — `all-MiniLM-L6-v2` |
| Similarity search | Cosine similarity using scikit-learn |
| Data processing | pandas, NumPy |
| Text chunking | LangChain text splitters |
| Database | SQLite |
| Agent orchestration | Custom Python agent classes |
| Language model | `openai/gpt-oss-120b`, as configured for the current application |
| Knowledge retrieval | Retrieval-Augmented Generation (RAG) using saved embeddings and historical metadata |

**Implementation note:** ChromaDB was installed and evaluated during development, but the current retrieval implementation uses saved embeddings and in-memory cosine similarity rather than ChromaDB as its active vector search backend.

## Project Documentation

The project documentation covers the design, architecture, agents, and knowledge base:

- `docs/01_concepts.md` — Defect analysis concepts, stack traces, RAG, and semantic similarity.
- `docs/02_architecture.md` — System architecture, data flow, and technology choices.
- `docs/03_agents.md` — Responsibilities and input/output design for the five agents.
- `docs/04_knowledge_base.md` — Historical knowledge base structure and storage design.
- `docs/User_guide.md` — Instructions for using the application.

## Project Structure

- `src/` — Streamlit application and supporting modules.
- `data/` — Historical defect datasets, knowledge base files, and application data.
- `docs/` — Design documents and user documentation.
- `notebooks/` — Experiments and development notebooks.
- `requirements.txt` — Python dependencies.
- `README.md` — Project overview and documentation.

## Future Improvements

- Expand the historical defect dataset across more languages and frameworks.
- Improve duplicate detection and retrieval quality through further evaluation.
- Increase automated test coverage and reliability.
- Evaluate alternative vector database backends and retrieval strategies.
- Continue validating fix recommendations against confirmed resolutions.
