# API Testing Redmine Using Postman

## Overview

This section documents the **API-level testing** of the Redmine application using **Postman**.
The objective was to validate that core Redmine services function correctly at the API layer and that they can be **created, updated, fetched, and deleted** through REST endpoints.

Unlike UI testing, Postman verifies the **backend logic directly**, ensuring that the system behaves correctly even without the web interface.

---

## Test Setup

* **Application:** Redmine (Docker deployment)
* **Base URL:** `http://localhost:3000`
* **Tool:** Postman
* **Authentication:** API Key (`X-Redmine-API-Key`)
* **Environment Variables:**

  * `BASE_URL`
  * `API_KEY`

---

## API Modules Tested

### Issues Module

* Get Issue Statuses
* Create Issue
* Get Issue
* Get Issue Priorities
* Update Issue
* Delete Issue

### Projects Module

* Get Trackers
* Create Project
* Get Projects
* Check Current User

A third folder, **Security Tests**, was reserved for future validation of authentication and permission controls.

---

## Authentication Strategy

Authentication was applied at the **collection level** using:

```
Header: X-Redmine-API-Key
Value: {{API_KEY}}
```

This ensures all requests inherit authentication without repeating it.

---

## Global Header Injection

Since Postman does not provide global headers, a **collection-level pre-request script** was used:

```javascript
pm.request.headers.upsert({ key: "Accept", value: "application/json" });
pm.request.headers.upsert({ key: "Content-Type", value: "application/json" });
```

This guarantees consistent request formatting.

---

## Dynamic Test Data

To prevent duplicate issues, a dynamic subject was generated for each request:

```javascript
const randomId = Math.floor(Math.random() * 10000);
pm.variables.set("dynamic_subject", "API Bug #" + randomId);
```

This ensures every test run remains independent.

---

## Chained API Execution

After creating an issue, its ID was captured:

```javascript
pm.environment.set("created_issue_id", pm.response.json().issue.id);
```

This ID was reused for:

* Updating the issue
* Deleting the issue

This simulates a **real workflow lifecycle**.

---

## Assertions

Each API call was validated using Postman test scripts:

```javascript
pm.test("Status code is 201", function () {
  pm.response.to.have.status(201);
});
```

This confirms correct backend behavior.

---

## Observations & Insights

1. **Redmine API is stable** for CRUD operations when accessed through REST.
2. **Authentication is enforced correctly** at the API layer (unlike UI behavior in Selenium).
3. **Dynamic request chaining works reliably**, enabling automated workflows.
4. Backend validations return meaningful HTTP status codes (200, 201, 204, 422).
5. API testing exposed system behavior without browser/session constraints.

---

## Value of Postman Testing

Postman allowed validation of **backend correctness, data integrity, and workflow continuity** without relying on the UI layer, making it an essential part of the overall Redmine quality assurance strategy.

---
