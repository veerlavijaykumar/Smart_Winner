# 🎟️ EventHub – Event Booking System

A production-ready full-stack Event Booking System built with the MERN stack, inspired by Eventbrite/Ticketmaster.

---

## 📸 Screenshots

> _Place screenshots here after running the app._
>
> | Home Page | Event Detail | Admin Dashboard |
> |-----------|-------------|-----------------|
> | ![home](screenshots/home.png) | ![detail](screenshots/event-detail.png) | ![admin](screenshots/admin.png) |

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | React 18 + Vite 5 |
| Styling | Tailwind CSS 3 |
| Routing | React Router v6 |
| HTTP Client | Axios |
| Payment | Stripe (test mode) |
| Backend | Node.js 18 + Express 4 |
| Database | MongoDB 7 + Mongoose 8 |
| Auth | JWT + bcrypt |
| Email | Nodemailer |
| Scheduler | node-cron |

---

## ✨ Features

- Browse & search upcoming events with filters (category, price, date)
- Pagination for event listings
- Event detail page with Stripe checkout
- JWT Authentication (register / login)
- Role-based access (User / Admin)
- Protected routes on both frontend and backend
- Admin Dashboard (stats, manage events, manage bookings)
- Create / Edit events with full form validation
- Real-time ticket availability validation
- Booking confirmation emails (Nodemailer)
- 24-hour event reminder emails (node-cron)
- Calendar UI for event date display
- Toast notifications
- Responsive design (mobile-first)

---

## 📁 Folder Structure

```
Smart_Winner_Internship/
├── backend/
│   ├── config/          # Database connection
│   ├── controllers/     # Route handler logic
│   │   ├── authController.js
│   │   ├── eventController.js
│   │   ├── bookingController.js
│   │   ├── paymentController.js
│   │   └── adminController.js
│   ├── middleware/      # Auth, error, validation middleware
│   ├── models/          # Mongoose schemas (User, Event, Booking)
│   ├── routes/          # Express routes
│   ├── utils/           # JWT helper, email service, cron job
│   ├── .env.example
│   ├── package.json
│   └── server.js
│
└── frontend/
    ├── src/
    │   ├── api/          # Axios API service modules
    │   ├── components/   # Reusable UI components
    │   │   ├── admin/
    │   │   ├── checkout/
    │   │   ├── events/
    │   │   ├── layout/
    │   │   └── ui/
    │   ├── context/      # React AuthContext
    │   ├── pages/        # Route-level page components
    │   │   └── admin/
    │   ├── App.jsx
    │   ├── main.jsx
    │   └── index.css
    ├── index.html
    ├── vite.config.js
    ├── tailwind.config.js
    └── package.json
```

---

## ⚙️ Environment Variables

### Backend (`backend/.env`)

```env
PORT=5000
NODE_ENV=development

# MongoDB Atlas or local
MONGO_URI=mongodb://localhost:27017/event_booking

# JWT
JWT_SECRET=your_super_secret_jwt_key_change_in_production
JWT_EXPIRE=30d

# Stripe
STRIPE_SECRET_KEY=your_stripe_secret_key_here
STRIPE_PUBLISHABLE_KEY=REMOVEDxxxxxxxxxxxxxxxxxxxxxxxx
STRIPE_WEBHOOK_SECRET=whsec_xxxxxxxxxxxxxxxxxxxxxxxx

# Email (Gmail example)
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_USER=your_email@gmail.com
EMAIL_PASS=your_app_password
EMAIL_FROM=noreply@eventbooking.com

# Frontend URL (for CORS)
CLIENT_URL=http://localhost:3000
```

### Frontend (`frontend/.env`)

```env
VITE_API_URL=http://localhost:5000/api
VITE_STRIPE_PUBLISHABLE_KEY=REMOVEDxxxxxxxxxxxxxxxxxxxxxxxx
```

---

## 🚀 Setup & Installation

### Prerequisites

| Tool | Version |
|------|---------|
| Node.js | v18+ |
| npm | v9+ |
| MongoDB | v6+ (local) or MongoDB Atlas |

---

### 1. Clone the repository

```bash
git clone <your-repo-url>
cd Smart_Winner_Internship
```

---

### 2. Setup Backend

```bash
cd backend

# Install dependencies
npm install

# Copy .env.example and fill in your values
cp .env.example .env

# Start development server
npm run dev
```

Backend runs on: **http://localhost:5000**

---

### 3. Setup Frontend

