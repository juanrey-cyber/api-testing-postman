# API Testing with Postman — QA Practice API

**EN | ES**

## What this proves / Qué demuestra

**EN:** I can test a REST API like a QA engineer: send requests, assert status codes, validate response bodies and schemas, and cover error cases (400/401/404) and auth failures — not just the happy path. 14 requests, 27 assertions, all green.

**ES:** Puedo probar una API REST como QA: enviar peticiones, verificar códigos de estado, validar cuerpos y esquemas de respuesta, y cubrir casos de error (400/401/404) y fallos de autenticación — no solo el camino feliz. 14 peticiones, 27 verificaciones, todas en verde.

## What is inside / Contenido

| File | What it is |
|---|---|
| `QA-Practice-API.postman_collection.json` | Postman collection v2.1 — 14 requests in 2 folders, each with test scripts |
| `QA-Practice-API.postman_environment.json` | Environment with the 2 base URLs as variables |
| `expected-output.md` | Expected result of every request (verified 25-nov-2026) |
| `guia-de-estudio.md` | Study guide in Spanish: concepts, interview questions, exercises |

**Folder 01 — JSONPlaceholder (CRUD):** GET all users, GET user by ID, GET unknown user (404), GET posts by user, POST create post (201), PUT update post, DELETE post.

**Folder 02 — httpbin (errors and auth):** status 200/400/404, basic-auth without credentials (401), bearer without token (401), query-param echo, schema/contract check on all users.

## APIs used / APIs usadas

- **JSONPlaceholder** (https://jsonplaceholder.typicode.com) — free fake REST API for testing.
- **httpbin** (https://httpbin.org) — free HTTP request/response test service.

Both return **synthetic demo data, not real users**. No API key, no account, no real data. / Los datos son de demostración, no usuarios reales. Sin clave, sin cuenta, sin datos reales.

## How to run / Cómo correrlo

**Option A — Postman (GUI):**
1. Open Postman → Import → select `QA-Practice-API.postman_collection.json` and `QA-Practice-API.postman_environment.json`.
2. Select the environment **"QA Practice API - Local"** (top right).
3. Open the collection → Run → Run all requests.

**Option B — Newman (terminal, no Postman needed):**
```bash
npx newman run QA-Practice-API.postman_collection.json -e QA-Practice-API.postman_environment.json
```

Expected: **14 requests, 27 assertions, 0 failures.** / Esperado: 14 peticiones, 27 verificaciones, 0 fallos.

## Skills covered / Skills que cubre

REST API testing · Postman collections & environments · status-code assertions · JSON schema/contract checks · error-case testing (400/401/404) · auth failure testing · query params · response-time assertions.

## Series / Serie

QA portfolio (same author):
- [`sql-practice`](https://github.com/juanrey-cyber/sql-practice) — SQL: JOINs, GROUP BY, CTEs, window functions (SQLite, verified answers)
- `playwright-qa` — coming next / siguiente
- `python-qa-scripts` — coming next / siguiente

## Honest note / Nota honesta

This is practice built while learning API testing ("aprender mientras se aplica"): real requests, real assertions, verified by running them. It does not claim production QA experience. / Esto es práctica construida mientras aprendo API testing: peticiones reales, verificaciones reales, comprobadas corriéndolas. No afirma experiencia de QA en producción.
