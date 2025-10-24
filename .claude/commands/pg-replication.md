# PostgreSQL Logical Replication Setup

You are helping a Database Reliability Engineer create a Python CLI tool for setting up PostgreSQL logical replication.

## Context
- Follow TDD principles: write tests first
- Apply SOLID principles, especially Single Responsibility and Interface Segregation
- Use Pythonic idioms and follow the Zen of Python
- Ensure idempotent operations (safe to run multiple times)

## Requirements
- Create CLI using Click or Typer
- Implement configuration validation before applying changes
- Include comprehensive error handling with specific PostgreSQL error codes
- Log all operations with structured logging
- Support dry-run mode
- Generate rollback scripts
- Verify replication slots, publications, and subscriptions
- Monitor replication lag

## Testing Strategy
- Unit tests for each component
- Integration tests with testcontainers-python for PostgreSQL
- Mock external dependencies
- Test edge cases (connection failures, permission issues, conflicts)

Please implement following Clean Code principles and DRY. Structure code with clear separation of concerns using Domain Driven Design patterns.
