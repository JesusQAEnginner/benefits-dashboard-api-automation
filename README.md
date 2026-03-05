# 🧪 Benefits API Automation Framework

Automated API testing framework designed to validate the **Employees & Benefits module** using **Postman + Newman CLI execution**.

The framework focuses on validating **business rules, financial calculations, and full CRUD workflows** under deterministic execution conditions.

---

# 🚀 Technology Stack

* Postman
* Newman CLI
* newman-reporter-htmlextra
* Node.js
* REST API Testing

---

# ⚙️ Collection Variables

This collection uses **Postman Collection Variables** to ensure consistent and deterministic execution across environments.

| Variable     | Purpose                                                  |
| ------------ | -------------------------------------------------------- |
| `baseUrl`    | Base API endpoint used by all requests                   |
| `username`   | Authenticated user used for ownership validation         |
| `authToken`  | Basic authorization token used in request headers        |
| `employeeId` | Dynamically stored employee ID used across CRUD requests |

These variables allow the test suite to avoid hardcoded values and maintain reproducibility.

![Collection Variables](docs/screenshots/collection-variables.png)

> ⚠️ The `authToken` value shown in the screenshot is for testing purposes only. Credentials are stored using Postman variables to avoid hardcoding sensitive data.

---

# 🎯 Project Objective

Validate the employer's ability to:

* Add employees
* Calculate benefit costs correctly
* Edit employee data
* Delete employees
* Maintain data consistency across API requests

All tests are designed to run **deterministically through CLI execution** and produce an **HTML execution report**.

---

# 🔁 End-to-End CRUD Validation Flow

The collection executes the following workflow:

1. **POST – Create Employee**
2. **GET by ID – Validate persistence**
3. **GET All – Validate employee appears in the dashboard list**
4. **PUT – Update employee data**
5. **GET by ID – Validate update persistence**
6. **DELETE – Remove employee**
7. **GET by ID – Confirm deletion (negative scenario)**
8. **GET All – Validate list integrity**

This ensures the **complete employee lifecycle** is validated through the API.

---

# 🔗 UI ↔ API Traceability Matrix (Playwright Findings)

During Playwright UI automation development, several UI issues were identified.
API validation tests were added to verify whether the behavior originates from the backend or the frontend layer.

| UI Bug | UI Symptom | API Validation Added | Endpoint | Method | Expected Result |
|------|-------------|----------------------|----------|--------|----------------|
| BUG-001 | Employees table sometimes loads empty after automated navigation | Validate employee list contains created record | `/api/Employees` | GET | Response array contains created employee |
| BUG-002 | Employee modal sometimes remains open after submission | Validate employee persistence after creation | `/api/Employees/{id}` | GET | Employee record exists and fields are valid |

These tests help determine whether the issue originates from the **UI rendering layer** or the **backend API behavior**.
---

# 💰 Business Rules Validation

The automation suite verifies **benefits cost calculations** using the following financial model.

### Constants

Employee Gross Pay (per paycheck): **$2000**
Paychecks per year: **26**
Annual employee benefit cost: **$1000**
Dependent benefit cost: **$500 per dependent**

---

### Calculation Model

Yearly Benefits = 1000 + (Dependents × 500)

Benefits Per Paycheck = Yearly Benefits ÷ 26

Net Paycheck = 2000 − Benefits Per Paycheck

---

### Assertions Validate

* Correct **gross salary value**
* Accurate **benefits cost calculation**
* Correct **net paycheck value**
* **Net pay must always be lower than gross**
* **Benefits cost must never be negative**
* Decimal precision tolerance validation

---

# 🧪 Test Coverage

## Employee Creation Validation

* Data persistence verification
* Dynamic UUID capture
* Ownership validation
* Financial calculation validation
* Dashboard visibility verification

---

## Employee Update Validation

* Field update validation
* Payroll preview recalculation
* Persistence re-validation

---

## Employee Deletion Validation

* Correct HTTP response codes
* Negative scenario validation
* Record cleanup confirmation

---

## Boundary Testing

Dependents values tested:

| Dependents | Expected Behavior          |
| ---------- | -------------------------- |
| 0          | Valid                      |
| 1          | Valid                      |
| 32         | Maximum allowed            |
| >32        | Request should be rejected |

---

# 🔍 Technical Validation Strategies

The framework implements several reliability strategies:

* Dynamic UUID handling
* Collection variable storage
* No hardcoded request identifiers
* Status code validation (200, 201, 400, 404, etc.)
* Response schema integrity checks
* Ownership validation
* Safe JSON parsing for error scenarios

---

# ⚙️ Installation

Install Newman and the HTML reporter globally:

```
npm install -g newman
npm install -g newman-reporter-htmlextra
```

---

# ▶️ Run Test Collection

Execute the API test suite with Newman:

```
newman run Paylocity_Benefits_Dashboard-API_Testing-Postman_Collection.json
```

You may also import the collection directly into **Postman** and execute it using the **Collection Runner**.

---

# 📊 Generate HTML Test Report

To generate a detailed HTML report:

```
newman run Paylocity_Benefits_Dashboard-API_Testing-Postman_Collection.json \
-r htmlextra \
--reporter-htmlextra-export report.html
```

---

# 📈 Report Features

The generated HTML report includes:

* Total requests executed
* Assertion pass/fail summary
* Response metrics
* Request and response bodies
* Visual execution dashboard

---

# 🌐 Example Report

Latest execution report hosted on GitHub Pages:

https://jesusqaenginner.github.io/Paylocity_Benefits_Dashboard-API_Automation-Postman/reports/report.html

---

# 🚀 CI/CD Readiness

This project supports automated execution through CI pipelines.

Capabilities include:

* GitHub Actions compatibility
* Headless CLI execution
* Version-controlled API validation
* Pipeline-based automated testing

---

# 📈 Engineering Value Demonstrated

This project showcases:

* Production-style API automation
* Business rule validation
* Financial calculation testing
* Deterministic test design
* CLI-based automation execution
* Automated reporting for stakeholders

---

# 👤 Author

**Jesus Ricardo Hernandez Campos**

QA Automation Engineer

API Testing • Test Automation • Quality Engineering

---

# 🏆 Quality Engineering Philosophy

Quality engineering goes beyond defect detection.

The goal is to **reduce risk, validate business logic, and ensure system reliability through automated validation of critical workflows.**
