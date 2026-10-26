# Employee Management System

Full-stack practice project:
- Frontend: React + Vite
- Backend: Java 17+, Spring Boot 3, Spring Web, Spring Data JPA, Validation
- Database: MariaDB

## Features
- List employees
- Search by name, email, or department
- Add employee
- Edit employee
- Delete employee
- Basic validation and REST API error responses

## Requirements
- Java 17 or newer
- Maven 3.9+
- Node.js 20+ and npm
- MariaDB 10.6+ (or compatible)

## 1. Create the database

Log in to MariaDB and run:

```sql
CREATE DATABASE employee_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
CREATE USER 'ems_user'@'localhost' IDENTIFIED BY 'ChangeThisPassword!';
GRANT ALL PRIVILEGES ON employee_db.* TO 'ems_user'@'localhost';
FLUSH PRIVILEGES;
```

Use your own password. Do not use a production database password in source control.

## 2. Start the backend

Edit `backend/src/main/resources/application.properties` if your database username, password, host, or port differs.

From the `backend` directory:

```bash
mvn spring-boot:run
```

API base URL: `http://localhost:8080/api/employees`

The app uses `spring.jpa.hibernate.ddl-auto=update` for local practice so JPA creates/updates the table automatically. For production, use database migrations such as Flyway instead.

## 3. Start the frontend

In a second terminal:

```bash
cd frontend
npm install
npm run dev
```

Open the local URL printed by Vite, normally `http://localhost:5173`.

## API endpoints

| Method | Endpoint | Purpose |
|---|---|---|
| GET | `/api/employees` | List all employees |
| GET | `/api/employees/{id}` | Get one employee |
| POST | `/api/employees` | Create employee |
| PUT | `/api/employees/{id}` | Update employee |
| DELETE | `/api/employees/{id}` | Delete employee |

### Example POST body

```json
{
  "firstName": "Asha",
  "lastName": "Rao",
  "email": "asha.rao@example.com",
  "department": "Engineering",
  "jobTitle": "Software Engineer",
  "salary": 65000.00
}
```

## Project structure

```text
employee-management-system/
├── backend/
│   ├── pom.xml
│   └── src/main/
│       ├── java/com/example/ems/
│       │   ├── EmployeeManagementApplication.java
│       │   ├── config/WebConfig.java
│       │   ├── controller/EmployeeController.java
│       │   ├── dto/EmployeeRequest.java
│       │   ├── exception/GlobalExceptionHandler.java
│       │   ├── exception/ResourceNotFoundException.java
│       │   ├── model/Employee.java
│       │   ├── repository/EmployeeRepository.java
│       │   └── service/EmployeeService.java
│       └── resources/application.properties
└── frontend/
    ├── package.json
    ├── index.html
    └── src/
        ├── main.jsx
        ├── App.jsx
        ├── api.js
        └── style.css
```

## Practice extensions
1. Add departments as a separate table with a foreign key.
2. Add pagination and server-side search.
3. Add login with Spring Security and role-based access.
4. Add unit/integration tests.
5. Add Docker Compose for React, Spring Boot, and MariaDB.
6. Deploy the frontend and backend separately and configure HTTPS.
