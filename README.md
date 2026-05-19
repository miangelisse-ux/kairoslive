# ⛪ Kairos Live

https://kairos-livezip--miangelisse.replit.app/

Real-time church service operating system for scripture, sermons, and live presentation control.

Kairos Live is a SaaS platform that helps churches run Sunday services with live scripture display, sermon flow control, and multi-device synchronization — replacing PowerPoint, slide decks, and fragile presentation setups.

---

## 🚀 What It Does

Kairos Live lets churches run services in real time:

- 📖 Display Bible verses instantly on screens
- 🎤 Build and control sermon flows
- 📱 Control services from mobile or desktop
- 🖥️ Sync multiple display screens in real time
- 🌍 Switch Bible translations instantly
- 💳 Manage subscriptions via Stripe

---

## ⚡ Key Features

### 📺 Live Display
- Fullscreen projector mode (`/display`)
- Real-time updates (no refresh needed)
- Always shows last known state
- Clean church-branded presentation view

### 🎛️ Sermon Control
- Create sermon flows
- Add verses, text, and slides
- Next / previous / start / stop controls
- Mobile-friendly remote control (`/remote`)

### 📖 Bible System
- Multiple translations (KJV, RVR, BBE, etc.)
- Reference lookup (John 3:16)
- Keyword search for live use

### 🏢 Church Workspaces
- Each church has its own isolated space
- Role-based access (admin / user)
- Secure multi-tenant system

### 💳 Subscriptions
- Monthly & yearly plans
- Stripe billing integration
- Upgrade / downgrade anytime

---

## 🧠 Tech Stack

- React + Vite
- TypeScript
- Express.js backend
- PostgreSQL + Drizzle ORM
- JWT authentication (httpOnly cookies)
- Server-Sent Events (real-time updates)
- Stripe payments

---

## 📦 Project Structure

```
artifacts/
  api-server/        Backend API (Express)
  church-display/    Frontend (Dashboard + Display + Remote)

lib/
  db/                Database schema (Drizzle)
  api-spec/          API contracts
  api-client-react/  React API hooks
```

---

## 🔐 Environment Variables

```env
DATABASE_URL=
JWT_SECRET=

OWNER_EMAIL=miangelisse@gmail.com

STRIPE_SECRET_KEY=
STRIPE_WEBHOOK_SECRET=

STRIPE_STARTER_PRICE_ID=
STRIPE_GROWTH_PRICE_ID=
STRIPE_PRO_PRICE_ID=

STRIPE_STARTER_YEARLY_PRICE_ID=
STRIPE_GROWTH_YEARLY_PRICE_ID=
STRIPE_PRO_YEARLY_PRICE_ID=

RESEND_API_KEY=
REPLIT_DOMAINS=
```

---

## 🧭 Routes

- `/` → Landing page  
- `/login` → Sign in  
- `/signup` → Create account  
- `/dashboard` → Church dashboard  
- `/display` → Live projector screen  
- `/remote` → Sermon controller  
- `/sermons/:id` → Sermon builder  
- `/billing` → Subscription management  
- `/settings` → Church settings  
- `/admin` → Owner dashboard  

---

## 🔄 How It Works

1. Create an account  
2. Subscribe to a plan  
3. Create a church workspace  
4. Build sermon flow (verses + slides)  
5. Connect display screen  
6. Control live service in real time  

---

## 🧩 Real-Time System

- Backend is the source of truth
- Display listens for updates in real time
- Remote controls update backend only
- No direct edits from display screen

This ensures all devices stay perfectly in sync during live services.

---

## 🏛️ Multi-Tenant System

- Each church is fully isolated
- Data is scoped by church workspace
- Users only access their own church
- Admins manage their own environment
- Owner has global system access

---

## 💡 Core Idea

> Sunday services should never fail because of software.

Everything is built to be:
- fast
- simple
- real-time
- reliable
- volunteer-friendly

---

## 🧪 Status

Kairos Live is live and in active production use:

- SaaS system fully working
- Stripe payments active
- Real-time display system live
- Multi-tenant architecture deployed

---

## 🚀 Run Locally

```bash
npm install
npm run dev
```

Then open the Replit web preview.

---

## 👑 Owner

Kairos Live by SureCatch

Owner: `surecatchautomations@gmail.com`

---

## 📄 License

Proprietary — all rights reserved.
