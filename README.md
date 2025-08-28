# Python Project Standards / Datum Brain

This repository contains the company-wide standard configuration files and project structure for Python projects at DatumBrain. These standards ensure consistency, maintainability, and quality across all Python projects.

## 📋 Overview

This template provides a standardized setup for Python projects including:

- **Code quality tools** (Ruff, Black, MyPy)
- **Testing framework** (Pytest with coverage)
- **Project structure** (src layout)
- **Configuration files** (pyproject.toml, .gitignore, .editorconfig)

## 🚀 Quick Start

### Using this Template

1. Clone this repository as a template for your new project:

   ```bash
   git clone https://github.com/datumbrain/python-template your-project-name
   cd your-project-name
   ```

2. Update project-specific details:

   - Rename `src/your_package_name` to your actual package name
   - Update package name references in `pyproject.toml`
   - Update author information and project metadata

3. Install Poetry (if not already installed):

   ```bash
   curl -sSL https://install.python-poetry.org | python3 -
   ```

4. Install dependencies:

   ```bash
   poetry install
   ```

5. Activate the virtual environment:
   ```bash
   poetry shell
   ```

## 📁 Project Structure

```
.
├── src/                    # Source code directory
│   └── your_package_name/  # Your main package
│       └── __init__.py     # Package initialization
├── tests/                  # Test directory
│   ├── __init__.py        # Test package initialization
│   └── conftest.py        # Pytest configuration and fixtures
├── .editorconfig          # Editor configuration for consistency
├── .gitignore             # Git ignore patterns
├── pyproject.toml         # Project configuration and dependencies
└── README.md              # Project documentation
```

### Directory Explanations

- **`src/`**: Contains all production code. Using src layout prevents accidentally importing from the repository root.
- **`tests/`**: Contains all test files. Tests should mirror the structure of the src directory.
- **`.editorconfig`**: Ensures consistent coding styles between different editors and IDEs.
- **`pyproject.toml`**: Central configuration file for the project, including dependencies, build system, and tool configurations.

## 🛠️ Configuration Files

### pyproject.toml

The `pyproject.toml` file is the central configuration hub containing:

- **Project metadata**: Name, version, description, authors
- **Dependencies**: Using Poetry for dependency management
- **Tool configurations**:
  - **Ruff**: Fast Python linter and formatter
  - **MyPy**: Static type checking
  - **Pytest**: Testing framework configuration
  - **Coverage**: Code coverage settings
  - **Black**: Code formatting (optional, alongside Ruff)

### .gitignore

Comprehensive gitignore file covering:

- Python artifacts (`__pycache__`, `*.pyc`, etc.)
- Virtual environments (`venv`, `.venv`, etc.)
- IDE files (`.idea`, `.vscode`)
- Test and coverage reports
- OS-specific files (`.DS_Store`, `Thumbs.db`)

### .editorconfig

Standardizes:

- Character encoding (UTF-8)
- Line endings (LF for Unix-style)
- Indentation (4 spaces for Python)
- Trailing whitespace handling
- File-specific settings for YAML, JSON, Markdown, etc.

## 🧰 Development Tools

### Code Quality

#### Ruff (Linting and Formatting)

```bash
# Run linter
poetry run ruff check .

# Fix auto-fixable issues
poetry run ruff check --fix .

# Format code
poetry run ruff format .
```

#### MyPy (Type Checking)

```bash
poetry run mypy src
```

#### Black (Alternative Formatter)

```bash
poetry run black src tests
```

### Testing

#### Run Tests

```bash
# Run all tests
poetry run pytest

# Run with coverage
poetry run pytest --cov

# Run specific test file
poetry run pytest tests/test_module.py

# Run tests in parallel
poetry run pytest -n auto
```

#### Test Markers

```bash
# Run only unit tests
poetry run pytest -m unit

# Skip slow tests
poetry run pytest -m "not slow"

# Run integration tests
poetry run pytest -m integration
```

### Pre-commit Hooks

Set up pre-commit hooks to automatically run checks before commits:

