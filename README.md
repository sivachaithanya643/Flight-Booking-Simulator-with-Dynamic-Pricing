# ✈️ Flight Booking Simulator with Dynamic Pricing

A **FastAPI-based web application** built using **Python, React, HTML, and CSS**, designed to simulate flight bookings with **dynamic pricing logic** instead of fixed ticket prices.  
Developed as part of an internship, this project focuses on backend logic, frontend interaction, and a realistic airline-like booking simulation.

---

## 🎥 Project Overview

### 🌟 Features
- 🔐 Secure user authentication (Signup, Login, Logout)
- 🛫 Search and book flights with **dynamically changing prices**
- 💸 Prices vary based on **seat availability**, **time to departure**, and **demand**
- 🧾 Displays booking details and ticket confirmation after simulated payment
- 🔁 Supports both **one-way** and **round-trip** bookings
- 📜 Allows users to view and manage their booking history
- 🧑‍💼 Admin panel for managing flights, users, and dynamic pricing logic
- 💻 Responsive and clean UI built with **React**
- 🧩 Fully self-contained — no external airline APIs required

---

## 🧩 Tech Stack

**Frontend**
- React  
- HTML5  
- CSS3  

**Backend**
- FastAPI (Python Framework)

**Database**
- MySQL  

**Development Tools**
- Visual Studio Code  
- Git & GitHub  
- Axios (for frontend-backend communication)
- SQLAlchemy / Pydantic (for database models and validation)

---

## 🏗️ System Architecture

The project follows a **Three-Tier Architecture**:

1️⃣ **Presentation Layer (Frontend)**  
   - Built using **React** for a dynamic and responsive user experience  
   - Provides real-time flight data and dynamic price updates  

2️⃣ **Application Layer (Backend - FastAPI)**  
   - Handles authentication, flight search, and booking logic  
   - Implements dynamic pricing algorithms and seat availability tracking  
   - Exposes RESTful APIs consumed by the React frontend  

3️⃣ **Data Layer (Database - MySQL)**  
   - Stores user, flight, and booking information  
   - Maintains transaction details and price adjustments  

**Flow:**  
`User → React Frontend → FastAPI Endpoints → MySQL Database → JSON Response → Rendered UI`

---

## ⚙️ Differentiation from Existing Systems

| Feature | Existing Systems | This Project |
|----------|------------------|---------------|
| **Pricing Model** | Fixed/API-based | Dynamic algorithmic pricing |
| **Purpose** | Real-world airline booking | Educational & experimental |
| **Integration** | External APIs | Self-contained |
| **Complexity** | Heavy backend systems | Simplified for simulation |
| **Customization** | Limited | Fully configurable logic |

---

## 📂 Project Structure

### 🧠 Backend (FastAPI)
backend/
│
├── main.py # FastAPI app entry point
├── models.py # Database models
├── routes/ # API route definitions
├── schemas/ # Pydantic models
├── services/ # Pricing, booking, and logic services
└── utils/ # Helper functions

frontend/
│
├── public/
│ └── index.html
│
├── src/
│ ├── components/
│ │ ├── FlightCard.js
│ │ ├── FlightSearch.js
│ │ ├── BookingForm.js
│ │ └── BookingConfirmation.js
│ │
│ ├── pages/
│ │ ├── Home.js
│ │ ├── SearchResults.js
│ │ └── Booking.js
│ │
│ ├── services/
│ │ └── api.js # Axios service for API calls
│ │
│ ├── App.js
│ └── index.js
│
└── package.json

database/
└── flight_booking.sql # MySQL schema for flights, bookings, and users



---

## 🧠 Future Scope

- 💡 **Coupon Code System** — Apply discounts during booking *(in progress)*  
- 💬 **Email Notifications** — Send booking and payment confirmations  
- 🔁 **Refund Module** — Handle flight cancellations and refunds  
- 🧭 **Real API Integration** — Connect with live airline APIs like Amadeus or Skyscanner  
- 📊 **Admin Dashboard** — Visualize bookings, pricing trends, and demand analytics  

---

## ⚡ Justification

- 🧱 Fully self-contained — no real airline data required  
- 🧠 Demonstrates **real-world dynamic pricing and booking logic**  
- 📱 Built with **React frontend** and **FastAPI backend**  
- 🧩 Modular and extensible — easy to adapt for research or academic purposes  

---


## 🛠️ Installation
### 1️⃣ Clone the Repository
```bash
git clone https://github.com/your-username/flight-booking-simulator.git
cd flight-booking-simulator

2️⃣ Setup Backend
cd backend
pip install -r requirements.txt
uvicorn main:app --reload

3️⃣ Setup Frontend
cd frontend
npm install
npm start

4️⃣ Setup Database

Install MySQL and create a database named flight_booking
Import the schema:
mysql -u root -p flight_booking < database/flight_booking.sql

5️⃣ Access the App
Frontend: http://localhost:3000
Backend API: http://127.0.0.1:8000


📜 License
This project is licensed under the MIT License — see the LICENSE file for details.


👨‍💻 Author
Kambham Siva Chaithanya Reddy
Internship Project — Flight Booking Simulator with Dynamic Pricing
Developed using FastAPI, React, and MySQL, featuring Dynamic Pricing Algorithms for realistic flight booking simulation.
