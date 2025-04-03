## React - ASP.NET - Sql Sever - Docker Compose

https://www.youtube.com/watch?v=XTqwvQAv9Lg&t=40s

## Overview
The functionality of this application is limited to a single entity - Movie. Movies can be listed, viewed, created, updated and deleted - basically full crud operations from the UI
to the database. It uses some standard and popular patterns in the way that it is designed - clean architecture principles and CQRS - which I've detailed in this project here - https://github.com/peter-fullstack/Clean-Architecture-CQRS-EF-Core

The focus of this solution is on the packing and runtime that Doker provides and how much this can simplify developer setup and deployments generally.

The full solution when running provions 3 docker containers:

 1. The front end React App browser client
 2. The back end C# web api endpoints  
 3. An instance of MS Sql Server

The docker runtime and commands handle building and then hosting the container instances and wiring up the communication between them with a bridging network.

<img src="https://github.com/peter-fullstack/React-ASPNET-SqlServer-Docker/blob/main/Images/dockerContainers.jpg" alt="App Screenshot" width="80%" style='padding:auto'>

The React App and Web Api each have their own Docker file that the docker-compose file references to build the 2 apps, package images and then run each of them in their
own container. The Sql Server instance uses an image from the Github repo.

When the full application is running you can each of see each the containers in Docker desktop - docker compose groups the 3 containes together and enables communication between them.

![Alt text](Images/dockerdesktop.jpg)

The names of the container instances correspond with the definitions in the docker-compose.yaml file.

## Docker Compose

This solution demonstrates the use of docker compose to bring up 3 containers representing the key components of the application as docker containes.

- UI - this is implemented as a React App - see the Client folder in the Movies.Presentation project.

- Web API - this implements operations for creating, updating and deleting Movices. This is implemented in the Movies.Presentation and the Application, Domain and Infrastructure projects.

- Sql Server - an instance of the database server is made available in a docker container

To run the full solution use a command prompt and navigate to the root folder of the solution - the one that containes the docker-compose.yml file - and issue the command:

docker docker-compose up

## Solution summary - from Github Copilot

This project implements a Clean Architecture design with CQRS (Command Query Responsibility Segregation) principles. It is structured into multiple layers, each with a clear separation of concerns. Here's a summary of the key components:

## Project Structure
### Domain Layer:

Contains core business logic and domain entities.
Dependency-free (no references to other layers or external libraries like EF Core or MediatR).
Encapsulates business rules and behaviors.

### Application Layer:

Implements CQRS using MediatR.
Contains commands, queries, and validators (e.g., CreateOrderCommand, CreateOrderValidator).
Focuses on application-specific business rules and orchestration.
Infrastructure Layer:

### Infrastructure Layer:

Handles persistence using Entity Framework Core.
Implements repositories and database-related logic.
Uses SQL Server as the database provider.

### Web Layer:

Provides a minimal API for endpoints.
Registers endpoints using clean, feature-based vertical slicing (e.g., MapOrdersEndpoints).
Configures middleware, dependency injection, and exception handling.
Test Projects:

Web.Tests:
Full integration tests using Testcontainers for SQL Server.
Tests cover end-to-end scenarios, including API endpoints, database interactions, and business logic.
Other test projects (e.g., Application.Tests, Infrastructure.Tests) focus on unit testing specific layers.
Key Features
CQRS:

Commands handle state changes (e.g., creating or updating orders).
Queries handle data retrieval without modifying state.
Clean Architecture Principles:

Clear separation of concerns between layers.
Dependency inversion: Higher-level layers depend on abstractions, not implementations.
Entity Framework Core:

Used for database interactions.
Migrations are applied programmatically during development and testing.
Integration Testing:

Uses WebApplicationFactory to spin up the API for testing.
Testcontainers.MsSql provides an isolated SQL Server instance for integration tests.
Minimal APIs:

Simplified endpoint registration and configuration.
Focus on clean and concise API design.
Code Review Highlights
WebApiTestBase:

Provides a base class for integration tests.
Sets up a Testcontainers SQL Server instance and overrides the production database configuration.
Uses WebApplicationFactory to create an HTTP client for testing API endpoints.
Error Handling:

Exception handling middleware is configured to handle validation errors and return structured error responses.
Dependency Injection:

Services like AppDbContext, MediatR, and validators are registered in the DI container.
Scoped services like AppDbContext are resolved correctly within test scopes.
Potential Improvements
Explicit Program Class:

The Program.cs file uses top-level statements. Explicitly defining a Program class improves compatibility with WebApplicationFactory.
Scoped DbContext in Tests:

Ensure AppDbContext is resolved within a valid scope in tests to avoid ObjectDisposedException.
Test Coverage:

Ensure both happy path and edge cases are covered in integration and unit tests.
