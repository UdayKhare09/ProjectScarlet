We are creating a java microservice based application.
We are creating user authentication, authorization and management first we will use key cloak as authentication server.
We will use postgresql as database.

We will have all authentication methods like password, two factor(totp, email otp), passkeys, oauth2(google,github,etc).

We will keep both android and web clients in mind.

User will have roles, email(unique), UUID(Primary Key for all other tables)

We will use flyway as database migration tool.

We will use spring boot for microservice. 

We will use docker for containerization and docker compose for orchestration. and later kubernetes.