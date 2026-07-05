# BloodConnect
 
AI-powered emergency blood donor matching platform built on the MERN stack.
 
Unlike static donor directories, BloodConnect actively ranks and notifies the most suitable donors for each emergency request — combining distance, donation eligibility, blood-type compatibility, and donor response history into a transparent match score, with AI-generated explanations for why each donor was selected.
 
---
 
## The problem
 
Existing blood donor apps are mostly static directories — search by blood group and city, then manually call down a list. During real emergencies this wastes critical time: there's no way to know who's actually eligible right now, who's likely to respond, or who's genuinely nearest.
 
## What it does
 
1. Donors register with their blood group, location, and donation history.
2. A hospital/patient/relative posts an urgent request — blood group, units needed, urgency, location (can be typed in plain language and parsed by AI).
3. A matching engine ranks eligible donors by distance, eligibility (90-day donation gap), blood-type compatibility, and a response-rate score based on donation history.
4. Top-ranked donors are notified (SMS/WhatsApp) with an AI-generated explanation of why they were matched.
5. A live dashboard tracks response status in real time and auto-escalates (wider radius, next tier) if no one responds in time.
---
 
## Tech stack
 
| Layer | Technology |
|---|---|
| Frontend | React, Tailwind CSS |
| Backend | Node.js, Express |
| Database | MongoDB (Mongoose, geospatial `2dsphere` indexing) |
| Real-time | Socket.io |
| AI | OpenAI API (request parsing + match explanations) |
| Notifications | Twilio (SMS/WhatsApp) |
| Auth | JWT, bcrypt |
 
---
 
## Project structure
 
```
bloodconnect/
├── client/                  # React frontend
│   └── src/
│       ├── components/
│       ├── pages/
│       ├── context/
│       └── api/
│
├── server/                  # Node/Express backend
│   ├── config/               # DB connection
│   ├── models/                 # Mongoose schemas
│   ├── controllers/              # Route logic
│   ├── routes/                     # API route definitions
│   ├── middleware/                   # Auth & role checks
│   ├── services/                       # Matching engine, AI service, notifications
│   └── server.js
│
└── README.md
```
 
---
 
## Getting started
 
### Prerequisites
- Node.js (LTS version)
- A MongoDB Atlas account (free tier works)
- An OpenAI API key
- A Twilio account (sandbox is free) — optional until notification features are built
### Installation
 
```bash
git clone https://github.com/<your-username>/bloodconnect.git
cd bloodconnect
 
# Backend
cd server
npm install
 
# Frontend
cd ../client
npm install
```
 
### Environment variables
 
Create a `.env` file inside `server/` (never commit this file):
 
```
PORT=5000
MONGO_URI=your_mongodb_atlas_connection_string
JWT_SECRET=any_long_random_string
OPENAI_API_KEY=your_openai_api_key
TWILIO_SID=your_twilio_sid
TWILIO_AUTH_TOKEN=your_twilio_auth_token
```
 
### Running locally
 
```bash
# Backend (from server/)
npm run dev
 
# Frontend (from client/, in a separate terminal)
npm run dev
```
 
---
 
## API endpoints
 
| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/auth/register` | Register a new user (donor/requester/admin) |
| POST | `/api/auth/login` | Log in and receive a JWT |
| GET | `/api/donor/profile` | Get the logged-in donor's profile |
| PUT | `/api/donor/profile` | Update donor availability/info |
| POST | `/api/request` | Create a new emergency blood request |
| GET | `/api/request/:id/matches` | Get ranked donor matches for a request |
| POST | `/api/request/:id/respond` | Donor accepts/declines a match |
| GET | `/api/admin/analytics` | Category-wise donor/request analytics |
 
*(Full route list will grow as each phase is implemented — see Roadmap below.)*
 
---
 
## Roadmap
 
- [ ] Project setup, auth (register/login), role-based access
- [ ] Donor profile module + geospatial donor search
- [ ] Emergency request module
- [ ] Matching & ranking engine
- [ ] AI integration (request parsing + match explanations)
- [ ] SMS/WhatsApp notifications
- [ ] Real-time status dashboard (Socket.io) + auto-escalation
- [ ] Admin analytics dashboard
- [ ] Deployment
---
 
## Author
 
Built by [Chaitanya Purkar] as a final-year CSE project.
 
