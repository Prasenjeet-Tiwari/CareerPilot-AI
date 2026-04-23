

# CareerPilot-AI

**AI-Powered Interview Preparation & Resume Optimization Platform**

> A full-stack GenAI application that analyzes resumes against job descriptions, generates targeted interview questions, and produces ATS-optimized resumes — with hallucination-free AI outputs and enterprise-grade authentication.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Tech Stack](#tech-stack)
- [System Architecture](#system-architecture)
- [Getting Started](#getting-started)
- [Environment Variables](#environment-variables)
- [API Documentation](#api-documentation)
- [Project Structure](#project-structure)
- [Engineering Highlights](#engineering-highlights)


---

## Overview

CareerPilot-AI bridges the gap between job seekers and applicant tracking systems. Users upload their resume (PDF) and paste a target job description. The platform:

1. **Extracts** and parses PDF content using `Multer` + `pdf-parse`
2. **Analyzes** skill gaps by comparing resume content against the JD via `Google Gemini AI`
3. **Generates** role-specific interview questions and ATS-friendly resume content
4. **Exports** a polished, formatted PDF resume using a `Gemini HTML → Puppeteer` conversion pipeline
5. **Persists** all user history securely in `MongoDB Atlas` with `JWT` protected sessions

The frontend follows a strict **4-layer React architecture** (UI → API Services → Context API → Custom Hooks) to ensure scalability and separation of concerns.

---

## Key Features

| Feature | Description |
|---|---|
| **📄 Intelligent PDF Parsing** | Extracts raw text from uploaded resumes using Multer and pdf-parse |
| **🎯 Skill Gap Analysis** | Compares resume against job descriptions using Gemini AI |
| **🤖 AI Interview Questions** | Generates contextual, role-specific technical and behavioral questions |
| **✅ Hallucination Guard** | Zod schema validation ensures structured, predictable AI outputs |
| **📑 ATS Resume Generator** | Produces optimized HTML content and converts to PDF via Puppeteer |
| **🔐 Secure Authentication** | JWT-based auth with token blacklisting for secure logout |
| **📜 Persistent History** | MongoDB Atlas stores previous analyses and generated resumes per user |

---

## Tech Stack

**Frontend**
- React.js
- Context API (Global State Management)
- Custom Hooks (Business Logic Abstraction)
- CSS3 / Responsive Design

**Backend**
- Node.js
- Express.js (REST API)
- JWT Authentication + Token Blacklisting
- Multer (File Upload)
- pdf-parse (PDF Text Extraction)
- Puppeteer (PDF Generation)

**AI & Data**
- Google Gemini API
- Zod (Output Schema Validation)

**Database**
- MongoDB Atlas
- Mongoose ODM

---

## System Architecture

```
┌─────────────────┐      ┌──────────────────┐      ┌─────────────────┐
│   React Client  │──────▶│  Express Server  │──────▶│  MongoDB Atlas  │
│  (4-Layer Arch) │◀─────▶│   (REST API)     │◀─────▶│   (User Data)   │
└─────────────────┘      └──────────────────┘      └─────────────────┘
                                │
                                ▼
                    ┌──────────────────────┐
                    │   Google Gemini AI   │
                    │  + Zod Validation    │
                    └──────────────────────┘
                                │
                    ┌───────────┴───────────┐
                    ▼                       ▼
            [Skill Gap Analysis]    [Interview Questions]
                    │                       │
                    ▼                       ▼
            [HTML Resume Gen] ──▶ [Puppeteer PDF Export]
```

---

## Getting Started

### Prerequisites

- Node.js (v18+)
- npm or yarn
- MongoDB Atlas cluster (or local MongoDB instance)
- Google Gemini API key

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/Prasenjeet-Tiwari/CareerPilot-AI.git
cd CareerPilot-AI

# 2. Install server dependencies
cd server
npm install

# 3. Install client dependencies
cd ../client
npm install
```

### Configuration

Create a `.env` file in the `/server` directory. See [Environment Variables](#environment-variables) below.

### Running the Application

```bash
# Terminal 1 — Start the backend
cd server
npm run dev

# Terminal 2 — Start the frontend
cd client
npm start
```

The application will be available at `http://localhost:3000`.

---

## Environment Variables

Create a `.env` file in the `server/` directory:

```env
# Server Configuration
PORT=5000
NODE_ENV=development

# Database
MONGODB_URI=your_mongodb_atlas_connection_string

# Authentication
JWT_SECRET=your_super_secret_jwt_key
JWT_EXPIRE=7d

# AI Service
GEMINI_API_KEY=your_google_gemini_api_key

# Client URL (for CORS)
CLIENT_URL=http://localhost:3000
```

> **Security Note:** Never commit your `.env` file. The repository should include a `.env.example` file without real values.

---

## API Documentation

### Authentication

| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/api/auth/register` | Register a new user |
| `POST` | `/api/auth/login` | Authenticate user, returns JWT |
| `POST` | `/api/auth/logout` | Blacklist JWT token, secure logout |

### Resume & Analysis

| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/api/resume/upload` | Upload PDF resume (Multer multipart) |
| `POST` | `/api/analysis/gaps` | Analyze skill gaps (Resume vs JD) |
| `POST` | `/api/interview/questions` | Generate AI interview questions |
| `POST` | `/api/resume/optimize` | Generate ATS-optimized HTML content |
| `GET`  | `/api/resume/download/:id` | Download generated PDF via Puppeteer |
| `GET`  | `/api/history` | Fetch user's analysis history |

### Request Example: Skill Gap Analysis

```http
POST /api/analysis/gaps
Authorization: Bearer <jwt_token>
Content-Type: application/json

{
  "resumeText": "Extracted text from PDF...",
  "jobDescription": "We are looking for a React developer with TypeScript..."
}
```

### Response Example

```json
{
  "success": true,
  "data": {
    "missingSkills": ["TypeScript", "Jest", "CI/CD"],
    "matchedSkills": ["React", "Node.js", "MongoDB"],
    "recommendations": "Focus on unit testing and DevOps fundamentals...",
    "score": 72
  }
}
```

---

## Project Structure

```
CareerPilot-AI/
├── client/                     # React Frontend
│   ├── public/
│   ├── src/
│   │   ├── components/         # Reusable UI components
│   │   ├── context/            # AuthContext, AppContext
│   │   ├── hooks/              # useAuth, useResume, useAnalysis
│   │   ├── services/           # API service layer (axios instances)
│   │   ├── pages/              # Route-level pages
│   │   ├── utils/              # Helpers & formatters
│   │   └── App.jsx
│   └── package.json
│
├── server/                     # Node.js Backend
│   ├── config/                 # DB connection, env validation
│   ├── controllers/            # Route controllers
│   ├── middleware/             # Auth, error handling, upload
│   ├── models/                 # Mongoose schemas (User, Resume, History)
│   ├── routes/                 # API route definitions
│   ├── utils/                  # Gemini client, Zod schemas, Puppeteer PDF
│   ├── server.js               # Entry point
│   └── package.json
│
├── .env.example
├── .gitignore
└── README.md
```

---

## Engineering Highlights

### 1. Four-Layer React Architecture
The frontend is deliberately architected into four distinct layers to prevent prop-drilling and separate concerns:
- **UI Layer:** Pure presentational components
- **API Service Layer:** Centralized Axios instances with interceptors for JWT
- **Context Layer:** Global state for auth and app-wide data
- **Custom Hooks Layer:** Encapsulated business logic (e.g., `useResumeUpload`, `useAnalysis`)

### 2. JWT Authentication with Token Blacklisting
Standard JWTs are stateless, meaning a leaked token remains valid until expiry. CareerPilot implements a **token blacklist** in MongoDB, ensuring immediate invalidation upon logout — a critical security practice for production applications.

### 3. Hallucination-Free AI Outputs with Zod
Raw LLM outputs are non-deterministic. We enforce strict **Zod schemas** on Gemini responses, validating structure and types before they reach the client. If the AI hallucinates or returns malformed JSON, the request fails gracefully with a typed error rather than corrupting the UI.

### 4. Server-Side PDF Pipeline
The ATS resume generation uses a two-stage pipeline:
1. **Gemini** generates optimized, semantic HTML content tailored to the job description
2. **Puppeteer** renders the HTML headlessly and exports a print-ready PDF on the server

This approach guarantees consistent styling across devices and prevents client-side rendering inconsistencies.

### 5. Secure File Handling
Resume uploads use `Multer` with strict file-type validation (PDF only) and size limits. Parsed text is processed server-side; original files are handled as streams where possible to minimize memory footprint.

---



