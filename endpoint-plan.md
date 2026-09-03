# RaceDay - Complete API Endpoint Plan

## 📋 Overview
This document outlines all RESTful API endpoints for the RaceDay Event Management System. Each endpoint includes the HTTP method, route, description, required role, request body, and expected response.

## 🔗 Base URL
/api

## 🔐 Authentication
All endpoints except registration and login require a valid JWT token in the Authorization header:

---

## 🏠 Authentication Endpoints

| HTTP Method | Route | Description | Role Required | Request Body | Expected Response |
|-------------|-------|-------------|---------------|--------------|-------------------|
| POST | /api/auth/register | Register a new user account | None | `{ "email": "user@example.com", "password": "securepass", "fullName": "John Doe", "role": "Participant" }` | **201 Created** - User details without password<br>**400 Bad Request** - Validation error<br>**409 Conflict** - Email already exists |
| POST | /api/auth/login | Login and receive JWT token | None | `{ "email": "user@example.com", "password": "securepass" }` | **200 OK** - `{ "token": "jwt_token", "user": { "userId": 1, "email": "...", "role": "..." } }`<br>**401 Unauthorized** - Invalid credentials |

---

## 👤 User Profile Endpoints

| HTTP Method | Route | Description | Role Required | Request Body | Expected Response |
|-------------|-------|-------------|---------------|--------------|-------------------|
| GET | /api/users/profile | Get current user's profile | Any (logged in) | None | **200 OK** - User profile with role-specific details<br>**401 Unauthorized** - Not logged in |
| PUT | /api/users/profile | Update current user's profile | Any (logged in) | `{ "fullName": "Updated Name", "email": "new@email.com" }` | **200 OK** - Updated profile<br>**400 Bad Request** - Validation error<br>**409 Conflict** - Email already taken |

---

## 📅 Event Endpoints

| HTTP Method | Route | Description | Role Required | Request Body | Expected Response |
|-------------|-------|-------------|---------------|--------------|-------------------|
| GET | /api/events | List all events with filters | None (public) | None (Query params: ?status=upcoming&location=CapeTown) | **200 OK** - Array of events |
| GET | /api/events/{id} | Get specific event details with categories | None (public) | None | **200 OK** - Event with categories<br>**404 Not Found** - Event not found |
| POST | /api/events | Create a new event | Organiser | `{ "eventName": "Cape Town Cycle Tour", "description": "Annual cycle tour", "eventDate": "2026-03-15", "location": "Cape Town", "startTime": "06:00:00", "status": "Upcoming" }` | **201 Created** - Created event<br>**400 Bad Request** - Validation error<br>**401 Unauthorized** - Not logged in<br>**403 Forbidden** - Not an organiser |
| PUT | /api/events/{id} | Update an existing event | Organiser (event owner) | `{ "eventName": "Updated Name", "description": "...", "eventDate": "2026-03-16" }` | **200 OK** - Updated event<br>**400 Bad Request** - Validation error<br>**403 Forbidden** - Not event owner<br>**404 Not Found** - Event not found |
| DELETE | /api/events/{id} | Delete an event | Organiser (event owner) | None | **204 No Content** - Deleted successfully<br>**403 Forbidden** - Not event owner<br>**404 Not Found** - Event not found |
| GET | /api/events/{id}/categories | Get all categories for an event | None (public) | None | **200 OK** - Array of categories<br>**404 Not Found** - Event not found |

---

## 🏷️ Category Endpoints

| HTTP Method | Route | Description | Role Required | Request Body | Expected Response |
|-------------|-------|-------------|---------------|--------------|-------------------|
| POST | /api/events/{eventId}/categories | Add a new category to an event | Organiser (event owner) | `{ "categoryName": "Half Marathon", "distance": 21.1, "entryFee": 450.00, "startTime": "06:30:00", "maxParticipants": 1000 }` | **201 Created** - Category details<br>**400 Bad Request** - Validation error<br>**403 Forbidden** - Not event owner<br>**404 Not Found** - Event not found |
| PUT | /api/categories/{id} | Update an existing category | Organiser (event owner) | `{ "categoryName": "Updated", "distance": 10.0, "entryFee": 300.00, "startTime": "07:00:00" }` | **200 OK** - Updated category<br>**403 Forbidden** - Not event owner<br>**404 Not Found** - Category not found |
| DELETE | /api/categories/{id} | Delete a category | Organiser (event owner) | None | **204 No Content** - Deleted successfully<br>**403 Forbidden** - Not event owner<br>**404 Not Found** - Category not found |

---

## 📝 Enrolment Endpoints

