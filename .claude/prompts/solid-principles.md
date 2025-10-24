# SOLID Principles for Python

## Single Responsibility Principle (SRP)
A class should have only one reason to change.

**Example:**
```python
# Bad: Class handles both database operations and formatting
class UserManager:
    def save_user(self, user): ...
    def format_user_display(self, user): ...

# Good: Separate concerns
class UserRepository:
    def save(self, user): ...

class UserFormatter:
    def format_display(self, user): ...
```

## Open/Closed Principle (OCP)
Software entities should be open for extension but closed for modification.

**Example:**
```python
# Bad: Need to modify class to add new exporters
class MetricsExporter:
    def export(self, metrics, format):
        if format == 'json': ...
        elif format == 'prometheus': ...

# Good: Use abstraction for extension
class MetricsExporter(ABC):
    @abstractmethod
    def export(self, metrics): ...

class JsonExporter(MetricsExporter): ...
class PrometheusExporter(MetricsExporter): ...
```

## Liskov Substitution Principle (LSP)
Subtypes must be substitutable for their base types.

**Example:**
```python
# Bad: Subclass changes expected behavior
class ReadOnlyDatabase(Database):
    def write(self, data):
        raise NotImplementedError()  # Breaks LSP

# Good: Proper abstraction hierarchy
class Database(ABC):
    @abstractmethod
    def read(self, query): ...

class WritableDatabase(Database):
    @abstractmethod
    def write(self, data): ...
```

## Interface Segregation Principle (ISP)
Clients shouldn't depend on interfaces they don't use.

**Example:**
```python
# Bad: Fat interface
class DatabaseOperations(ABC):
    def read(self): ...
    def write(self): ...
    def backup(self): ...
    def replicate(self): ...

# Good: Focused interfaces
class Readable(ABC):
    def read(self): ...

class Writable(ABC):
    def write(self): ...

class Replicatable(ABC):
    def replicate(self): ...
```

## Dependency Inversion Principle (DIP)
Depend on abstractions, not concretions.

**Example:**
```python
# Bad: Depends on concrete implementation
class MetricsCollector:
    def __init__(self):
        self.db = PostgreSQLDatabase()  # Concrete dependency

# Good: Depends on abstraction
class MetricsCollector:
    def __init__(self, db: DatabaseInterface):
        self.db = db  # Abstract dependency
```

Apply these principles to create maintainable, flexible systems.
