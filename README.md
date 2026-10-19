<div align="center">

# ♻️ BeryBox

**A community reuse platform where people and organizations donate, claim, and barter usable goods nearby — with real-time chat, map discovery, AI-assisted matching, and courier checkout.**

<br/>

<a href="https://berybox.web.id"><img src="https://img.shields.io/badge/▶_Live_Demo-0F766E?style=for-the-badge" alt="Live Demo"/></a>

<br/><br/>

<img src="https://img.shields.io/badge/React_19-20232A?style=for-the-badge&logo=react&logoColor=61DAFB" alt="React"/>
<img src="https://img.shields.io/badge/Redux_Toolkit-764ABC?style=for-the-badge&logo=redux&logoColor=white" alt="Redux Toolkit"/>
<img src="https://img.shields.io/badge/Vite-646CFF?style=for-the-badge&logo=vite&logoColor=white" alt="Vite"/>
<img src="https://img.shields.io/badge/Tailwind_CSS-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white" alt="Tailwind CSS"/>
<img src="https://img.shields.io/badge/Leaflet-199900?style=for-the-badge&logo=leaflet&logoColor=white" alt="Leaflet"/>
<img src="https://img.shields.io/badge/Express_5-000000?style=for-the-badge&logo=express&logoColor=white" alt="Express"/>
<img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white" alt="PostgreSQL"/>
<img src="https://img.shields.io/badge/Sequelize-52B0E7?style=for-the-badge&logo=sequelize&logoColor=white" alt="Sequelize"/>
<img src="https://img.shields.io/badge/Socket.IO-010101?style=for-the-badge&logo=socketdotio&logoColor=white" alt="Socket.IO"/>
<img src="https://img.shields.io/badge/Gemini-8E75B2?style=for-the-badge&logo=googlegemini&logoColor=white" alt="Gemini"/>
<img src="https://img.shields.io/badge/Groq-F55036?style=for-the-badge" alt="Groq"/>
<img src="https://img.shields.io/badge/Midtrans-002855?style=for-the-badge" alt="Midtrans"/>
<img src="https://img.shields.io/badge/AWS_EC2-232F3E?style=for-the-badge&logo=amazonwebservices&logoColor=FF9900" alt="AWS EC2"/>

</div>

---

## 📌 Overview

Plenty of usable things — clothes, books, toys, furniture — end up thrown away while someone nearby could use them. **BeryBox** connects those people. Users list items to **donate**, **offer to an organization** (orphanages, volunteer groups, communities), or **barter**, and others nearby can claim or make an offer.

Every exchange runs through a guided flow: request → approval → pickup or paid courier → tracking → review. Users and owners talk in a **real-time inbox**, a floating AI assistant (**BeryBot**) helps people find relevant items, and an **AI barter matcher** suggests fair swaps. A separate **admin CMS** handles reports and organization verification.

**My role:** built the user client and the admin CMS (React, Redux Toolkit, Leaflet, ImageKit, Socket.IO, Midtrans Snap), extended the Express/Sequelize API with BeryBot, AI barter matching, and courier payments, and deployed the apps to Vercel and the API to AWS EC2.

The project is a monorepo with three apps: the user **client**, the admin **CMS**, and an Express **server** (deployed to AWS EC2) kept at **90%+ Jest/Supertest coverage**.

---

## 🏗️ Architecture

