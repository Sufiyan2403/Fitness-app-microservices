 🏋️ Fitness Microservices

A scalable Fitness Tracker application built using **Spring Boot Microservices architecture**.
This project focuses on clean architecture principles, RESTful API design, and proper backend engineering practices.




This project follows a **microservices-based structure** where:

* Each service is independent
* Each service has its own Spring Boot application
* Each service will eventually have its own database

---

# 🧠 Architectural Principles Followed

## 1️⃣ Separation of Concerns

* Controller → Handles HTTP layer
* Service → Business logic
* Repository → Database interaction
* DTO → Data transfer between layers

---

## 2️⃣ Entity vs DTO

### Why Not Expose Entities Directly?

Entities represent database structure.

Exposing them directly:

* Leaks sensitive fields (like password)
* Couples API to database schema
* Can cause infinite recursion in relationships
* Reduces flexibility

---

## DTO (Data Transfer Object)

DTOs are used to:

* Control what data is sent to the client
* Hide sensitive information
* Shape response structure
* Improve performance
* Prevent tight coupling

### Types Used

* `RegisterRequestDTO` → For incoming registration data
* `UserResponseDTO` → For outgoing user response

---

# 🔥 Register API Implementation

### Endpoint

```
POST /api/users/register
```

---

# 🧱 Annotations Used and Why

## @RestController

* Combines `@Controller` and `@ResponseBody`
* Tells Spring this class handles REST APIs
* Automatically converts objects to JSON

---

## @RequestMapping("/api/users")

* Sets base URL for the controller
* Keeps endpoints organized
* Makes API clean and structured

---

## @PostMapping("/register")

* Handles HTTP POST requests
* Used for creating resources

---

## @Service

* Marks class as business logic layer
* Spring manages it as a bean
* Promotes clean separation from controller

---

## @Repository

* Handles database operations
* Enables JPA repository features
* Integrates with Spring Data

---

## @AllArgsConstructor (Lombok)

* Automatically generates constructor
* Used for constructor-based dependency injection
* Keeps code clean and readable

---

## @Entity

* Marks class as database entity
* Maps object to database table

---

# 📦 ResponseEntity Usage

Instead of returning objects directly, this project uses:

```java
ResponseEntity<T>
```

### Why?

Because HTTP response consists of:

1. Status Code
2. Headers
3. Body

ResponseEntity allows:

* Custom status codes (200, 201, 400, 404)
* Controlled responses
* Professional REST API behavior

Example:

```java
return ResponseEntity.status(HttpStatus.CREATED).body(userResponseDTO);
```

---

# 🧠 Why ResponseEntity Is Important

Without it:

* You lose control over status codes
* You cannot properly design REST APIs
* Error handling becomes inconsistent

With it:

* APIs follow REST standards
* Frontend can rely on status codes
* Error handling becomes structured

---

# 🔐 Security Consideration

Passwords are:

* Never returned in responses
* Not exposed via DTO
* Hidden from API layer

