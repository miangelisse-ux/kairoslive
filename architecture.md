## 🧠 C4 Architecture Overview (System Levels)

Kairos Live architecture is described using a C4-style breakdown:

- **Level 0 (Context):** External users interacting with the platform  
- **Level 1 (Container):** Core services and system boundaries  
- **Level 2 (Component):** Internal service responsibilities

---

## 🌍 Level 0 — System Context

```mermaid
flowchart LR

Church[⛪ Church Staff] --> Kairos[Kairos Live Platform]
Kairos --> Audience[👥 Congregation Viewing Displays]
Kairos --> Stripe[💳 Stripe Billing System]
```

### Context Description
Kairos Live acts as the central coordination system between church operators, live audiences, and external billing infrastructure.

---

## 🏗️ Level 1 — Container Architecture

```mermaid
flowchart TB

User[👤 Users / Admins]

subgraph Kairos Live System

Frontend[🖥️ Frontend Clients]
API[🚀 API Server]
DB[(🗄️ PostgreSQL)]
SSE[📡 Real-Time SSE Layer]
Billing[💳 Billing Service]

end

Stripe[Stripe API]

User --> Frontend
Frontend --> API
API --> DB
API --> SSE
API --> Billing
Billing --> Stripe
Stripe --> Billing
```

### Container Description
Kairos Live is composed of five core containers:

- Frontend clients (dashboard, remote, display)
- API server (core business logic)
- PostgreSQL database (system of record)
- SSE layer (real-time sync)
- Billing service (Stripe integration)

---

## ⚙️ Level 2 — Core Backend Components

```mermaid
flowchart LR

API[API Server]

Auth[Auth / RBAC]
Sermon[Sermon Engine]
Church[Church / Multi-Tenant Logic]
Billing[Subscription Logic]
Realtime[SSE Event Dispatcher]
DB[(PostgreSQL)]

API --> Auth
API --> Sermon
API --> Church
API --> Billing
API --> DB

Sermon --> Realtime
Realtime --> Frontend[Display Clients]
```

---

## 🔄 Runtime System Behavior Model

Kairos Live operates as a **server-authoritative event-driven system**:

```mermaid
flowchart TD

Action[User Action - Remote / Admin]
API[API Server]
DB[(Database Update)]
Event[SSE Event Emission]
Clients[All Display Clients]

Action --> API
API --> DB
DB --> API
API --> Event
Event --> Clients
```

### Key Behavior Rules

- Backend is the **single source of truth**
- Clients never modify shared state directly
- All updates propagate through SSE events
- Database persists authoritative state
- Displays are passive renderers

---

## 📡 Real-Time Architecture Summary

- Server-Sent Events (SSE) handles live synchronization
- No polling or client-side state replication
- Event-driven propagation model ensures consistency
- Multiple displays stay synchronized in real time

---

## 🧠 Architectural Insight

This system is designed around:

- **Event-driven architecture**
- **Multi-tenant SaaS isolation**
- **Server-authoritative state management**
- **Real-time distributed synchronization**

---

Kairos Live architecture is best understood through multiple system views:

- 🏗️ Container View (high-level system structure)
- 🔄 Runtime Flow View (how requests execute)
- 📡 Real-Time Event Flow (SSE system behavior)
- 💳 Billing Lifecycle Flow (Stripe integration)

---

## 🏗️ 1. Container Architecture (C4 Level 2)

```mermaid
flowchart TB

User[👤 User]
Admin[🧑‍💼 Admin]
Display[🖥️ Display Screen]

subgraph Frontend
  Dashboard[Admin Dashboard]
  Remote[Remote Controller]
  DisplayApp[Display Client]
end

subgraph Backend
  API[API Server]
  Auth[Auth + RBAC]
  Sermon[Sermon Engine]
  Realtime[SSE Event Bus]
  Billing[Billing Service]
end

DB[(PostgreSQL)]
Stripe[Stripe API]

User --> Dashboard
Admin --> Dashboard
Admin --> Remote
Display --> DisplayApp

Dashboard --> API
Remote --> API
DisplayApp --> Realtime

API --> Auth
API --> Sermon
API --> Billing
API --> DB

Sermon --> DB
Auth --> DB
Realtime --> DisplayApp

Billing --> Stripe
Stripe --> Billing
Billing --> DB
```

---

## 🔄 2. Runtime Request Flow (Command Execution)

This shows how a sermon action propagates through the system.

```mermaid
sequenceDiagram
participant User as Remote User
participant API as API Server
participant DB as Database
participant SSE as SSE Layer
participant Display as Display Client

User->>API: POST /remote/action (next slide)
API->>DB: Update sermon state
DB-->>API: Confirm update
API->>SSE: Emit event (slide_update)
SSE-->>Display: Push real-time update
Display-->>User: Updated slide shown
```

---

## 📡 3. Real-Time SSE Event Flow

This shows the live synchronization model.

```mermaid
sequenceDiagram
participant Admin
participant API
participant SSE
participant Screen1 as Display 1
participant Screen2 as Display 2

Admin->>API: Update sermon item
API->>SSE: Broadcast event
SSE-->>Screen1: verse_update
SSE-->>Screen2: verse_update
```

---

## 💳 4. Stripe Billing Lifecycle

```mermaid
sequenceDiagram
participant User
participant API
participant Stripe
participant DB

User->>API: Start subscription
API->>Stripe: Create checkout session
Stripe-->>User: Payment page
User->>Stripe: Complete payment
Stripe->>API: Webhook event
API->>DB: Update subscription status
DB-->>API: Confirm update
API-->>User: Access granted
```

---

## 🧠 5. System Behavior Model

Kairos Live operates on a **server-authoritative event-driven model**:

```mermaid
flowchart LR

A[User Action] --> B[API Server]
B --> C[(Database)]
B --> D[SSE Event Bus]
D --> E[All Clients Update]

C --> B
```

### Key Principles:
- Backend is single source of truth
- Clients are passive renderers
- SSE handles all synchronization
- Database validates state consistency

---
