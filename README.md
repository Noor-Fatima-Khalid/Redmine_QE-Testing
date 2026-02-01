## Overview

This repository contains the **deployment and testing of the Redmine open-source project management tool ([https://www.redmine.org/](https://www.redmine.org/))**. It covers:

* Deployment using **Docker Desktop** on Windows with WSL2
* **API testing using Postman**
* Functional and UI testing using **Python Selenium**
* Performance/load testing using **JMeter**
* Functional issues reporting and test case documentation

---

## API Testing (Postman)

Postman was used to validate Redmine’s **backend REST APIs** independently of the UI.
The goal was to ensure that core operations can be performed through API endpoints and return correct responses.

### Modules Tested

**Issues**

* Get Issue Statuses
* Create Issue
* Get Issue
* Get Issue Priorities
* Update Issue
* Delete Issue

**Projects**

* Get Trackers
* Create Project
* Get Projects
* Check Current User

### Authentication

* Type: API Key
* Header: `X-Redmine-API-Key`
* Value: `{{API_KEY}}`

Authentication is configured at the **collection level** so all requests inherit it automatically.

### Environment Variables

| Variable | Description                                                             |
| -------- | ----------------------------------------------------------------------- |
| BASE_URL | Redmine base URL (e.g., [http://localhost:3000](http://localhost:3000)) |
| API_KEY  | Redmine API access key                                                  |

### Dynamic Data & Chaining

* Unique issue subjects are generated for every run.
* Created issue IDs are stored and reused for update and delete requests.

### Assertions

Each request validates:

* Status codes (200, 201, 204)
* Response structure
* Returned IDs for chaining

---

## Load/Performance Testing (JMeter)

JMeter test plan: `jmeter/redmine_load_test.jmx`
Tests multiple concurrent users on:

* Login
* Project creation
* Issue creation
* Enumeration creation

### Run JMeter test plan:

* Open Apache JMeter
* Load `redmine_load_test.jmx`
* Execute test and analyze results

---

## Functional/UI Testing (Selenium)

Dependencies:

```
pip install selenium webdriver-manager
```

The Selenium script covers:

* Login to Redmine
* Navigate to Projects and create a new project
* Administration sections: Users, Groups, Roles & Permissions, Workflow, Custom Fields, Enumerations, Settings, Information
* Navigate to "My page"

### Run script:

```
python selenium/selenium_script.py
```

Test case table and functional issues are documented in `docs.docx`.

---

## Observed Functional Issues

| Issue                          | Description                                                          |
| ------------------------------ | -------------------------------------------------------------------- |
| Creating project without login | Allows project creation without authentication                       |
| Tracker creation               | Default status cannot be blank; prevents creating tracker for issues |

Full functional issues table is available in
`Functional Testing using Selenium/docs.docx`.

---

### Notes

* Redmine is deployed locally using Docker with SQLite database.
* Selenium scripts include simple waits (`time.sleep`) for stability; these can be replaced with explicit waits for production-grade automation.

---
