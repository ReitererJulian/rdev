# Main Project

The main project for the next days, months or whatever will be a `ToDo-Manager` using a Java `Spring Boot` backend and a Flutter frontend.

The entire app should be hosted on my PiStack first without `Kubernetes` on one machine and after further progression on two `Raspberry Pis` using Kubernetes.

The goal is to get continuously better and learn modern software development through adding more things every step of development. 

## Tech Stack

### Backend

- Java
- Spring Boot
- Spring Data JPA
- PostgreSQL

### Frontend

- Flutter

### Infrastructure

- Docker
- Kubernetes (Pi Stack)

### Testing

- JUnit
- Mockito
- Integration Tests

### Other

- Git
- Python (automation scripts)


## Phase 1 (Prototype)

The first prototype should be very simple. No crazy UI no crazy backend.
Nothing like accounts or other stuff that can be added in the future. 
Just a barebones application that runs at least.

Something like one input field for new tasks and one output for all tasks.
With these endpoints:

### Backend

```
GET /api/todos
GET /api/todos/{id}
POST /api/todos
PUT /api/todos/{id}
DELETE /api/todos/{id}
```

### Database

```
TodoItem

- id
- title
- completed
```

### Flutter UI

- TextField
- Add button
- Task list
- Checkbox
- Delete button

# Phase 2 (Backend update)

After finishing the prototype the backend will be expanded and updated to get closer to the final version. 

This will be achieved by adding these things:

- Validation
- Exception Handling
- Logging
- DTOs
- Better project structure
- Configuration
- Environment variables

---

# Goals


## Portfolio

- Resume Website
    - HTML
    - CSS
    - Responsive Design
    - Dark / Light Mode
    - Contact Form
    - SEO Basics
    - Deploy (GitHub Pages / Cloudflare)
    - Custom Domain

- Clean GitHub Profile
    - README
    - Pinned Projects
    - Good Documentation
    - Meaningful Commit Messages
    - Consistent Project Structure

## Backend (Java)

- REST API
    - Spring Boot
    - CRUD
    - JWT Authentication
    - Role-based Authorization
    - Validation
    - Global Exception Handling
    - Logging
    - Configuration Profiles
    - Swagger / OpenAPI
    - Docker Support

- Spring
    - Dependency Injection
    - Spring Data JPA
    - Spring Security
    - Configuration
    - Scheduling
    - Caching

## Python

- Automation Scripts
- Web Scraping
- File Processing
- REST API Client
- CLI Applications
- Async Programming
- Data Processing

## Frontend

- Flutter
    - Material Design
    - Responsive Layout
    - Navigation
    - REST Integration
    - Authentication
    - Local Storage
    - State Management (Riverpod/BLoC)

- HTML / CSS
    - Flexbox
    - Grid
    - Animations
    - Accessibility
    - Responsive Design

## Database

- PostgreSQL
    - SQL
    - Joins
    - Indexes
    - Views
    - Transactions
    - Performance
    - Backup & Restore
    - Database Migrations (Flyway)

## DevOps

- Docker
    - Dockerfiles
    - Docker Compose
    - Multi-stage Builds

- Kubernetes Cluster
    - Second Pi 5
    - High Availability
    - Ingress
    - Persistent Volumes
    - ConfigMaps
    - Secrets
    - Helm
    - Monitoring
    - Backups

- GitHub Actions
    - Build
    - Test
    - Docker Build
    - Automatic Deploy

## Testing

- JUnit
- Mockito
- Integration Tests
- Testcontainers
- Flutter Widget Tests
- API Testing (Postman / Bruno)
- Code Coverage

## Architecture

- Clean Architecture
- SOLID Principles
- Design Patterns
- Layered Architecture
- Dependency Injection

## Security

- JWT
- OAuth2 Basics
- Password Hashing
- HTTPS
- OWASP Top 10
- Secrets Management

## Linux

- Bash
- SSH
- Nginx
- Systemd
- Networking
- Cron Jobs

## Git

- Branching Strategy
- Pull Requests
- Code Reviews
- Merge Conflicts
- Semantic Versioning

## Projects

- Resume Website
- Personal Finance App
- Spring Boot REST API
- Flutter Mobile App
- Python Automation Project
- Kubernetes Homelab

## Documentation

- Restructure rdev Repository
