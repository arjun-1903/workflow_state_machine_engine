# 🚀 Workflow State Machine Engine

A backend system built using Java and Spring Boot that manages entity lifecycle transitions using a configurable state machine approach. It ensures only valid state transitions are allowed while maintaining a complete audit trail of changes.

---

## 🧠 Overview

This project implements a **workflow engine** where entities move through predefined states based on allowed transitions.

It is designed to:

* Prevent invalid state transitions
* Maintain data consistency
* Provide full audit history
* Support evolving workflows through versioning

---

## ⚙️ Tech Stack

* Java 17
* Spring Boot 3
* Spring Data JPA (Hibernate)
* SQLite
* Maven

---

## 🏗️ Architecture

```
Controller → Service → Engine → Repository → Database
```

* **Controller**: Handles HTTP requests
* **Service**: Business logic & transaction handling
* **Engine (StateMachine)**: Pure logic for validating transitions
* **Repository**: Database access via JPA

---

## 🔥 Key Features

* Configurable workflows using JSON
* Strict state transition validation
* Versioned workflows
* Full audit trail of transitions
* Transaction-safe updates
* Defensive validation

---

## 📦 API Endpoints

### Create Workflow

```
POST /workflow
```

Example:

```json
{
  "name": "Order Workflow",
  "states": ["PENDING", "APPROVED", "SHIPPED", "DELIVERED"],
  "transitions": {
    "PENDING": ["APPROVED"],
    "APPROVED": ["SHIPPED"],
    "SHIPPED": ["DELIVERED"]
  }
}
```

---

### Create Entity

```
POST /entity
```

```json
{
  "entityId": "order-123",
  "workflowId": "<workflow-id>",
  "initialState": "PENDING"
}
```

---

### Transition Entity

```
POST /entity/{id}/transition
```

```json
{
  "toState": "APPROVED",
  "performedBy": "admin"
}
```

---

### Other Endpoints

```
GET /workflow/{id}
GET /entity/{id}
GET /entity/{id}/history
```

---

## 🧪 Example Flow

```
PENDING → APPROVED → SHIPPED → DELIVERED
```

Invalid transitions like:

```
PENDING → DELIVERED
```

are rejected.

---

## 🧠 Design Highlights

* Decoupled StateMachine engine
* Validation-first approach
* JSON-based workflow configuration
* Full audit tracking

---

## 🚀 Running the Project

Use Maven wrapper:

```
./mvnw spring-boot:run
```

(On Windows)

```
.\mvnw spring-boot:run
```

---

## 🧾 Resume Description

Developed a configurable and versioned workflow state machine engine in Java using Spring Boot, enforcing valid state transitions through a decoupled logic layer with audit tracking.

---

## 📌 Future Improvements

* Concurrency control (optimistic locking)
* External event hooks
* Distributed workflow support

---
