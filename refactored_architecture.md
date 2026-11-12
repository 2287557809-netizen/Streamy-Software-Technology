# Streamy Refactored Architecture

## Dependency Inversion and Code Smell Resolution

### 1. Final Decoupled Class Diagram
This diagram illustrates the refactored architecture addressing the Data Clump code smell by introducing `CreateUserRequest`, and decoupling `UserController` from concrete services by introducing the `ICreateUserService` interface.

```mermaid
---
title: Final Decoupled Architecture
---
classDiagram
    class UserController {
        <<Class>>
        -ICreateUserService _createUserService
        +UserController(ICreateUserService createUserService)
        +Create(string email, string username) User
    }

    class CreateUserRequest {
        <<Class>>
        +string Email
        +string Username
        +Validate() bool
    }

    class ICreateUserService {
        <<Interface>>
        +Call(CreateUserRequest createUserRequest) User
    }

    class CreateUserService {
        <<Class>>
        -UserModel _userModel
        -SendWelcomeEmailService _sendWelcomeEmailService
        -Kafka _kafka
        +CreateUserService(UserModel um, SendWelcomeEmailService es, Kafka k)
        +Call(CreateUserRequest createUserRequest) User
        -CheckActiveUsers(List~User~ users) bool
    }

    class UserModel {
        <<Class>>
        +FindUsersByEmail(string email) List~User~
        +CreateUser(string email, string username) User
    }

    class User {
        <<Class>>
        +int UserId
        +string Username
        +string Email
    }

    class SendWelcomeEmailService {
        <<Class>>
        +Call(User user) bool
    }

    class Kafka {
        <<Class>>
        +PublishUserCreatedEvent(User user) bool
    }

    UserController ..> CreateUserRequest : depends on
    UserController ..> ICreateUserService : depends on
    CreateUserService ..|> ICreateUserService : implements

    CreateUserService ..> UserModel : depends on
    UserModel ..> User : depends on
    CreateUserService ..> SendWelcomeEmailService : depends on
    CreateUserService ..> Kafka : depends on