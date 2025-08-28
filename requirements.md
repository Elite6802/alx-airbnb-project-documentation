# Airbnb Clone Backend Requirement Specifications

## 📚 Overview
This document contains the **technical and functional requirements** for three key backend features of the Airbnb Clone project.  
Each feature includes API endpoints, input/output specifications, validation rules, and performance criteria.

---

## 1. User Authentication

### Description
Handles registration, login, and session management for guests and hosts.

### API Endpoints

| Method | Endpoint             | Description                 |
|--------|--------------------|-----------------------------|
| POST   | /api/auth/register  | Register a new user         |
| POST   | /api/auth/login     | Authenticate user           |
| POST   | /api/auth/logout    | Terminate user session      |
| GET    | /api/users/profile  | Retrieve user profile       |
| PUT    | /api/users/profile  | Update user profile         |

### Input/Output Specifications

**Register User**  
- Input (JSON):
```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "SecureP@ss123",
  "role": "guest"
}
```
- Output (JSON):

```json
{
  "message": "User registered successfully",
  "userId": 1,
  "token": "jwt_token_here"
}
``` 
**Login User**

- Input (JSON):

```json
{
  "email": "john@example.com",
  "password": "SecureP@ss123"
}
```
- Output (JSON):
```json
{
  "message": "Login successful",
  "token": "jwt_token_here"
}
```
### Validation Rules
- Email must be valid and unique

- Password must be at least 8 characters, including letters and numbers

- Role must be either "guest" or "host"

### Performance Criteria
- Authentication endpoints must respond within 200ms under normal load

- Support at least 1000 concurrent login requests without failure

## 2. Property Management
###cDescription
- Allows hosts to create, update, delete, and retrieve property listings.

### API Endpoints
| Method | Endpoint               | Description                       |
|--------|------------------------|-----------------------------------|
| POST   | /api/properties         | Create a new property listing     |
| GET    | /api/properties         | Retrieve all properties           |
| GET    | /api/properties/:id     | Retrieve a single property        |
| PUT    | /api/properties/:id     | Update a property listing         |
| DELETE | /api/properties/:id     | Delete a property listing         |


### Input/Output Specifications
- Create Property

Input (JSON):

``` json
{
  "title": "Cozy Apartment",
  "description": "2-bedroom apartment in downtown",
  "location": "Nairobi, Kenya",
  "price": 50,
  "amenities": ["Wi-Fi", "Pool"],
  "availability": ["2025-09-01", "2025-09-30"]
}
```
Output (JSON):

```json

{
  "message": "Property created successfully",
  "propertyId": 101
}
```
### Validation Rules
- Title and description are required

- Price must be a positive number

- Availability must be a valid date range

- Amenities must be from predefined options

### Performance Criteria
-  Property creation, update, and deletion must respond within 250ms

- Retrieval of property listings supports pagination for large datasets

## 3. Booking System
### Description
- Manages property bookings by guests, including date validation, cancellations, and booking status tracking.

## API Endpoints
| Method | Endpoint                    | Description              |
|--------|----------------------------|--------------------------|
| POST   | /api/bookings              | Create a new booking     |
| GET    | /api/bookings              | Retrieve all bookings    |
| GET    | /api/bookings/:id          | Retrieve a single booking|
| PUT    | /api/bookings/:id/cancel   | Cancel a booking         |
| PATCH  | /api/bookings/:id/status   | Update booking status    |


### Input/Output Specifications
## Create Booking

Input (JSON):

```json
{
  "userId": 1,
  "propertyId": 101,
  "startDate": "2025-09-10",
  "endDate": "2025-09-15",
  "guests": 2
}
```
Output (JSON):

```json

{
  "message": "Booking confirmed",
  "bookingId": 1001,
  "status": "confirmed"
}
```
## Validation Rules
- Booking dates must not overlap existing bookings for the same property

- Start date must be before end date

- Number of guests must not exceed property capacity

## Performance Criteria
- Booking creation and validation must respond within 300ms

- System should handle 500 concurrent booking requests without double-booking conflicts
