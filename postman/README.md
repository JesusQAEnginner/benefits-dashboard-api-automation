# 📮 Postman Collection Directory

## 📌 Overview

This folder contains the exported Postman collection used for API validation of the Employees & Benefits module.

The collection supports deterministic execution through collection variables and can be executed either in Postman or through Newman CLI.

---

## 📁 Contents

### `paylocity-benefits-dashboard.postman_collection.json`
Main Postman collection containing:

- CRUD validation
- Business rule assertions
- Financial calculation checks
- UI bug support validations
- Boundary and negative scenarios

---

## 🎯 Purpose

This folder exists to provide:

- Source collection for API testing
- Importable test suite for Postman
- CLI execution source for Newman
- Version-controlled API automation artifact

---

## ▶️ Usage

Import the collection into Postman or execute it using Newman.

### Example CLI execution

```bash
newman run postman/paylocity-benefits-dashboard.postman_collection.json
