# JOB HUB — AI-Powered Internship & Placement Platform

> **"Find the right opportunity before you even search for it."**

JOB HUB is an AI-first career platform designed primarily for university students and fresh graduates. It connects job seekers with internships and entry-level positions using deep resume understanding, hybrid semantic job matching, skill-gap analysis, and intelligent location-based alerts.

---

## 🌟 Core Differentiator: Proactive AI Placement

Unlike generic, passive job boards where students must repeatedly search and filter, JOB HUB proactively matches candidates to opportunities the moment an employer publishes a role:

1. **Job Description Parsing**: Extracts required skills, preferred skills, experience level, and academic prerequisites.
2. **Semantic Text Embeddings**: Generates multi-dimensional document vectors of candidate profiles and job requirements.
3. **Hybrid Scoring Engine**: Computes explainable match scores (0–100%) using 4 weighted dimensions:
   - **40%** Semantic similarity (TF-IDF & sentence vectors)
   - **30%** Technical skill overlap (canonical taxonomy coverage)
   - **15%** Academic degree and internship experience fit
   - **15%** Geographic proximity and job type alignment
4. **Location-Aware Proximity**: Uses the Haversine formula to compute great-circle distance between the candidate's explicitly configured hub and the employer's facility.
5. **Instant Alert Delivery**: If the match satisfies the student's configured threshold (e.g., ≥ 70%), an in-app alert and notification are dispatched immediately.

---

## 🎯 Key Capabilities by Persona

### 👨‍🎓 Job Seeker (Student / Graduate)
- **AI Resume Parsing**: Uploads PDF or DOCX (up to 5 MB); extracts education, CGPA, technical skills, projects, and work experience.
- **Review & Correction Workflow**: Review AI-extracted fields with interactive skill chips before confirming the profile.
- **Intelligent Dashboard**: View Profile Strength (87%), New Matches count, Nearby Opportunities, and Top Matches.
- **Explainable Match Scores**: Understand *why* a role matches (*"✓ Your Python experience matches"*, *"✓ 3.4 km from your preferred location"*, *"• Missing: Docker"*).
- **Skill Gap Roadmap**: Personalized learning recommendations and curated tutorials for missing skills.
- **Location-Based Alerts**: Configurable hub (e.g. Savar, Banani, Dhanmondi, Uttara) with customizable radius (2 km, 5 km, 10 km, 20 km) and privacy guarantee (no continuous GPS tracking).
- **Horizontal Application Tracker**: Pipeline monitoring through `APPLIED` → `VIEWED` → `SHORTLISTED` → `INTERVIEW` → `HIRED`.
- **Real-Time Recruiter Chat**: Direct messaging with hiring managers with persistent job context.

### 🏢 Recruiter / Employer
- **Company Management**: Verified company profiles (e.g., TechNova Labs, Brain Station 23, Therap BD).
- **AI Job Description Assistant**: Automatically detects and separates required vs. preferred skills and qualifications.
- **Ranked Candidate Pipeline**: Applicants ordered dynamically by match percentage.
- **Stage Progression Controls**: Move candidates through the hiring pipeline with automatic notifications sent to candidates.
- **Direct Candidate Messaging**: Reach out to top-matching students with 1 click.

### 🛡️ Platform Admin
- **Operations Dashboard**: Total users, candidate distributions, and successful match metrics.
- **Visual Analytics**: Skill demand breakdown, geographic hub distribution, and candidate match curves.
- **User Governance**: Deactivate or suspend accounts.
- **Recruiter Approvals**: Review and verify new employers.

---

## 🏗️ Architecture & Monorepo Structure

