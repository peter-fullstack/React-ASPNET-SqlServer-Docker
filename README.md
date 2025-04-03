## React - ASP.NET - Sql Sever - Docker Compose

https://www.youtube.com/watch?v=XTqwvQAv9Lg&t=40s

## Docker Compose

This solution demonstrates the use of docker compose to bring up 3 containers representing the key components of the application.

UI - this is implemented as a React App - see the Client folder in the Movies.Presentation project.

Web API - this implements operations for creating, updating and deleting Movices. This is implemented in the Movies.Presentation and the Application, Domain and Infrastructure projects.

Sql Servere - an instance of the database server is made available in a docker container




### Clean Architecture (popularized by Robert C. Martin) emphasizes:

### Separation of concerns

Independence from frameworks, UI, and databases

Testability

Business rules as the core

### Key Layers in Clean Architecture:

Domain Layer (Core business logic)

Application Layer (Use cases/application logic)

Infrastructure Layer (External concerns: DB, APIs, etc.)

Presentation Layer (UI/API)

Uses:
Mediator

CQRS 

Domain

Infrastucture


Testing

React App

Web API

Sql Server

Docker

Docker Compose
