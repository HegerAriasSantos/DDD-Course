# Notes about DDD y CQRS

## Structure

```
|-- API
|   |-- Api
|   |   ├── Errors
|   |   |   ├── CodeErrorException.cs
|   |   |   ├── CodeErrorResponse.cs
|   |   |-- Middleware
|   |   |   ├── ErrorHandlingMiddleware.cs
|   |   |   ├── ErrorLoggingMiddleware.cs
|   |   ├── Controllers
|   |   |   ├── UsersController.cs
|   |   ├── Program.cs
|-- Core
|   ├── Application
|   |   ├── Behaviors
|   |   |   ├── UnhandledExceptionVehaviour.cs
|   |   |   ├── ValidationVehaviour.cs
|   |   ├── Contracts
|   |   |   ├── Persistence
|   |   |   |   ├── IUnitOfWork.cs
|   |   |   |   ├── IRepository.cs
|   |   |   ├── Services
|   |   |   |   ├── IUserService.cs
|   |   ├── Constants
|   |   |   ├── Constants.cs
|   |   ├── Exceptions
|   |   |   ├── NotFoundException.cs
|   |   |   ├── BadRequestException.cs
|   |   |   ├── ValidationException.cs
|   │   ├── Features
|   │   │   ├── Users
|   │   │   │   ├── Commands
|   │   │   │   │   ├── CreateUser
|   |   |   |   |   |   ├── CreateUserCommand.cs
|   |   |   |   |   |   ├── CreateUserCommandHandler.cs
|   |   |   |   |   |   ├── CreateUserCommandValidator.cs
|   │   │   │   │   ├── DeleteUser
|   |   |   |   |   |   ├── DeleteUserCommand.cs
|   |   |   |   |   |   ├── DeleteUserCommandHandler.cs
|   |   |   |   |   |   ├── DeleteUserCommandValidator.cs
|   │   │   │   │   ├── UpdateUser
|   |   |   |   |   |   ├── UpdateUserCommand.cs
|   |   |   |   |   |   ├── UpdateUserCommandHandler.cs
|   |   |   |   |   |   ├── UpdateUserCommandValidator.cs
|   │   │   │   ├── Queries
|   │   │   │   │   ├── GetUserById
|   |   |   |   |   |   ├── GetUserByIdQuery.cs
|   |   |   |   |   |   ├── GetUserByIdQueryHandler.cs
|   |   |   |   |   |   ├── GetUserByIdQueryValidator.cs
|   │   │   │   │   ├── GetUsers
|   |   |   |   |   |   ├── GetUsersQuery.cs
|   |   |   |   |   |   ├── GetUsersQueryHandler.cs
|   |   |   |   |   |   ├── GetUsersQueryValidator.cs
|   │   │   │   ├── UserDto.cs
|   |   |   |   ├── UserProfileMapping.cs
|   ├── Domain
|   |   ├── Entities
|   |   |   ├── Common
|   |   |   |   ├── BaseEntity.cs
|   |   |   ├── User.cs
|   |   ├── ValueObjects
|   |   |   ├── Common
|   |   |   |   ├── ValueObject.cs
|   |   |   ├── Email.cs
|   |   |   ├── Name.cs
|   |   |   ├── Password.cs
|   |   |   ├── Phone.cs
|   |   |   ├── Role.cs
|   |   |   ├── UserId.cs
├── Infrastructure
|   ├── Persistence
|   |   ├── Context
|   |   |   ├── ApplicationDbContext.cs
|   |   ├── Repositories
|   |   |   ├── Base
|   |   |   |   ├── BaseRepository.cs
|   |   |   ├── UserRepository.cs
|   |   ├── UnitOfWork
|   |   |   ├── UnitOfWork.cs
|   |   ├── Migrations
|   |   |   ├── 20210620123456_InitialCreate.cs
|   |   |   ├── 20210620123456_InitialCreate.Designer.cs
|   |   |   ├── ApplicationDbContextModelSnapshot.cs
|   |   |   ├── ApplicationDbContextModelSnapshot.Designer.cs
|   |   ├── Seed
|   |   |   ├── ApplicationDbContextSeed.cs
```

## Layers

- **API**: This layer is responsible for receiving requests from the client and returning responses. It is the entry point of the application.

  - **Api**: This layer contains the controllers of the application.

