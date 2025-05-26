


# 🎟️ QR Code Ticket Booking System

This is a full-featured ticket booking system built using **Flask** and **SQLite** with the following features:

- User registration and login (session-based)
- Event creation with automatic seat generation
- Seat selection during booking (up to 4 tickets per user)
- QR code generation for booked tickets
- Admin authorization to create events

---

## 📦 Features

### ✅ User Authentication
- **Session-based login** (`/login-session`)
- **Logout** endpoint to clear session
- **Token-based endpoints** for secure booking and ticket access

### ✅ Event Management
- Create new events (admins only)
- Auto-generate seats (5 rows × 10 columns = 50 seats)
- Store booked & available seats

### ✅ Seat Booking
- Select up to **4 specific seats per event**
- Prevents overbooking and duplicate booking
- Updates event's booked/available seat count

### ✅ Ticket QR Code
- Retrieve your ticket via `/ticket/<event_id>`
- QR includes: event name, user ID, seat numbers
- Returned as Base64 image string

---

## 🧱 Database Schema

### `users`
| id | username | password_hash |
|----|----------|----------------|

### `events`
| id | name | date | location | seats | booked | user_id |
|----|------|------|----------|--------|--------|---------|

### `seats`
| id | event_id | seat_label | is_booked | user_id |
|----|----------|------------|------------|----------|

### `bookings`
| id | event_id | user_id | seats_booked |
|----|----------|----------|----------------|

---

## 🧪 API Endpoints

### 🔐 Authentication

- `POST /register` — Register a new user  
- `POST /login-session` — Login and start session  
- `POST /logout` — Logout and clear session  

### 🎫 Events

- `POST /events` — Create a new event (session required)  
- `GET /events` — List all events  
- `GET /seats/<event_id>` — Get seat status for an event  

### 🪑 Booking

- `POST /book` — Book up to 4 specific seats (token required)  
  ```json
  {
    "event_id": 1,
    "seats": ["A1", "A2"]
  }

* Returns error if:

  * More than 4 seats selected
  * Any selected seat already booked

### 📷 QR Ticket

* `GET /ticket/<event_id>` — Returns your booked seats and a QR code (token required)

---

## 🚀 Running the Project

1. Clone the repo:

   ```bash
   git clone <your_repo_url>
   cd ticket-booking-system
   ```

2. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

3. Run the server:

   ```bash
   flask run
   ```

4. Use [Insomnia](https://insomnia.rest/) or [Postman](https://www.postman.com/) to test the endpoints.

---

## 📌 Notes

* QR code is returned as a Base64 PNG string, viewable using:

  * Online Base64 image viewers
  * Paste in browser: `data:image/png;base64,<your_qr_code>`
* Events can only be created by logged-in users
* Booking restricted to 4 seats per user per event

---

## 📫 Contact

For questions or suggestions, feel free to reach out.

---