```
┌──────────────────────────────┐   ┌──────────────────────────────┐
│   Client  (React + Vite)     │   │   CMS  (React + Vite)        │
│   Vercel · port 5173         │   │   Vercel · port 4174         │
│                              │   │                              │
│  Redux Toolkit · React Router│   │  Dashboard stats             │
│  Leaflet + OpenStreetMap     │   │  Organization verification   │
│  socket.io-client (inbox)    │   │  Reports: resolve/warn/ban   │
│  ImageKit uploads            │   │  AI organization research    │
│  Google Sign-In · Snap.js    │   │                              │
└──────────────┬───────────────┘   └──────────────┬───────────────┘
               │ REST + WebSocket                 │ REST
               ▼                                  ▼
┌─────────────────────────────────────────────────────────────────┐
│               Server  (Express 5 + Socket.IO) · AWS EC2         │
│                                                                 │
│  JWT auth · role authorization · helmet · rate limiting         │
│  Items · Requests · Shipping · Credits · Reviews · Reports      │
│  Conversations & messages · Notifications · Admin               │
│                                                                 │
│  ┌────────────┐  ┌──────────────────┐  ┌─────────────────────┐  │
│  │ PostgreSQL │  │ AI: Gemini →     │  │ ImageKit · Midtrans │  │
│  │ (Sequelize)│  │ Groq → local     │  │ Nominatim · Google  │  │
│  └────────────┘  │ fallback         │  │ Places · Google ID  │  │
│                  └──────────────────┘  └─────────────────────┘  │
└─────────────────────────────────────────────────────────────────┘
```

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| 🎁 **Three Ways to Share** | List items as a public donation, an offer to an organization, or a barter |
| ✅ **Donation Standards** | Items are checked for condition, category, and banned keywords (medicine, weapons, expired goods…) |
| 🗺️ **Map Discovery** | Nearby items and organizations shown on a Leaflet + OpenStreetMap map |
| 🔒 **Location Privacy** | Exact coordinates are never exposed; addresses come from Nominatim reverse geocoding |
| 🏠 **Organizations** | Verified orphanages and communities with photos from Google Places; owners can claim a profile |
| 🔄 **AI Barter Matching** | AI suggests barter pairs based on what each user offers and wants |
| 🤖 **BeryBot** | Floating AI assistant that answers using BeryBox's own items and organizations |
| 💬 **Real-time Inbox** | Socket.IO chat with typing indicators and live notifications |
| 🚚 **Pickup or Courier** | Free pickup when close (< 10 km), or a paid courier (Rp10.000 + Rp1.500/km) via Midtrans Snap |
| 📦 **Request Tracking** | Step-by-step progress from claim to delivery, with tracking updates |
| 💰 **Credit Settlement** | Barter value differences are settled with in-app credits |
| ⭐ **Reviews & Reports** | Rate exchanges and report items, users, or organizations |
| 🛡️ **Admin CMS** | Dashboard stats, organization verification, report handling (resolve, warn, ban) |
| 🔐 **Authentication** | Email/password and Google Sign-In with JWT; roles: `user`, `organization`, `admin` |

---

## 🛠️ Tech Stack

### 🖥️ Client & CMS
| Technology | Role |
|-----------|------|
| **React 19** + **Vite** | Two separate SPAs: user client and admin CMS |
| **Redux Toolkit** | Auth and notification state |
| **React Router 7** | Routing with role-based route guards |
| **Tailwind CSS 4** | Styling (design tokens via `@theme`) |
| **Leaflet** + **React Leaflet** | Maps and location picker |
| **socket.io-client** | Real-time chat and notifications |
| **Axios** | API client |
| **Motion** · **Phosphor Icons** | Animations and icons |
| **ImageKit** | Direct photo uploads from the browser |
| **Midtrans Snap.js** | Courier payment popup |

### ⚙️ Server
| Technology | Role |
|-----------|------|
| **Express 5** | REST API |
| **Socket.IO** | Chat rooms, typing events, and push notifications |
| **PostgreSQL** + **Sequelize** | Database, migrations, and seeders |
| **jsonwebtoken** + **bcryptjs** | Authentication |
| **google-auth-library** | Google ID token verification |
| **@google/generative-ai** + **groq-sdk** | BeryBot chat and barter matching (Gemini first, Groq fallback) |
| **imagekit** | Signed upload parameters |
| **midtrans-client** | Courier payment and webhook handling |
| **helmet** + **express-rate-limit** | Security headers and login/message rate limits |
| **Jest** + **Supertest** | Tests with 90%+ coverage |

---

## 🔌 REST API

Base URL: `http://localhost:3000` (no `/api` prefix) · Protected routes need `Authorization: Bearer <access_token>`

