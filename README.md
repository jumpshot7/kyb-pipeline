# KYB Compliance Pipeline

This project is a Know Your Business (KYB) compliance pipeline. Using cross referenced New York City DCPW (formerly DCA) business licenses against New York State corporate entities to detect compliance anomalies, such as dissolved entities still holding active licenses, address mismatches, or entities formed after their license was issued.

## Architecture & Tech Stack

The project is split into three main components:

*   **Data Pipeline (`pipeline/` and `backend/`)**: 
    *   Downloads raw CSV datasets from Socrata directly to Google Cloud Storage (GCS).
    *   Uses Apache Beam to stream, process, and validate the data (via Pydantic) into a PostgreSQL database.
    *   Runs fuzzy matching (optimized by zip code pre-filtering) to compare NYC businesses against NYS entities and compute anomaly flags.
*   **Backend API (`backend/api.py`)**: 
    *   A FastAPI application that queries the processed anomaly and entity data from Postgres.
*   **Frontend (`frontend/`)**: 
    *   A Next.js dashboard to visualize the anomalies and compliance results.

## Repository Structure

```text
.
├── backend/       # FastAPI application, data fetchers, and pipeline orchestration
├── frontend/      # Next.js UI application
├── pipeline/      # SQL schema and Apache Beam runner logic
└── tests/         # Unit and integration tests
```
<img width="1904" height="913" alt="Screenshot 2026-04-30 205413" src="https://github.com/user-attachments/assets/80243754-afc2-4a38-af39-52c6c8be604b" />