```bash
# Install pre-commit
poetry add --group dev pre-commit

# Create .pre-commit-config.yaml
cat > .pre-commit-config.yaml << EOF
repos:
  - repo: https://github.com/astral-sh/ruff-pre-commit
    rev: v0.1.0
    hooks:
      - id: ruff
        args: [--fix]
      - id: ruff-format
  - repo: https://github.com/pre-commit/mirrors-mypy
    rev: v1.5.0
    hooks:
      - id: mypy
        additional_dependencies: [types-all]
EOF

# Install the git hook scripts
poetry run pre-commit install

# Run against all files (first time)
poetry run pre-commit run --all-files
```

## 📏 Coding Standards

### Style Guide

- **Line Length**: 88 characters (Black/Ruff default)
- **Indentation**: 4 spaces
- **Quotes**: Double quotes for strings
- **Imports**: Sorted and grouped (via Ruff/isort)
- **Docstrings**: Google style convention

### Type Hints

All new code should include type hints:

```python
def calculate_total(items: list[float], tax_rate: float = 0.1) -> float:
    """Calculate total with tax.

    Args:
        items: List of item prices.
        tax_rate: Tax rate to apply.

    Returns:
        Total amount including tax.
    """
    subtotal = sum(items)
    return subtotal * (1 + tax_rate)
```

### Testing Standards

- Minimum 80% code coverage
- Tests organized in `tests/` mirroring `src/` structure
- Use pytest fixtures for reusable test data
- Descriptive test names: `test_<function>_<scenario>_<expected_outcome>`

## 🔄 Workflow

### Development Workflow

1. Create a feature branch:

   ```bash
   git checkout -b feature/your-feature-name
   ```

2. Make your changes in `src/`

3. Write/update tests in `tests/`

4. Run quality checks:

   ```bash
   poetry run ruff check .
   poetry run ruff format .
   poetry run mypy src
   poetry run pytest --cov
   ```

5. Commit your changes:

   ```bash
   git add .
   git commit -m "feat: add your feature description"
   ```

6. Push and create a pull request

### Commit Message Convention

Follow conventional commits:

- `feat:` New feature
- `fix:` Bug fix
- `docs:` Documentation changes
- `style:` Code style changes (formatting)
- `refactor:` Code refactoring
- `test:` Test changes
- `chore:` Build process or auxiliary tool changes

## 📦 Building and Publishing

### Building the Package

```bash
poetry build
```

This creates distribution files in the `dist/` directory.

### Publishing to PyPI

```bash
# Configure PyPI token
poetry config pypi-token.pypi your-token

# Publish
poetry publish
```

### Publishing to Private Repository

```bash
# Configure private repository
poetry config repositories.private https://your-repo-url
poetry config http-basic.private username password

# Publish
poetry publish -r private
```

## 🔍 Common Tasks

### Adding Dependencies

```bash
# Add production dependency
poetry add package-name

# Add development dependency
poetry add --group dev package-name

# Add specific version
poetry add package-name@^2.0.0
```

### Updating Dependencies

```bash
# Update all dependencies
poetry update

# Update specific package
poetry update package-name
```

### Virtual Environment

```bash
# Activate virtual environment
poetry shell

# Run command in virtual environment
poetry run python script.py

# Show environment info
poetry env info
```

## 📚 Resources

- [Poetry Documentation](https://python-poetry.org/docs/)
- [Ruff Documentation](https://docs.astral.sh/ruff/)
- [Pytest Documentation](https://docs.pytest.org/)
- [MyPy Documentation](https://mypy.readthedocs.io/)
- [PEP 8 Style Guide](https://pep8.org/)
- [Type Hints (PEP 484)](https://www.python.org/dev/peps/pep-0484/)

## 🤝 Contributing

When contributing to projects using this template:

1. Follow the established project structure
2. Ensure all tests pass
3. Maintain or improve code coverage
4. Follow the coding standards
5. Update documentation as needed

## 📄 License

This template is available for all DatumBrain projects. For specific project licenses, check the individual repository.

---

**Maintained by**: DatumBrain Engineering Team  
**Last Updated**: 2024
