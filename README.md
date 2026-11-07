# 💰 Money Manager

A full-stack personal finance tracker. Users sign up, activate their account by email, log in with JWT, and manage income and expenses by category — with a dashboard, filters, Excel export, and automated email reminders.

**Stack:** React · Tailwind CSS · Spring Boot · Spring Security · MySQL

---

## ✨ Features

- **Authentication** — registration with email activation link, JWT-based login (stateless)
- **Categories** — create and update custom income/expense categories (per user)
- **Income & Expense** — add, list, and delete transactions linked to a category
- **Dashboard** — total balance, total income, total expense, recent transactions
- **Filters** — search by type, date range, keyword, with sorting
- **Excel export** — download income/expense as `.xlsx`, or have it emailed (Apache POI)
- **Email notifications** — scheduled daily reminders and daily expense summary
- **Data isolation** — every query is scoped to the logged-in user
- **Profile photo** — uploaded from the frontend to Cloudinary

---

## 🏗️ Project Structure

```
backend/            # Spring Boot backend
└── src/main/java/.../
    ├── config/          # Security & CORS configuration
    ├── controller/      # REST controllers
    ├── dto/             # Request/response objects
    ├── entity/          # JPA entities (Profile, Category, Income, Expense)
    ├── repository/      # Spring Data JPA repositories
    ├── security/        # JWT request filter
    ├── service/         # Business logic (email, Excel, notifications, ...)
    └── util/            # JWT utility

frontend/      # React frontend (Vite)
└── src/
    ├── components/      # Reusable UI (Menubar, Sidebar, forms, lists, charts)
    ├── pages/           # Landing, Login, Signup, Home, Income, Expense, Category, Filter
    ├── context/         # AppContext (global user state)
    ├── hooks/           # useUser (route protection)
    └── util/            # axios config, API endpoints, helpers
```

---

## 🔌 API Overview

Base URL: `http://localhost:8080/api/v1.0`

| Method | Endpoint | Description | Auth |
|---|---|---|---|
| POST | `/register` | Register a new user | Public |
| GET | `/activate?token=` | Activate account | Public |
| POST | `/login` | Log in, returns JWT | Public |
| GET | `/profile` | Current user profile | JWT |
| POST / GET | `/categories` | Add / list categories | JWT |
| GET | `/categories/{type}` | Categories by type | JWT |
| PUT | `/categories/{categoryId}` | Update a category | JWT |
| POST / GET | `/incomes` | Add / list current-month incomes | JWT |
| DELETE | `/incomes/{id}` | Delete an income | JWT |
| POST / GET | `/expenses` | Add / list current-month expenses | JWT |
| DELETE | `/expenses/{id}` | Delete an expense | JWT |
| GET | `/dashboard` | Dashboard summary | JWT |
| POST | `/filter` | Filter transactions | JWT |
| GET | `/excel/download/income` | Download income Excel | JWT |
| GET | `/excel/download/expense` | Download expense Excel | JWT |
| GET | `/email/income-excel` | Email income Excel | JWT |
| GET | `/email/expense-excel` | Email expense Excel | JWT |
| GET | `/status`, `/health` | Health check | Public |

---

## 🚀 Getting Started (Local)

### Prerequisites
- Java 21
- Maven (or use the included `mvnw`)
- Node.js 18+
- MySQL 8+

### 1. Database
```sql
CREATE DATABASE moneymanager;
```
Tables are created automatically (`spring.jpa.hibernate.ddl-auto=update`).

### 2. Backend

Set these environment variables (never commit real secrets):

| Variable | Example |
|---|---|
| `DB_URL` | `jdbc:mysql://localhost:3306/moneymanager` |
| `DB_USERNAME` | `root` |
| `DB_PASSWORD` | `your_password` |
| `SMTP_HOST` | `smtp.gmail.com` |
| `SMTP_PORT` | `587` |
| `GMAIL_USERNAME` | `you@gmail.com` |
| `GMAIL_PASSWORD` | Gmail **App Password** |
| `JWT_SECRET` | long random string (32+ chars) |
| `MONEY_MANAGER_FRONTEND_URL` | `http://localhost:5173` |
| `MONEY_MANAGER_BACKENDURL` | `http://localhost:8080/api/v1.0` |

> Use whichever SMTP provider you configured (Gmail or Brevo) and match the variable names in `application.properties`.

Run:
```bash
cd backend
./mvnw spring-boot:run
```
Backend starts on `http://localhost:8080`.

### 3. Frontend
In `src/util/apiEndpoints.js` set:
```js
export const BASE_URL = "http://localhost:8080/api/v1.0";
```
Then:
```bash
cd frontend
npm install
npm run dev
```
Frontend starts on `http://localhost:5173`.

---

## 🐳 Docker (backend)

```bash
./mvnw clean package -DskipTests
docker build -t moneymanager .
docker run -p 9090:9090 --env-file .env moneymanager
```

---

## 🧰 Tech Details

**Backend:** Spring Boot, Spring Security, Spring Data JPA (Hibernate), JJWT, Spring Mail, Apache POI, Lombok, MySQL

**Frontend:** React, Vite, Tailwind CSS, React Router, Axios, Recharts, React Hot Toast, Lucide React, Moment, Emoji Picker React

---

## 🗺️ Roadmap

- [ ] Apache Kafka for async email and report generation
- [ ] AI-powered expense categorization and monthly insights
- [ ] Natural-language finance chatbot
- [ ] Password reset flow
- [ ] Budget limits and recurring transactions

---

## 👤 Author

**Mohini Chaudhari** — [GitHub](https://github.com/mohini-chaudhari2)
