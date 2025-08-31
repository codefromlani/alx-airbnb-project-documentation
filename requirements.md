# 📄 Backend Feature Requirements – Airbnb Clone

This document outlines the technical and functional requirements for three major backend modules of the Airbnb Clone project: *User Authentication, **Property Management, and **Booking System*.

---

## 🔐 1. User Authentication

### ✅ Functional Requirements
- Allow users to register as a guest or host.
- Allow users to login securely.
- Provide JWT-based token authentication.
- Enable OAuth login using Google (optional).

### 🔧 API Endpoints

| Method | Endpoint        | Description             |
|--------|------------------|-------------------------|
| POST   | /api/v1/register | Register a new user     |
| POST   | /api/v1/login    | Login existing user     |
| GET    | /api/v1/profile  | Retrieve user profile   |

### 🧾 Input/Output Specifications

*Register (POST /register)*  
Input:
json
{
  "username": "alice",
  "email": "alice@example.com",
  "password": "securePassword123"
}

Output
{
  "message": "User created successfully",
  "token": "<JWT>"
}

⚙️ Validation Rules
	•	Email must be unique and in proper format.
	•	Password must be at least 8 characters.
	•	Username is required.

⚡ Performance Criteria
	•	Token issued in under 1 second.
	•	Profile retrieval response < 500ms.

⸻

🏠 2. Property Management

✅ Functional Requirements
	•	Hosts can create, edit, and delete property listings.
	•	Listings include title, description, location, price, images, and amenities.

API Endpoints 
    
Method    Endpoint                  Description
POST      /api/v1/properties        Create a property listing
PUT       /api/v1/properties/:id    Update a property listing
DELETE    /api/v1/properties/:id    Delete a property listing
GET       /api/v1/properties        List all properties

🧾 Input/Output Specifications

Create (POST /properties)
{
  "title": "Beachside Apartment",
  "description": "Spacious 2-bedroom with ocean view",
  "location": "Lekki, Lagos",
  "price": 120,
  "amenities": ["Wi-Fi", "AC", "Parking"],
  "images": ["img1.jpg", "img2.jpg"]
}

⚙️ Validation Rules
	•	Title and location required.
	•	Price must be a positive number.
	•	Minimum one image required.

⚡ Performance Criteria
	•	Listings load in under 2 seconds.
	•	Pagination supported for >1000 entries.

⸻

📆 3. Booking System

✅ Functional Requirements
	•	Guests can book available properties for specific dates.
	•	Prevent overlapping bookings.
	•	Allow cancellation with time constraints.

API Endpoints 
Method   Endpoint                Description
POST     /api/v1/bookings        Create a new booking
GET      /api/v1/bookings/:id    View a specific booking
DELETE   /api/v1/bookings/:id    Cancel a booking

🧾 Input/Output Specifications

Create (POST /bookings)

Input:
{
  "property_id": "abc123",
  "start_date": "2025-07-15",
  "end_date": "2025-07-20"
}

Output:
{
  "message": "Booking confirmed",
  "booking_id": "bk123456"
}

⚙️ Validation Rules
	•	Dates must be in the future.
	•	End date must be after start date.
	•	Booking must not overlap with existing ones.

⚡ Performance Criteria
	•	Availability check under 1s.
	•	Booking creation response under 2s.

⸻

📌 Notes
	•	All endpoints are prefixed with /api/v1/.
	•	Authentication is required for all endpoints except registration/login.
	•	Rate limiting (e.g., 100 req/min) will be applied to prevent abuse.

⸻

🛠 Technologies Used
	•	Framework: Django + Django REST Framework
	•	Auth: JWT via djangorestframework-simplejwt
	•	Database: PostgreSQL
	•	Storage: Cloudinary or file-based
	•	Payments: Stripe (planned integration)

⸻

📁 File Location

This file is located in the root of the repository:
/requirements.md

---
