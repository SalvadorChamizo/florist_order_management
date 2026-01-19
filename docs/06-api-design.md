# API Design

## Purpose

This document defines the public REST API of the Floristería Order Management System.
It serves as a **contract between frontend and backend**, describing available endpoints, request/response structures, and error handling.

The API is designed to be:
- Clear and predictable
- Easy to consume by a frontend application
- Stable and versionable

---

## API Versioning

All endpoints are prefixed with a version identifier:
```text
/api/v1
```

This allows future evolution without breaking existing clients.

---

## Authentication

All endpoints require authentication unless explicitly stated otherwise.

Authentication is handled via:
- Token-based authentication (detaild defined in security design)

The API assumes that authenticated user context is available for authorization.

---

## Resources Overview

Main resources exposed by the API:
- Orders
- Customers
- Products
- Users (internal)

---

## Orders API

### Create Order

**POST** `/api/v1/orders`

Creates a new order and its associated customer if necessary.

The client does not need to create a customer explicitly before creating an order.
Customer creation is handled as part of the order creation workflow.

**Request Body**
```json
{
    "customer": {
        "name": "María López",
        "phoneNumber": "600123123",
        "email": "marialopez@example.com"
    },
    "productId": "uuid",
    "pickupDate": "2026-11-01",
    "paymentStatus": "false",
    "notes": "10 Red roses with ornaments",
    "totalPrice": 45.00
}
```

**Response**
- `201 Created`
```json
{
    "id": "uuid",
    "orderNumber": "ORD-2026-001",
    "status": "CREATED"
}
```

---

### List Orders

**GET** `/api/v1/orders`

Optional query parameters:
- status
- pickupDate

**Response**
- `200 OK`
```json
[
    {
        "id": "uuid",
        "orderNumber": "ORD-2026-001",
        "status": "READY",
        "pickupDate": "2026-11-01",
        "totalPrice": 45.00
    }
]
```

---

### Get Order by ID

**GET** `/api/v1/orders/{orderId}`

**Response**

- `200 OK`
```json

{
    "id": "uuid",
    "orderNumber": "ORD-2026-001",
    "status": "IN_PROGRESS",
    "pickupDate": "2026-11-01",
    "totalPrice": 45.00,
    "notes": "12 Red roses with ornaments",
    "customer": {
        "id": "uuid",
        "name": "María López",
        "phoneNumber": "600123123",
        "email": "marialopez@example.com"
    },
    "product": {
        "id": "uuid",
        "name": "Rose Bouquet"
    }
}
```
---

### Update Order Status

**PATCH** `/api/v1/orders/{orderId}/status`

**Request Body**
```json
{
    "status": "READY"
}
```

**Response**
- `200 OK`

---

## Customers API

### Create Customer

**POST** `/api/v1/customers`

**Request Body**
```json
{
    "name": "María López",
    "phoneNumber": "600123123"
}
```

**Response**
- `201 Created`
```json
{
    "id": "uuid"
}
```

---

## Products API

### List Products

**GET** `/api/v1/products`

**Response**
- `200 OK`
```json
[
    {
        "id": "uuid",
        "name": "Rose Bouquet",
        "basePrice": 40.00
    }
]
```

---

## Error Handling

The API uses standard HTTP status codes.

### Common Error Responses

### 400 Bad Request
```json
{
    "error": "INVALID_REQUEST",
    "message": "Pickup date must be in the future"
}
```

### 404 Not Found
```json
{
    "error": "RESOURCE_NOT_FOUND",
    "message": "Order not found"
}
```

### 403 Forbidden
```json
{
    "error": "ACCESS_DENIED",
    "message": "Operation not allowed"
}
```

---

## Data Validation Rules
- Required fields must be present
- Dates must follow ISO-8601 format
- Prices must be non-negative
- Status transitions must follow domain rules

---

## API Boundaries
- The API does not expose internal domain models directly
- DTOs are used for request and response payloads
- Business rules are enforced at the application layer

---

