# Student Skill and Placement Management System

A complete **Flask + SQLAlchemy** web application built as a B.Tech project for managing
student profiles, skills, company listings, job postings, and placement applications — all with
role-based access for **Admin** and **Student** users.

---

## 📋 Table of Contents

1. [Project Overview](#1-project-overview)
2. [Features](#2-features)
3. [Technology Stack](#3-technology-stack)
4. [Project Structure](#4-project-structure)
5. [Installation](#5-installation)
6. [Running the Application](#6-running-the-application)
7. [Default Login Credentials](#7-default-login-credentials)
8. [Admin Features](#8-admin-features)
9. [Student Features](#9-student-features)
10. [Database Models](#10-database-models)
11. [URL Routes Reference](#11-url-routes-reference)
12. [Sample Data](#12-sample-data)
13. [CSV Export Reports](#13-csv-export-reports)
14. [Screenshots Overview](#14-screenshots-overview)
15. [Troubleshooting](#15-troubleshooting)
16. [License](#16-license)

---

## 1. Project Overview

The **Student Skill and Placement Management System** is a full-stack web application that
helps educational institutions manage the campus placement process digitally. It provides:

- A student portal to maintain profiles, add skills, apply for jobs, and track application status.
- An admin portal to manage companies, job postings, and student applications — with analytics
  charts and CSV export reports.

---

## 2. Features

| Feature | Admin | Student |
|---|---|---|
| Login / Register | ✅ | ✅ |
| View Dashboard with Charts | ✅ | ✅ |
| Manage Companies (CRUD) | ✅ | View Only |
| Manage Jobs (CRUD) | ✅ | View + Apply |
| Manage All Applications | ✅ | Own Only |
| View All Students | ✅ | ❌ |
| Update Application Status | ✅ | ❌ |
| Manage Own Profile | ❌ | ✅ |
| Add / Edit / Delete Skills | ❌ | ✅ |
| CSV Export Reports | ✅ | ❌ |

---

## 3. Technology Stack

| Component | Technology |
|---|---|
| Backend Framework | Flask 3.0.3 |
| ORM | Flask-SQLAlchemy 3.1.1 |
| Database | SQLite |
| Password Hashing | Werkzeug 3.0.3 |
| Frontend | Bootstrap 5.3, Bootstrap Icons |
| Charts | Chart.js 4.4.0 |
| Templating | Jinja2 |
| Language | Python 3.10+ |

---

## 4. Project Structure

```
student_placement_system/
├── app.py                        # Main Flask application, blueprint registration, seed data
├── config.py                     # App configuration (secret key, DB URI)
├── requirements.txt              # Python dependencies
├── README.md                     # This file
│
├── database/                     # Auto-created; holds placement.db (SQLite)
│
├── models/
│   ├── __init__.py
│   ├── user.py                   # User model (admin / student roles)
│   ├── student.py                # StudentProfile model
│   ├── skill.py                  # Skill model
│   ├── company.py                # Company model
│   ├── job.py                    # Job model
│   └── application.py            # Application model
│
├── routes/
│   ├── __init__.py
│   ├── auth_routes.py            # Login, Register, Logout
│   ├── student_routes.py         # Profile view/edit
│   ├── skill_routes.py           # Skill CRUD
│   ├── company_routes.py         # Company CRUD
│   ├── job_routes.py             # Job CRUD + search/filter
│   ├── application_routes.py     # Apply, My Applications, Admin Manage
│   ├── dashboard_routes.py       # Home, Admin Dashboard, Student Dashboard
│   └── report_routes.py          # Reports index, CSV exports
│
├── templates/
│   ├── base.html                 # Shared layout with navbar and footer
│   ├── home.html                 # Landing page
│   ├── login.html
│   ├── register.html
│   ├── student/
│   │   ├── dashboard.html
│   │   ├── profile.html          # View + Edit mode
│   │   └── skills.html           # Skills table with modals
│   ├── admin/
│   │   ├── dashboard.html        # Charts + Stat cards
│   │   ├── students.html
│   │   └── manage_applications.html
│   ├── jobs/
│   │   ├── list.html             # Search + Filter + Cards
│   │   ├── detail.html
│   │   └── form.html
│   ├── companies/
│   │   ├── list.html
│   │   └── form.html
│   ├── applications/
│   │   └── my_applications.html
│   └── reports/
│       └── index.html
│
└── static/
    ├── css/style.css             # Custom academic-style CSS
    └── js/script.js              # Auto-dismiss alerts, delete confirmations
```

---

## 5. Installation

### Prerequisites
- Python 3.10 or later
- pip

### Steps

```bash
# 1. Navigate to the project folder
cd student_placement_system

# 2. (Recommended) Create a virtual environment
python -m venv venv

# 3. Activate it
# On Windows:
venv\Scripts\activate
# On Mac/Linux:
source venv/bin/activate

# 4. Install dependencies
pip install -r requirements.txt
```

---

## 6. Running the Application

```bash
python app.py
```

The application will:
1. Auto-create the `database/` folder and `placement.db` SQLite file.
2. Insert sample data automatically (admin + 5 students + 4 companies + 6 jobs + 8 applications).
3. Start the Flask development server at **http://127.0.0.1:5000**

Open your browser and go to: **http://localhost:5000**

---

## 7. Default Login Credentials

### Admin Account
| Field | Value |
|---|---|
| Username | `admin` |
| Password | `admin123` |

### Student Accounts (password for all: `student123`)

| Username | Name | Department | CGPA |
|---|---|---|---|
| `rahul_s` | Rahul Sharma | Information Technology | 8.5 |
| `priya_m` | Priya Mehta | Information Technology | 7.8 |
| `arjun_k` | Arjun Kumar | Computer Science | 9.1 |
| `sneha_p` | Sneha Patel | Computer Science | 8.2 |
| `vikram_r` | Vikram Rao | Electronics | 7.5 |

---

## 8. Admin Features

- **Dashboard**: View total student/company/job/application counts. Two Chart.js charts:
  - Bar chart: Top 5 Jobs by number of applications
  - Doughnut chart: Application status distribution (Applied / Shortlisted / Selected / Rejected)
- **Students**: View all registered students in a table with CGPA badges, skills count, and
  application count.
- **Companies**: Add, edit, delete companies. Each company shows number of linked jobs.
- **Jobs**: Post new jobs, edit existing ones, delete, activate/deactivate. Search by title
  and filter by company.
- **Applications**: View all applications. Update status per application using an inline
  dropdown (Applied → Shortlisted → Selected → Rejected).
- **Reports**: Preview tables (first 10 rows each) for students, companies, jobs, applications.
  Download CSV exports for students, all applications, and selected-only students.

---

## 9. Student Features

- **Dashboard**: See skills count, applications count, active job count, and profile summary.
- **Profile**: View and edit personal and academic information (name, roll number, department,
  year, CGPA, gender, phone, career interest, resume link).
- **Skills**: Add skills with category (Programming, Database, Web Dev, etc.) and proficiency
  level (Beginner / Intermediate / Advanced). Edit and delete skills.
- **Jobs**: Browse all active jobs. Search by title, filter by company. Apply with one click.
  See "Already Applied" badge if already applied.
- **My Applications**: Track all submitted applications with status badges:
  - 🔵 Applied | 🟡 Shortlisted | 🟢 Selected | 🔴 Rejected

---

## 10. Database Models

| Model | Table | Key Fields |
|---|---|---|
| User | users | id, username, email, password_hash, role |
| StudentProfile | student_profiles | user_id, roll_number, name, dept, year, cgpa |
| Skill | skills | student_id, name, category, proficiency |
| Company | companies | name, industry, location, email, website |
| Job | jobs | title, company_id, required_skills, min_cgpa, deadline |
| Application | applications | student_id, job_id, status, applied_at |

---

## 11. URL Routes Reference

| Route | Method | Access | Description |
|---|---|---|---|
| `/` | GET | All | Home/landing page |
| `/auth/login` | GET, POST | Guest | Login form |
| `/auth/register` | GET, POST | Guest | Register form |
| `/auth/logout` | GET | Logged in | Logout |
| `/dashboard/admin` | GET | Admin | Admin dashboard |
| `/dashboard/student` | GET | Student | Student dashboard |
| `/admin/students` | GET | Admin | All students list |
| `/student/profile` | GET | Student | View profile |
| `/student/profile/edit` | GET, POST | Student | Edit profile |
| `/skill/` | GET | Student | List skills |
| `/skill/add` | POST | Student | Add skill |
| `/skill/edit/<id>` | POST | Student | Edit skill |
| `/skill/delete/<id>` | POST | Student | Delete skill |
| `/company/` | GET | Logged in | List companies |
| `/company/add` | GET, POST | Admin | Add company |
| `/company/edit/<id>` | GET, POST | Admin | Edit company |
| `/company/delete/<id>` | POST | Admin | Delete company |
| `/job/` | GET | Logged in | List jobs (search+filter) |
| `/job/<id>` | GET | Logged in | Job detail |
| `/job/add` | GET, POST | Admin | Post new job |
| `/job/edit/<id>` | GET, POST | Admin | Edit job |
| `/job/delete/<id>` | POST | Admin | Delete job |
| `/application/apply/<job_id>` | POST | Student | Apply to job |
| `/application/my` | GET | Student | My applications |
| `/application/manage` | GET | Admin | All applications |
| `/application/update_status/<id>` | POST | Admin | Update status |
| `/report/` | GET | Admin | Reports index |
| `/report/export/students` | GET | Admin | Download students CSV |
| `/report/export/applications` | GET | Admin | Download applications CSV |
| `/report/export/selected` | GET | Admin | Download selected CSV |

---

## 12. Sample Data

The `seed_data()` function in `app.py` auto-creates:

- **1 Admin**: username=`admin`, email=`admin@placement.com`
- **5 Students** with profiles, skills (2–3 each)
- **4 Companies**: TechCorp Solutions, InfoSys Ltd, DataWave Analytics, CloudNine Technologies
- **6 Jobs** across companies with deadlines and eligibility criteria
- **8 Applications** with mixed statuses (Applied, Shortlisted, Selected, Rejected)

Seeding runs **only if the database is empty** — safe to call on every startup.

---

## 13. CSV Export Reports

Three CSV exports available (Admin only, from `/report/`):

1. **students_report.csv** — Roll number, name, dept, CGPA, skills count, applications count
2. **applications_report.csv** — Full application details with student + job info
3. **selected_students_report.csv** — Only "Selected" applications for placement record

---

## 14. Screenshots Overview

| Page | What to Expect |
|---|---|
| Home | Hero section, 6 feature cards, Login/Register buttons |
| Login | Simple card form with demo credentials hint |
| Admin Dashboard | 5 stat cards + bar chart + doughnut chart |
| Student Dashboard | 3 stat cards + profile summary + quick links |
| Jobs List | Cards with search bar and company filter |
| My Applications | Table with color-coded status badges |
| Reports | 4 preview tables + 3 CSV download buttons |

---

## 15. Troubleshooting

**Q: I get `ModuleNotFoundError: No module named 'flask'`**
> Make sure you activated the virtual environment and ran `pip install -r requirements.txt`.

**Q: The database file doesn't exist / `OperationalError`**
> Delete `database/placement.db` (if corrupted) and restart `python app.py`. The DB and
> tables are recreated automatically.

**Q: Charts not showing on admin dashboard**
> Check that Chart.js loaded (requires internet for CDN). The bar/doughnut charts require
> at least one application to exist in the database.

**Q: `sqlite3.OperationalError: unable to open database file`**
> The `database/` directory couldn't be created. Make sure you run `python app.py` from
> inside the `student_placement_system/` folder.

**Q: Application status not updating**
> Make sure you're logged in as `admin`. Only admins can update application statuses.

---

## 16. License

This project is created for educational purposes as a B.Tech final-year project.
Free to use, modify, and extend for academic use.

---

*Built with ❤️ using Flask, SQLAlchemy, Bootstrap 5, and Chart.js*
