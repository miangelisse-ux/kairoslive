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
