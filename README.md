# 📦 SmartDrop — MERN Stack Delivery Platform

> **Fast. Smart. Reliable Delivery.** — Vellore's hyperlocal delivery app, converted from a single HTML file into a full production-grade MERN application.

---

## 🏗 Project Structure

```
smartdrop/
├── backend/                    ⚙️  Node.js + Express API
│   ├── config/
│   │   └── db.js               MongoDB connection
│   ├── models/
│   │   ├── User.js             User schema (user/partner/admin)
│   │   ├── Order.js            Order schema with timeline
│   │   └── Support.js          Support ticket schema
│   ├── controllers/
│   │   ├── userController.js   Auth, register, login, profile
│   │   ├── orderController.js  CRUD + stats
│   │   └── supportController.js Ticket management
│   ├── routes/
│   │   ├── userRoutes.js
│   │   ├── orderRoutes.js
│   │   └── supportRoutes.js
│   ├── middleware/
│   │   └── authMiddleware.js   JWT protect, adminOnly, partnerOnly
│   ├── .env.example
│   ├── server.js               Entry point
│   └── package.json
│
└── frontend/                   ⚛️  React + Vite
    ├── src/
    │   ├── api/
    │   │   ├── axios.js        Axios instance + interceptors
    │   │   └── index.js        API helper functions
    │   ├── context/
    │   │   ├── AuthContext.jsx JWT auth state
    │   │   └── LangContext.jsx EN / Tamil bilingual
    │   ├── components/
    │   │   ├── Navbar.jsx      Desktop top nav + mobile bottom nav
    │   │   ├── Footer.jsx
    │   │   ├── StatusBadge.jsx Reusable order/payment badge
    │   │   └── Spinner.jsx     Loading indicator
    │   ├── pages/
    │   │   ├── Home.jsx        Hero, cards, stats, features
    │   │   ├── Book.jsx        Booking form + live fare calc
    │   │   ├── Track.jsx       Order tracking + timeline + map
    │   │   ├── Partner.jsx     Partner dashboard (orders/earnings/register)
    │   │   ├── Support.jsx     Support ticket form
    │   │   ├── History.jsx     Order history with filter
    │   │   ├── Login.jsx       Login + register modal
    │   │   ├── Admin.jsx       Admin dashboard (KPI/orders/partners/pricing/support)
    │   │   └── AdminLogin.jsx  Dark admin login portal
    │   ├── styles/
    │   │   └── global.css      All design tokens from original HTML
    │   ├── App.jsx             Router
    │   └── main.jsx            React entry point
    ├── index.html
    ├── vite.config.js
    └── package.json
```

---

## 🚀 Quick Start

### 1. Prerequisites
- Node.js ≥ 18
- MongoDB running locally **or** a MongoDB Atlas connection string

### 2. Clone / Extract the project
```bash
cd smartdrop
```

### 3. Set up Backend
```bash
cd backend

# Copy and fill in environment variables
cp .env.example .env
# Edit .env:
#   MONGO_URI=mongodb://localhost:27017/smartdrop
#   JWT_SECRET=your_super_secret_key
#   PORT=5000

npm install
npm run dev        # starts on http://localhost:5000
```

### 4. Set up Frontend
```bash
cd frontend
npm install
npm run dev        # starts on http://localhost:5173
```

### 5. (Optional) Run both together from root
```bash
cd smartdrop
npm install        # installs concurrently
npm run dev        # starts backend + frontend together
```

---

## 🌐 API Endpoints

### Auth
| Method | Endpoint               | Access  | Description          |
|--------|------------------------|---------|----------------------|
| POST   | /api/users/register    | Public  | Register new user    |
| POST   | /api/users/login       | Public  | Login + get JWT      |
| GET    | /api/users/me          | Private | Get current user     |
| GET    | /api/users             | Admin   | Get all users        |
| GET    | /api/users/partners    | Admin   | Get all partners     |

### Orders
| Method | Endpoint               | Access        | Description            |
|--------|------------------------|---------------|------------------------|
| POST   | /api/orders            | Public        | Create order           |
| GET    | /api/orders/:id        | Public        | Track by orderId       |
| GET    | /api/orders/myorders   | Private       | User's own orders      |
| GET    | /api/orders            | Admin         | All orders             |
| GET    | /api/orders/stats      | Admin         | Dashboard stats        |
| PUT    | /api/orders/:id        | Admin/Partner | Update status          |

### Support
| Method | Endpoint               | Access  | Description            |
|--------|------------------------|---------|------------------------|
| POST   | /api/support           | Public  | Submit ticket          |
| GET    | /api/support           | Admin   | All tickets            |
| PUT    | /api/support/:id       | Admin   | Update ticket status   |

---

## 🔐 Authentication

JWT-based auth. The token is stored in `localStorage` and automatically attached to every request via Axios interceptor.

**Roles:**
- `user` — can book, track, view history
- `partner` — can view assigned orders, mark delivered
- `admin` — full access to dashboard, pricing, support

**Admin Portal:** Navigate to `/admin-login`
- Demo credentials: `admin@smartdrop.in` / `admin123`
- Locks after 3 failed attempts for 5 minutes

---

## 🌏 Bilingual Support (EN / தமிழ்)

The app supports full English and Tamil translations via `LangContext`. Toggle using the language buttons in the hero section or the navbar. All UI strings are driven by translation keys.

---

## 🎨 Design

- Pixel-perfect recreation of the original HTML design
- All CSS custom properties (tokens) preserved exactly
- Responsive: desktop top-nav, mobile bottom-nav
- Fonts: Outfit (headings), Nunito (body), Mukta (Tamil)

---

## ✨ Features

| Feature | Status |
|---------|--------|
| Book delivery with fare calc | ✅ |
| Real-time order tracking + timeline | ✅ |
| Animated map simulation | ✅ |
| Partner dashboard (orders/earnings/register) | ✅ |
| Admin dashboard (KPI/orders/partners/pricing/support) | ✅ |
| JWT auth with role-based access | ✅ |
| EN/Tamil bilingual | ✅ |
| Support ticket system | ✅ |
| Order history with filter | ✅ |
| Admin login lockout (3 attempts) | ✅ |
| Toast notifications | ✅ |
| Mobile responsive (bottom nav) | ✅ |
| Axios API integration + error handling | ✅ |
| Loading + error states | ✅ |
| Demo/offline fallback mode | ✅ |

---

## 📦 Tech Stack

| Layer     | Technology                          |
|-----------|-------------------------------------|
| Frontend  | React 18, Vite, React Router DOM v6 |
| Styling   | Custom CSS (design tokens), no framework |
| HTTP      | Axios with interceptors             |
| State     | React Context (Auth + Lang)         |
| Backend   | Node.js, Express 4                  |
| Database  | MongoDB + Mongoose                  |
| Auth      | JWT + bcryptjs                      |
| Dev tools | Nodemon, Concurrently               |
| Toasts    | react-hot-toast                     |

---

## 🛠 Extending the App

- **Payment (Stripe/Razorpay):** Add a `/api/orders/payment` route and integrate the SDK in `Book.jsx`
- **Real-time tracking:** Add Socket.io to the backend and listen in `Track.jsx`
- **Push notifications:** Add Firebase FCM to the backend order update flow
- **TypeScript:** Run `vite --template react-ts` and rename `.jsx` → `.tsx`
- **Tailwind CSS:** Install Tailwind and replace `global.css` class names

---

## 🧑‍💻 Made for Vellore

SmartDrop was designed specifically for Vellore's hyperlocal delivery market — covering Vellore City, Katpadi, Gudiyatham, Ranipet, and surrounding areas.
