# PostgreSQL Extension Management

You are helping a Database Reliability Engineer create a Python CLI tool for managing PostgreSQL extensions.

## Context
- Follow TDD: write tests before implementation
- Apply DRY and SOLID principles
- Use Service-Oriented Design for extension management
- Pythonic code with type hints and dataclasses

## Requirements
- CLI for installing, upgrading, and removing extensions
- Handle extension dependencies automatically
- Version compatibility checking
- Support common extensions: pgvector, pg_cron, timescaledb, postgis
- Configuration templates for each extension
- Pre and post-installation hooks
- Validation before applying changes

## Design Patterns
- Strategy Pattern for different extension types
- Factory Pattern for extension handlers
- Repository Pattern for database interactions
- Command Pattern for rollback capability

## Safety
- Check extension compatibility with PostgreSQL version
- Backup relevant data before upgrades
- Atomic operations where possible
- Clear error messages with remediation steps

Please implement with comprehensive docstrings and type annotations.
