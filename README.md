# Genuiz — AI Exam Generator

Educational platform that uses **Artificial Intelligence** to generate dynamic quizzes and provide adaptive feedback to students.

---

## Table of Contents
- [Main Features](#-main-features)
- [Security](#-security)
- [Results](#-results)
- [Tech Stack](#-tech-stack)
- [Prerequisites](#-prerequisites)
- [Install dependencies](#-install-dependencies)
- [Database setup](#-database-setup)
- [Run app](#-run-app)
- [Use cases](#-use-cases)
- [License](#-license)

---

## Main Features
- Exam and question generation using **OpenAI API**.  
- Scalable backend with **Node.js + MySQL** deployed on **Vercel**.  
- Authentication with **Google OAuth2** and password encryption with **bcrypt**.  
- Adaptive feedback to personalize the learning experience.

---

## Security
- Role and permission control in the database.  
- Password encryption with **bcrypt**.  
- Authentication management with **Google OAuth2**.

---

## Results
- Scalable architecture to support multiple courses and users.  
- Personalized assessments and secure result storage.

---

## Tech Stack
- **Languages:** JavaScript, SQL  
- **Frameworks/Libraries:** React, Node.js, Express  
- **Cloud & Infrastructure:** Supabase, Vercel  
- **Database:** MySQL  
- **Security:** Google OAuth2, bcrypt

---

## Prerequisites
- **Node.js 16+**  
- **MySQL 8+**  
- Google OAuth credentials and OpenAI API Key  

Create a `.env` file in the root:  
\`\`\`
OPENAI_API_KEY=your_api_key
GOOGLE_CLIENT_ID=your_google_id
GOOGLE_CLIENT_SECRET=your_google_secret
\`\`\`

---

## Install dependencies
\`\`\`bash
npm install dotenv express passport cookie-parser express-session passport-local passport-google-oauth20 mysql bcrypt connect-flash
\`\`\`

---

## Database setup

Run in MySQL:

```sql
CREATE DATABASE genuiz;
USE genuiz;

CREATE TABLE role (
    id INT AUTO_INCREMENT PRIMARY KEY,
    role_name ENUM('student','teacher') NOT NULL
);

CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    username VARCHAR(50) NOT NULL,
    password VARCHAR(255) NULL,
    role_id INT NULL,
    google_id VARCHAR(255) NULL,
    FOREIGN KEY (role_id) REFERENCES role(id)
);

CREATE TABLE exams_json (
    id INT AUTO_INCREMENT PRIMARY KEY,
    teacher_id INT NOT NULL,
    title VARCHAR(50) NOT NULL,
    topic VARCHAR(255) NOT NULL,
    description_ VARCHAR(255) NULL,
    level ENUM('easy','medium','hard') NULL,
    date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    exam_code VARCHAR(50) UNIQUE NOT NULL,
    exam_data JSON,
    FOREIGN KEY (teacher_id) REFERENCES users(id) ON DELETE CASCADE
);

CREATE TABLE exam_results (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    exam_id INT NOT NULL,
    score DECIMAL(5,2) NOT NULL,
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE,
    FOREIGN KEY (exam_id) REFERENCES exams_json(id) ON DELETE CASCADE
);
```

## Run app
\`\`\`bash
node app.js
\`\`\`

Access at:  
\`\`\`
http://localhost:3000
\`\`\`

---

## Use cases
- Quiz generation for universities.  
- Self-study tool.  
- Support for teachers in fast evaluation creation.

---

## License
Academic use.