<details>
<summary><strong>Auth & Users</strong></summary>

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/register` | Register as `user` or `organization` |
| POST | `/login` | Log in (rate-limited) |
| POST | `/google-login` | Log in with Google |
| GET / PATCH | `/me` | View or update my profile |
| GET | `/users/:id` | Public user profile |
| GET | `/users/:id/reviews` | Reviews for a user |
| GET | `/images/auth` | ImageKit upload signature |
</details>

<details>
<summary><strong>Items & Requests</strong></summary>

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/items` | Feed with filters and pagination |
| GET | `/items/mine` | My items |
| GET | `/items/:id` | Item detail |
| POST | `/items` | Create an item |
| PATCH | `/items/:id` | Update my item |
| POST | `/items/:id/complete` | Mark as completed |
| DELETE | `/items/:id` | Cancel my item |
| POST | `/requests` | Claim, offer to an organization, or propose a barter |
| GET | `/requests/incoming` · `/requests/outgoing` | Requests I received / sent |
| PATCH | `/requests/:id` | Accept or reject |
| POST | `/requests/:id/shipping` | Choose pickup or courier |
| POST | `/requests/:id/pay` · `/pay/confirm` | Courier payment via Midtrans |
| PATCH | `/requests/:id/tracking` | Update delivery tracking |
| POST | `/requests/:id/redeem-credit` | Settle with credits |
| GET | `/history` | Completed exchanges |
| POST | `/midtrans/notification` | Midtrans webhook |
</details>

<details>
<summary><strong>Chat, Organizations & Notifications</strong></summary>

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/conversations` | Start a conversation |
| GET | `/conversations` | Inbox |
| GET / POST | `/conversations/:id/messages` | Message history / send (rate-limited) |
| GET | `/organizations` | Organization list |
| GET | `/organizations/:id` | Organization detail |
| POST | `/organizations` | Register an organization |
| POST | `/organizations/claim` | Claim an existing organization profile |
| GET | `/places/photo` | Organization photo proxy |
| GET | `/notifications` | My notifications |
| PATCH | `/notifications/:id/read` · `/notifications/read-all` | Mark as read |
</details>

<details>
<summary><strong>AI, Reviews & Admin</strong></summary>

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/ai/chat` | Ask BeryBot |
| POST | `/ai/match` | AI barter matching |
| POST | `/reviews` | Review a completed exchange |
| POST | `/reports` | Report an item, user, or organization |
| GET | `/admin/stats` | Dashboard statistics |
| GET / POST | `/admin/organizations` | List or add organizations |
| PATCH | `/admin/organizations/:id` | Approve or reject |
| POST | `/admin/ai/organization` | AI research on an organization |
| GET / PATCH | `/admin/reports` · `/admin/reports/:id` | List and resolve reports |
| POST | `/admin/users/:id/warn` · `/admin/users/:id/ban` | Moderate users |
| DELETE | `/admin/items/:id` | Remove an item |
</details>

<details>
<summary><strong>Socket.IO events</strong></summary>

| Direction | Event | Description |
|-----------|-------|-------------|
| client → server | `join_conversation` | Join a conversation room |
| client → server | `send_message` | Send a chat message |
| client → server | `typing` · `stop_typing` | Typing indicator |
| server → client | `new_message` | New message in a conversation |
| server → client | `user_typing` · `user_stop_typing` | The other user is typing |
| server → client | `new_notification` | Live notification |
</details>

---

## 🗂️ Project Structure

```
berybox/
├── client/                    # User app (React + Vite)
│   └── src/
│       ├── pages/             # Landing, Home, ItemDetail, ItemForm, Organizations,
│       │                      # Activity, Inbox, BarterMatch, Profile, History…
│       ├── components/        # AppShell, Cards, BeryBot, LocationPicker, UI kit
│       ├── context/           # UiContext, SocketContext
│       ├── hooks/             # useGeolocation, useImageKitUpload
│       ├── store/             # Redux: auth, notifications
│       └── api/               # Axios instance + endpoint calls
│
├── cms/                       # Admin app (React + Vite)
│   └── src/pages/             # Login, Dashboard, Organizations, Reports
│
└── server/                    # Express API + Socket.IO
    ├── routes/ controllers/
    ├── middlewares/           # authentication, authorization, errorHandler
    ├── helpers/               # jwt, haversine, shipping, credit, eligibility,
    │                          # geoPrivacy, nominatim, imagekit, midtrans…
    ├── services/              # Gemini, Groq, AI, messages, notifications
    ├── socket/                # Socket.IO setup and events
    ├── models/ migrations/ seeders/
    ├── postman/               # Postman collection
    └── __tests__/             # Jest + Supertest suites
```

