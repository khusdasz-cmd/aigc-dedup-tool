# Contributing to aigc-dedup-tool

Thank you for your interest in contributing to **aigc-dedup-tool** — an AIGC text
deduplication and paraphrasing engine for Chinese academic writing. We welcome
bug reports, feature suggestions, and code contributions.

---

## Table of Contents

- [How to Report a Bug](#how-to-report-a-bug)
- [How to Suggest a Feature](#how-to-suggest-a-feature)
- [How to Submit a Pull Request](#how-to-submit-a-pull-request)
- [Code Style](#code-style)
- [Development Setup](#development-setup)
- [License](#license)

---

## How to Report a Bug

If you find a bug, please open an issue on GitHub:

1. Go to the [Issues page](https://github.com/khusdasz-cmd/aigc-dedup-tool/issues).
2. Click **New Issue** and select the bug report template.
3. Include the following information:
   - A clear, descriptive title.
   - Steps to reproduce the bug (minimal reproduction is ideal).
   - Expected vs. actual behaviour.
   - Python version, OS, and any relevant environment details.
   - Full error output or logs, if applicable.

Before opening a new issue, please search existing (open and closed) issues to
avoid duplicates.

---

## How to Suggest a Feature

We are always open to ideas that make aigc-dedup-tool more useful. To suggest a
feature:

1. Go to the [Issues page](https://github.com/khusdasz-cmd/aigc-dedup-tool/issues).
2. Click **New Issue** and select the feature request template.
3. Describe:
   - The problem you are trying to solve (not just the solution you want).
   - How the feature would work or what it would look like.
   - Any alternatives you have considered.

Small, focused proposals are easier to discuss and implement. If the change is
substantial, consider starting a discussion before writing code.

---

## How to Submit a Pull Request

### 1. Fork and Clone

Fork the repository on GitHub, then clone your fork locally:

```bash
git clone https://github.com/<your-username>/aigc-dedup-tool.git
cd aigc-dedup-tool
```

### 2. Create a Branch

Create a feature branch from `main`:

```bash
git checkout -b feat/my-feature   # for new features
# or
git checkout -b fix/my-bugfix     # for bug fixes
```

Use a descriptive name. Branches should do **one thing**.

### 3. Make Your Changes

Write your code following the [Code Style](#code-style) guidelines. Keep
changes minimal — every line should be necessary for the fix or feature.

### 4. Test

Run the existing test suite and add tests for your changes:

```bash
pytest tests/
```

Ensure all tests pass before committing.

### 5. Commit

Write clear, conventional commit messages:

```
feat: add support for L0-level deduplication

Explain what the change does and why it is needed.
Keep the body wrapped at 72 characters.
```

Common prefixes: `feat`, `fix`, `refactor`, `docs`, `test`, `style`, `chore`.

### 6. Push and Open a Pull Request

Push your branch to your fork:

```bash
git push origin feat/my-feature
```

Then open a pull request against the `main` branch of the upstream repository.
In the PR description:

- Reference any related issues (e.g. "Closes #42").
- Summarise what the change does and why.
- Note any behavioural changes or breaking changes.
- Attach relevant test output if applicable.

### 7. Review

A maintainer will review your PR. Please respond to feedback and update your
branch if needed. Once approved, your PR will be merged.

**Before merging**, the reviewer will verify:

- [ ] All tests pass.
- [ ] New code has test coverage.
- [ ] The diff is minimal and focused.
- [ ] Code follows the project style.
- [ ] No `print` / debug statements remain (use logging).

---

## Code Style

### Python

- Follow **PEP 8** conventions.
- Use **4 spaces** for indentation (no tabs).
- Keep lines at **88 characters** max (compatible with Black).

### Type Hints

All public functions and methods **must** include type annotations:

```python
def deduplicate(texts: list[str], threshold: float = 0.85) -> list[str]:
    ...
```

### Tests

- Write tests using **pytest**.
- Place tests in the `tests/` directory, mirroring the package structure.
- Name test files and functions with a `test_` prefix.
- Aim for one test function per logical behaviour.

### Docstrings

Use **Google-style** docstrings for public modules, classes, and functions:

```python
def rewrite(text: str, level: int = 2) -> str:
    """Paraphrase the input text at the specified depth level.

    Args:
        text: The original Chinese text to rewrite.
        level: Deduplication depth (1 = light, 2 = moderate, 3 = deep).

    Returns:
        The rewritten text.

    Raises:
        ValueError: If level is not 1, 2, or 3.
    """
```

### Additional Guidelines

- Prefer readability over cleverness.
- Use `logging` instead of `print` for diagnostic output.
- Do not commit commented-out code or unused imports.
- Keep functions small and single-purpose.

---

## Development Setup

### Prerequisites

- Python 3.10 or later
- pip (or uv, for faster dependency management)

### Clone and Install

```bash
git clone https://github.com/khusdasz-cmd/aigc-dedup-tool.git
cd aigc-dedup-tool
```

Create a virtual environment and install the package in editable mode with
development dependencies:

```bash
python -m venv .venv
source .venv/bin/activate      # Linux / macOS
# .venv\Scripts\activate       # Windows

pip install -e ".[dev]"
```

### Run Tests

```bash
pytest tests/ -v
```

To run tests with coverage:

```bash
pytest tests/ --cov=aigc_dedup_tool --cov-report=term-missing
```

### Lint and Format

```bash
ruff check .
ruff format --check .
```

---

## License

By contributing, you agree that your contributions will be licensed under the
project's [MIT License](LICENSE).
