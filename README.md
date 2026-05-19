# ⛪ Kairos Live

Real-time church service operating system for scripture, sermons, and live multi-screen presentation control.

Kairos Live is a SaaS platform that replaces traditional church presentation tools with a live, connected system for running Sunday services in real time.

---

## 🚀 What It Does

Kairos Live helps churches run services without slides or manual syncing:

- 📖 Instant Bible verse display
- 🎤 Sermon flow control system
- 📱 Mobile + desktop remote control
- 🖥️ Multi-screen live synchronization
- 🌍 Bible translation switching
- 💳 Subscription-based SaaS (Stripe)

---

## ⚡ Key Features

### 📺 Live Display
- `/display` fullscreen projector mode  
- Real-time updates (no refresh needed)  
- Persistent last-known state  
- Church-branded display mode  

### 🎛️ Sermon Control
- Build sermon flows  
- Verse + text slides  
- Next / previous / start / stop controls  
- Mobile remote (`/remote`)  

### 📖 Bible System
- Multiple translations  
- Reference lookup (John 3:16)  
- Keyword search  

### 🏢 Multi-Tenant System
- Isolated church workspaces  
- Role-based access  
- Secure data separation  

### 💳 Billing
- Stripe subscriptions  
- Monthly + yearly plans  
- Billing portal integration  

---

## 🧠 Tech Stack

- React + Vite  
- TypeScript  
- Express.js  
- PostgreSQL + Drizzle ORM  
- JWT Authentication (httpOnly cookies)  
- Server-Sent Events (SSE)  
- Stripe  

---

## ⚙️ Setup

```bash
npm install
npm run dev
```

---

## 🧭 Routes

- `/` → Landing page  
- `/login` → Login  
- `/signup` → Sign up  
- `/dashboard` → Church dashboard  
- `/display` → Live projector screen  
- `/remote` → Sermon controller  
- `/sermons/:id` → Sermon builder  
- `/billing` → Subscription management  
- `/settings` → Church settings  
- `/admin` → Owner panel  

---

## 🔄 How It Works

1. Create account  
2. Subscribe  
3. Create church workspace  
4. Build sermon flow  
5. Connect display screens  
6. Run live service  

---

## 🧩 Real-Time System

Backend controls all state.

- Backend = source of truth  
- SSE pushes updates  
- Displays only listen  
- Remote sends commands  

---

## 🏛️ Multi-Tenant Model

- Each church is isolated  
- Data scoped by workspace  
- Admin-per-church access  
- Owner global override  

---

## 🧠 Architecture (Optional Deep Dive)

<details>
<summary>Click to expand system architecture</summary>

- Server-authoritative event model  
- SSE-based real-time sync  
- State stored in PostgreSQL  
- Remote controls as command layer  
- Display clients are passive subscribers  

Command flow:

```
Remote → Backend → Database → SSE → Displays
```

</details>

---

## 🔥 Philosophy

> Sunday services should never fail because of software.

Built for:

- reliability  
- simplicity  
- real-time control  
- volunteer usability  

---

## 🧪 Status

- SaaS live in production  
- Stripe billing active  
- Real-time system working  
- Multi-tenant architecture deployed  

---

## 👑 Owner

Kairos Live by SureCatch  

