# 🧠 Kairos Live — Architecture

---

## 🧠 Architecture Overview

Kairos Live is a **real-time, server-authoritative SaaS platform** for live church service orchestration.

It enables synchronized control of sermons, scripture display, and multi-device presentations using an event-driven backend architecture.

The system is built around four core principles:

- Backend is the single source of truth  
- Clients are stateless renderers  
- Real-time updates are event-driven (SSE)  
- Multi-tenant isolation is enforced at the data layer  

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
Billing[💳 Billing Service]

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
Responsible for all business logic and system state mutations:
- Sermon creation and management
- Authentication (JWT cookies)
- Role-based access control (RBAC)
- State updates and validation
- Subscription enforcement

---

### 🗄️ Database (PostgreSQL + Drizzle)
System of record for all persistent data:

- Users
- Churches (multi-tenant isolation)
- Sermons
- Sermon items (verses, slides, text)
- Subscription state

All records are scoped by `church_id`.

---

### 🖥️ Frontend Clients
Stateless UI clients that render server state:

- Admin Dashboard → system control
- Remote Controller → live sermon control
- Display Screen → fullscreen presentation output

Clients never mutate shared state directly.

---

### 📡 Real-Time Layer (SSE)
Handles all live synchronization between clients.

- Backend emits events on state changes
- Clients subscribe to event stream
- No polling or client-side syncing required
- All connected displays update instantly

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
Event[SSE Event Broadcast]
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
3. Database is updated (source of truth)
4. SSE event is emitted
5. All display clients update instantly

---

## 🏢 Multi-Tenant Architecture

Kairos Live is fully multi-tenant.

### Isolation Model:
- Each church has a unique `church_id`
- All queries are scoped per tenant
- Users cannot access other church data
- Admins operate within their workspace only
- Owner has global system access

---

## 💳 Billing System (Stripe)

Stripe handles all payment processing and acts as the external billing authority.

### Billing Flow:

```text
User selects plan
→ Stripe Checkout Session
→ Payment completed
→ Stripe webhook sent to backend
→ Subscription updated in database
→ Access permissions applied
```

### Responsibilities:
- Subscription lifecycle management
- Plan upgrades and downgrades
- Webhook verification
- Access control enforcement

---

## 📡 Real-Time System Design

- Server-Sent Events (SSE) provides real-time updates
- Backend is the authoritative event emitter
- Clients are passive subscribers
- All state changes flow through the API layer
- System guarantees eventual consistency across all displays

---

## 🧠 System Design Characteristics

Kairos Live demonstrates the following architectural patterns:

- Event-driven architecture
- Server-authoritative state management
- Multi-tenant SaaS design
- Stateless frontend clients
- Real-time synchronization via SSE
- Externalized billing system (Stripe)

---

## 🚀 Summary

Kairos Live is a distributed, real-time SaaS system designed for synchronized live service management across multiple devices and users.

It demonstrates production-level system design principles including event-driven architecture, multi-tenancy, and real-time state propagation.

---
