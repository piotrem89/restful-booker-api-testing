# Test Cases – Restful-Booker API



## 1. Ping API (`/ping`)

| ID            | Title / Description                             | Type | Method & Endpoint | Payload / Input Data | Expected Status | Expected Response Body |
|:--------------|:------------------------------------------------| :--- |:------------------|:---------------------|:----------------|:-----------------------|
| `TC_PING_001` | Check API availability (Smoke Test)  | Positive | `GET /ping`       | None                 | `201 Created`   | Message: "Created"      |



## 2. Auth API (`/auth`)

| ID            | Title / Description                             | Type | Method & Endpoint | Payload / Input Data                                                                  | Expected Status | Expected Response Body                               |
|:--------------|:------------------------------------------------| :--- |:------------------|:--------------------------------------------------------------------------------------|:----------------|:-----------------------------------------------------|
| `TC_AUTH_001` | Generate authentication token with valid data   | Positive | `POST /auth`      | Valid JSON with all required fields ("username" : "admin", "password" : "password123") | `200 OK`        | JSON object with token property: {"token": "string"} |
| `TC_AUTH_002` | Generate authentication token with invalid data | Negative | `POST /auth`      | JSON with invalid login or password                                                   | `200 OK`        | Message: "Reason: Bad credentials."                    |



## 3. Booking API (`/booking`)

| ID | Title / Description | Type | Method & Endpoint | Payload / Input Data | Expected Status | Expected Response Body |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `TC_BOOK_001` | Create new booking with valid data | Positive | `POST /booking` | Valid JSON with all required fields (`firstname`, `lastname`, `totalprice`, `depositpaid`, `bookingdates`, `additionalneeds`) | `200 OK` | JSON object containing generated `bookingid` and complete `booking` details matching input data. |
| `TC_BOOK_002` | Create booking with missing required field | Negative | `POST /booking` | JSON missing mandatory `lastname` field | `400 Bad Request` | Error message or payload rejection. |
| `TC_BOOK_003` | Create booking with invalid data type for price | Negative | `POST /booking` | JSON with string value in numeric `totalprice` field (e.g., `"totalprice": "one hundred"`) | `400 Bad Request` | Error response rejecting invalid field types. |
| `TC_BOOK_004` | Create booking with invalid date format | Negative | `POST /booking` | JSON with invalid format in `bookingdates.checkin` (e.g., `"2026-13-45"`) | `400 Bad Request` | System rejects invalid date format. |


## 4. Update Booking API (`/booking/{id}`)

| ID              | Title / Description                         | Type     | Method & Endpoint     | Payload / Input Data                                                                                                                                                                                            | Expected Status   | Expected Response Body                                       |
|:----------------|:--------------------------------------------|:---------|:----------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------------|:-------------------------------------------------------------|
| `TC_UPDATE_001` | Full update booking with valid auth token   | Positive | `PUT /booking/{id}`   | Valid JSON with all required fields (`firstname`, `lastname`, `totalprice`, `depositpaid`, `bookingdates`, `additionalneeds`), and valid token                                                                  | `200 OK`          | JSON object containing complete updated booking details      |
| `TC_UPDATE_002` | Full update booking with invalid auth token | Negative | `PUT /booking/{id}`   | Valid JSON with all required fields (`firstname`, `lastname`, `totalprice`, `depositpaid`, `bookingdates`, `additionalneeds`), and invalid token                                                                | `403 Forbidden`   | Plain text message (Forbidden)                               |
| `TC_UPDATE_003` | Full update booking without auth token      | Negative | `PUT /booking/{id}`   | Valid JSON with all required fields (`firstname`, `lastname`, `totalprice`, `depositpaid`, `bookingdates`, `additionalneeds`)                                                                                   | `403 Forbidden`   | Plain text message (Forbidden)                               |
| `TC_UPDATE_004` | Partial update booking (first name only)    | Positive | `PATCH /booking/{id}` | Partial JSON ({"firstname": "James"}) and valid token                                                                                                                                                           | `200 OK`          | JSON object with updated firstname and original other fields |
| `TC_UPDATE_005` | Partial update with invalid data type       | Negative | `PATCH /booking/{id}` | Partial JSON ({"totalprice": "invalid"}) and valid token                                                                                                                                                        | `400 Bad Request` | Plain text message (Bad Request)                             |
| `TC_UPDATE_006` | Update booking with checkout date before checkin date   | Negative | `PUT /booking/{id}`   | Valid token and valid JSON with all required fields (`firstname`, `lastname`, `totalprice`, `depositpaid`, `bookingdates`, `additionalneeds`) but invalid dates (checkin: "2024-10-10", checkout: "2024-10-01") | `400 Bad Request` | Error response    |



