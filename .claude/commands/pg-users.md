# PostgreSQL User and Role Management

You are helping a Database Reliability Engineer create a Python CLI tool for managing PostgreSQL users and roles.

## Context
- Security-first approach
- Follow least privilege principle
- TDD with comprehensive security test cases
- Apply Clean Code and SOLID principles

## Requirements
- Create, modify, and remove users/roles
- Manage role inheritance and memberships
- Grant/revoke privileges with precision
- Password rotation with secure generation
- Audit logging of all permission changes
- Configuration as code (YAML/JSON templates)
- Idempotent operations

## Security Considerations
- Never log passwords
- Use environment variables or secret managers for credentials
- Validate privilege escalation attempts
- Generate strong random passwords
- Support SCRAM-SHA-256 authentication
- Implement connection limits and timeouts

## Design
- Use Builder Pattern for role configuration
- Repository Pattern for database operations
- Value Objects for credentials and permissions
- Service Layer for business logic

Include comprehensive error handling and clear audit trails.
