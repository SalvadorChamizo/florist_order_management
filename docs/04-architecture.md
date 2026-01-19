# Architecture

## Purpose

This document describes the high-level architecture of the Floristería Order Management System.
It outlines the chosen architectural style, its main components, and the rationale behind key technical decisions.

The goal is to provide a **clear, maintainable, and scalable structure** appropriate for the project scope and team size.

---

## Architectural Overview

The system is implemented as a **modular monolithic application** following a **layered architecture**.

This approach was chosen to:
- Minimize unnecessary complexity
- Maintain clear separation of responsibilities
- Enable fast development and easy deployment
- Support future evolution without major redesign
---

## Architectural Style

### Monolithic Modular Architecture

The application is deployed as a single unit but internally organized into well-defined modules and layers.

**Rationale**
- The project is developed by a single developer
- The domain is well-defined and limited in scope
- Operational simplicity is a priority
- Microservices would introduce unnecessary overhead

**Alternatives Considered**
- Microservices architecture -> rejected due to operational and cognitive complexity
- Full hexagonal architecture -> rejected to avoid excessive abstraction for the current scope

---

## Layered Architecture

The system follows a layered architecture with the following conceptual layers:

### 1. Presentation Layer
- Exposes RESTful APIs
- Handles HTTP request and responses
- Performs input validation
- Maps external representations to internal data structures

### 2. Application Layer
- Implements use cases and business workflows
- Coordinates domain objects
- Enforces application-level rules
- Acts as the main entry point for business operations

### 3. Domain Layer
- Represents the core business concepts
- Contains entities, value objects, and domain enums
- Encapsulates business rules and invariants
- Remains independent of frameworks where possible

### 4. Infrastructure Layer
- Handles persistence and external concerns
- Implements repositories
- Manages security, configuration, and technical integrations

---

## Dependency Rules

Dependencies between layers follow a strict top-down rule:

- Presentation -> Application
- Application -> Domain
- Infrastructure -> Domain

The Domain layer does not depend on any other layer.

This ensures: 
- High cohesion within layers
- Low coupling between layers
- Improved testability and maintainability

---

## Backend Architecture

The backend is structured according to the layered model, with clear separation between:

- Controllers (Presentation)
- Services (Application)
- Domain models (Domain)
- Persistence and configuration (Infrastructure)

The backend exposes a REST API that serves as the single communication interface with the frontend.

---

## Frontend Architecture

The frontend is implemented as a single-page application (SPA).

**Key characteristics**
- Component-based architecture
- Clear separation between UI components, pages, and data access
- Centralized API communication
- Strong typing via TypeScript

The frontend communicates exclusively with the backend via HTTP APIs.

---

## Data Persistence

- Relational database
- Centralized persistence layer
- Transactions managed at the application boundary

The data model is derived from the domain model to maintain consistency between business concepts and stored data.

---

## Scalability Considerations

The chosen architecture supports:
- Vertical scaling of the application
- Incremental feature growth
- Refactoring toward more advanced architectures if required

No premature optimization for horizontal scalability is introduced.

---

## Architectural Principles

- Simplicity over complexity
- Explicit separation of concerns
- Clear ownership of responsibilities
- Avoidance of premature optimization
- Design for change, not speculation

---