| HTTP Method | Route | Description | Role Required | Request Body | Expected Response |
|-------------|-------|-------------|---------------|--------------|-------------------|
| POST | /api/categories/{categoryId}/enrol | Enrol a participant in a category | Participant | `{ "participantId": 1 }` | **201 Created** - Enrolment details with race number<br>**400 Bad Request** - Already enrolled<br>**403 Forbidden** - Not a participant<br>**404 Not Found** - Category not found<br>**409 Conflict** - Already enrolled in this category |
| GET | /api/participants/{participantId}/enrolments | Get all enrolments for a participant | Participant (own profile) | None | **200 OK** - Array of enrolments with event details<br>**403 Forbidden** - Accessing another user's enrolments<br>**404 Not Found** - Participant not found |
| GET | /api/enrolments/{id} | Get specific enrolment details | Participant (own) or Organiser | None | **200 OK** - Enrolment with result (if available)<br>**403 Forbidden** - Not authorized<br>**404 Not Found** - Enrolment not found |
| PUT | /api/enrolments/{id} | Update enrolment status | Organiser (event owner) | `{ "status": "Paid" }` | **200 OK** - Updated enrolment<br>**400 Bad Request** - Invalid status<br>**403 Forbidden** - Not event organiser<br>**404 Not Found** - Enrolment not found |
| DELETE | /api/enrolments/{id} | Cancel an enrolment | Participant (own) or Organiser | None | **204 No Content** - Cancelled successfully<br>**403 Forbidden** - Not authorized<br>**404 Not Found** - Enrolment not found |

---

## 🏆 Result Endpoints

| HTTP Method | Route | Description | Role Required | Request Body | Expected Response |
|-------------|-------|-------------|---------------|--------------|-------------------|
| POST | /api/enrolments/{enrolmentId}/results | Add a result for an enrolment | Organiser (event owner) | `{ "finishTime": "03:45:22", "position": 45, "status": "Finished" }` | **201 Created** - Result details<br>**400 Bad Request** - Result already exists<br>**403 Forbidden** - Not event organiser<br>**404 Not Found** - Enrolment not found |
| PUT | /api/results/{id} | Update an existing result | Organiser (event owner) | `{ "finishTime": "03:40:15", "position": 42, "status": "Finished" }` | **200 OK** - Updated result<br>**403 Forbidden** - Not event organiser<br>**404 Not Found** - Result not found |
| GET | /api/events/{eventId}/results | Get all results for an event | None (public) | None (Query params: ?categoryId=1) | **200 OK** - Array of results with participant names<br>**404 Not Found** - Event not found |
| GET | /api/participants/{participantId}/results | Get all results for a participant | Participant (own) or Organiser | None | **200 OK** - Array of results with event details<br>**403 Forbidden** - Not authorized<br>**404 Not Found** - Participant not found |
| GET | /api/events/{eventId}/leaderboard | Get leaderboard for an event | None (public) | None (Query params: ?categoryId=1&limit=10) | **200 OK** - Sorted leaderboard with positions<br>**404 Not Found** - Event not found |

---

## 📊 Statistics Endpoints

| HTTP Method | Route | Description | Role Required | Request Body | Expected Response |
|-------------|-------|-------------|---------------|--------------|-------------------|
| GET | /api/events/{eventId}/stats | Get event statistics | Organiser (event owner) | None | **200 OK** - `{ "totalEnrolments": 150, "categories": [...], "averageFinishTime": "04:15:30" }`<br>**403 Forbidden** - Not event owner<br>**404 Not Found** - Event not found |
| GET | /api/participants/{participantId}/stats | Get participant statistics | Participant (own) or Organiser | None | **200 OK** - `{ "totalEvents": 5, "bestPosition": 12, "averageTime": "04:20:15" }`<br>**403 Forbidden** - Not authorized<br>**404 Not Found** - Participant not found |

---

## 📊 Endpoint Summary

### By Category
Authentication: 2 endpoints
User Profile: 2 endpoints
Events: 6 endpoints
Categories: 3 endpoints
Enrolments: 5 endpoints
Results: 5 endpoints
Statistics: 2 endpoints
─────────────────────────────
TOTAL: 25 endpoints

### By Role
Public (No auth): 3 endpoints (GET /events, GET /events/{id}, GET /events/{id}/categories)
Any (Logged in): 2 endpoints (User profile endpoints)
Participant: 4 endpoints (Enrolment, viewing own results)
Organiser: 16 endpoints (Create, update, delete operations)

---

## 🔐 HTTP Status Codes Used

| Status Code | Meaning | Usage |
|-------------|---------|-------|
| 200 OK | Success | GET and PUT requests |
| 201 Created | Resource created | POST requests (register, create event, enrol) |
| 204 No Content | Success - no content | DELETE requests |
| 400 Bad Request | Validation error | Invalid data sent |
| 401 Unauthorized | Not logged in | Missing/invalid JWT token |
| 403 Forbidden | Insufficient permissions | Role mismatch |
| 404 Not Found | Resource doesn't exist | Invalid ID |
| 409 Conflict | Resource conflict | Duplicate email, already enrolled |

---

## 📝 Error Response Format

All error responses follow this format:
```json
{
  "status": "error",
  "message": "A user-friendly error message",
  "errors": [
    {
      "field": "email",
      "message": "Email is already registered"
    }
  ],
  "timestamp": "2026-09-02T14:30:00Z"
}
