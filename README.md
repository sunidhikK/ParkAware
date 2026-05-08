# 🅿️ Smart Parking System

A full-stack, production-quality Smart Parking System web application with beautiful UI, JWT authentication, real-time slot management, and comprehensive admin analytics — all simulated via software with no hardware required.

![Tech Stack](https://img.shields.io/badge/React-18-blue) ![Express](https://img.shields.io/badge/Express-4-green) ![SQLite](https://img.shields.io/badge/SQLite-3-orange) ![Tailwind](https://img.shields.io/badge/Tailwind-3-purple)

---

## 📋 Prerequisites

- **Node.js** v18+ (download from [nodejs.org](https://nodejs.org))
  - To check: run `node -v` in terminal — should show `v18.x.x` or higher
- **npm** (comes with Node.js — verify with `npm -v`)
- **Terminal** (Command Prompt / PowerShell on Windows, Terminal on macOS/Linux)

---

## 🪟 Windows Setup (Step-by-Step)

### 1. Install Node.js
- Download the **Windows Installer (.msi)** from https://nodejs.org (LTS version recommended)
- Run the installer → click Next through all steps → check "Automatically install tools" if prompted → Finish
- **Restart your PC** after installing

### 2. Verify Installation
Open **Command Prompt** (Win+R → type `cmd` → Enter) or **PowerShell** and run:
```cmd
node -v
npm -v
```
Both should show version numbers. If not, reinstall Node.js.

### 3. Extract the Project
- Right-click `smart_parking.zip` → **Extract All** → Choose a location (e.g., `C:\Users\YourName\Desktop\smart_parking`)

### 4. Install Dependencies
Open **Command Prompt** and run:
```cmd
cd C:\Users\YourName\Desktop\smart_parking\backend
npm install

cd ..\frontend
npm install
```
(Replace `YourName` with your actual Windows username)

### 5. Start Backend Server
Open **Command Prompt** (Terminal 1):
```cmd
cd C:\Users\YourName\Desktop\smart_parking\backend
npm run dev
```
You should see: `🚗 Smart Parking Backend running on http://localhost:5000`

**⚠️ Keep this window open!**

### 6. Start Frontend Server
Open a **new Command Prompt** window (Terminal 2):
```cmd
cd C:\Users\YourName\Desktop\smart_parking\frontend
npm run dev
```
You should see: `Local: http://localhost:5173/`

### 7. Open the App
Open your browser (Chrome recommended) and go to: **http://localhost:5173**

### 🛑 To Stop the Servers
Press `Ctrl+C` in each Command Prompt window.

---

## 🚀 Quick Start — macOS / Linux (3 commands)

After extracting the zip, open a terminal in the `smart_parking` folder:

```bash
# 1. Install all dependencies (backend + frontend)
cd backend && npm install && cd ../frontend && npm install && cd ..

# 2. Start backend (keep this terminal open)
cd backend && npm run dev
```

Open a **second terminal** in the `smart_parking` folder:

```bash
# 3. Start frontend
cd frontend && npm run dev
```

Open **http://localhost:5173** in your browser. That's it!

---

## 🚀 Detailed Setup Guide

### Step 1: Extract the zip

Extract `smart_parking.zip` to any folder. You'll see:
```
smart_parking/
├── backend/       ← Node.js + Express API server
├── frontend/      ← React + Vite app
└── README.md      ← This file
```

### Step 2: Install Backend Dependencies

Open a terminal, navigate into the project, and run:

```bash
cd smart_parking/backend
npm install
```

This installs: express, better-sqlite3, jsonwebtoken, bcryptjs, cors

### Step 3: Install Frontend Dependencies

In the same terminal (or a new one):

```bash
cd smart_parking/frontend
npm install
```

This installs: react, vite, tailwindcss, framer-motion, recharts, axios, lucide-react, etc.

### Step 4: Start the Backend Server

Open a terminal and run:

```bash
cd smart_parking/backend
npm run dev
```

The backend starts on **http://localhost:5000**. On first run, it automatically:
- Creates the SQLite database (`backend/db/parking.db`)
- Seeds **60 parking slots** across 3 floors (A, B, C — 20 each)
- Pre-occupies **15 slots** with active parking sessions
- Creates **5 recent completed sessions** for activity history
- Creates a default **admin** and **customer** account

> ⚠️ **Keep this terminal open** — the backend must stay running.

### Step 5: Start the Frontend Dev Server

Open a **second terminal** and run:

```bash
cd smart_parking/frontend
npm run dev
```

The frontend starts on **http://localhost:5173**

### Step 5: Open the App

Navigate to **http://localhost:5173** in your browser.

> 💡 **Tip**: To run both servers simultaneously with one command, install `concurrently` globally: `npm i -g concurrently`, then from the project root: `concurrently "cd backend && npm run dev" "cd frontend && npm run dev"`

---

## 🔐 Default Login Credentials

| Role     | Email                 | Password     |
|----------|-----------------------|--------------|
| Admin    | admin@parking.com     | admin123     |
| Customer | customer@parking.com  | customer123  |

---

## 🎯 Feature Walkthrough

### Customer Features

1. **Login/Register** — Sign in or create a new customer account from the login page.

2. **Dashboard** — After login, see an overview with:
   - Available/Occupied/Total slot counts with animated counters
   - Active parking session card (if you have one) with live duration timer
   - Quick-action links to Parking View and History

3. **Parking View** — The main booking interface:
   - **Floor Switcher** — Toggle between Floor A, B, C with animated indicator
   - **Slot Grid** — Color-coded cards: green (available), red (occupied), amber (reserved)
   - **Slot Types** — Each slot shows its type: Regular, EV, Handicap, or VIP with icons
   - Click any green slot → **Booking Modal** opens
   - Enter vehicle number plate
   - Choose **Park Now** (immediate) or **Reserve** (15-minute hold)
   - If you already have active parking, click your slot → **Checkout Modal**
   - Click **Exit & Pay** to calculate fare and receive a **digital receipt**

4. **Parking History** — View all past parking sessions:
   - Entry/exit times, duration, charges
   - Click **Receipt** on any completed session to view/print the digital receipt

5. **Dark/Light Mode** — Toggle from the sidebar

### Admin Features

1. **Dashboard** — Comprehensive overview:
   - 8 stat cards: Total Slots, Occupied, Available, Revenue Today, Total Revenue, Active Vehicles, Reserved, Long-Parked (12h+)
   - **Revenue Analytics Chart** — Daily or weekly view with interactive area chart (Recharts)
   - **Recent Activity** table — Latest parking events

2. **Parking Logs** — Full parking record table:
   - All fields: ID, Vehicle, Customer, Slot, Floor, Entry/Exit, Duration, Charge, Status
   - **Search & Filter** — By date, vehicle number, or slot number
   - **Pagination** — Navigate through records
   - **Export CSV** — Download all filtered records as a CSV file

3. **Slot Management** — Visual grid with admin controls:
   - View all slots per floor with their current status
   - **Manual Override** — Mark any slot as Available or Occupied
   - Warnings shown for vehicles parked over 12 hours

---

## ⚙️ System Details

### Parking Slots (Auto-Seeded)

| Floor | Regular (70%) | EV (15%) | Handicap (10%) | VIP (5%) | Total |
|-------|--------------|----------|----------------|----------|-------|
| A     | 14           | 3        | 2              | 1        | 20    |
| B     | 14           | 3        | 2              | 1        | 20    |
| C     | 14           | 3        | 2              | 1        | 20    |
| **Total** | **42**   | **9**    | **6**          | **3**    | **60**|

### Pricing

| Period       | Rate       | Details                              |
|-------------|------------|--------------------------------------|
| Normal      | ₹30/hour   | First hour flat, then ₹0.50/min     |
| Peak Hours  | ₹50/hour   | 9–11 AM & 5–8 PM (IST)              |
| Minimum     | ₹20        | Regardless of duration               |

### Reservation Timer

- Reserved slots auto-release after **15 minutes** if the user doesn't check in
- Backend checks and cleans expired reservations every 60 seconds

### Long-Parking Warnings

- Vehicles parked over **12 hours** are flagged with a warning icon
- Admin dashboard shows a count of long-parked vehicles

---

## 🛠️ Tech Stack

| Layer      | Technology                                      |
|------------|------------------------------------------------|
| Frontend   | React 18, Tailwind CSS 3, Framer Motion, Vite  |
| Backend    | Node.js, Express.js                             |
| Database   | SQLite (via better-sqlite3)                     |
| Auth       | JWT (jsonwebtoken + bcryptjs)                   |
| Charts     | Recharts                                        |
| Icons      | Lucide React                                    |
| HTTP       | Axios                                           |
| Routing    | React Router v6                                 |
| Dates      | date-fns                                        |

---

## 📁 Project Structure

```
smart-parking/
├── backend/
│   ├── server.js              # Express server entry point
│   ├── package.json
│   ├── db/
│   │   └── database.js        # SQLite setup, seeding, cleanup
│   ├── middleware/
│   │   └── auth.js            # JWT authentication middleware
│   ├── routes/
│   │   ├── auth.js            # Auth routes (login, register, me)
│   │   ├── slots.js           # Slot routes (list, reserve, park, checkin)
│   │   ├── parking.js         # Parking routes (exit, history, receipt)
│   │   └── admin.js           # Admin routes (stats, logs, revenue, export)
│   └── controllers/
│       ├── authController.js
│       ├── slotController.js
│       ├── parkingController.js
│       └── adminController.js
│
└── frontend/
    ├── index.html
    ├── package.json
    ├── vite.config.js
    ├── tailwind.config.js
    ├── postcss.config.js
    └── src/
        ├── main.jsx
        ├── App.jsx
        ├── index.css           # Tailwind + custom glassmorphism styles
        ├── api/
        │   └── axios.js        # Axios instance with auth interceptor
        ├── context/
        │   ├── AuthContext.jsx  # Auth state management
        │   └── ThemeContext.jsx # Dark/Light theme toggle
        ├── components/
        │   ├── Sidebar.jsx     # Navigation sidebar with icons
        │   ├── SlotCard.jsx    # Animated parking slot card
        │   ├── BookingModal.jsx    # Book/Reserve slot dialog
        │   ├── CheckoutModal.jsx   # Exit/Checkin dialog
        │   ├── ReceiptModal.jsx    # Digital receipt with print
        │   ├── StatsCard.jsx       # Animated stat counter card
        │   ├── FloorSwitcher.jsx   # Floor A/B/C toggle
        │   └── ProtectedRoute.jsx  # Role-based route guard
        └── pages/
            ├── Login.jsx
            ├── Register.jsx
            ├── CustomerDashboard.jsx
            ├── ParkingView.jsx
            ├── MyHistory.jsx
            ├── AdminDashboard.jsx
            ├── AdminParkingLog.jsx
            └── AdminSlotManagement.jsx
```

---

## 🎨 UI Design

- **Dark theme** with deep navy/purple gradients and glassmorphism
- **Vibrant accents**: Cyan, Emerald, Violet
- **Smooth animations**: Framer Motion page transitions, slot card animations, animated counters
- **Slot cards**: Pulse animation on occupied, glow on hover for available
- **Responsive**: Works on desktop and mobile
- **Dark/Light mode**: One-click toggle from sidebar

---

## 📡 API Endpoints

### Auth
- `POST /api/auth/register` — Register new customer
- `POST /api/auth/login` — Login (returns JWT)
- `GET /api/auth/me` — Get current user (requires auth)

### Slots
- `GET /api/slots?floor=A` — List slots (optional floor filter)
- `GET /api/slots/:id` — Get single slot
- `POST /api/slots/:id/park` — Park immediately
- `POST /api/slots/:id/reserve` — Reserve for 15 min
- `POST /api/slots/:id/checkin` — Check in after reservation

### Parking
- `POST /api/parking/:id/exit` — Exit and calculate fare
- `GET /api/parking/my-history` — Customer's parking history
- `GET /api/parking/active-session` — Current active session
- `GET /api/parking/receipt/:id` — Get receipt for completed session

### Admin (requires admin role)
- `GET /api/admin/stats` — Dashboard statistics
- `GET /api/admin/logs` — Parking logs with filters
- `GET /api/admin/revenue?period=daily` — Revenue analytics
- `PATCH /api/admin/slots/:id` — Override slot status
- `GET /api/admin/export` — Export records as CSV
