# Project Requirements: `crypto-analysis-mcp`

## Goal

Reimplement [kukapay/crypto-indicators-mcp](https://github.com/kukapay/crypto-indicators-mcp) using:

- **Python**
- **httpx** for HTTP communication
- **[mcp](https://pypi.org/project/mcp/)** for Model Context Protocol
- **[uv](https://docs.astral.sh/uv/)** for dependency and project management

---

## Development Principles

Apply the following principles:

- **Clean Architecture** — well-defined separation of concerns
- **OOP** — object-oriented design
- **SOLID** — maintainable and extendable components
- **KISS** — keep implementations simple and focused
- **DRY** — avoid code duplication

> ⚠ Avoid overengineering. Implement only what's necessary for functionality.

---

## Project Structure

Structure the project according to Clean Architecture:

crypto_analysis_mcp/ 
│ 
├── app/ # Core application logic 
│   ├── domain/ # Entities and pure business rules 
│   ├── use_cases/ # Application services and orchestrators 
│   ├── interfaces/ # Interface definitions (ports) 
│   ├── infrastructure/ # Adapters (e.g. API clients using httpx) 
│   └── main.py # Entry point 
│ 
├── tests/ # All test layers 
│   ├── unit/ # Unit tests (domain, use_cases) 
│   ├── integration/ # Integration tests (adapters, infrastructure) 
│   └── e2e/ # End-to-end tests (workflow validation) 
│ 
├── pyproject.toml # Project config, managed by uv 
├── README.md 
└── .env # Optional config/secrets

---

## Development Workflow for AI Agent

1. **Initialize project with `uv`**:
   - Create `pyproject.toml`
   - Add and install base dependencies:
     - `httpx`, `mcp`, `pydantic`, `python-dotenv`
     - Dev tools: `pytest`, `pytest-cov`, `pytest-asyncio`, `ruff`, `mypy`

2. **Feature implementation loop**:
   - Pick a functionality from the original repo
   - Split it into `use_case`, `domain`, and `interface/infrastructure`
   - Implement code and **corresponding tests**
   - Run all tests (unit/integration/e2e) before proceeding to next step

3. **Code coverage goal**:
   - ≥ 90% test coverage
   - Measured via `pytest-cov`
   - Classify tests:
     - Unit: domain logic, pure use cases
     - Integration: real API client use, service calls
     - E2E: full workflows from `main.py`

---

## AI Agent Checkpoints Before Each Step

- Is this the **minimal complete unit** of functionality?
- Are **inputs and outputs clearly defined**?
- Will this step include **sufficient test coverage**?
- Are **dependencies organized correctly** by layer?
- Are we **avoiding over-abstraction or premature optimization**?

---

## Example `pyproject.toml`

```toml
[project]
name = "crypto-analysis-mcp"
version = "0.1.0"
description = "Crypto indicator analysis using MCP protocol"
dependencies = [
    "httpx",
    "mcp",
    "pydantic",
    "python-dotenv"
]

[project.optional-dependencies]
dev = [
    "pytest",
    "pytest-cov",
    "pytest-asyncio",
    "ruff",
    "mypy"
]

---

## Testing Philosophy

Test as you go: no feature without a test

**Write tests for:
- Expected behavior
- Edge cases
- Failures**

Include mocks or stubs only where integration is not feasible

Keep test output clean and actionable