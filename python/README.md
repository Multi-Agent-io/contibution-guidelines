> This is a work-in-progress page, feel free to ask questions, submit feedback and additions via PR and issues for
> this repository.

# Contribution guidelines for Python Projects

> TL;DR: Use our [pre-commit](https://pre-commit.com/) configuration file

---

## Overall

In our projects we follow several rules, such as:

- **Full PEP8 compliance**. In our projects we write fully PEP8 compliant code, following not only the formatting rules
  and recommendations, listed in PEP8, but also the Black code style extending the provided rules.

- **Pythonic code**. All code we write must follow the Python philosophy, including, but not limited to explicit style,
  minimalistic approach, extended usage of built-in Python features such as generators, decorators, etc.

- **Fully annotated code**. All our code features thorough type annotations for the return values of the functions and
  methods, for all the class attributes and all the variables, if they accept a return of a function, which type might
  not be obvious.

- As a good rule of thumb, we make use of the best static analyzers. The minimal toolkit is Mypy, Flake8 and Black. Mypy
  check must pass with the `--strict` option. This ensures the code is well annotated, well formatted, PEP8 compliant
  and does not contain any obvious bugs and syntax errors.

- **Private/protected fields and methods**. We discourage use double underlines (also called "dunder") as it impacts readability and testability, and isn’t really private. Prefer a single underscore instead.

<table>
  <thead>
    <tr>
      <th>Bad practice</th>
      <th>Good practice</th>
    </tr>
  </thead>
<tbody>
<tr>
  <td>

  ```python
  class SomeClass:
    def __init__(self) -> None:
      self.__a == 1

    def __some_method(self) -> None:
      print('Hello')

  # You have access to 'dunder' methods/field like this:

  >>> SomeClass()._SomeClass__a
  >>> 1

  >>> SomeClass()._SomeClass__some_method()
  >>> 'Hello'
  ```

  </td>
  <td>

  ```python
  class SomeClass:
    def __init__(self) -> None:
      self._a == 1

    def _some_method(self) -> None:
      print('Hello')

  # You still able to access those methods/field, but it's much readable:

  >>> SomeClass()._a
  >>> 1

  >>> SomeClass()._some_method()
  >>> 'Hello'
  ```

  </td>
</tr>
</tbody>
</table>

### Fully documented code

Every method and class must contain information, such as its purpose and behaviour. The ultimate goal is to write
self-documenting code, the one that does not need any comments to understand. This can be achieved through good naming
and explicit code style. Refer to "Refactoring" and "Clean code" books or their summaries for more information.

### Project dependency management

We recommend using [Poetry](<(https://python-poetry.org/)>) as your default dependency management system. It is also
useful for package builders as it automatically generates a `pyproject.toml` file for your project, containing all the
relevant information about your package and allowing for easy wheel generation.

### Logging

We recommend to use [Loguru](https://loguru.readthedocs.io/) for logging purposes.

### Testing

We recommend to use [Pytest](https://docs.pytest.org) for code testing purposes.

## Common settings

These are the settings you might find useful for your CLI tools.

_In poetry.toml include lines:_

```toml
[virtualenvs]
in-project = true
```

A good practice will be to put your static checker's and linter's configuration in `pyproject.toml`. These packages
should also be included as development dependencies.

> We recommend setting your max line length to 120 characters.

---

### Formatters

- black

```bash
$ black src -l 120
```

### Static checkers

- mypy

```bash
$ mypy src --strict --exclude "test*, .venv" --ignore-missing-imports --allow-untyped-decorators --warn-incomplete-stub --implicit-reexport
```
