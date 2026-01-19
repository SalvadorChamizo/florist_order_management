# Security

## Purpose

This document describes the security considerations of the Floristería Order Management System.
It defines how authentication and authorization are handled and outlines basic security principles applied to the system.

The goal is to ensure **reasonable security for an internal business application**, without introducing unnecessary complexity.

---

## Security Scope

The system is intended for:
- Internal use only
- A small number of trusted users
- A controlled environment

As a result, security measures are **pragmatic rather than enterprise-grade**.

---

## Authentication

### Overview

The system requires authentication for all API endpoints.

Authentication is handled outside the domain model and belongs to the infrastructure layer.

### Credentials Storage

- User passwords are **never stored in plain text**
- Passwords are stored as secure hashes
- A strong one-way hashing algorithm is used (bcrypt)

Example stored data:
- username
- passwordHash

The domain model does not have access to password data.

---

## Authorization

### Roles

The system supports the following roles:
- ADMIN
- EMPLOYEE

### Authorization Rules

- All authenticated users can:
    - Create orders
    - View orders
    - Update order status

- ADMIN users can:
    - Manage users
    - Manage products

Authorization is enforced at the application layer.

---

## API Security

- All API endpoints require authentication
- Authorization checks are applied before executing business logic
- The API does not expose internal domain entities directly
- Input data is validated before processing

---

## Data Protection

- Sensitive data is not exposed unnecessarily in API responses
- Only required fields are returned to the client
- Internal identifiers are treated as opaque values

---

## Error Handling and Information Disclosure

- Error messages do not expose internal system details
- Stack traces and internal exceptions are not returned to clients
- Error responses are standardized

---

## Threat Awareness

The system considers basic threats such as:
- Unauthorized access
- Invalid or malicious input
- Accidental data exposure

Advanced threats (e.g. DDoS, penetration attacks) are considered out of scope.

---

## Security Principles

- Least privilege
- Separation of concerns
- Secure defaults
- Defense against common mistakes rather than advanced attacks

---