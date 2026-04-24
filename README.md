# JWT Authentication System

A complete JWT-based authentication system built with Spring Boot
and Spring Security. Implements secure user registration, login,
and role-based access control.

## Tech Stack
- Java 21
- Spring Boot 3.2.5
- Spring Security
- JWT (jjwt 0.11.5)
- Spring Data JPA
- MySQL Database
- BCrypt Password Encoding
- Lombok

## Features
- User registration with validation
- Secure login with JWT token generation
- BCrypt password hashing (never stores plain text)
- Role-based access control (USER / ADMIN)
- Protected API endpoints
- Stateless authentication
- Token expiry (24 hours)

## Security Flow
Register → BCrypt hash password → Save to DB → Return JWT token
Login    → Verify password → Generate JWT → Return token
Request  → JwtFilter checks token → Validate → Allow/Deny

## API Endpoints

| Method | URL | Access | Description |
|--------|-----|--------|-------------|
| POST | /api/auth/register | Public | Register new user |
| POST | /api/auth/login | Public | Login and get token |
| GET | /api/admin/** | ADMIN only | Admin endpoints |

## Sample Requests

**Register:**
```json
POST /api/auth/register
{
    "name": "Ravi Kumar",
    "email": "ravi@gmail.com",
    "password": "password123"
}
```

**Response:**
```json
{
    "token": "eyJhbGciOiJIUzI1NiJ9...",
    "role": "USER",
    "message": "Registration successful!"
}
```

**Using the token:**
GET /api/protected-endpoint
Headers:
Authorization: Bearer eyJhbGciOiJIUzI1NiJ9...

## How to Run

1. Create MySQL database
```sql
CREATE DATABASE authdb;
```

2. Update `application.properties`
```properties
spring.datasource.url=jdbc:mysql://localhost:3306/authdb
spring.datasource.username=root
spring.datasource.password=yourpassword
jwt.secret=YourSecretKeyHere
jwt.expiration=86400000
```

3. Run the application
```bash
mvn spring-boot:run
```

## What I Learned
- Spring Security configuration
- JWT token generation and validation
- BCrypt password hashing
- Role-based access control
- Stateless authentication
- Security filter chain
- @Value for reading properties