---

## 🚀 Getting Started

### Prerequisites
- Node.js >= 20
- PostgreSQL
- Keys for [ImageKit](https://imagekit.io), [Gemini](https://aistudio.google.com/apikey) and/or [Groq](https://console.groq.com), [Midtrans Sandbox](https://dashboard.sandbox.midtrans.com), and Google OAuth (optional: Google Places)

### 1. Clone the repository
```bash
git clone https://github.com/mrusdiana/berybox.git
cd berybox
```

### 2. Start the server
```bash
cd server
cp .env-example.txt .env           # fill in DB, JWT, AI, ImageKit, Midtrans keys
npm install
npx sequelize-cli db:create
npx sequelize-cli db:migrate
npx sequelize-cli db:seed:all      # demo users, items, and organizations
npm run dev                        # http://localhost:3000
```

### 3. Start the client
```bash
cd client
cp .env.example .env
npm install
npm run dev                        # http://127.0.0.1:5173
```

### 4. Start the admin CMS (optional)
```bash
cd cms
cp .env.example .env
npm install
npm run dev                        # http://127.0.0.1:4174
```

> Missing optional keys don't crash the app — the related feature is disabled with a message in the UI.

<details>
<summary><strong>Environment variables</strong></summary>

**server/.env**

| Variable | Description |
|----------|-------------|
| `PORT`, `NODE_ENV` | Server settings |
| `JWT_SECRET`, `JWT_EXPIRES_IN` | Token settings |
| `DB_*` / `DATABASE_URL` / `TEST_DATABASE_URL` | PostgreSQL connection |
| `GEMINI_API_KEY`, `GEMINI_MODEL` | Gemini (primary AI) |
| `GROQ_API_KEY`, `GROQ_MODEL` | Groq (AI fallback) |
| `IMAGEKIT_PUBLIC_KEY`, `IMAGEKIT_PRIVATE_KEY`, `IMAGEKIT_URL_ENDPOINT` | Image uploads |
| `CLIENT_ORIGIN`, `CMS_ORIGIN` | Allowed CORS origins |
| `NOMINATIM_USER_AGENT` | User-Agent for reverse geocoding |
| `GOOGLE_CLIENT_ID`, `GOOGLE_PLACES_API_KEY` | Google login and organization photos |
| `MIDTRANS_SERVER_KEY`, `MIDTRANS_CLIENT_KEY`, `MIDTRANS_IS_PRODUCTION` | Courier payments |

**client/.env**

| Variable | Description |
|----------|-------------|
| `VITE_API_URL` | Backend URL (default `http://localhost:3000`) |
| `VITE_CMS_URL` | Where admin accounts are redirected |
| `VITE_GOOGLE_CLIENT_ID` | Google Sign-In |
| `VITE_IMAGEKIT_PUBLIC_KEY`, `VITE_IMAGEKIT_URL_ENDPOINT` | Photo uploads |
| `VITE_MIDTRANS_CLIENT_KEY`, `VITE_MIDTRANS_IS_PRODUCTION` | Snap.js |

**cms/.env**

| Variable | Description |
|----------|-------------|
| `VITE_API_URL` | Leave empty locally — Vite proxies `/login` and `/admin` to the server |
| `VITE_CLIENT_URL` | Link back to the user client |
</details>

---

## 🧪 Testing

```bash
cd server
npm test                   # run all suites
npm run test:coverage      # coverage report (> 90%)
```

External services (Gemini, Groq, ImageKit, Nominatim, Midtrans, Socket.IO) are mocked, so tests never hit the network. A Postman collection is available in `server/postman/`.

---

<div align="center">

Made with ❤️ by [Muhamad Rusdiana](https://github.com/mrusdiana) · [Portfolio](https://muhamad-rusdiana.vercel.app)

</div>