```bash
cd frontend

# Install dependencies
npm install

# Copy .env.example and fill in your values
cp .env.example .env

# Start development server
npm run dev
```

Frontend runs on: **http://localhost:3000**

---

## 💳 Stripe Test Cards

Use these card numbers in the Stripe checkout (test mode):

| Card | Number | Expiry | CVC |
|------|--------|--------|-----|
| Visa (success) | `4242 4242 4242 4242` | Any future date | Any 3 digits |
| Visa (decline) | `4000 0000 0000 0002` | Any future date | Any 3 digits |
| 3D Secure | `4000 0025 0000 3155` | Any future date | Any 3 digits |

---

## 👤 Default Test Users

> Create these by registering via the UI or seeding.

| Role | Email | Password |
|------|-------|----------|
| User | user@test.com | password123 |
| Admin | admin@test.com | password123 |

> In development mode, select "Admin" in the register form to create an admin account.

---

## 📡 API Endpoints

### Auth
| Method | Route | Access |
|--------|-------|--------|
| POST | `/api/auth/register` | Public |
| POST | `/api/auth/login` | Public |
| GET | `/api/auth/me` | Private |
| PUT | `/api/auth/profile` | Private |

### Events
| Method | Route | Access |
|--------|-------|--------|
| GET | `/api/events` | Public |
| GET | `/api/events/featured` | Public |
| GET | `/api/events/:id` | Public |
| POST | `/api/events` | Admin |
| PUT | `/api/events/:id` | Admin |
| DELETE | `/api/events/:id` | Admin |

### Bookings
| Method | Route | Access |
|--------|-------|--------|
| POST | `/api/bookings` | Private |
| GET | `/api/bookings/my` | Private |
| GET | `/api/bookings/:id` | Private |
| PUT | `/api/bookings/:id/cancel` | Private |

### Payments
| Method | Route | Access |
|--------|-------|--------|
| GET | `/api/payments/config` | Public |
| POST | `/api/payments/create-intent` | Private |
| POST | `/api/payments/webhook` | Stripe |

### Admin
| Method | Route | Access |
|--------|-------|--------|
| GET | `/api/admin/stats` | Admin |
| GET | `/api/admin/users` | Admin |
| GET | `/api/admin/bookings` | Admin |
| PUT | `/api/admin/events/:id/availability` | Admin |
| PUT | `/api/admin/events/:id/toggle` | Admin |

---

## 📧 Email Configuration

In **development** mode, emails are logged to the terminal console instead of being sent (no SMTP required).

For production, configure Gmail or any SMTP provider in your `.env`. For Gmail, use an **App Password** (not your account password) with 2FA enabled.

---

## 🔔 Event Reminders

A cron job runs every hour and sends reminder emails to users whose events are happening in approximately 24 hours. This is automatic and requires no additional setup.

---

## 🏗️ Build for Production

### Backend
```bash
cd backend
NODE_ENV=production node server.js
# Or use PM2: pm2 start server.js --name event-api
```

### Frontend
```bash
cd frontend
npm run build
# Serve dist/ with nginx or any static host (Vercel, Netlify, etc.)
```

---

## 🔒 Security Notes

- Passwords are hashed with **bcrypt** (12 salt rounds)
- JWTs expire after **30 days** (configurable)
- Admin role cannot be self-assigned in production mode
- Stripe webhooks are verified with the webhook secret
- All admin routes are double-protected (JWT + role check)
- CORS is restricted to the frontend URL in production

---

## 📦 Key Dependencies

```
Backend:
  express ^4.18.2        – HTTP framework
  mongoose ^8.0.3        – MongoDB ODM
  bcryptjs ^2.4.3        – Password hashing
  jsonwebtoken ^9.0.2    – JWT auth
  stripe ^14.5.0         – Payment processing
  nodemailer ^6.9.7      – Email sending
  node-cron ^3.0.3       – Scheduled reminders
  express-validator ^7.0.1 – Input validation

Frontend:
  react ^18.2.0          – UI framework
  vite ^5.0.8            – Build tool
  tailwindcss ^3.3.6     – Utility CSS
  react-router-dom ^6.20.1 – Client-side routing
  @stripe/react-stripe-js ^2.4.0 – Stripe UI
  axios ^1.6.2           – HTTP client
  react-hot-toast ^2.4.1 – Toast notifications
  react-calendar ^4.8.0  – Calendar UI
  date-fns ^2.30.0       – Date formatting
  react-icons ^4.12.0    – Icon library
```

---

## 📄 License

MIT © 2026 EventHub
