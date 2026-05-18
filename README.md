# Adhira: Women's Support Platform

[![Flutter](https://img.shields.io/badge/Frontend-Flutter-02569B?logo=flutter)](https://flutter.dev/)
[![Node.js](https://img.shields.io/badge/Backend-Node.js-339933?logo=node.js)](https://nodejs.org/)
[![MongoDB](https://img.shields.io/badge/Database-MongoDB-47A248?logo=mongodb)](https://www.mongodb.com/)
[![Groq AI](https://img.shields.io/badge/AI-Groq%20(Llama--3)-f87020?logo=llama)](https://groq.com/)
[![Google Gemini](https://img.shields.io/badge/Moderation-Gemini%20AI-4285F4?logo=google)](https://ai.google.dev/)

**Adhira** is a comprehensive, cross-platform women's support application designed to provide continuous emotional, educational, and community assistance. Moving beyond traditional reactive emergency applications, Adhira builds a holistic ecosystem that addresses ongoing emotional well-being, community connection, and safe digital expression.

---

##  Core Features

*   **24/7 AI-Powered Contextual Chatbot**
    *   Powered by the **Llama-3-8B model via the Groq API** for ultra-low latency inference (< 300ms).
    *   Provides instant, context-aware, and empathetic guidance regarding safe actions, legal steps, and emotional reassurance.
*   **AI-Moderated Anonymous Community Forums**
    *   A safe space for users to share experiences, publish blogs, and read articles.
    *   Integrated with **Google Gemini API** for real-time sentiment analysis, automatically detecting and filtering abusive, toxic, or self-harm-related sentiments before they are posted.
*   **Direct Volunteer Assistance & Rating System**
    *   Users can directly message vetted volunteers for personalized help and peer-to-peer advice.
    *   Includes a built-in rating system (1-5 stars) ensuring a reliable, quality-driven, and highly accountable support network.
*   **Secure Role-Based Ecosystem**
    *   Robust JWT authentication and Role-Based Access Control (RBAC) securely separates Standard Users from Volunteers, ensuring strict data privacy.

---

## System Architecture

Adhira operates on a modernized, scalable 3-tier Client-Server architecture:

1.  **Presentation Layer (Flutter):** A unified Dart codebase providing a seamless, highly responsive cross-platform experience across Android, iOS, and Web.
2.  **Application Layer (Node.js/Express):** Central RESTful API gateway handling business logic, user authentication, AI API orchestration, and real-time community feeds.
3.  **Data Layer (MongoDB):** A flexible NoSQL database storing user profiles, chat histories, volunteer ratings, and community content efficiently.

---

## Run on Windows (PowerShell)

### Quick Start (print commands)
From the project root, you can run the provided script to start services:
```powershell
powershell -ExecutionPolicy Bypass -File .\run-windows.ps1 -Port 5000
```

### 1) Start MongoDB Locally
Ensure MongoDB is running before starting the backend. Use one of these methods:
*   Installed as a Windows service: `net start MongoDB`
*   Manual start: `mongod --dbpath C:\data\db`

### 2) Run Backend
Navigate to the backend directory and set up your environment:
```powershell
cd Backend
npm install
$env:PORT=5000
if (!(Test-Path .env)) { Copy-Item .env.example .env }
npm run dev
```
*The backend listens on `http://127.0.0.1:5000`.*

**Optional: Enable Groq-powered AI Chatbot**
To enable Llama-3 AI replies, provide your Groq API key:
```powershell
$env:GROQ_API_KEY="your_groq_key"        # For current session
$env:GROQ_MODEL="llama-3.1-8b-instant"   # Optional model selection
npm run dev
```
*Note: Without the Groq API key, the chatbot will fall back to built-in safety replies.*

To persist the key across all new terminals:
```powershell
setx GROQ_API_KEY "your_groq_key"
setx GROQ_MODEL "llama-3.1-8b-instant"
```

### 3) (Optional) Seed Admin User
```powershell
cd Backend
npm run seed:admin
```
*Default login: `admin / admin` (can be configured in `Backend/.env`).*

### 4) Run Flutter Frontend
Navigate to the frontend directory and launch the app:
```powershell
cd frontend
flutter pub get
flutter run -d chrome --dart-define=API_BASE_URL=http://127.0.0.1:5000
```
*Note: If your backend runs on a different port, update the `API_BASE_URL` accordingly.*

---

## Important Notes

*   **Role Selection:** Account creation now requires selecting a role (`user` or `volunteer`). If a logged-in account has no role (e.g., first-time Google sign-in), the app will prompt for role selection before granting dashboard access.
*   **Fallback AI:** If the `GROQ_API_KEY` is not present, the chatbot gracefully downgrades to a predefined set of built-in safety responses.

---

## Future Scope
*   **Predictive Analytics:** Utilizing machine learning on interaction patterns to proactively suggest professional help.
*   **Professional Counseling Integration:** Introducing verified professional psychologists for tiered support.
*   **Multilingual Support:** Enhancing the AI and UI to support regional languages for wider accessibility.

---

**Team:** Suhana Singh, Muskaan, Supriya Serene