- **Core**: This layer contains the business logic of the application. It is divided into three sub-layers:

  - **Application**: This layer contains the application logic of the application. It is divided into three sub-layers:

    - **Behaviors**: This layer contains the behaviors that are applied to all requests. For example, validation, logging, etc.

    - **Contracts**: This layer contains the interfaces that define the contracts of the application. For example, repositories, services, etc.

    - **Features**: This layer contains the features of the application. Each feature is divided into three sub-layers:

      - **Commands**: This layer contains the commands that are used to perform actions. For example, create, update, delete, etc.

      - **Queries**: This layer contains the queries that are used to retrieve data. For example, get by id, get all, etc.

      - **MappingProfiles**: This layer contains the mapping profiles that are used to map entities to DTOs and vice versa.

  - **Domain**: This layer contains the domain logic of the application. It is divided into two sub-layers:

    - **Entities**: This layer contains the entities of the application. For example, user, role, etc.

    - **ValueObjects**: This layer contains the value objects of the application. For example, email, name, password, etc.

- **Infrastructure**: This layer contains the infrastructure logic of the application. It is divided into three sub-layers:

  - **Persistence**: This layer contains the persistence logic of the application. It is divided into three sub-layers:

    - **Context**: This layer contains the database context of the application.

    - **Repositories**: This layer contains the repositories of the application.

    - **UnitOfWork**: This layer contains the unit of work of the application.

  - **Migrations**: This layer contains the migrations of the application.

  - **Seed**: This layer contains the seed data of the application.

## Principles

- **Single Responsibility Principle (SRP)**: Each class should have only one reason to change.

- **Open/Closed Principle (OCP)**: Classes should be open for extension but closed for modification.

- **Liskov Substitution Principle (LSP)**: Objects of a superclass should be replaceable with objects of a subclass without affecting the correctness of the program.

- **Interface Segregation Principle (ISP)**: Clients should not be forced to depend on interfaces they do not use.

- **Dependency Inversion Principle (DIP)**: High-level modules should not depend on low-level modules. Both should depend on abstractions.

## Patterns

- **Repository Pattern**: This pattern is used to abstract the data access logic of the application.

- **Unit of Work Pattern**: This pattern is used to abstract the transaction logic of the application.

- **Mediator Pattern**: This pattern is used to decouple the request and the handler of the application.

- **Decorator Pattern**: This pattern is used to add behavior to an object dynamically.

- **Factory Pattern**: This pattern is used to create objects without specifying the exact class of object that will be created.

## Concepts

- **Domain-Driven Design (DDD)**: This is an approach to software development that focuses on the domain of the application.

- **Command-Query Responsibility Segregation (CQRS)**: This is an architectural pattern that separates the read and write operations of the application.

- **Clean Architecture**: This is an architectural pattern that separates the concerns of the application into layers.

- **SOLID Principles**: These are a set of principles that are used to design software that is easy to maintain and extend.

- **Separation of Concerns (SoC)**: This is a design principle that states that the concerns of the application should be separated into different layers.

- **Inversion of Control (IoC)**: This is a design principle that states that the control of the application should be inverted.

- **Dependency Injection (DI)**: This is a design pattern that is used to inject dependencies into a class.

- **Domain Events**: These are events that are raised by the domain of the application.

- **Value Objects**: These are objects that are immutable and represent a value.

- **Entities**: These are objects that have an identity and are mutable.

- **DTOs**: These are objects that are used to transfer data between layers.

- **Mapping Profiles**: These are objects that are used to map entities to DTOs and vice versa.

- **Behaviors**: These are objects that are used to apply behaviors to all requests.

- **Contracts**: These are interfaces that define the contracts of the application.

- **Features**: These are the features of the application.

- **Commands**: These are objects that are used to perform actions.

- **Queries**: These are objects that are used to retrieve data.

- **Repositories**: These are objects that are used to abstract the data access logic of the application.

- **Unit of Work**: This is an object that is used to abstract the transaction logic of the application.

- **Migrations**: These are objects that are used to manage the database schema.

- **Seed Data**: This is data that is used to populate the database.

## Libraries

- **Microsoft.EntityFrameworkCore.Tools**: This is a library that is used to implement the migrations of the application.

- **AutoMapper**: This is a library that is used to map entities to DTOs and vice versa.

- **AutoMapper.Extensions.Microsoft.DependencyInjection**: This is a library that is used to configure AutoMapper in the application.

- **FluentValidation**: This is a library that is used to validate the requests of the application.

- **FluentValidation.DependencyInjectionExtensions**: This is a library that is used to configure FluentValidation in the application.

- **MediatR.Extensions.Microsoft.DependencyInjection**: This is a library that is used to configure MediatR in the application.

- **Microsoft.Extensions.Logging.Abstractions**: This is a library that is used to implement the logging of the application.

- **Microsoft.EntityFrameworkCore.SqlServer**: This is a library that is used to implement the persistence logic of the application.
