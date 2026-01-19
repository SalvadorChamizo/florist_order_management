# Requirements

## Purpose

This document defines the functional and non-functional requirements of the Floristería Order Management System.
It describes **what the system must do**, without prescribing implementation details.

---

## Functional Requirements

### FR-1: Order Creation
The system must allow authorized users to create a new order with the following information:
- Customer details (name, phone number)
- Product or arrangement type
- Custom message or notes
- Pickup date
- Total price

**Acceptance Criteria**
- All mandatory fields must be validated
- Each order must be assigned a unique identifier
- The initial order status must be set automatically

---

### FR-2: Order Status Management
The system must allow authorized users to update the status of an order.

Supported statuses:
- CREATED
- IN_PROGRESS
- READY
- COLLECTED
- CANCELED

**Acceptance Criteria**
- Only valid status transitions are allowed
- The current status of an order must be visible at all times

---

### FR-3: Order Listing and Search
The system must provide a list of orders with filtering capabilities.

Supported filters:
- Pickup date
- Order status
- Key words

**Acceptance Criteria**
- Results must reflect the latest persisted data
- Filters must be combinable

---

### FR-4: Customer Receipt Generation

The system must generate a printable receipt for each order.

Receipt must include:
- Order identifier
- Customer name
- Pickup date
- Order details
- Total price

**Acceptance Criteria**
- Receipt must be generated on demand
- Receipt format must be printable (PDF or equivalent)

---

### FR-5: User Authentication and Authorization
The system must restrict access based on user authentication and role.

Roles:
- ADMIN
- EMPLOYEE

**Acceptance Criteria**
- Only authenticated users can access the system
- Role-based access must be enforced for sensitive operations

---

## Non-Functional Requirements

### NFR-1: Usability
The system must be usable during high-demand periods with minimal friction.

- Simple and clear user flows
- No unnecessary steps to create or update orders

---

### NFR-2: Performance
The system must remain responsive under peak load conditions.

- Orders must not be lost or duplicated
- Partial or invalid data must not be persisted

---

### NFR-3: Reliability
The system must ensure data persistence and consistency.

- Orders must not be lost or duplicated
- Partial or invalid data must not be persisted

---

### NFR-4: Security
The system must implement basic security measures.

- Authentication required for all operations
- Authorization enforced via roles
- Sensitive data must not be exposed unintentionally

---

### NFR-5: Maintainability
The system must be structured to allow future changes with minimal impact.

- Clear separation of concerns
- Readable and well-organized codebase
- Documented architecture and decisions

---

## Assumptions and Constraints

- The system is intended for internal use only
- A single physical location is supported
- Internet connectivity is available during operation

---

