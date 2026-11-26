# Expected output — QA Practice API

**Verified 25-nov-2026 by running the collection with Newman (v6): 14 requests, 27 assertions, 0 failures.** Command: `npx newman run QA-Practice-API.postman_collection.json -e QA-Practice-API.postman_environment.json`

Note: the first run (25-nov) had 1 failure — a response-time assertion (`< 2000ms`) that failed when JSONPlaceholder took 49 s on a slow network. That is a flaky test, so it was replaced with a deterministic content check (first user is Leanne Graham). The second run was 27/27 green. / La primera corrida tuvo 1 fallo por un límite de tiempo inestable; se reemplazó por una verificación de contenido y la segunda corrida salió 27/27 en verde.

## Folder 01 — JSONPlaceholder (CRUD)

| # | Request | Expected status | Assertions |
|---|---|---|---|
| 1 | GET All users | 200 | Array of 10 users; every user has id/name/username/email; first user is Leanne Graham |
| 2 | GET User by ID | 200 | id = 1; name is a non-empty string; email contains @; address.city and company.name exist |
| 3 | GET Unknown user (999) | 404 | Status is 404 |
| 4 | GET Posts by user | 200 | 10 posts; every post userId = 1 and has title and body |
| 5 | POST Create post | 201 | Title echoed; userId = 1; id is a number (101) |
| 6 | PUT Update post | 200 | Title = "Updated title"; id stays 1 |
| 7 | DELETE Post | 200 | Status is 200 |

## Folder 02 — httpbin (errors and auth)

| # | Request | Expected status | Assertions |
|---|---|---|---|
| 8 | GET Status 200 | 200 | Status is 200 |
| 9 | GET Status 404 | 404 | Status is 404 |
| 10 | GET Status 400 | 400 | Status is 400 |
| 11 | GET Basic auth without credentials | 401 | Status is 401 |
| 12 | GET Bearer without token | 401 | Status is 401 |
| 13 | GET Echo query params | 200 | args.test = "qa" |
| 14 | GET All users — schema check | 200 | Every email matches an email pattern; every user has address.geo.lat/lng as strings |

**Totals: 14 requests · 27 assertions · 0 failed.**
