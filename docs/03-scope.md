# Scope

## Purpose

This document defines the scope of the Floristería Order Management System.
Its goal is to clearly establish **what is included in the project**, **what is intentionally excluded**, and **what may be considered for future iterations**, in order to avoid scope creep and uncontrolled complexity.

## In-Scope (MVP)

The following features are included in the initial Minimum Viable Product (MVP):

### Order Management
- Create new orders
- View and list existing orders
- Update order status according to the defined lifecycle
- Search and filter orders by pickup date, status and key words

### Customer Management
- Associate customer information with an order
- Store basic customer details (name, phone number and (optional) email)

### User Management
- User authentication
- Role-based authorization
- Support for ADMIN and EMPLOYEE roles

### Receipt Generation
- Generate a printable receipt for each order
- Include essential order and customer information

### System Characteristics
- Single-location operation
- Web-based interface
- Centralized data persistence

---

## Out of Scope (Explicitly Excluded)

The following features are intentionally excluded from the MVP:

### Payments and Billing
- Online payment processing
- Payment gateways
- Invoicing systems

### Notifications and Communication
- SMS or WhatsApp alerts
- Automated reminders

### Inventory and Stock Management
- Real-time stock tracking
- Supplier management
- Material consumption analysis

### Advanced Analytics
- Sales reports
- Performance metrics
- Historical trend analysys

### Multi-Platform Support
- Mobile applications
- Offline-first functionality

---

## Future Considerations

The following features may be considered in future iterations of the system:

- Inventory and stock management
- Order statistics and dashboards
- Notification system for order readiness
- Multi-location support
- Customer history and loyalty features

These features are **intentionally postponed** to maintain focus on the core problem.

---

## Design Constraints

- The system is designed for a small internal team
- Simplicity and clarity are prioritized over feature richness
- The architecture must support incremental growth without major refactoring

---

## Scope Principles

- Solve the core business problem first
- Prefer simplicity over completeness
- Avoid premature optimization
- Deliver a stable and maintainable MVP

---