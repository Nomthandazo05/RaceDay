# 🏃 RaceDay - Event Management System (Part 2: RESTful API)

![.NET CI/CD](https://github.com/YOUR-USERNAME/RaceDay/actions/workflows/dotnet.yml/badge.svg)


## 📖 Overview

RaceDay is a comprehensive full-stack web-based event management system designed specifically for the South African road running, walking, and cycling community. The platform connects **Event Organisers** with **Participants**, streamlining the entire event lifecycle from creation to results tracking.

**Part 2** focuses on building the **RESTful API** that powers the entire RaceDay system. This API handles all data operations, enforces role-based access, and is fully tested before the MVC front-end is built in Part 3.

---

## 🎯 What This Part Delivers

- ✅ **ASP.NET Core Web API** built with C#
- ✅ **SQL Server database** via Entity Framework Core (Code-First)
- ✅ **Role-based authentication** (Organiser vs Participant)
- ✅ **JWT session management** for secure API access
- ✅ **Swagger UI** for live endpoint testing
- ✅ **Unit tests** covering authentication, CRUD, and role enforcement
- ✅ **GitHub Actions CI/CD** pipeline that builds and tests on every push

---

## 👥 User Roles

### 🎯 Event Organiser
- Register and login as an Organiser
- Create, update, and delete events
- Define categories (age/distance) for each event
- View all enrolments for their events
- Capture finish times and finishing positions
- View own profile and update details

### 🏃 Participant
- Register and login as a Participant
- Browse upcoming events (public)
- Enrol in events by selecting a category
- View personal enrolment history
- View personal race results
- View own profile and update details

### 🔓 Public (No Authentication)
- Browse all events
- View event details and categories
- View event results and leaderboards

---

## 🛠️ Technology Stack

| Layer | Technology |
|-------|------------|
| **Framework** | ASP.NET Core 8.0 Web API |
| **Language** | C# 12 |
| **ORM** | Entity Framework Core 8 (Code-First) |
| **Database** | SQL Server (LocalDB or Express) |
| **Authentication** | JWT (JSON Web Tokens) |
| **Password Hashing** | BCrypt.Net |
| **API Documentation** | Swagger / Swashbuckle |
| **Testing** | xUnit, Moq, FluentAssertions, EF Core InMemory |
| **CI/CD** | GitHub Actions |
| **IDE** | Visual Studio 2022 |

---

## 📁 Project Structure
RaceDay/
├── .github/
│ └── workflows/
│ └── dotnet.yml # CI/CD pipeline
├── docs/
│ ├── erd.png # Part 1 ERD
│ ├── endpoint-plan.md # Part 1 Endpoint Plan
│ ├── raceday.sql # Part 1 SQL Script
│ └── screenshots/
│ └── green-build.png # CI/CD green build screenshot
├── RaceDay.API/
│ ├── Controllers/
│ │ ├── AuthController.cs # Register & Login
│ │ ├── UsersController.cs # Profile endpoints
│ │ ├── EventsController.cs # Event CRUD
│ │ ├── CategoriesController.cs # Category CRUD
│ │ ├── EnrolmentsController.cs # Enrolment operations
│ │ └── ResultsController.cs # Result operations
│ ├── Models/
│ │ ├── User.cs
│ │ ├── Organiser.cs
│ │ ├── Participant.cs
│ │ ├── Event.cs
│ │ ├── Category.cs
│ │ ├── Enrolment.cs
│ │ └── Result.cs
│ ├── DTOs/
│ │ ├── AuthDTOs.cs
│ │ ├── UserDTOs.cs
│ │ ├── EventDTOs.cs
│ │ ├── CategoryDTOs.cs
│ │ ├── EnrolmentDTOs.cs
│ │ └── ResultDTOs.cs
│ ├── Data/
│ │ └── RaceDayDbContext.cs
│ ├── appsettings.json
│ ├── appsettings.Development.json
│ └── Program.cs
├── README.md
└── .gitignore

---

## 🚀 Getting Started

### Prerequisites

Ensure you have the following installed:

| Tool | Version | Download Link |
|------|---------|---------------|
| Visual Studio 2022 | 17.8+ | [Download](https://visualstudio.microsoft.com/) |
| .NET SDK | 8.0 | [Download](https://dotnet.microsoft.com/download) |
| SQL Server | 2019+ | [Download](https://www.microsoft.com/en-us/sql-server/sql-server-downloads) |
| SQL Server Management Studio | 19+ | [Download](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms) |
| Git | Latest | [Download](https://git-scm.com/) |

### Installation & Setup

#### 1. Clone the Repository

```bash
git clone https://github.com/YOUR-USERNAME/RaceDay.git
cd RaceDay

📖 Swagger UI
Swagger is configured with JWT support. To test protected endpoints:
Run the API and navigate to https://localhost:7000/swagger
Call POST /api/auth/login to get a JWT token
Click the 🔓 Authorize button at the top
Enter Bearer <your_token> and click Authorize
All protected endpoints are now accessible from Swagger

📝 Learning Outcomes Achieved
By completing Part 2, I have demonstrated the ability to:
✅ Build a RESTful API using ASP.NET Core Web API in C#
✅ Connect the API to a SQL Server database using Entity Framework Core
✅ Implement role-based session authentication for Organiser and Participant roles
✅ Write and run unit tests for API endpoints
✅ Configure automated CI/CD using GitHub Actions
✅ Follow the Part 1 specification (ERD, endpoint plan, SQL script)
