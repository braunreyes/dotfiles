# Gang of Four Design Patterns for Database Engineering

## Creational Patterns

### Factory Pattern
Create objects without specifying exact class.

**Use Case:** Creating different database connection types
```python
class DatabaseConnectionFactory:
    @staticmethod
    def create(db_type: str) -> DatabaseConnection:
        if db_type == 'postgresql':
            return PostgreSQLConnection()
        elif db_type == 'replica':
            return ReplicaConnection()
```

### Builder Pattern
Construct complex objects step by step.

**Use Case:** Building complex database configurations
```python
class DatabaseConfigBuilder:
    def __init__(self):
        self.config = {}

    def with_host(self, host):
        self.config['host'] = host
        return self

    def with_pool_size(self, size):
        self.config['pool_size'] = size
        return self

    def build(self) -> DatabaseConfig:
        return DatabaseConfig(self.config)
```

### Singleton Pattern
Ensure only one instance exists.

**Use Case:** Database connection pool
```python
class ConnectionPool:
    _instance = None

    def __new__(cls):
        if cls._instance is None:
            cls._instance = super().__new__(cls)
        return cls._instance
```

## Structural Patterns

### Adapter Pattern
Convert interface of a class to another interface.

**Use Case:** Adapting different metric exporters
```python
class PrometheusAdapter(MetricsExporter):
    def __init__(self, prometheus_client):
        self.client = prometheus_client

    def export(self, metrics):
        return self.client.push(self._convert(metrics))
```

### Decorator Pattern
Add behavior to objects dynamically.

**Use Case:** Adding logging/retry to database operations
```python
class RetryDecorator:
    def __init__(self, operation, max_retries=3):
        self.operation = operation
        self.max_retries = max_retries

    def execute(self):
        for attempt in range(self.max_retries):
            try:
                return self.operation.execute()
            except Exception:
                if attempt == self.max_retries - 1:
                    raise
```

### Repository Pattern
Abstraction layer between domain and data access.

**Use Case:** Database access abstraction
```python
class UserRepository(ABC):
    @abstractmethod
    def find_by_id(self, user_id: int) -> User: ...

    @abstractmethod
    def save(self, user: User) -> None: ...

class PostgreSQLUserRepository(UserRepository):
    def find_by_id(self, user_id: int) -> User:
        # PostgreSQL specific implementation
```

## Behavioral Patterns

### Strategy Pattern
Define family of algorithms, make them interchangeable.

**Use Case:** Different backup strategies
```python
class BackupStrategy(ABC):
    @abstractmethod
    def backup(self, database): ...

class FullBackupStrategy(BackupStrategy):
    def backup(self, database): ...

class IncrementalBackupStrategy(BackupStrategy):
    def backup(self, database): ...
```

### Observer Pattern
Define one-to-many dependency for notifications.

**Use Case:** Monitoring and alerting
```python
class MetricsCollector:
    def __init__(self):
        self.observers = []

    def attach(self, observer):
        self.observers.append(observer)

    def notify(self, metrics):
        for observer in self.observers:
            observer.update(metrics)
```

### Command Pattern
Encapsulate request as object.

**Use Case:** Database migrations with undo capability
```python
class Migration(ABC):
    @abstractmethod
    def execute(self): ...

    @abstractmethod
    def rollback(self): ...

class AddColumnMigration(Migration):
    def execute(self):
        # Add column logic

    def rollback(self):
        # Remove column logic
```

### Template Method Pattern
Define skeleton of algorithm, let subclasses override steps.

**Use Case:** ETL pipeline with customizable steps
```python
class ETLPipeline(ABC):
    def run(self):
        data = self.extract()
        transformed = self.transform(data)
        self.load(transformed)

    @abstractmethod
    def extract(self): ...

    @abstractmethod
    def transform(self, data): ...

    @abstractmethod
    def load(self, data): ...
```

### State Pattern
Allow object to alter behavior when state changes.

**Use Case:** Database connection states
```python
class ConnectionState(ABC):
    @abstractmethod
    def connect(self, context): ...
    @abstractmethod
    def disconnect(self, context): ...

class ConnectedState(ConnectionState):
    def connect(self, context):
        print("Already connected")

    def disconnect(self, context):
        # Disconnect logic
        context.state = DisconnectedState()
```

Choose patterns based on specific problems, not for their own sake.
