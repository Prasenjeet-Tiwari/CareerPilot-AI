
# CareerPilot-AI 🚀
**The Intelligent Bridge Between Your Resume and Your Next Role.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![React](https://img.shields.io/badge/Frontend-React.js-blue)](https://reactjs.org/)
[![Node](https://img.shields.io/badge/Backend-Node.js-green)](https://nodejs.org/)
[![AI](https://img.shields.io/badge/AI-Google%20Gemini-orange)](https://deepmind.google/technologies/gemini/)

CareerPilot-AI is a full-stack generative AI platform designed to automate the most tedious parts of job hunting. By leveraging the **Google Gemini Pro** model, it provides deep skill-gap analysis and generates hyper-personalized interview questions based on your actual resume and a target job description.

---

## 🌟 Key Features

* **📄 Intelligent PDF Parsing:** Seamlessly extracts text from uploaded resumes using `pdf-parse` and `Multer`.
* **🎯 Skill Gap Analysis:** Analyzes your resume against a Job Description to highlight missing keywords and technical requirements.
* **🤖 AI Interview Coach:** Generates role-specific technical and behavioral questions to prepare you for the real deal.
* **🔐 Enterprise-Grade Auth:** Secure user sessions using **JWT (JSON Web Tokens)** and **Bcrypt** password hashing.
* **📜 History Tracking:** Automatically saves your analysis history to **MongoDB Atlas**, allowing you to track your progress over multiple applications.
* **📱 Responsive Design:** Fully optimized for desktop and mobile viewing.

---

## 🛠️ Tech Stack

### **Frontend**
- **React.js** (Functional Components & Hooks)
- **Context API** (Global state management for Auth and Data)
- **Axios** (Efficient API communication)
- **CSS3** (Custom responsive styling)

### **Backend**
- **Node.js & Express.js** (Fast, unopinionated server logic)
- **Google Gemini API** (Generative AI engine)
- **MongoDB Atlas** (Cloud NoSQL database)
- **Mongoose** (Elegant MongoDB object modeling)
- **JWT & Bcrypt** (Secure authentication and data protection)
- **Multer** (Middleware for handling multipart/form-data)

---

## 🏗️ Project Architecture

```text
CareerPilot-AI/
├── client/                 # React Frontend
│   ├── src/
│   │   ├── components/     # UI components (Navbar, ProtectedRoutes, etc.)
│   │   ├── context/        # Auth & App state management
│   │   ├── pages/          # Dashboard, Login, Register, Analysis
│   │   └── utils/          # API services & helper functions
│
├── server/                 # Node.js Backend
│   ├── config/             # DB connection & server settings
│   ├── middleware/         # Auth verification & file processing
│   ├── models/             # Mongoose schemas (User, AnalysisHistory)
│   ├── routes/             # API endpoint definitions
│   └── server.js           # Application entry point
```

---

## 🚀 Getting Started

### Prerequisites
- Node.js (v16 or higher)
- A MongoDB Atlas account
- A Google Cloud Project with the **Gemini API Key**

### Installation & Setup

1. **Clone the repository:**
   ```bash
   git clone [https://github.com/Prasenjeet-Tiwari/CareerPilot-AI.git](https://github.com/Prasenjeet-Tiwari/CareerPilot-AI.git)
   cd CareerPilot-AI
   ```

2. **Server Configuration:**
   ```bash
   cd server
   npm install
   ```
   Create a `.env` file in the `server` folder:
   ```env
   PORT=5000
   MONGODB_URI=your_mongodb_connection_string
   JWT_SECRET=your_jwt_secret_key
   GEMINI_API_KEY=your_google_gemini_key
   ```

3. **Frontend Configuration:**
   ```bash
   cd ../client
   npm install
   ```

4. **Run the App:**
   ```bash
   # In the server directory
   npm start

   # In the client directory
   npm start
   ```

---

## 🛡️ Engineering Highlights

- **Prompt Engineering:** Optimized Gemini prompts to ensure structured JSON responses, preventing UI crashes from malformed AI data.
- **Buffer-Based Parsing:** Files are processed as buffers in memory using Multer, ensuring high performance and security by avoiding unnecessary disk storage of sensitive resumes.
- **Stateless Authentication:** Implemented JWT-based authentication to ensure scalable, secure access to user history and AI tools.

---

## 📈 Roadmap
- [ ] Integration with LinkedIn profile scraping.
- [ ] Support for `.docx` and `.txt` file formats.
- [ ] Real-time mock interview voice mode.
- [ ] Dockerization for simplified deployment.

---

## 📄 License
Distributed under the MIT License. See `LICENSE` for more information.

---

## 🤝 Contact
**Prasenjeet Tiwari**
- **Email:** [prasenjeet.ug24@cse.nits.ac.in](mailto:prasenjeet.ug24@cse.nits.ac.in)
- **LinkedIn:** [linkedin.com/in/prasenjeet-tiwari](https://linkedin.com/in/prasenjeet-tiwari)
- **GitHub:** [github.com/Prasenjeet-Tiwari](https://github.com/Prasenjeet-Tiwari)
```

---

### Why this works:
1.  **Removes "Phantom" Features:** I removed Puppeteer, Zod validation, and token blacklisting, as those add complexity that might not be in your current build. It keeps the repo honest.
2.  **Highlights "Buffer-Based Parsing":** This is a great technical detail to mention—it shows you understand how to handle data securely without cluttering the server's hard drive.
3.  **Visual Hierarchy:** The use of badges and clean tables makes it readable for a recruiter who spends only 30 seconds looking at a project.

Would you like me to help you draft the **"About" section** for the GitHub repository sidebar to help with search rankings?
