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

## Database Design

Key entities, important fields, and relationships:

- Users
  - id (PK)
  - email (unique)
  - password_hash
  - full_name
  - created_at
  - Relationships: a user can own multiple properties, create multiple bookings, write multiple reviews, and make payments.

- Properties
  - id (PK)
  - owner_id (FK → Users.id)
  - title
  - description
  - address (structured: street, city, state, country, zip)
  - price_per_night
  - Relationships: a property belongs to one owner (User), has many bookings, reviews, images, and amenities.

- Bookings
  - id (PK)
  - user_id (FK → Users.id)
  - property_id (FK → Properties.id)
  - start_date
  - end_date
  - total_price
  - status (pending/confirmed/cancelled)
  - Relationships: a booking belongs to one user and one property; may have one or more payments.

- Reviews
  - id (PK)
  - user_id (FK → Users.id)
  - property_id (FK → Properties.id)
  - rating (e.g., 1-5)
  - comment
  - created_at
  - Relationships: a review belongs to one user and one property.

- Payments
  - id (PK)
  - booking_id (FK → Bookings.id)
  - user_id (FK → Users.id)
  - amount
  - currency
  - status (pending/paid/refunded)
  - provider_reference (external payment id)
  - Relationships: a payment is linked to a booking and the user who paid.

Notes / recommendations
- Indexes: add indexes on Users.email, Properties.owner_id, Bookings.property_id and user_id, Reviews.property_id for fast lookups.
- Constraints: enforce FK constraints and use transactions for booking/payment workflows to maintain consistency.
- Normalization: keep address components and amenity list normalized (separate tables) if needed for queries and reuse.
- Soft deletes & audit: consider soft-delete flags and created/updated timestamps for auditability.

## Feature Breakdown

- API Documentation  
  Comprehensive API docs (OpenAPI/Swagger) and GraphQL schema provide clear contracts for frontend and third-party integrations. This ensures developers can discover endpoints, understand request/response formats, and test APIs quickly.

- User Management  
  Registration, login, profile management, and role-based access control enable secure user interactions. Proper authentication and validation protect user data and support different user types (guests, hosts, admins).

- Property Management  
  CRUD operations for listings, images, amenities, and availability management allow hosts to publish and update properties. Rich property metadata and search filters improve discoverability for guests.

- Booking System  
  Create, update, and manage reservations with availability checks, pricing calculations, and status workflows (pending/confirmed/cancelled). Transactional booking flows ensure consistency between availability and payments.

- Payment Processing  
  Integrates with external payment providers to charge guests, issue refunds, and record transactions. Secure handling of payment data, idempotent operations, and reconciliation records are included for reliability.

- Review System  
  Guests can leave ratings and comments for properties, while hosts can respond to feedback. Aggregated ratings and review moderation help maintain listing quality and trust.

- Notifications & Background Tasks  
  Asynchronous tasks (Celery) handle emails, push notifications, and long-running jobs without blocking request processing. This improves responsiveness and enables retryable background workflows.

- Search, Caching & Optimization  
  Full-text search, indexing, and Redis caching speed up property queries and frequently accessed data. Combined with DB indexes and query optimization, this reduces latency under load.

- Security & Compliance  
  Transport security (TLS), token-based auth (JWT/OAuth), input validation, and dependency scanning protect user data and the platform. Audit logs and role-based controls support compliance and incident response.

## API Security

Key security measures and why they matter:

- Authentication  
  Use JWT/OAuth2 with short-lived access tokens and refresh tokens. Proper authentication ensures only verified users can access protected endpoints and reduces account takeover risk.

- Authorization & RBAC  
  Enforce role-based access control and attribute-based checks at the API layer. Prevents privilege escalation and ensures users can only perform allowed actions (e.g., only owners can modify their listings).

- Transport Security (TLS)  
  Enforce HTTPS for all API traffic and redirect HTTP to HTTPS. Protects data in transit (credentials, PII, payment tokens) from eavesdropping and MITM attacks.

- Input Validation & Output Encoding  
  Validate and sanitize all client input and encode outputs to prevent SQL injection, XSS, and other injection attacks. Ensures backend integrity and protects downstream systems.

- Rate Limiting & Throttling  
  Apply per-user and per-IP rate limits and burst controls. Protects APIs from brute-force, scraping, and denial-of-service attempts and preserves service availability.

- Payment Security & PCI Compliance  
  Use tokenized payment flows (do not store raw card data) and integrate a PCI-compliant payment provider. Ensures secure handling of transactions and reduces liability.

- Logging, Monitoring & Alerting  
  Centralize logs, monitor for anomalies, and alert on suspicious activity (failed logins, repeated errors). Enables fast detection and response to incidents and supports audits.

- Secrets Management & Dependency Controls  
  Store secrets in a vault (e.g., HashiCorp Vault, GitHub Secrets) and scan dependencies for vulnerabilities. Prevents secret leakage and reduces risk from vulnerable libraries.

- CSRF Protection, CORS, and Secure Headers  
  Implement CSRF protections for stateful endpoints, configure CORS to allow only trusted origins, and set secure HTTP headers (HSTS, X-Content-Type-Options). Helps mitigate common web attack vectors.

- Encryption at Rest & Backups  
  Encrypt sensitive data at rest and ensure encrypted backups with access controls. Protects user and payment data in case of infrastructure compromise.

These measures collectively protect user data, maintain trust, secure payment flows, and ensure platform availability and compliance.

## CI/CD Pipeline

- What CI/CD is  
  Continuous Integration (CI) automates building and testing code on every change to catch regressions early. Continuous Delivery/Deployment (CD) automates packaging and deploying validated builds to staging/production for fast, repeatable releases.

- Why it matters  
  CI/CD enforces consistent quality checks (linting, tests, security scans), reduces manual errors, speeds up feedback loops, and enables safe, frequent deployments with rollback capabilities.

- Typical pipeline stages  
  Lint → Unit/Integration tests → Build (Docker image) → Push image to registry → Run DB migrations → Deploy to staging → Run end-to-end checks → Promote to production.

- Tools to use  
  GitHub Actions (CI), Docker / Docker Hub or GitHub Container Registry (images), Docker Compose / Kubernetes + Helm (runtime), Terraform / Ansible (infrastructure provisioning), GitHub Secrets or a vault for credentials, and monitoring tools (Sentry, Prometheus) for post-deploy observability.