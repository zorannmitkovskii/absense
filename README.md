# Absence Management System

A SaaS-based Vacation & Leave Management System built with Spring Boot, PostgreSQL, Keycloak, and Vue.js.

## Features

- **Absence Tracking**: Track various types of absences including vacation, sick leave, personal leave, etc.
- **Approval Workflows**: Managers can approve or reject absence requests from their team members.
- **Role-Based Dashboards**: Different views for HR, employees, and managers.
- **Email and Slack Notifications**: Automatic notifications for absence requests, approvals, and rejections.
- **Calendar Integration**: Sync approved absences with Google Calendar.
- **Analytics**: View absence trends and reports.

## Tech Stack

- **Backend**: Spring Boot 3.4.5, Java 21
- **Database**: PostgreSQL
- **Authentication**: Keycloak
- **Frontend**: Vue.js (planned)
- **Notifications**: Email, Slack API
- **Calendar**: Google Calendar API

## Getting Started

### Prerequisites

- Java 21
- Maven
- PostgreSQL
- Keycloak Server

### Setup

1. **Clone the repository**

   ```bash
   git clone https://github.com/yourusername/absense.git
   cd absense
   ```

2. **Configure the application**

   Update `src/main/resources/application.yml` with your database, Keycloak, email, Slack, and Google Calendar settings.

3. **Build the application**

   ```bash
   mvn clean install
   ```

4. **Run the application**

   ```bash
   mvn spring-boot:run
   ```

   The application will be available at `http://localhost:8080`.

### Keycloak Setup

1. Start a Keycloak server (version 23.0.6 or later).
2. Create a new realm called `absense`.
3. Create a new client called `absense-app`.
4. Configure the client as follows:
   - Access Type: `confidential`
   - Valid Redirect URIs: `http://localhost:8080/*`
   - Web Origins: `http://localhost:8080`
5. Create the following roles:
   - `EMPLOYEE`
   - `MANAGER`
   - `HR`
6. Create users and assign appropriate roles.

## API Documentation

The API provides endpoints for managing users, roles, and absences. Here are some key endpoints:

### User Endpoints

- `GET /api/users`: Get all users (HR, MANAGER)
- `GET /api/users/{id}`: Get a user by ID (HR, MANAGER, self)
- `POST /api/users`: Create a new user (HR)
- `PUT /api/users/{id}`: Update a user (HR, self)
- `DELETE /api/users/{id}`: Delete a user (HR)

### Absence Endpoints

- `GET /api/absences`: Get all absences (HR)
- `GET /api/absences/{id}`: Get an absence by ID (HR, owner, manager)
- `POST /api/absences`: Create a new absence request (all authenticated users)
- `PUT /api/absences/{id}`: Update an absence (HR, owner)
- `DELETE /api/absences/{id}`: Delete an absence (HR, owner)
- `PUT /api/absences/{id}/approve`: Approve an absence (HR, manager)
- `PUT /api/absences/{id}/reject`: Reject an absence (HR, manager)
- `PUT /api/absences/{id}/cancel`: Cancel an absence (HR, owner)

## Project Structure

```
src/main/java/com/zm/absense/
├── config/                  # Configuration classes
├── controller/              # REST controllers
├── model/                   # Entity classes
├── repository/              # JPA repositories
├── scheduler/               # Scheduled tasks
├── service/                 # Service interfaces and implementations
└── AbsenseApplication.java  # Main application class
```

## Future Enhancements

- Vue.js frontend with role-based dashboards
- Enhanced analytics and reporting
- Mobile application
- Integration with other calendar systems
- Support for team absence views

## License

This project is licensed under the MIT License - see the LICENSE file for details.
