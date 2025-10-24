# DRY Principle - Don't Repeat Yourself

Every piece of knowledge must have a single, unambiguous, authoritative representation within a system.

## Identifying Duplication

### Code Duplication
```python
# Bad: Repeated connection logic
def get_users():
    conn = psycopg2.connect(host='localhost', database='mydb')
    cursor = conn.cursor()
    cursor.execute("SELECT * FROM users")
    return cursor.fetchall()

def get_orders():
    conn = psycopg2.connect(host='localhost', database='mydb')
    cursor = conn.cursor()
    cursor.execute("SELECT * FROM orders")
    return cursor.fetchall()

# Good: Extract common logic
class DatabaseRepository:
    def __init__(self, connection_string: str):
        self.connection_string = connection_string

    def execute_query(self, query: str, params=None):
        with psycopg2.connect(self.connection_string) as conn:
            with conn.cursor() as cursor:
                cursor.execute(query, params)
                return cursor.fetchall()

class UserRepository(DatabaseRepository):
    def get_all(self):
        return self.execute_query("SELECT * FROM users")

class OrderRepository(DatabaseRepository):
    def get_all(self):
        return self.execute_query("SELECT * FROM orders")
```

### Configuration Duplication
```python
# Bad: Repeated configuration
class DevDatabase:
    host = 'localhost'
    port = 5432
    pool_size = 10
    timeout = 30

class TestDatabase:
    host = 'localhost'
    port = 5432
    pool_size = 5
    timeout = 30

# Good: Inherit common configuration
@dataclass
class BaseConfig:
    host: str = 'localhost'
    port: int = 5432
    timeout: int = 30

@dataclass
class DevConfig(BaseConfig):
    pool_size: int = 10

@dataclass
class TestConfig(BaseConfig):
    pool_size: int = 5
```

### Logic Duplication
```python
# Bad: Repeated validation logic
def create_user(username, email):
    if not username or len(username) < 3:
        raise ValueError("Invalid username")
    if not email or '@' not in email:
        raise ValueError("Invalid email")
    # Create user

def update_user(user_id, username, email):
    if not username or len(username) < 3:
        raise ValueError("Invalid username")
    if not email or '@' not in email:
        raise ValueError("Invalid email")
    # Update user

# Good: Extract validation
class UserValidator:
    @staticmethod
    def validate_username(username: str) -> None:
        if not username or len(username) < 3:
            raise ValueError("Invalid username")

    @staticmethod
    def validate_email(email: str) -> None:
        if not email or '@' not in email:
            raise ValueError("Invalid email")

    @classmethod
    def validate_user_data(cls, username: str, email: str) -> None:
        cls.validate_username(username)
        cls.validate_email(email)

def create_user(username, email):
    UserValidator.validate_user_data(username, email)
    # Create user

def update_user(user_id, username, email):
    UserValidator.validate_user_data(username, email)
    # Update user
```

## Techniques to Eliminate Duplication

### Extract Function
```python
# Bad
def process_metrics_json():
    metrics = fetch_metrics()
    metrics['timestamp'] = datetime.now().isoformat()
    metrics['host'] = socket.gethostname()
    return json.dumps(metrics)

def process_metrics_prometheus():
    metrics = fetch_metrics()
    metrics['timestamp'] = datetime.now().isoformat()
    metrics['host'] = socket.gethostname()
    return format_prometheus(metrics)

# Good
def enrich_metrics(metrics: dict) -> dict:
    metrics['timestamp'] = datetime.now().isoformat()
    metrics['host'] = socket.gethostname()
    return metrics

def process_metrics_json():
    metrics = enrich_metrics(fetch_metrics())
    return json.dumps(metrics)

def process_metrics_prometheus():
    metrics = enrich_metrics(fetch_metrics())
    return format_prometheus(metrics)
```

### Use Inheritance
```python
# Bad: Repeated setup/teardown
class UserTest:
    def setUp(self):
        self.conn = connect_db()
    def tearDown(self):
        self.conn.close()

class OrderTest:
    def setUp(self):
        self.conn = connect_db()
    def tearDown(self):
        self.conn.close()

# Good: Base test class
class DatabaseTest:
    def setUp(self):
        self.conn = connect_db()
    def tearDown(self):
        self.conn.close()

class UserTest(DatabaseTest):
    def test_user_creation(self):
        # Test logic

class OrderTest(DatabaseTest):
    def test_order_creation(self):
        # Test logic
```

### Use Composition
```python
# Good: Shared behavior through composition
class ConnectionManager:
    def __init__(self, connection_string: str):
        self.connection_string = connection_string

    def get_connection(self):
        return psycopg2.connect(self.connection_string)

class UserService:
    def __init__(self, conn_manager: ConnectionManager):
        self.conn_manager = conn_manager

class OrderService:
    def __init__(self, conn_manager: ConnectionManager):
        self.conn_manager = conn_manager
```

### Configuration as Code
```python
# Bad: Hardcoded SQL in multiple places
cursor.execute("SELECT * FROM users WHERE status = 'active'")
cursor.execute("SELECT * FROM users WHERE status = 'active'")

# Good: Single source of truth
class Queries:
    GET_ACTIVE_USERS = "SELECT * FROM users WHERE status = 'active'"
    GET_PENDING_ORDERS = "SELECT * FROM orders WHERE status = 'pending'"

cursor.execute(Queries.GET_ACTIVE_USERS)
```

### Template Pattern
```python
# Good: Common structure with customizable steps
class ETLJob(ABC):
    def run(self):
        self.validate()
        data = self.extract()
        transformed = self.transform(data)
        self.load(transformed)
        self.notify()

    def validate(self):
        # Common validation logic
        pass

    def notify(self):
        # Common notification logic
        pass

    @abstractmethod
    def extract(self): ...

    @abstractmethod
    def transform(self, data): ...

    @abstractmethod
    def load(self, data): ...
```

## When Duplication is Acceptable

1. **Different domains**: Similar code serving different bounded contexts
2. **Temporary duplication**: During refactoring, before patterns emerge
3. **Performance**: When abstraction adds unacceptable overhead
4. **Clear trade-offs**: When coupling is worse than duplication

Remember: DRY is about knowledge duplication, not just code duplication. Two similar code blocks might represent different concepts.
