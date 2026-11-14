# Smart Lost & Found Portal – Recover

A complete full-stack web application for reporting, searching and recovering lost belongings in public places.

## 🚀 Tech Stack
- **Frontend**: React + Vite + Tailwind CSS + Recharts
- **Backend**: FastAPI + SQLAlchemy + SQLite
- **Auth**: JWT + bcrypt
- **AI Matching**: TF-IDF + Cosine Similarity + Perceptual Hashing

---

## ⚙️ Installation & Setup

### Prerequisites
- Python 3.10+ 
- Node.js 18+
- npm 9+

### 1. Clone / Navigate to Project
```powershell
cd c:\lost_and_found_portal
```

### 2. Backend Setup
```powershell
cd backend

# Install Python dependencies
pip install -r requirements.txt

# Initialize database and seed demo data
python seed.py

# Start the backend server
uvicorn app.main:app --reload --port 8000
```

The API will be available at: http://localhost:8000  
Swagger docs: http://localhost:8000/docs

### 3. Frontend Setup (new terminal)
```powershell
cd frontend

# Install Node dependencies
npm install

# Start the development server
npm run dev
```

The application will be available at: http://localhost:5173

---

## 🔐 Demo Credentials

| Role  | Email                    | Password    |
|-------|--------------------------|-------------|
| Admin | admin@recover.local      | admin@123   |
| User  | priya@demo.local         | demo@123    |
| User  | rahul@demo.local         | demo@123    |
| User  | anjali@demo.local        | demo@123    |
| User  | kiran@demo.local         | demo@123    |

---

## 🗂️ Project Structure

```
lost_and_found_portal/
├── backend/
│   ├── app/
│   │   ├── main.py           # FastAPI app entry point
│   │   ├── config.py         # Settings from .env
│   │   ├── database.py       # SQLAlchemy engine + session
│   │   ├── models/           # SQLAlchemy models
│   │   ├── schemas/          # Pydantic request/response schemas
│   │   ├── routers/          # API route handlers
│   │   │   ├── auth.py
│   │   │   ├── lost_items.py
│   │   │   ├── found_items.py
│   │   │   ├── matches.py
│   │   │   ├── recovery.py
│   │   │   ├── notifications.py
│   │   │   └── admin.py
│   │   ├── services/
│   │   │   ├── matching_service.py   # TF-IDF + cosine similarity
│   │   │   ├── image_matching.py     # Perceptual hashing
│   │   │   └── notification_service.py
│   │   ├── auth/             # JWT + password hashing
│   │   └── utils/            # Helpers
│   ├── uploads/              # Uploaded images stored here
│   ├── seed.py               # Demo data seeder
│   ├── .env                  # Environment variables
│   └── requirements.txt
│
├── frontend/
│   ├── src/
│   │   ├── components/       # Reusable UI components
│   │   ├── pages/            # Page components
│   │   │   └── admin/        # Admin-only pages
│   │   ├── layouts/          # Layout wrappers
│   │   ├── services/         # API service functions
│   │   ├── context/          # React context (Auth)
│   │   └── utils/            # Helper functions
│   ├── vite.config.js
│   └── package.json
│
└── README.md
```

---

## 🧠 Intelligent Matching Algorithm

### Text Matching
1. Fields combined: item name, category, description, brand, colour, features, location
2. Text preprocessed: lowercase, punctuation removed, whitespace normalized
3. TF-IDF vectorization applied
4. Cosine similarity calculated → score 0–100%

### Image Matching
1. Images loaded and resized to 128×128
2. Perceptual hash (pHash) computed
3. Hamming distance between hashes → similarity 0–100%

### Combined Score
- Text: 70% weight
- Image: 30% weight (skipped gracefully if no image)

### Score Interpretation
| Score     | Label              |
|-----------|--------------------|
| 80–100%   | High Match         |
| 60–79%    | Moderate Match     |
| 40–59%    | Low Match (shown)  |
| Below 40% | Not shown          |

---

## 📋 Features

- ✅ User registration & JWT login
- ✅ Report lost items with photo upload
- ✅ Report found items with photo upload
- ✅ Automatic TF-IDF + image matching on submission
- ✅ Browse & search with filters
- ✅ Potential matches page with score breakdown
- ✅ Recovery request workflow (5-stage)
- ✅ Admin dashboard with charts
- ✅ Admin: approve/reject matches & recovery requests
- ✅ In-app notification system
- ✅ Role-based access control (user/admin)
- ✅ Responsive design (mobile + desktop)

---

## 🔧 Configuration

Edit `backend/.env` to change:
- `SECRET_KEY` – Change in production!
- `ACCESS_TOKEN_EXPIRE_MINUTES` – Token lifetime
- `TEXT_MATCH_WEIGHT` / `IMAGE_MATCH_WEIGHT` – Matching weights
- `MATCH_THRESHOLD` – Minimum score to store a match (0.0–1.0)

---

## 📸 Image Uploads
Images are stored in `backend/uploads/`. Max size: 5MB. Allowed formats: JPG, PNG, GIF, WebP.

---

## 🎓 Academic Note
This project is built for a PBL (Project-Based Learning) academic submission demonstrating:
- Full-stack web development
- Database design & ORM
- NLP-based similarity (TF-IDF + cosine similarity)
- Computer vision (perceptual hashing)
- JWT authentication & RBAC
- RESTful API design
- Data visualization with charts
