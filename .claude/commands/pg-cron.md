# PostgreSQL pg_cron Job Management

You are helping a Database Reliability Engineer create a Python CLI tool for managing pg_cron jobs.

## Context
- Follow TDD methodology
- Pythonic code with proper error handling
- Apply Domain Driven Design for job management domain
- SOLID principles for maintainable code

## Requirements
- CLI for creating, updating, and removing pg_cron jobs
- Job templates for common tasks (vacuuming, archiving, maintenance)
- Schedule validation (cron expression syntax)
- Job monitoring and failure alerting
- Job history and execution logs
- Dry-run mode to test jobs before scheduling

## Features
- Parse and validate cron expressions
- Job dependency management
- Retry logic for failed jobs
- Notification integration (email, Slack, PagerDuty)
- Job versioning and rollback
- Resource usage tracking

## Design Patterns
- Command Pattern for job execution
- Observer Pattern for monitoring and alerts
- Template Method for job types
- State Pattern for job lifecycle management

Implement with type hints, docstrings, and comprehensive logging.
