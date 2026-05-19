# Kairos Live

Cloud-ready church presentation and scripture projection platform built for live services, volunteer teams, and multi-screen worship environments.

---

## Production Use

Kairos Live is designed to streamline live church presentation workflows by centralizing scripture projection, media control, and service management into a single real-time platform.

The system reduces presentation friction during services, improves volunteer coordination, and enables churches to manage live displays from multiple devices.

It functions as a lightweight SaaS workflow platform for real-time worship presentation and service operations.

---

## Problem

Many churches rely on:

- Manual scripture entry during services  
- Static slide software with limited collaboration  
- Complex AV workflows requiring technical operators  
- Inconsistent volunteer coordination  
- Expensive enterprise presentation software  
- Limited support for remote or multi-screen control  

Kairos Live solves these issues through a browser-based, cloud-ready presentation workflow system optimized for live worship environments.

---

## Usage

1. Admin creates or schedules a service  
2. Scriptures, songs, announcements, and media are added to the service queue  
3. Volunteers or operators connect to the live session  
4. Display screens sync in real time  
5. Presentation changes are broadcast instantly to connected displays  
6. Remote controllers can manage slides and scripture progression  
7. Live updates propagate without refreshing connected clients  

---

## Tech Stack

- React  
- TypeScript  
- Firebase / Supabase architecture concepts  
- Real-time database synchronization  
- WebSocket-style live updates  
- Cloud-hosted infrastructure  
- Authentication and session management  
- Responsive browser-based UI  

---

## Core Features

- Real-time scripture projection  
- Multi-screen synchronized displays  
- Live service management  
- Remote presentation controls  
- Browser-based access across devices  
- Volunteer-friendly workflow design  
- Real-time content updates without refresh  
- Presentation queue management  
- Responsive display system  
- Authentication and role-based workflows  
- Cloud-ready SaaS architecture  

---

## System Logic Overview

1. User authenticates into the platform  
2. Service session is created or loaded  
3. Presentation content is added to the queue  
4. Connected display clients subscribe to live updates  
5. Controller actions trigger real-time state updates  
6. Updates propagate across all connected clients  
7. Display screens render synchronized presentation content  

---

## Engineering Considerations

- **Real-Time Synchronization:** Live updates are propagated instantly across connected clients  
- **Scalable Architecture:** Designed for cloud-hosted multi-user environments  
- **Responsive UI:** Optimized for desktop, tablet, and presentation displays  
- **Operational Reliability:** Built for uninterrupted live-service workflows  
- **Workflow Simplicity:** Designed for non-technical volunteer usability  
- **Session State Management:** Synchronizes presentation state across clients  
- **Event-Driven Design:** Real-time actions trigger synchronized UI updates  

---

## SaaS & Cloud Alignment

Kairos Live is designed as a cloud-ready SaaS platform and aligns with modern distributed application architecture patterns.

The platform can map directly to cloud-native infrastructure such as:

- AWS Lambda / Cloud Functions  
- Firebase / Supabase real-time databases  
- API Gateway architectures  
- Cloud authentication providers  
- CDN-backed presentation delivery  
- WebSocket event systems  
- Multi-tenant SaaS infrastructure  

This project demonstrates:

- Real-time application architecture  
- SaaS platform design  
- Event-driven systems  
- Cloud workflow orchestration  
- Frontend/backend state synchronization  

---

## Future Improvements

- Mobile remote control app  
- OBS and livestream integration  
- AI-assisted scripture and song suggestions  
- Offline fallback mode  
- Multi-campus organization support  
- Presentation analytics dashboard  
- Service templates and automation  
- Advanced role permissions  
- Stripe subscription management  
- Internationalization (i18n) support  

---

## Setup

1. Clone the repository  
2. Install dependencies  
3. Configure environment variables  
4. Start the development server  
5. Connect database and authentication providers  

---

## Configure Environment

```env
VITE_API_URL=your_api_url
VITE_FIREBASE_API_KEY=your_key
VITE_AUTH_DOMAIN=your_domain
VITE_PROJECT_ID=your_project_id
```

---

## Run Locally

```bash
npm install
npm run dev
```

---

## Flow Overview

```text
Service Creation → Content Queue → Real-Time Sync Engine → Display Clients → Live Presentation Output
```

---

## How to Run

### Development Mode

```bash
npm run dev
```

Runs the local development server with live reload enabled.

---

### Production Build

```bash
npm run build
```

Generates an optimized production build for deployment.

---

## Summary

Kairos Live is a real-time worship presentation platform that combines cloud-ready SaaS architecture, live synchronization systems, and operational workflow automation into a single presentation environment.

The project demonstrates real-world engineering concepts used in:

- SaaS platforms  
- Real-time collaboration systems  
- Cloud-native applications  
- Event-driven architectures  
- Operational workflow platforms  
- Multi-client synchronization systems  

---
