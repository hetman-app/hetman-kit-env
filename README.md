<img src="https://raw.githubusercontent.com/hetman-app/hetman-pipeline/main/docs/assets/full-white-text.webp" alt="Hetman Logo" width="200" height="38" />

**Hetman Kit Environment** is a developer-centric environment variable manager. It leverages the **Hetman Pipeline** engine to treat environment variables not just as strings, but as strictly validated and transformed data structures.

## Installation

```bash
pip install hetman-kit-env
```

## Why use this?

Standard `os.environ.get` returns strings and provides no validation. **Hetman Kit Environment** allows you to:

1. **Validate** length, patterns, and types immediately.
2. **Transform** values (lowercase, strip, cast) during retrieval.
3. **Parse** JSON structures stored in environment strings automatically.
4. **Enforce** existence for missing variables.

## Usage Example

```python
from hetman_kit_env import EnvironmentVariable
from pipeline import Condition, Match, Transform

# Set the path for your .env file
EnvironmentVariable.dotenv_path = ".env"

# Define a validated environment variable
# This will raise an exception if the key is missing or validation fails
SECRET_KEY = EnvironmentVariable[str](
    name="SECRET_KEY",
    type=str,
    conditions={
        Condition.ExactLength: 32
    },
    matches={
        Match.Text.Letters: None
    },
    transform={
        Transform.Lowercase: None
    }
)

# Access the processed value
print(SECRET_KEY.get)

```

## Core Features

-   **Strict Typing**: Use Python generics `EnvironmentVariable[T]` for better IDE support and type safety.
-   **JSON Ready**: Built-in `json.loads` support for complex environment configurations.
-   **Pipeline Integration**: Full access to the Pipeline execution flow (Type Check -> Setup -> Conditions -> Matches -> Transformations).
-   **Singleton .env Loading**: The `.env` file is loaded once and shared across all instances.

---

## Documentation

This package uses the **Hetman Pipeline** logic for its core processing. To learn more about available conditions, matches, and transformations, visit [Official Documentation](https://pipeline.hetman.app)
