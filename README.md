1. Project Overview
A robust, scalable RESTful API built with Spring Boot to handle core e-commerce operations. This system manages product catalogs, user authentication, shopping carts, and order processing.

Tech Stack
Framework: Spring Boot 3.x

Language: Java 21

Database: PostgreSQL (Production) / H2 (Development)

ORM: Spring Data JPA

Security: Spring Security + JWT (JSON Web Tokens)

Validation: Hibernate Validator

2. System Architecture
The project follows a Layered Architecture to ensure separation of concerns:

Controller Layer: Handles HTTP requests and maps them to service methods.

Service Layer: Contains business logic (e.g., price calculations, inventory checks).

Repository Layer: Interacts with the database using JPA/Hibernate.

Model/Entity Layer: Defines the database schema and data structures.

3. Database Schema (ERD)
The system is built around the following core entities:

User: Stores credentials, roles (ADMIN/CUSTOMER), and profiles.

Product: Catalog items with name, price, and stock levels.

Category: Logical grouping of products.

CartItem: Temporary items linked to a User.

Order: Finalized purchase records with status tracking (PENDING, SHIPPED, DELIVERED).
This documentation focuses on the theoretical underpinnings, design patterns, and architectural principles of the Spring Boot E-commerce Backend. It serves as a conceptual guide for understanding why the system is built this way.

📘 Theoretical Documentation: E-Commerce Backend System
1. Architectural Pattern: Layered (n-Tier) Architecture
The system is built on the Layered Architecture principle, which promotes "Separation of Concerns." Each layer has a specific responsibility:

Presentation Layer (REST Controllers): Responsible for exposing endpoints, handling HTTP methods (GET, POST, etc.), and managing request/response mapping.

Business Logic Layer (Services): This is the "brain" of the application. It handles calculations, transaction management, and coordinates between different repositories.

Data Access Layer (Repositories): An abstraction over the database. It allows the application to remain database-agnostic by using Spring Data JPA.

Domain Layer (Entities): Represents the data structures and the database schema.

2. Core Spring Framework Concepts
To understand the backend, one must understand these fundamental Spring mechanisms:

Dependency Injection (DI) & Inversion of Control (IoC)
Instead of classes creating their own dependencies (e.g., a Controller manually creating a Service object), the Spring IoC Container manages the lifecycle of objects (Beans). This makes the code:

Loosely Coupled: Classes don't need to know how their dependencies are instantiated.

Testable: Dependencies can be easily replaced with "Mocks" during unit testing.

Aspect-Oriented Programming (AOP)
Used for "Cross-Cutting Concerns"—functionality that spans multiple layers.

Transaction Management: Ensuring that an order is only saved if the payment is successful (all-or-nothing).

Logging & Security: Intercepting requests to check for valid tokens before they reach the Controller.

3. REST API Design Principles
The API follows Representational State Transfer (REST) constraints:

Statelessness: Each request contains all the information needed to process it (handled via JWT).

Resource-Based: URLs are based on nouns (e.g., /products), not verbs.

Hateoas (Ideal): Providing links in responses to guide the client on what they can do next.

Standard HTTP Methods:

GET: Retrieve data (Idempotent).

POST: Create new resources.

PUT/PATCH: Update existing resources.

DELETE: Remove resources.

4. Database Design & Persistence (JPA/Hibernate)
The project utilizes Object-Relational Mapping (ORM) to bridge the gap between Java objects and Relational Database tables.

Key Theoretical Concepts:
Object-Relational Mapping: Mapping a Java Class to a SQL Table and a Class Property to a Table Column.

Relationship Mapping:

One-to-Many: One Category contains many Products.

Many-to-Many: One Order can contain many Products, and one Product can be in many Orders.

Lazy vs. Eager Loading: * Lazy: Data is only fetched from the DB when specifically requested (better for performance).

Eager: Data is fetched immediately with the parent object.

5. Security & Authentication Theory
Security is implemented using a Filter Chain mechanism.

Authentication: Verifying who the user is (Login).

Authorization: Verifying what the user is allowed to do (Role-Based Access Control - RBAC).

JWT (JSON Web Tokens): A compact, URL-safe means of representing claims to be transferred between two parties. It allows the server to verify the user's identity without storing session data in memory.

6. Testing Strategies
To ensure reliability, the system follows the Testing Pyramid:

Unit Tests: Testing individual methods in the Service layer using JUnit and Mockito to mock dependencies.

Integration Tests: Testing the interaction between layers (e.g., ensuring the Repository correctly saves to a real or in-memory H2 database).

End-to-End (E2E) Tests: Testing the full request-response cycle from the Controller down to the Database.

7. Data Validation & Exception Handling
JSR-303/JSR-380 Bean Validation: Using annotations like @NotNull, @Min, and @Size to ensure data integrity before it reaches the database.

Global Exception Handling: Centralizing error logic so that the API always returns a consistent JSON structure, regardless of where the error occurred.
