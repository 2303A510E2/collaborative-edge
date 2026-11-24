# collaborative-edge
A MERN-based project collaboration portal connecting students, teachers, and industry. Features role-based dashboards, project proposals, supervision, submissions, evaluations, notifications, and an AI assistant. 


Collaborative Edge

A full-stack project collaboration portal that connects students, teachers, administrators, and industry representatives throughout the final-year project lifecycle.

Project attribution: This repository is an adaptation of Collaborative Edge, originally created by Umair Habib. Sohail Arif customized the profile and contact section and prepared this repository for deployment. The original MIT license and copyright notice are retained in LICENSE.

Features

Separate dashboards and permissions for students, teachers, industry representatives, and administrators

Project idea submission, review, approval, selection, and supervision workflows

Student groups, milestone and deliverable submissions, and supervisor feedback

Notifications, evaluations, charts, and success stories

Account registration, email verification, password reset, and admin account approval

Gemini-powered AI assistant

MongoDB GridFS file storage

Responsive React interface

Technology stack

Frontend: React 19, Vite, React Router, Tailwind CSS, Framer Motion, Chart.js

Backend: Node.js, Express 5, REST API

Database and file storage: MongoDB, Mongoose, GridFS

Authentication: JWT cookies, bcrypt password hashing, role-based access control

Run locally

Prerequisites

Node.js 20 or later

MongoDB local instance or MongoDB Atlas database

SMTP credentials for email verification and password reset

Gemini API key if you want to use the AI assistant

Setup

From the repository root:

npm run install:all
cp backend/.env.example backend/.env
cp frontend/.env.example frontend/.env

Fill in the environment variables before starting the app. At minimum, configure the MongoDB connection, JWT and reset-token secrets, email credentials, and frontend/backend URLs. Keep secrets out of GitHub.

For local development, set the following values in backend/.env:

MONGO_URI=your_mongodb_connection_string
JWT_SECRET=replace_with_a_long_random_secret
SECRET_KEY=replace_with_a_different_long_random_secret
EMAIL_USER=your_smtp_email
EMAIL_PASS=your_smtp_app_password
FRONTEND_URL=http://localhost:5173
VITE_REACT_APP_BACKEND_BASEURL=http://localhost:5000
GEMINI_API_KEY=your_gemini_api_key
NODE_ENV=development

In frontend/.env, set:

VITE_REACT_APP_BACKEND_BASEURL=http://localhost:5000

Start the frontend and backend together:

npm run dev

The frontend runs at http://localhost:5173 and the API at http://localhost:5000.

To initialize the first administrator, set ADMIN_EMAIL and ADMIN_PASSWORD in backend/.env before the first startup. Use a strong password and remove or rotate these values after setup.

Deploy on Render

Deploy the frontend and backend as separate services from the same GitHub repository.

Backend web service

Root directory: backend

Build command: npm install

Start command: npm start

Add the backend environment variables listed below. Render supplies the PORT variable.

Frontend static site

Root directory: frontend

Build command: npm install && npm run build

Publish directory: dist

Set VITE_REACT_APP_BACKEND_BASEURL to the public URL of your backend before the frontend build.

Add a rewrite from /* to /index.html for React Router routes.

Production environment variables

Set these on the backend service:

MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_long_random_secret
SECRET_KEY=a_different_long_random_secret
EMAIL_USER=your_smtp_email
EMAIL_PASS=your_smtp_app_password
FRONTEND_URL=https://your-frontend.onrender.com
VITE_REACT_APP_BACKEND_BASEURL=https://your-backend.onrender.com
GEMINI_API_KEY=your_gemini_api_key
NODE_ENV=production

Set this on the frontend static site:

VITE_REACT_APP_BACKEND_BASEURL=https://your-backend.onrender.com

Replace the example Render URLs with the URLs Render assigns to your services. After changing frontend environment variables, trigger a new frontend deploy so Vite rebuilds the static assets.

Scripts

Command

Location

Purpose

npm run install:all

Repository root

Install root, backend, and frontend dependencies

npm run dev

Repository root

Start frontend and backend for development

npm start

backend/

Start the production API server

npm run build

frontend/

Build the static frontend into dist/

npm run lint

frontend/

Run ESLint

npm run check

backend/

Check backend JavaScript syntax

Security notes

Never commit .env files, database credentials, SMTP app passwords, or API keys.

Use unique, long random values for JWT_SECRET and SECRET_KEY.

Restrict MongoDB Atlas network access to the addresses required by your deployment where possible.

Configure FRONTEND_URL to the exact deployed frontend origin so credentialed API requests are accepted.
