# PostgreSQL Metrics Extraction

You are helping a Database Reliability Engineer create a Python tool for extracting PostgreSQL metrics.

## Context
- Performance-focused implementation
- TDD with performance benchmarks
- Clean Code principles
- Efficient querying without impacting database performance

## Requirements
- Extract metrics from pg_stat_* views
- Custom metric definitions via configuration
- Multiple export formats (Prometheus, JSON, CloudWatch)
- Connection pooling for efficiency
- Caching to reduce database load
- Configurable collection intervals

## Metrics Categories
- Connection statistics
- Query performance
- Replication lag
- Table and index statistics
- Lock information
- Vacuum and autovacuum stats
- Disk usage and growth trends

## Design
- Strategy Pattern for different metric exporters
- Adapter Pattern for various monitoring systems
- Decorator Pattern for metric transformations
- Singleton Pattern for connection pool

## Performance
- Batch queries when possible
- Async operations for concurrent collection
- Minimize database overhead
- Efficient data structures

Include comprehensive tests and proper resource cleanup.
