# Contribution guideline for Python Projects

> TL;DR: Use our [pre-commit](https://pre-commit.com/) configuration file

---

## Overall

In our projects we follow several rules, such as:

### PEP8

### Fully annotated code

_`mypy --strict` must pass_

### Fully documentated code

Every method and class must contain information, such as purpose and its behaviour.

### [Poetry project dependency management](https://python-poetry.org/)

_In poetry.toml include lines:_

```toml
[virtualenvs]
in-project = true
```

### pyproject.toml configuration file for linters and test frameworks

### [Pytest](https://docs.pytest.org) for code testing purposes

### [Loguru](https://loguru.readthedocs.io/) for logging purposes

### Max line length 120 lines

---

## Linters

### black

```bash
$ black src -l 120
```

## Static checkers

### mypy

```bash
$ mypy src --strict --exclude "test*, .venv" --ignore-missing-imports --allow-untyped-decorators --warn-incomplete-stub --implicit-reexport
```
