# Test Plan – Restful-Booker API

## 1. Scope of Testing
- **Application:** Restful-Booker API (`https://restful-booker.herokuapp.com`)
- **Documentation:** Open API / Swagger (`https://restful-booker.herokuapp.com/apidoc/index.html`)

## 2. Test Objectives
- Check if API responses match documentation (JSON structure, status codes).
- Test authentication when changing or deleting data.
- Check how the system handles wrong or missing data (Negative Tests).

## 3. Test Scope
### In-Scope:
- **Functional Testing:**
  - `POST /auth` – Create token
  - `GET /booking` & `GET /booking/{id}` – Get booking list and details
  - `POST /booking` – Create a new booking
  - `PUT /booking/{id}` – Full update of booking
  - `PATCH /booking/{id}` – Partial update of booking
  - `DELETE /booking/{id}` – Delete a booking
  - `GET /ping` – Check if API works (Smoke Test)

### Out-of-Scope:
- UI testing (the app has no user interface)
- Performance and load testing
- Security / Penetration testing (beyond standard auth header validation)

## 4. Test Tools
- **Postman:** Manual testing and JSON validation
- **Python + PyCharm:** Writing test scripts
- **pytest:** Framework for running tests
- **requests:** Python library for HTTP requests

## 5. Entry & Exit Criteria
### Entry Criteria:
1. API is working (`/ping` returns 201).
2. API documentation is available.
3. Test cases are prepared.

### Exit Criteria:
1. All test cases are executed (manual and automated).
2. No critical bugs found.
3. All pytest scripts pass successfully.