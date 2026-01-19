# Domain Model

## Purpose

This document defines the core domain model of the Floristeria Order Management System.
It describes the main business entities, their responsibilities, relationships, and key rules.

The domain model represents **business concepts**, independent of technical implementation details.

---

## Core Domain Concepts

The system is centered around the management of flower orders placed by customers and handled by employees.

The main domain concepts are:
- Order
- Customer
- Product
- User

---

## Entity: Order

### Description
Represents a customer order for a floral arrangement, including its lifecycle and associated data.

### Attributes
- id: unique identifier
- orderNumber: human-readable order reference
- status: current state of the order
- paymentStatus: order already paid or not
- pickupDate: scheduled date for order pickup
- totalPrice: final price of the order
- notes: optional custom message or instructions
- createdAt: creation timestamp

### Responsibilities
- Maintain its current lifecycle state
- Enforce valid status transitions
- Represent a complete and consistent order

---

## Entity: Customer

### Description
Represents a customer placing one or more orders.

### Attributes
- id: unique identifier
- name: customer name
- phoneNumber: contact phone number
- email: contact email

### Responsibilities
- Store customer contact information
- Be associated with one or more orders

---

## Entity: Product

### Description
Represents a type of floral arrangement or product offered by the floristería.

### Attributes
- id: unique identifier
- name: product name
- basePrice: default price
- description: optional description

### Responsibilities
- Define the type of product associated with an order
- Provide pricing reference information

---

## Entity: User

### Description
Represents an internal system user (employee or administrator).

### Attributes
- id: unique identifier
- username: login identifier
- role: user role (ADMIN or EMPLOYEE)

### Responsibilities
- Authenticate into the system
- Perform authorized operations based on role

---

## Order Lifecycle

Orders follow a predefined lifecycle represented by the `OrderStatus` enum:

```text
CREATED -> IN_PROGRESS -> READY -> COLLECTED
                 X CANCELED
```

### Status Definitions
- CREATED: Order has been registered but not yet prepared
- IN_PROGRESS: Order is being prepared
- READY: Order is ready for pickup
- COLLECTED: Order has been collected by the customer
- CANCELED: Order has been canceled before collection

### Business Rules
- An order cannot transition from COLLECTED or CANCELED to any other state
- Status transitions must follow the defined lifecycle
- Status changes must be explicitly triggered by authorized users

---

## Relationships
- A Customer can have multiple Orders (1:N)
- A User can create and manage multiple Orders (1:N)
- An Order is associated with exactly one Customer
- An Order references exactly one Product

---

## Domain Invariants
The following invariants must always hold true:

- An Order must always have a valid status
- An Order must be associated with a Customer
- An Order must have a pickup date
- An Order must have a non-negative total price

---

## Domain Boundaries
- The domain model does not handle persistence concerns
- The domain model does not include authentication or authorization logic
- The domain model does not depend on external frameworks

---

