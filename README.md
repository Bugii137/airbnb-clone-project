# airbnb-clone-project

## Overview
Airbnb Clone Project is a full-stack learning project that simulates building a scalable booking platform. The focus is backend architecture, database design, API development, and security best practices.

## Goals
- Build a robust backend with secure APIs.
- Design a normalized relational database for listings, users, bookings, and reviews.
- Implement authentication, authorization, and input validation.
- Integrate CI/CD and containerization for repeatable deployments.
- Produce clear documentation and automated tests.

## Tech Stack
- Backend: Django (Python)
- Database: MySQL
- API: GraphQL (or REST where appropriate)
- Containerization: Docker
- CI/CD: GitHub Actions (or equivalent)
- Dev tools: Git, pytest (or Django tests)

## Technology Stack

- Django — A high-level Python web framework used to build the backend application, routing, models, and core business logic.
- Django REST Framework — Adds tools for quickly building RESTful APIs, serialization, authentication, and viewsets.
- GraphQL (e.g., Graphene) — Provides a flexible query layer for clients to request exactly the data they need, complementing or replacing REST endpoints.
- PostgreSQL — Recommended production relational database for reliable transactions, advanced indexing, and complex queries (alternative: MySQL, used in some dev setups).
- MySQL — Supported relational database option; can be used for development or deployments where MySQL is preferred.
- Celery — Distributed task queue for handling asynchronous work such as email notifications, background processing, and payment tasks.
- Redis — In-memory datastore used for caching, Celery broker/back-end, and fast session or rate-limit storage.
- Docker — Containerization for consistent development and production environments, simplifying dependency management and deployment.
- Git / GitHub — Version control and repository hosting; GitHub Actions for CI/CD automation (tests, linting, builds, and deployment).
- pytest / Django tests — Test frameworks for unit and integration testing to ensure code quality and prevent regressions.
- OpenAPI / Swagger — API documentation tooling to describe REST endpoints, request/response schemas, and make integration easier.
- Nginx / Gunicorn (or uWSGI) — Recommended production web server and WSGI application server for serving the Django app behind a reverse proxy.
- TLS / OAuth / JWT — Security components and protocols for secure transport (TLS) and authentication/authorization (OAuth2 or JWT tokens).

## Project Structure (suggested)
- backend/        — Django app
- db/             — DB schema & migrations
- infra/          — Docker & deployment configs
- tests/          — Unit and integration tests
- README.md

## Getting Started
1. Create a public GitHub repo named `airbnb-clone-project`.
2. Clone locally:
```sh
git clone <repo-url>
cd airbnb-clone-project
```

## Team Roles

- Backend Developer  
  Designs and implements API endpoints, business logic, data models, authentication/authorization, and integration with background tasks and external services.

- Database Administrator (DBA)  
  Designs the relational schema, manages migrations, indexing, backups, performance tuning, and ensures data integrity and recovery procedures.

- DevOps Engineer  
  Builds and maintains CI/CD pipelines, containerization, infrastructure as code, monitoring, and scalable deployment and rollback strategies.

- QA Engineer  
  Creates and runs automated and manual tests, validates API behavior, performs regression testing, and documents/report issues for remediation.

- Frontend Developer  
  Implements user interfaces, integrates with REST/GraphQL APIs, ensures responsive accessible UI, and collaborates on API contracts and error handling.

- Product Manager  
  Defines product requirements, prioritizes features, coordinates stakeholders, and validates that delivered functionality meets user and business needs.

- Security Engineer  
  Conducts threat modeling, enforces secure coding and dependency management practices, performs vulnerability assessments, and advises on data protection and access controls.

- UX Designer  
  Designs user flows, wireframes, and interaction patterns to ensure the product is intuitive, usable, and aligned with user goals.