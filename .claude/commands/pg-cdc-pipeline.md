# PostgreSQL CDC Pipeline to S3

You are helping a Database Reliability Engineer create a Python tool for Change Data Capture (CDC) pipelines from PostgreSQL to S3.

## Context
- Follow TDD principles with integration tests
- Apply Domain Driven Design for data pipeline domain
- SOLID principles for extensible architecture
- Pythonic async/await for high throughput

## Requirements
- Capture changes using logical replication
- Transform data to analytics-friendly formats (Parquet, JSON)
- Partition data in S3 by date/time
- Handle schema evolution
- Exactly-once delivery semantics
- Configurable batch sizes and flush intervals
- Dead letter queue for failed records

## Features
- Initial snapshot + ongoing CDC
- Filtering and transformation rules
- Compression (gzip, snappy, zstd)
- S3 folder structure optimization
- Data quality validation
- Monitoring and alerting
- Graceful shutdown and state persistence

## Design Patterns
- Pipeline Pattern for data flow
- Chain of Responsibility for transformations
- Observer Pattern for monitoring
- State Pattern for pipeline lifecycle
- Repository Pattern for state storage

## Reliability
- Checkpointing and resume capability
- Retry logic with exponential backoff
- Circuit breaker for external services
- Health checks and readiness probes

Implement with type safety, comprehensive error handling, and observability.
