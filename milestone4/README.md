# Milestone 4 — UI (Streamlit)

This UI calls the Milestone 3 FastAPI backend.

## What this milestone adds

- A Streamlit frontend for uploading contracts and asking questions
- A FastAPI backend for analysis, auth, and history persistence
- A shared local SQLite store for user sessions and saved runs

## 1) Start the backend

```powershell
cd milestone3\backend
uvicorn app:app --reload --port 8000
```

## 2) Start the UI

```powershell
cd milestone4\UI\UI
pip install -r requirements.txt

# Optional: point UI to a different backend base URL
set BACKEND_URL=http://127.0.0.1:8000

streamlit run app.py
```

## Login + history

- Authentication and analysis history are stored in the **backend SQLite DB** (not in the UI).
- After login, every Ask / Launch Analysis run is saved automatically.
- Use the sidebar **Recent Analyses** or the **History** page to reopen a previous run.

## Configuration tips

- Set `BACKEND_URL` before starting Streamlit if the backend is not on `127.0.0.1:8000`.
- Keep the backend running while using the UI.
- If uploads fail, confirm the backend can read the file path and that CORS is not blocking the request.

## What gets sent to the backend

- Uploads are sent as real files to `POST /analyze` (multipart form-data).
- The question box is passed as `question`.
- UI tone options are mapped to backend tones (`executive` or `simple`).
