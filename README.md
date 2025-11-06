# Project Management Tool

## Team Members
- AL-RAMAHI NIDAL Group 1241B  
- LAURA ERASO LORENZO  Erasmus  
-João Filipe Correia Andrade Sousa
---

## Project Description

The **Project Management Tool** is a microservices-based web application designed to help teams efficiently manage projects, tasks, and collaboration. It provides integrated features for **Task Management**, **Collaboration**, and **Reporting & Analytics** to streamline communication and enhance project transparency.

### Key Functionalities
- **Task Management** – Create, assign, and track project tasks with priorities, statuses, and deadlines.  
- **Collaboration** – Real-time messaging and commenting within tasks for effective teamwork.  
- **Reporting & Analytics** – Generate detailed reports and performance summaries for progress tracking.

### Architectural Choice
After evaluating Monolithic, Microservices, and Containerized architectures, the project adopts a **Microservices Architecture** for its scalability, modularity, and fault tolerance. Each service—**Task Management**, **Collaboration**, and **Reporting**—runs independently and communicates asynchronously through **RabbitMQ**.  
All services are **containerized using Docker** and registered dynamically with **Eureka Server** for service discovery and load balancing.

### Technologies Used
- **Spring Boot** – For backend microservice development  
- **RabbitMQ** – For asynchronous message brokering  
- **Eureka Server** – For service discovery and registry  
- **Docker** – For containerized and consistent deployments  
- **MySQL** – For relational database storage  
- **Postman** – For API testing and validation  

---

## Design Patterns and Justifications

To ensure flexibility, scalability, and clean architecture, the project uses several key software design patterns. Each one addresses specific functional and structural needs within the system.

---

### 1. Observer Pattern
**Where Used:** RabbitMQ event-driven communication between microservices  

The **Observer Pattern** supports asynchronous updates across services. When the **Task Management Service** creates or updates a task, it publishes an event to RabbitMQ. The **Collaboration** and **Reporting Services** are observers that automatically react to these events.

**Problem Solved:** Enables real-time communication between services without direct dependencies.  
**Advantages:**  
- Improves scalability by decoupling services.  
- Increases fault tolerance — failures in one service don’t affect others.  
- Enables reactive, event-driven data synchronization.

---

### 2. Singleton Pattern
**Where Used:** Eureka Server and shared configuration components  

The **Singleton Pattern** ensures there is only one instance of critical shared components (e.g., Eureka Server, database connection pools). This prevents redundant initialization and keeps the configuration consistent across the system.

**Problem Solved:** Prevents multiple conflicting instances of essential components.  
**Advantages:**  
- Saves resources and maintains global consistency.  
- Simplifies management of shared objects.  
- Reduces synchronization overhead.

---

### 3. Factory Pattern
**Where Used:** Creation of domain entities (Tasks, Messages, Reports) in microservices  

The **Factory Pattern** encapsulates the logic for creating objects with multiple parameters and dependencies. This pattern is used in the creation of `Task`, `Message`, and `Report` entities within their respective microservices.

**Problem Solved:** Simplifies and centralizes complex object creation logic.  
**Advantages:**  
- Promotes code reusability and consistency.  
- Supports easy modification when adding new entity types.  
- Reduces coupling between object creation and usage.

---

### 4. Facade Pattern
**Where Used:** API Gateway  

The **API Gateway** applies the **Facade Pattern** by serving as a single entry point for all client requests. It routes requests to appropriate microservices (Task, Collaboration, or Reporting) while abstracting internal complexity.

**Problem Solved:** Prevents clients from managing multiple service endpoints.  
**Advantages:**  
- Simplifies communication between frontend and backend.  
- Improves security by handling authentication and request filtering centrally.  
- Reduces client-side complexity and ensures consistency.

---

### 5. Repository Pattern
**Where Used:** Data access layer in each microservice  

Each microservice implements the **Repository Pattern** to handle database operations (CRUD). This separates persistence logic from business logic, making the system easier to maintain and test.

**Problem Solved:** Keeps business logic independent from database-specific queries.  
**Advantages:**  
- Improves testability by abstracting database interactions.  
- Simplifies migration to other database systems.  
- Promotes clean, maintainable, and organized code.

---

## Summary

This milestone defines the conceptual and architectural foundation of the **Project Management Tool**.  
By applying proven **design patterns** and adopting a **microservices architecture**, the system achieves modularity, scalability, and reliability. Each pattern is directly connected to real project requirements, ensuring both performance and maintainability in future milestones.

---
