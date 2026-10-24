# Expense Reimbursement Backend with Spring Data JPA

A Spring Boot implementation of the reimbursement domain, organized around controllers, services, JPA entities, and repository interfaces.

## Problem and approach

Reimbursement requests pass through employee submission, administrator review, and final resolution. This project explores how to model that workflow with Spring-managed components and repository-based persistence rather than writing JDBC operations in every DAO.

## Architecture

| Layer | Location | Responsibility |
| --- | --- | --- |
| Application | [ExpenseReimbursementSpringApplication.java](src/main/java/com/expensereimbursementspring/ExpenseReimbursementSpringApplication.java) | Spring Boot entry point. |
| Controllers | [controller/](src/main/java/com/expensereimbursementspring/controller/) | Maps employee, administrator, pending-request, and resolution operations. |
| Services | [service/](src/main/java/com/expensereimbursementspring/service/) | Coordinates lookups, updates, request persistence, approval, and denial logic. |
| Persistence | [dao/](src/main/java/com/expensereimbursementspring/dao/), [entities/](src/main/java/com/expensereimbursementspring/entities/) | Spring Data repositories and database entity relationships. |
| Transfer objects | [pojo/](src/main/java/com/expensereimbursementspring/pojo/) | Objects exchanged between application layers. |

The final-expense service contains logic to create a resolved record from a pending request and remove that pending record. The approval method is annotated as transactional.

## Technologies

Java 11, Spring Boot 2.6.4, Spring Web, Spring Data JPA, PostgreSQL, Maven, JUnit, and Mockito.

## Local preparation

1. Configure PostgreSQL connection settings in `src/main/resources/application.properties` or the equivalent local Spring configuration.
2. Review the entity model and initialize suitable lab data. Hibernate's schema update setting is enabled in the checked-in configuration.
3. Adapt the controller CORS origins to the frontend environment.
4. Review controller response serialization, path-variable bindings, and final-expense service registration before attempting an end-to-end integration.

The configured application port is 4444. Once the local integration issues are addressed, the Spring Boot entry command is:

```bash
mvn spring-boot:run
```

## Portfolio focus and current scope

Framework-based dependency injection, entity/repository modeling, service separation, and transaction boundaries. The repository also contains JUnit/Mockito examples under `src/test/java/`; several assertions and request checks are unfinished. It is a learning implementation that still needs integration verification, not a claim of a deployed production service.
