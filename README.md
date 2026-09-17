# FastAPI Item API (Udacity coursework)

A small FastAPI exercise from Udacity's ML DevOps Engineer Nanodegree: build and test a REST API with typed request/response models. There's no actual ML model behind this one — it's just the API layer itself, done in isolation.

## What it does

- **`TaggedItem` model** (Pydantic): validates an incoming record with `name`, `tags`, and `item_id`.
- **POST `/items/`**: accepts a `TaggedItem` and stores it in memory, keyed by `item_id`.
- **GET `/items/{item_id}`**: looks up a stored item by ID and returns it; returns a not-found message for an unknown ID.

## Tests

`test_main.py` uses FastAPI's `TestClient` to exercise the API. 2 of 3 tests currently pass (the POST and GET item tests). The third, `test_api_locally_get_root`, checks a `/` root route that `main.py` doesn't actually define, so it fails with a 404 — looks like a leftover test that never got reconciled with this version of the starter code.

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
   Interactive API docs are then available at `http://127.0.0.1:8000/docs`.
3. Run the tests:
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
