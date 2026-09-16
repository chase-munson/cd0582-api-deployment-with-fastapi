# Census Model Inference API (FastAPI)

A small FastAPI service exercising REST API design for machine learning model
inference: typed request/response models with Pydantic, a POST endpoint that
accepts a record and returns a result, and a GET endpoint that looks it back
up — the same request/response shape a real model-serving API would use.

## Problem

Before deploying an actual trained model behind an API, it's worth getting
the API layer right on its own: request validation, typed responses, and a
test suite that exercises both endpoints. This project builds and tests that
layer in isolation.

## Approach

- **FastAPI + Pydantic**: a `TaggedItem` model defines the shape of an
  incoming record (`name`, `tags`, `item_id`), validated automatically by
  Pydantic on every request.
- **POST `/items/`**: accepts a `TaggedItem` and stores it in memory, keyed
  by `item_id`.
- **GET `/items/{item_id}`**: looks up a stored item by ID and returns a
  formatted response; returns a not-found message for an unknown ID.
- **Testing**: `test_main.py` uses FastAPI's `TestClient` to exercise the
  POST and GET endpoints without needing a running server.

## How to run

1. Create a virtual environment and install dependencies:
   ```bash
   python -m venv venv
   source venv/bin/activate  # or venv\Scripts\activate on Windows
   pip install -r requirements.txt
   ```
2. Start the API locally:
   ```bash
   uvicorn main:app --reload
   ```
   The interactive API docs are then available at `http://127.0.0.1:8000/docs`.
3. Run the test suite:
   ```bash
   pytest
   ```

## Files

```
main.py           FastAPI app: TaggedItem model, POST/GET endpoints
test_main.py       Test suite using FastAPI's TestClient
requirements.txt   Pinned dependencies
cd0582.postman_collection.json   Postman collection for manual API testing
```

## Credits

This exercise (the FastAPI app, tests, and Postman collection) is coursework from Udacity's ML DevOps Engineer Nanodegree, forked from `udacity/cd0582-api-deployment-with-fastapi`. Udacity's own upstream repo for this exercise doesn't include a license, so no license is claimed here either.
