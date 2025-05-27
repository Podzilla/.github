# Podzilla Organization

## Overview
Podzilla is an open-source e-commerce platform built on a microservices architecture, designed to deliver a scalable, modular, and efficient solution for online retail. The platform is composed of multiple specialized repositories, each handling a distinct aspect of the e-commerce ecosystem, such as authentication, cart management, order processing, warehouse operations, courier logistics, ERP integration, frontend user experience, API gateway, infrastructure, and shared utilities. By leveraging modern technologies and best practices, Podzilla ensures robust performance, security, and extensibility for businesses of all sizes.

## Repositories
The Podzilla organization consists of the following repositories, each serving a specific function within the platform:
- **[Authentication](https://github.com/Podzilla/authentication)**: Manages user authentication and authorization using Spring Boot, Spring Security, and JWT.
- **[Cart](https://github.com/Podzilla/cart)**: Handles shopping cart functionality, including adding, updating, and removing items.
- **[Order](https://github.com/Podzilla/order)**: Manages order creation, processing, and tracking.
- **[Warehouse](https://github.com/Podzilla/warehouse)**: Oversees inventory management and stock tracking.
- **[Courier](https://github.com/Podzilla/courier)**: Coordinates delivery logistics and courier services.
- **[ERP](https://github.com/Podzilla/erp)**: Integrates enterprise resource planning for business operations like accounting and supply chain.
- **[Frontend](https://github.com/Podzilla/frontend)**: Provides the user interface for the Podzilla platform, built with modern web technologies.
- **[API-Gateway](https://github.com/Podzilla/api-gateway)**: Acts as the entry point for all client requests, routing them to appropriate microservices.
- **[Infrastructure](https://github.com/Podzilla/infrastructure)**: Manages deployment and orchestration using Kubernetes.
- **[Podzilla-Utils-Library](https://jitpack.io/#Podzilla/podzilla-utils-library)**: A shared utility library hosted on JitPack, providing RabbitMQ configurations for asynchronous communication between microservices via events and queues.

## Badges
![Java](https://img.shields.io/badge/Java-17-blue)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.2.0-green)
![Docker](https://img.shields.io/badge/Docker-24.0-blue)
![Kubernetes](https://img.shields.io/badge/Kubernetes-1.28-blue)
![RabbitMQ](https://img.shields.io/badge/RabbitMQ-3.12-orange)
![React](https://img.shields.io/badge/React-18.2-blue)
![Build Status](https://img.shields.io/github/actions/workflow/status/Podzilla/infrastructure/ci.yml?branch=main&label=CI%2FCD)
![License](https://img.shields.io/badge/License-MIT-green)

## Features
- **Modular Architecture**: Each microservice focuses on a single responsibility, enabling independent development, deployment, and scaling.
- **Asynchronous Communication**: Utilizes RabbitMQ (via `podzilla-utils-library`) for event-driven communication between services.
- **Scalable Infrastructure**: Kubernetes-based deployment ensures high availability and fault tolerance.
- **Secure Authentication**: Robust user authentication and authorization using JWT and Spring Security.
- **Rich User Experience**: A responsive frontend built with modern web technologies (e.g., React).
- **API Gateway**: Centralized request routing and load balancing for seamless client-service interactions.
- **Comprehensive Testing**: Unit and integration tests across all repositories using JUnit and other testing frameworks.
- **Code Quality**: Enforced through Checkstyle and consistent Java conventions across all services.

## Code Style
Podzilla repositories adhere to Java conventions and best practices for consistency and maintainability:
- **Naming Conventions**:
  - Classes: PascalCase (e.g., `OrderService`, `CartController`)
  - Methods and Variables: camelCase (e.g., `addItemToCart`, `orderId`)
  - Constants: UPPER_SNAKE_CASE (e.g., `MAX_CART_ITEMS`)
  - Packages: Lowercase with meaningful hierarchy (e.g., `com.podzilla.cart.service`)
- **Best Practices**:
  - Use descriptive names that reflect functionality (e.g., `processOrder` instead of `procOrd`).
  - Follow the single-responsibility principle for classes and methods.
  - Include JavaDoc for public APIs.
  - Enforce code quality with Checkstyle to maintain formatting and style consistency.
  - Use constants for magic numbers/strings.
  - Implement proper exception handling with logging.
- **Frontend**: For the Frontend repository, follow JavaScript/TypeScript conventions with ESLint for linting and Prettier for formatting.

## Architecture
Podzilla adopts a **microservices architecture** with **Domain-Driven Design (DDD)** and **Clean Architecture** principles. Each repository is structured into layers:
- **Models**: Represent domain entities (e.g., `Order`, `Product`).
- **Repositories**: Handle data persistence (e.g., JDBC for MySQL, MongoDB, or Redis).
- **Services**: Encapsulate business logic (e.g., `CartService`, `OrderService`).
- **Controllers**: Expose RESTful APIs (e.g., `/api/cart`, `/api/order`).
- **DTOs**: Decouple API contracts from domain models for flexible data exchange.

The **API-Gateway** routes requests to appropriate microservices, while **podzilla-utils-library** enables asynchronous communication via RabbitMQ events and queues. The **Infrastructure** repository uses Kubernetes for orchestration, ensuring scalability and resilience.

## Installation and Running
Each repository has its own setup instructions detailed in its README. Below is a general guide to set up the entire Podzilla ecosystem:

### Prerequisites
- Java 17
- Maven 3.8.6+
- Docker 24.0+
- Kubernetes (e.g., Minikube or a cloud provider like GKE, EKS)
- Node.js 18+ (for Frontend)
- MySQL 8.0+ or other databases as specified
- RabbitMQ 3.12+
- Git

### Setup
1. **Clone All Repositories**:
   ```bash
   git clone https://github.com/Podzilla/<repository>.git
   ```
   Replace `<repository>` with each repo name (e.g., `authentication`, `cart`, etc.).

2. **Install Podzilla-Utils-Library**:
   - Add the JitPack dependency to your `pom.xml` for microservices:
     ```xml
     <repositories>
         <repository>
             <id>jitpack.io</id>
             <url>https://jitpack.io</url>
         </repository>
     </repositories>
     <dependencies>
         <dependency>
             <groupId>com.github.Podzilla</groupId>
             <artifactId>podzilla-utils-library</artifactId>
             <version>main</version>
         </dependency>
     </dependencies>
     ```

3. **Configure Environment**:
   - Each repository includes a `.env.example` file. Copy it to `.env` and configure database, RabbitMQ, and other settings.

4. **Build and Run Microservices**:
   - For each microservice (e.g., Authentication, Cart):
     ```bash
     cd <repository>
     mvn clean install
     mvn spring-boot:run
     ```
   - Or use Docker:
     ```bash
     docker build -t podzilla-<repository> .
     docker run -p <port>:<port> --env-file .env podzilla-<repository>
     ```

5. **Deploy with Kubernetes**:
   - Navigate to the Infrastructure repository:
     ```bash
     cd infrastructure
     kubectl apply -f k8s/
     ```
   - Ensure Kubernetes is configured with appropriate secrets and environment variables.

6. **Run Frontend**:
   ```bash
   cd frontend
   npm install
   npm start
   ```
   The frontend will be available at `http://localhost:3000`.

7. **Access API Gateway**:
   - The API Gateway routes requests to microservices, typically at `http://localhost:8080`.

8. **Run Tests**:
   - For each microservice:
     ```bash
     cd <repository>
     mvn test
     ```
   - For Frontend:
     ```bash
     cd frontend
     npm test
     ```

## How to Contribute
We welcome contributions to any Podzilla repository! To contribute:
1. Fork the target repository.
2. Create a feature branch (`git checkout -b feature/your-feature`).
3. Make changes and ensure tests pass:
   - For microservices: `mvn test`
   - For Frontend: `npm test`
4. Run linting and code quality checks:
   - Microservices: `mvn checkstyle:check`
   - Frontend: `npm run lint`
5. Commit changes with a clear message (`git commit -m "Add your feature"`).
6. Push to your branch (`git push origin feature/your-feature`).
7. Open a pull request with a detailed description.
8. Ensure CI/CD pipelines pass.

Please adhere to the code style guidelines and include tests for new features or bug fixes.
