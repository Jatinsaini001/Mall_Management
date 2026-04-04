# 🏬 MallOS — Mall Management System

<div align="center">

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-2.x-000000?style=for-the-badge&logo=flask&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-Atlas-47A248?style=for-the-badge&logo=mongodb&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

**A full-stack web application for managing every aspect of a modern shopping mall — shops, staff, POS billing, inventory, security, and AI-powered insights.**

[🌐 Live Demo](#-live-demo) · [📸 Screenshots](#-screenshots) · [⚙️ Installation](#-installation) · [✨ Features](#-features)

</div>

---

## 📌 About The Project

MallOS solves a real operational problem: **managing a shopping mall is chaotic without a central system.** Shop rent tracking, employee records, daily billing, inventory control, customer loyalty, security incidents, and financial reports are all scattered across notebooks or Excel sheets.

MallOS brings everything into **one clean, role-based web dashboard** — accessible from any device, backed by MongoDB Atlas, and designed for actual mall operations.

---

## ✨ Features

### 🏪 Core Management
- **Shops** — Add/manage tenants, floors, rent amounts, and categories
- **Employees** — Full staff directory with department, salary, and join date
- **Inventory** — Product catalog with SKU, stock levels, cost/price, and low-stock alerts

### 💳 Point of Sale (POS)
- Live product search and cart system
- Discount support — percentage or flat amount
- Payment methods — Cash, Card, UPI (with QR code generation)
- Automatic stock deduction on every sale
- Loyalty points awarded to registered customers

### 📦 Orders & Returns
- Full order history with status pipeline (Pending / Completed / Returned)
- Stock auto-restored when order is marked as returned
- Detailed receipt view per order

### 👥 Customers & Suppliers
- Customer loyalty tiers (Bronze → Silver → Gold → Platinum)
- Points management and visit tracking
- Supplier directory with outstanding balance tracking

### 💰 Finance
- Expense recording by category
- Revenue vs expense profit/loss calculation
- Monthly expense charts

### 🔧 Operations
- **Maintenance** — Log repair requests with priority and technician assignment
- **Security** — Incident reporting with severity levels + CCTV camera status board
- **Mall Services** — Parking slots, events, food court stalls, cinema screens

### 📣 Marketing & Feedback
- Campaign management (Email / SMS / Social)
- Coupon/discount code system with usage limits
- Customer feedback and complaint management with staff responses

### 📊 Reports & AI Insights
- Monthly sales and expense charts
- Top products, payment breakdown, customer tier distribution
- AI-powered predictions: sales trend, fast/slow movers, dormant customer alerts
- Export reports to **Excel** or **PDF**

### 🔐 Authentication
- Three roles: **Admin**, **Manager**, **Cashier** — each with restricted access
- Session timeout after 30 minutes of inactivity
- Secure password hashing with Werkzeug

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| **Backend** | Python 3, Flask |
| **Database** | MongoDB Atlas (PyMongo) + SQLite (auth) |
| **Frontend** | Jinja2 Templates, HTML5, CSS3, Vanilla JS |
| **Auth** | Werkzeug password hashing, Flask sessions |
| **PDF Export** | ReportLab |
| **Excel Export** | Pandas + OpenPyXL |
| **Fonts** | Syne, DM Sans (Google Fonts) |
| **Deployment** | Render + MongoDB Atlas |

---

## 📁 Project Structure

```
mall_mgmt/
│
├── app.py                  ← All Flask routes (5 phases)
├── auth.py                 ← Authentication: login, logout, role decorators
├── database.py             ← MongoDB connection + all 17 collections
├── requirements.txt        ← Python dependencies
├── .env                    ← Secrets (NOT committed — see .env.example)
├── .env.example            ← Safe template to share with team
├── .gitignore              ← Git exclusions
│
├── templates/              ← Jinja2 HTML pages
│   ├── base.html           ← Master layout: sidebar, topbar, nav
│   ├── login.html          ← Login page
│   ├── dashboard.html      ← KPI overview + alerts
│   ├── pos.html            ← POS terminal
│   ├── orders.html         ← Order history
│   ├── inventory.html      ← Product catalog
│   ├── customers.html      ← Loyalty management
│   ├── suppliers.html      ← Supplier directory
│   ├── finance.html        ← Expense tracking
│   ├── reports.html        ← Charts + export
│   ├── aiinsights.html     ← AI predictions
│   └── ...                 ← (and more)
│
└── static/
    ├── css/style.css       ← Full dark theme + responsive CSS
    ├── js/main.js          ← Animations, flash dismiss
    └── qr/                 ← Auto-generated QR codes (not committed)
```

---

## ⚙️ Installation

### Prerequisites
- Python 3.10 or higher
- MongoDB Atlas account (free) **or** MongoDB installed locally
- Git

### Step 1 — Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/mallos.git
cd mallos
```

### Step 2 — Create a virtual environment

```bash
# Windows (CMD or PowerShell)
python -m venv venv
venv\Scripts\activate

# Mac / Linux
python3 -m venv venv
source venv/bin/activate
```

### Step 3 — Install dependencies

```bash
pip install -r requirements.txt
```

### Step 4 — Set up environment variables

```bash
# Windows
copy .env.example .env

# Mac/Linux
cp .env.example .env
```

Open `.env` and fill in your values:

```env
MONGO_URI=mongodb://localhost:27017/
DB_NAME=mall_management
SECRET_KEY=your_random_secret_key_here
```

> 💡 Generate a secure SECRET_KEY:
> ```bash
> python -c "import secrets; print(secrets.token_hex(32))"
> ```

### Step 5 — Run the app

```bash
python app.py
```

Open: **http://localhost:5000**

### Default Login Credentials

| Username | Password | Role |
|---|---|---|
| `admin` | `admin123` | Admin (full access) |
| `manager` | `manager123` | Manager |
| `cashier` | `cashier123` | Cashier (POS only) |

> ⚠️ Change these passwords immediately after first login.

---

## 🌐 Live Demo

Currently shared locally via **ngrok**:

```bash
# In a second terminal while app.py is running:
ngrok http 5000
```

Copy the `https://xxxx.ngrok.io` link and share it with anyone to access your local app.

---

## 📸 Screenshots

> Add screenshots to a `screenshots/` folder and update the table below.

| Dashboard | POS Terminal |
|---|---|
| ![Dashboard](dashboard.jpeg) | ![POS](POS.jpeg) |

| Reports | AI Insights |
|---|---|
| ![Reports](report.jpeg) | ![AI](aiinsights.jpeg) |

---

## ☁️ Deploy to Render (Free)

### 1. Set up MongoDB Atlas
1. [mongodb.com/atlas](https://www.mongodb.com/atlas) → Create free cluster
2. Database Access → Add user with read/write
3. Network Access → Allow `0.0.0.0/0`
4. Connect → Drivers → Copy URI

### 2. Deploy on Render
1. Push code to GitHub
2. [render.com](https://render.com) → New → Web Service → Connect repo
3. Settings:

| Setting | Value |
|---|---|
| Build Command | `pip install -r requirements.txt` |
| Start Command | `gunicorn app:app` |

4. Environment Variables → Add `MONGO_URI`, `DB_NAME`, `SECRET_KEY`
5. Click **Deploy**

---

## 🚀 Future Improvements

- [ ] SMS/Email notifications for low stock and maintenance alerts
- [ ] Dark/Light mode toggle
- [ ] Barcode scanner integration for POS
- [ ] Multi-mall support (multiple branches)
- [ ] Interactive Chart.js graphs on reports
- [ ] Automated MongoDB backups
- [ ] Two-Factor Authentication (TOTP)

---

## 📄 License

This project is licensed under the MIT License.

---

## 👨‍💻 Author

**Jatin Saini** · [GitHub](https://github.com/jatinsaini001)

---
<div align="center">Built with ❤️ using Flask & MongoDB</div>
