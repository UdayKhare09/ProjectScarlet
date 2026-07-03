# ProjectScarlet Architectural & Development Guidelines

This document outlines the core architecture and development guidelines for ProjectScarlet.

## 1. Authentication & Identity Management
- **Flow**: Use OAuth2 Authorization Code Flow with PKCE, proxied through `scarlet-gateway`.
- **User Sync**: Just-In-Time (JIT) synchronization. When a valid JWT is verified, if the user UUID does not exist in the `scarlet-user` database, dynamically register and create the user profile record.
- **Social Login / IDP**: Configured with dev placeholders. Merge account or add login method if the email already exists.
- **Multi-Factor Authentication (MFA) & Passkeys**:
  - Optional MFA (TOTP, Email OTP).
  - If a user authenticates via Social IDP or Passkeys, bypass 2FA.
  - If a user authenticates via Email + Password, require 2FA (TOTP or Email OTP) only if it is enabled for that user.
  - Registration is restricted to Social IDP or Email + Password.

## 2. Inter-Service Communication
- **Synchronous Communication**: Use **gRPC** for efficient, typed, sync inter-service calls.
- **Asynchronous Communication**: Use **RabbitMQ** for event-driven message exchange.
- **Distributed Transactions**: Use the **Choreography SAGA Pattern** over RabbitMQ for transactional workflows across microservices.

## 3. Tech Stack Standards
- **Backend**: Spring Boot 3.5.x, Java 17+, Spring Cloud Gateway.
- **Database**: PostgreSQL with UUID as primary keys.
- **Database Migrations**: Flyway.
- **Containerization**: Docker & Docker Compose.