```
JOB HUB/
├── frontend/                     # React + Vite + Tailwind CSS Frontend
│   ├── src/
│   │   ├── components/           # Navbar, Sidebar, JobCard, SkillMatchBreakdown, Modals
│   │   ├── pages/                # Dashboards, Search, Job Details, Applications, Profile, Chat
│   │   ├── context/              # AuthContext, NotificationContext
│   │   ├── services/             # Axios API client with JWT interceptor
│   │   ├── index.css             # Tailwind base layers, Inter typography
│   │   └── App.jsx               # Role-based routing and protected layouts
│   └── package.json
│
├── backend/                      # FastAPI Python Application
│   ├── app/
│   │   ├── api/                  # Auth, Jobs, Seekers, Recruiters, Applications, Chat, Admin, Resume
│   │   ├── models/               # SQLAlchemy Models (User, Job, Application, MatchRecord, etc.)
│   │   ├── schemas/              # Pydantic Schemas
│   │   ├── services/             # Hybrid Matching, Location Proximity, Notifications
│   │   ├── ai/                   # Resume Parser, Job Parser, Gemini LLM Client with Fallback
│   │   ├── auth/                 # Bcrypt Hashing, JWT Security, Dependency Injection
│   │   ├── websocket/            # Real-Time WebSocket Connection Manager
│   │   ├── config.py             # Settings and weight configurations
│   │   ├── database.py           # Database engine & session maker
│   │   └── main.py               # FastAPI entrypoint
│   ├── tests/                    # Pytest test suite (10/10 automated tests passing)
│   ├── seed_data.py              # Bangladesh seed data (12 companies, 32 jobs, 20 seekers)
│   └── requirements.txt
│
├── database/
│   ├── seed/schema.sql           # PostgreSQL reference schema with pgvector compatibility
│   └── migrations/
│
├── .env.example                  # Environment variables template
├── docker-compose.yml            # Dockerized PostgreSQL, Backend & Frontend
└── README.md
```

---

## 🔑 Demo Accounts (1-Click Switchers Available)

| Persona | Email | Password | Details |
| :--- | :--- | :--- | :--- |
| **Job Seeker** | `sarah.rahman@jobhub.io` | `password123` | Sarah Rahman • DIU SE Graduate • 87% Match • Savar |
| **Recruiter** | `recruiter@technova.io` | `password123` | Tanvir Ahmed • TechNova Labs (Savar) • 12 Active Jobs |
| **Platform Admin** | `admin@jobhub.io` | `password123` | Admin Console • Analytics & User Management |

*Note: You can switch between Job Seeker and Recruiter personas instantly via the **Demo Switch** dropdown in the top navigation bar. Platform Admin is accessible by signing in with the admin credentials above.*

---

## 🚀 Quick Start Guide

### Prerequisites
- **Python 3.10+**
- **Node.js 18+** & **npm**

---

### 1. Backend Setup

```powershell
# Navigate to backend
cd backend

# Install dependencies
python -m pip install -r requirements.txt

# Seed realistic demo database (12 companies, 32 jobs, 20 seekers, chats)
python seed_data.py

# Start the FastAPI server
python -m uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload
```

The backend API will be available at:
- API Base: `http://localhost:8000/api/v1`
- Interactive Swagger Documentation: `http://localhost:8000/docs`

---

### 2. Frontend Setup

```powershell
# Navigate to frontend in a new terminal
cd frontend

# Install dependencies
npm install

# Start the Vite development server
npm run dev
```

Open `http://localhost:5173` in your browser.

---

## 🧪 Running Automated Tests

Run the test suite covering authentication, location calculations, hybrid matching, and AI parsing:

```powershell
cd backend
python -m pytest -v tests/test_job_hub.py
```

Result: **10 passed in ~15s** (100% test pass rate).

---

## 🗺️ Geographic Hubs Covered (Bangladesh)
- **Savar / Daffodil Smart City** (23.8560, 90.2600)
- **Banani** (23.7937, 90.4043)
- **Mohakhali** (23.7776, 90.4005)
- **Dhanmondi** (23.7461, 90.3742)
- **Uttara** (23.8759, 90.3795)
- **Mirpur** (23.8071, 90.3686)
- **Gulshan** (23.7925, 90.4178)

---

## 🛡️ Security & Privacy Guarantees
- **No Live GPS Tracking**: Candidates choose their hub explicitly with customizable alert radiuses.
- **Ethical AI**: Name, age, gender, photo, religion, and marital status are never used in match calculations.
- **Zero Automatic Rejections**: Candidates are ranked by suitability; AI never automatically rejects applicants.
- **Secure Authentication**: Bcrypt salt rounds with standard HS256 JWT tokens.

---

## 📄 License
MIT License. Created for University Students & Placement Ecosystems.

##Author 
*Saif Al Saad*
