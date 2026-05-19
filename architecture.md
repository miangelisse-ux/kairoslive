# 🧠 Kairos Live — Architecture

---

## 🧠 System Overview

Kairos Live is a **multi-tenant, real-time SaaS platform** for live church service orchestration.

It enables synchronized control of sermons, scripture display, and multi-device presentation workflows through an **event-driven, server-authoritative architecture**.

All system behavior is driven by backend state changes and propagated in real time to connected clients.

---

## 🧠 Core Architectural Principles

- **Server-authoritative state** → backend is the single source of truth  
- **Event-driven updates** → real-time synchronization via SSE  
- **Stateless clients** → frontend only renders server state  
- **Multi-tenant isolation** → each church operates independently  
- **External billing authority** → Stripe manages subscriptions  

---

## 🏗️ System Architecture (C4 Model)

```mermaid
flowchart TB

Users[👤 Users / Admins]

subgraph Kairos Live System

Frontend[🖥️ Frontend Clients<br/>(Admin / Remote / Display)]
API[🚀 API Server<br/>(Express + TypeScript)]
DB[(🗄️ PostgreSQL<br/>System of Record)]
SSE[📡 SSE Real-Time Layer]
Billing[💳 Subscription Service]

end

Stripe[Stripe API]

Users --> Frontend
Frontend --> API

API --> DB
API --> SSE
API --> Billing

Billing --> Stripe
Stripe --> Billing

SSE --> Frontend
```

---

## ⚙️ Core Components

### 🚀 API Server
Handles all business logic and state mutations:
- Sermon creation and management
- Authentication (JWT cookies)
- Role-based access control (RBAC)
- State updates and validation
- Subscription enforcement

---

### 🗄️ Database (PostgreSQL + Drizzle)
System of record for all persistent data:

- Users
- Churches (multi-tenant scope)
- Sermons
- Sermon items (verses, slides, text)
- Subscription state

All records are scoped by `church_id`.

---

### 🖥️ Frontend Clients
Stateless UI clients responsible for rendering server state:

- **Admin Dashboard** → system control
- **Remote Controller** → live sermon control
- **Display Screen** → fullscreen presentation output

Clients never mutate shared state directly.

---

### 📡 Real-Time Layer (SSE)
Handles real-time synchronization across all connected clients.

- Backend emits events on state changes
- Clients subscribe to SSE stream
- No polling or manual refresh required
- All displays update instantly and consistently

### Event Types:
- `verse_update`
- `slide_update`
- `service_state`
- `service_control`

---

## 🔄 Runtime Execution Model

Kairos Live follows a strict event-driven execution pipeline:

```mermaid
flowchart TD

Action[User Action<br/>(Remote / Admin)]
API[API Server]
DB[(Database)]
Event[SSE Broadcast Layer]
Clients[Display Clients]

Action --> API
API --> DB
DB --> API
API --> Event
Event --> Clients
```

### Execution Flow:
1. User triggers action (remote/admin)
2. API validates request
3. Database is updated (system of record)
4. SSE event is emitted
5. All connected clients update in real time

---

## 📡 Real-Time System Behavior

- Server-Sent Events (SSE) provide live updates
- Backend is the only event producer
- Clients are passive subscribers
- No polling or client-side state syncing
- System ensures eventual consistency across all displays

---

## 🏢 Multi-Tenant Architecture

- Each church is isolated via `church_id`
- All data is tenant-scoped at the database level
- Authentication enforces workspace boundaries
- Users cannot access other tenants
- Admin roles are restricted per organization
- Owner has global system override access

---

## 💳 Billing System (Stripe)

Stripe is the external billing authority.

### Billing Flow

```text
User selects plan
→ Stripe Checkout Session created
→ Payment processed by Stripe
→ Stripe webhook sent to backend
→ Subscription state updated in database
→ Access permissions enforced
```

### Responsibilities:
- Subscription lifecycle management
- Plan upgrades and downgrades
- Webhook validation and reconciliation
- Access control enforcement

---

## 🧠 System Design Characteristics

Kairos Live demonstrates the following architecture patterns:

- Event-driven distributed system
- Server-authoritative state management
- Multi-tenant SaaS isolation
- Stateless frontend architecture
- Real-time synchronization via SSE
- External billing integration (Stripe)

---

## 🚀 Summary

Kairos Live is a production-grade, real-time SaaS system designed for synchronized live service management across distributed devices.

It demonstrates real-world system design principles including event-driven architecture, multi-tenancy, and server-authoritative state propagation.

---
