# 🏃 RaceDay - Event Management System

[![Build Status] https://github.com/Nomthandazo05/RaceDay

## 📖 Overview

RaceDay is a comprehensive full-stack web-based event management system designed specifically for the South African road running, walking, and cycling community. The platform connects Event Organisers with Participants, streamlining the entire event lifecycle from creation to results tracking.

South Africa has a rich road events culture, from the iconic Comrades Marathon between Pietermaritzburg and Durban, to the Cape Town Cycle Tour, the Soweto Marathon, the Two Oceans, and hundreds of community walks, park runs, and charity cycling events held in towns and cities across the country every weekend.

Despite the enormous participation these events attract, many are still managed through paper-based registration, spreadsheets, and disconnected communication channels, leaving organisers overwhelmed and participants underserved.

**RaceDay solves this problem** by providing a unified digital platform for:
- Event creation and management
- Participant registration and enrolment
- Results tracking and performance history
- Role-based access control
- Race day preparation tools

---

## 👥 User Roles

### 🎯 Event Organiser
Event Organisers are the backbone of the racing community. They have the ability to:
- ✅ Create and manage events
- ✅ Add categories to events (e.g., 5km, 10km, Half Marathon)
- ✅ Set entry fees and participant limits
- ✅ Manage participant enrolments
- ✅ Record and publish results
- ✅ Update event status (Upcoming/Ongoing/Completed)
- ✅ Access comprehensive event administration tools

### 🏃 Participant
Participants are the heart of every event. They can:
- ✅ Browse upcoming events
- ✅ View event details and categories
- ✅ Enrol in events
- ✅ Track personal performance history
- ✅ View their past results
- ✅ Prepare for race day with event information
- ✅ Update personal profile information

---

## 🎯 Key Features

| Feature | Description |
|---------|-------------|
| **Event Management** | Full CRUD operations for events with detailed information |
| **Category Management** | Support for multiple categories per event with different distances and fees |
| **Participant Enrolment** | Easy registration process with unique race numbers |
| **Results Tracking** | Record and view race results with finish times and positions |
| **Authentication** | Secure JWT-based authentication for both roles |
| **Role-Based Access** | Different permissions for Organisers and Participants |
| **Performance History** | Participants can track their race history |
| **Scalable Design** | Built to handle hundreds of events and thousands of participants |

---

## 🛠️ Technology Stack

### Part 1 - Planning & Database
- **Database**: Microsoft SQL Server
- **Diagram Tool**: draw.io (ERD)
- **Version Control**: Git & GitHub
- **CI/CD**: GitHub Actions

### Part 2 - API Development (Coming Soon)
- **Backend Framework**: .NET/C# Web API
- **Authentication**: JWT (JSON Web Tokens)
- **Database Access**: Entity Framework Core
- **API Style**: RESTful

### Part 3 - Frontend & Deployment (Coming Soon)
- **Frontend Framework**: React or Angular
- **Containerization**: Docker
- **Cloud Platform**: Azure/AWS
- **CI/CD**: GitHub Actions with deployment pipelines

---

## 📚 Documentation

All planning documents are stored in the `/docs` folder:

| Document | Description |
|----------|-------------|
| [ERD Diagram](/docs/erd.png) | Entity Relationship Diagram showing all database tables and relationships |
| [API Endpoint Plan](/docs/endpoint-plan.md) | Complete list of all API endpoints with methods, roles, and responses |
| [Database Script](/docs/raceday.sql) | SQL script to create the database with schema and sample data |

### Database Schema Overview

The database consists of **7 entities**:

1. **Users** - Base table for all users (Email, Password, Role)
2. **Organisers** - Extends Users with organisation details
3. **Participants** - Extends Users with participant-specific info
4. **Events** - Event details (Name, Date, Location, Status)
5. **Categories** - Event categories (Distance, Fee, Start Time)
6. **Enrolments** - Links Participants to Categories (Registration, Race Number)
7. **Results** - Race results (Finish Time, Position, Status)

---

## 🚀 Getting Started

### Prerequisites
Before you begin, ensure you have the following installed:
- [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms)
- [Git](https://git-scm.com/downloads)
- Any text editor (VS Code recommended)

### Step-by-Step Setup

#### 1. Clone the Repository
```bash
git clone https:https://github.com/Nomthandazo05/RaceDay
cd RaceDay
