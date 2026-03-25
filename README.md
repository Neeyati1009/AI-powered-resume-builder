# AI-Powered Resume Builder

Full-stack resume builder with AI-powered text enhancement, PDF resume importing, multi-template preview, and public shareable resume links.

## 🚀 Project Overview

- Frontend: React 19 + Vite + Tailwind CSS
- Backend: Node.js + Express + MongoDB + Mongoose
- Auth: JWT-based user registration/login
- AI: OpenAI Chat Completions for summary/job-notification enhancement and resume parsing
- Image upload: ImageKit with optional background removal
- Static: Dynamic resume preview with 4 templates

## 📁 Repository Structure

- `client/`: frontend app
  - `src/App.jsx`: React Router + auth restore
  - `src/pages/`: pages for Home, Login, Dashboard, ResumeBuilder, Preview
  - `src/components/`: form sections + template preview
  - `src/app/features/authSlice.js`: Redux auth state
  - `src/configs/api.js`: axios base URL from `VITE_BASE_URL`

- `server/`: backend API
  - `server.js`: Express server + routes
  - `configs/`: database, multer, ImageKit, OpenAI config
  - `controllers/`: business logic for users, resumes, ai
  - `models/`: `User` + `Resume`
  - `routes/`: user, resume, ai routes

## 🛠️ Features

- Register + login
- User resumes CRUD
- Public/private resume toggle
- Live resume builder with section navigation
  - Personal info
  - Professional summary
  - Experience
  - Education
  - Projects
  - Skills
- Template switcher and accent color picker
- Uploaded profile image (with optional background removal via ImageKit)
- AI enhancement endpoints:
  - professional summary boost
  - job description boost
  - resume text extraction from uploaded PDF
- Resume preview, print/download and share (Web Share API)

## ⚙️ Environment Variables

### `server/.env`
- `PORT` (optional, default 3000)
- `MONGODB_URI` (required) e.g. `mongodb://localhost:27017`
- `JWT_SECRET` (required)
- `OPENAI_API_KEY` (required)
- `OPENAI_BASE_URL` (optional for custom endpoint)
- `OPENAI_MODEL` (required, e.g. `gpt-4o-mini`, depending on your account)
- `IMAGEKIT_PRIVATE_KEY` (for photo uploads / transforms)

### `client/.env`
- `VITE_BASE_URL` e.g. `http://localhost:3000`

## 🧩 Backend API Endpoints

### Auth / User
- `POST /api/users/register`  `{name,email,password}`
- `POST /api/users/login` `{email,password}`
- `GET /api/users/data` protected, returns user info
- `GET /api/users/resumes` protected, returns user resumes

### Resumes
- `POST /api/resumes/create` protected, body `{title}`
- `PUT /api/resumes/update` protected, form-data:
  - `resumeId`
  - `resumeData` (JSON string)
  - optional `image` file
  - optional `removeBackground` = `yes`
- `DELETE /api/resumes/delete/:resumeId` protected
- `GET /api/resumes/get/:resumeId` protected
- `GET /api/resumes/public/:resumeId` public

### AI
- `POST /api/ai/enhance-pro-sum` protected `{userContent}`
- `POST /api/ai/enhance-job-desc` protected `{userContent}`
- `POST /api/ai/upload-resume` protected `{title,resumeText}`

## 🧪 Run Locally

### 1. Backend
```bash
cd server
npm install
# development with reload
npm run server
# production
npm start
```

### 2. Frontend
```bash
cd client
npm install
npm run dev
```

Open `http://localhost:5173` (or URL from Vite)

## 🧾 Usage

1. Register or login
2. Create resume or upload existing PDF
3. Fill sections, pick template and color
4. Save changes
5. Make public to share via URL (`/view/:resumeId`)
6. Print/download directly from builder

## 🔐 Authorization

- Stored JWT token in `localStorage`
- Requests use header `Authorization: <token>`

## 🧹 Notes

- `resume.public` toggles public access; unsafely exposes only when set
- PDF upload uses `react-pdftotext` client-side
- OpenAI data is used for enhancement and extraction only

## 📦 Deploy

1. Deploy backend on Node-host (Heroku, Railway, Vercel Serverless with proper startup)
2. Build frontend with `npm run build` in `client`
3. Serve static files and connect to API URL



## 📝 License
MIT (or set your own)
