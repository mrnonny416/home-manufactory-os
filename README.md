## Overview

**Home Manufactory OS (HMOS)** is a web-based system for managing **custom product manufacturing workflows** using a **template-driven process model**.

It solves a common problem faced by makers and small manufacturing teams:

> “As orders grow, manual tracking of parts, steps, and progress becomes unmanageable.”

HMOS provides a structured way to:
- Define products
- Create reusable manufacturing templates
- Track real execution through jobs and steps
- Monitor progress, cost, and responsibility across roles

The system is designed **from day one** to evolve into a **multi-tenant SaaS**.

---

## Core Concepts

### 1. Product
- What you sell
- Marketing-level entity
- Has **no execution logic**
- Immutable (versioned if needed)

Example:
IoT Controller Box
Custom 3D Printed Enclosure

---

### 2. Template
- A **manufacturing manual / SOP**
- Defines:
  - Steps
  - Dependencies between steps
  - Required parts
  - Estimated time & cost
- Immutable once published
- Can be cloned to create new versions

Example:
Black Aluminum Case v1.2
White PLA Case v1.0

---

### 3. Part Library
- Centralized part & material registry
- Tracks:
  - Cost
  - Stock
  - Supplier
  - Lead time
- Reusable across templates and products

---

### 4. Order
- Created when a customer selects:
Product + Template

- Represents **business intent**
- Does NOT represent actual work yet
- Triggers job creation

---

### 5. Job
- Runtime execution unit
- Created by **cloning a template snapshot**
- One order can create **multiple jobs**
- Each job represents actual work done by technicians

---

### 6. Job Step
- Executable checklist item
- Derived from template steps
- Has state:
WAITING → READY → IN_PROGRESS → COMPLETED / SKIPPED

- Tracks:
- Who did it
- When
- What parts were used
- Real cost vs estimate

---

## Canonical Workflow

Product
↓
Template (versioned, immutable)
↓
Product + Template
↓
Order
↓
Template Snapshot (clone)
↓
Job [n]
↓
JobStep [m]

---

## What the System Can Do (Current Design)

### ✔ Product & Template Management
- Create products
- Create templates per product
- Version & publish templates
- Clone templates to create new versions

### ✔ Process Definition
- Step-based workflow
- Step dependency graph (non-linear)
- Optional parts per step
- Parallel steps supported

### ✔ Order Handling
- Customer selects product + template
- Order generates jobs automatically
- Order tracks high-level progress

### ✔ Job Execution
- Jobs assigned to technicians
- Job steps executed independently
- Partial completion & rework supported

### ✔ Role-based Access
- Customer
- Technician (internal / outsource)
- Admin
- Investor / Viewer
- Developer

Each role has different read/write permissions.

---

## What Is Planned (Next Phases)

### 🔜 Phase 1.1
- JobStep dependency engine (DAG resolution)
- Permission matrix enforcement
- Audit logs

### 🔜 Phase 1.2
- Cost tracking (estimated vs actual)
- Stock auto-deduction
- Delay & SLA detection

### 🔜 Phase 2
- Finance dashboard
- Outsource job support
- File attachments (e.g. 3D print files)

### 🔜 Phase 3 (SaaS)
- Multi-tenant billing
- Subscription plans
- White-label support
- API keys & integrations

---

## Architecture Principles

- **Template immutability**
- **Runtime cloning**
- **Snapshot over reference**
- **MongoDB-first (NoSQL-friendly)**
- **Separation of business intent vs execution**
- **Designed for scale without refactor**

---

## Tech Stack (Planned)

- Frontend: Next.js
- Backend: Node.js / NestJS
- Database: MongoDB
- Auth: JWT / RBAC
- Queue (future): BullMQ / RabbitMQ

---

## Target Users

- Makers / DIY labs
- IoT & hardware startups
- Small factories
- Custom manufacturing services
- Engineering teams with complex workflows

---

## Philosophy

> Templates are law.  
> Orders are intent.  
> Jobs are reality.

---

## Status

🚧 **Early design & architecture phase**  
Currently focused on:
- Core domain modeling
- API design
- Schema validation

Implementation will follow after architecture is locked.

---

## License

TBD (MIT planned)

---

> This project is intentionally designed to start simple  
> and grow into a full manufacturing SaaS platform.
