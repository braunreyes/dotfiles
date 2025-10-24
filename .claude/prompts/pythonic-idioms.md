# Pythonic Idioms for Database Engineering

## Context Managers
Always use context managers for resource management.

```python
# Good: Automatic resource cleanup
with psycopg2.connect(dsn) as conn:
    with conn.cursor() as cur:
        cur.execute("SELECT * FROM users")

# Also good: Custom context manager
from contextlib import contextmanager

@contextmanager
def database_transaction(conn):
    try:
        yield conn
        conn.commit()
    except Exception:
        conn.rollback()
        raise
```

## List Comprehensions
Use for transforming collections efficiently.

```python
# Good: Clear and efficient
active_users = [user for user in users if user.is_active]

# Good: Dictionary comprehension
user_map = {user.id: user.name for user in users}

# Good: Set comprehension for uniqueness
unique_dbs = {conn.database for conn in connections}
```

## Generators
Use for memory-efficient iteration.

```python
# Good: Don't load all rows into memory
def fetch_large_result(cursor):
    while True:
        rows = cursor.fetchmany(1000)
        if not rows:
            break
        for row in rows:
            yield row

# Usage
for row in fetch_large_result(cursor):
    process(row)
```

## Unpacking and Multiple Assignment
```python
# Good: Clean unpacking
host, port, database = connection_string.split(':')

# Good: Extended unpacking
first, *middle, last = query_results

# Good: Dictionary unpacking
config = {**default_config, **user_config}
```

## Type Hints
Always use type hints for clarity and tooling.

```python
from typing import List, Optional, Dict, Any

def get_user(user_id: int) -> Optional[Dict[str, Any]]:
    """Fetch user by ID."""
    ...

def batch_insert(records: List[Dict[str, Any]]) -> int:
    """Insert multiple records, return count."""
    ...
```

## Dataclasses
Use for data structures instead of dictionaries.

```python
from dataclasses import dataclass, field
from typing import List

@dataclass
class DatabaseConfig:
    host: str
    port: int = 5432
    database: str = "postgres"
    options: Dict[str, Any] = field(default_factory=dict)

    @property
    def connection_string(self) -> str:
        return f"postgresql://{self.host}:{self.port}/{self.database}"
```

## Property Decorators
Use for computed attributes and validation.

```python
class Database:
    def __init__(self, connection_string: str):
        self._connection_string = connection_string
        self._connection = None

    @property
    def connection(self):
        if self._connection is None:
            self._connection = self._create_connection()
        return self._connection

    @property
    def is_connected(self) -> bool:
        return self._connection is not None
```

## Enum for Constants
Use Enum instead of string constants.

```python
from enum import Enum

class ReplicationState(Enum):
    STREAMING = "streaming"
    CATCHUP = "catchup"
    STOPPED = "stopped"

# Usage
if state == ReplicationState.STREAMING:
    ...
```

## Pathlib for File Operations
Use pathlib instead of os.path.

```python
from pathlib import Path

# Good: Modern path handling
backup_dir = Path("/var/backups")
backup_file = backup_dir / f"backup_{date}.sql"

if backup_file.exists():
    size = backup_file.stat().st_size
```

## F-strings for Formatting
Use f-strings for string formatting (not for SQL!).

```python
# Good: Logging and messages
logger.info(f"Connected to {host}:{port} as {user}")

# Bad: Never use f-strings for SQL (SQL injection risk!)
# cursor.execute(f"SELECT * FROM {table}")  # DANGEROUS!

# Good: Use parameterized queries
cursor.execute("SELECT * FROM users WHERE id = %s", (user_id,))
```

## Walrus Operator (:=)
Use for assignment in expressions (Python 3.8+).

```python
# Good: Avoid calling function twice
if (result := fetch_data()) is not None:
    process(result)

# Good: In list comprehension with filtering
active = [user for u in users if (user := process(u)) and user.is_active]
```

## itertools for Advanced Iteration
```python
from itertools import islice, groupby, chain

# Good: Batch processing
def chunked(iterable, size):
    it = iter(iterable)
    while chunk := list(islice(it, size)):
        yield chunk

for batch in chunked(records, 1000):
    bulk_insert(batch)
```

## functools for Utilities
```python
from functools import lru_cache, wraps

# Good: Cache expensive calls
@lru_cache(maxsize=128)
def get_table_schema(table_name: str):
    return fetch_schema(table_name)

# Good: Preserve function metadata in decorators
def retry(max_attempts: int):
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            for attempt in range(max_attempts):
                try:
                    return func(*args, **kwargs)
                except Exception as e:
                    if attempt == max_attempts - 1:
                        raise
        return wrapper
    return decorator
```

Write idiomatic Python that leverages language features effectively.
