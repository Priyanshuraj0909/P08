# SCSE3040 — Practical 08: Packing the Service into a Container

Delivery-time prediction service (FastAPI + scikit-learn) packed into a Docker image.

| Path | What it is |
|---|---|
| `labs/P08_ROLLNUMBER.ipynb` | The practical notebook, fully run (9/9 self-check) |
| `labs/work/Dockerfile` | Dockerfile for image `delivery-api:1.0` |
| `labs/work/Dockerfile.v2` | Task T2 fixed Dockerfile, image `delivery-api:2.0` |
| `labs/work/.dockerignore` | Build-context ignore file |
| `labs/work/.dockerignore.mine` | Task T1 ignore file |
| `labs/work/app.py`, `model.joblib`, `requirements.txt` | The service |
| `data/delivery_times.csv` | The 600-row dataset |

## Run locally
```bash
cd labs/work
docker build -t delivery-api:1.0 .
docker run --rm -p 8010:8000 delivery-api:1.0
# open http://127.0.0.1:8010/docs
```

## Endpoints
- `GET /health` → `{"status": "ok", "model_loaded": true}`
- `POST /predict` with `{"distance_km": 4, "prep_time_min": 30, "traffic_level": 3, "rain": 1}` → `{"delivery_min": 56.1, "model_version": "1.0.0"}`
