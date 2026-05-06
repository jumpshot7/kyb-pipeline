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
<img width="1911" height="916" alt="Screenshot 2026-05-06 155429" src="https://github.com/user-attachments/assets/d46c2b98-eeaa-40c3-907e-6b8f0d651cd0" />

</br>

<img width="1908" height="911" alt="Screenshot 2026-05-06 160843" src="https://github.com/user-attachments/assets/3e304846-a612-4507-b6d9-3fa1eefb8537" />


