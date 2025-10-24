# AI Agent Assisted Database Workflows

You are helping a Database Reliability Engineer build AI-powered agents for database operations.

## Context
- Follow Clean Code and SOLID principles
- TDD with mocked AI responses
- Pythonic async patterns
- Safety-first: AI assists but doesn't execute destructive operations without approval

## Requirements
- Natural language query to SQL generation
- Query optimization suggestions
- Anomaly detection in metrics
- Automated troubleshooting recommendations
- Interactive database exploration
- Schema design assistance

## Safety Mechanisms
- SQL query validation and dry-run
- Permission checks before execution
- Destructive operation approval flow
- Query cost estimation
- Audit logging of AI suggestions and actions

## AI Integration
- Use LangChain or similar framework
- Implement prompt templates for database tasks
- Context management (schema, statistics, history)
- Multi-step reasoning for complex tasks
- Retrieval-Augmented Generation (RAG) for documentation

## Design Patterns
- Strategy Pattern for different AI providers
- Chain of Responsibility for safety checks
- Template Method for agent workflows
- Observer Pattern for monitoring AI decisions

## Features
- Conversational interface for database operations
- Explain query plans in natural language
- Suggest indexes based on query patterns
- Generate test data
- Create documentation from schema

Implement with strong typing, comprehensive tests, and clear separation of AI logic from core database operations.
