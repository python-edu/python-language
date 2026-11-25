# Variables

- [Python documentation – Identifiers](https://docs.python.org/3.10/reference/lexical_analysis.html#identifiers)
- [Python documentation – Assignment statements](https://docs.python.org/3.10/reference/simple_stmts.html#assignment-statements)
- [PEP 8 – Naming conventions](https://peps.python.org/pep-0008/#naming-conventions)

---

# Naming requirements and conventions

- Requirements are defined by the Python language.
- Conventions are recommended coding practices.

| Rule | Good example | Bad example | Type |
|---|---|---|---|
| Start with a letter or an underscore | `band2`, `_band` | `2band` | [Requirement](https://docs.python.org/3.10/reference/lexical_analysis.html#identifiers) |
| Use letters, digits and underscores; no spaces or hyphens | `pixel_size` | `pixel size`, `pixel-size` | [Requirement](https://docs.python.org/3.10/reference/lexical_analysis.html#identifiers) |
| Do not use reserved keywords | `class_id` | `class` | [Requirement](https://docs.python.org/3.10/reference/lexical_analysis.html#keywords) |
| Match the case of the defined name | `rows = 800; rows` | `rows = 800; Rows` | [Requirement](https://docs.python.org/3.10/reference/lexical_analysis.html#identifiers) |
| Use only ASCII characters in names (`A-Z`, `a-z`, `0-9`, `_`) | `height`, `sigma` | `wysokość`, `σ` | [Convention](https://peps.python.org/pep-3131/#policy-specification) |
| Use `snake_case` for variables | `pixel_size` | `pixelSize`, `PixelSize` | [Convention](https://peps.python.org/pep-0008/#function-and-variable-names) |
| Use `UPPER_CASE` for constants | `BYTES_PER_MIB` | `bytes_per_mib` | [Convention](https://peps.python.org/pep-0008/#constants) |
| Avoid single-letter names `l`, `O` and `I` | `length` | `l` | [Convention](https://peps.python.org/pep-0008/#names-to-avoid) |

- Python allows non-ASCII identifiers, but use `ASCII-only` names in this course.
- The Python standard library uses ASCII-only identifiers (PEP 3131 policy).
- Use descriptive English names.
- Avoid names of built-in functions and types, such as `sum`, `round` and `int`.

---

# Assignment

General syntax: `name = expression`. Python evaluates the expression and binds the name to the resulting object.

- `=` assigns a value to a variable name.
- Define a variable before using it.

```python
rows = 800

cols = 1000

pixel_size = 10

rows * cols
800000

pixel_size ** 2
100
```

---

# Reassignment

```python
bands = 3

bands = 9

bands
9
```

---

# Augmented assignment

| Operator | Example | Equivalent for numbers |
|---|---|---|
| `+=` | `x += 2` | `x = x + 2` |
| `-=` | `x -= 2` | `x = x - 2` |
| `*=` | `x *= 2` | `x = x * 2` |
| `/=` | `x /= 2` | `x = x / 2` |
| `//=` | `x //= 2` | `x = x // 2` |
| `%=` | `x %= 2` | `x = x % 2` |
| `**=` | `x **= 2` | `x = x ** 2` |

```python
image_size = 800 * 1000 * 3 * 2

image_size
4800000

image_size /= 1024 ** 2

image_size
4.57763671875
```

---

# Constants

- Use `UPPER_CASE` for values intended to remain constant.
- Python does not enforce this convention.

```python
BYTES_PER_MIB = 1024 ** 2

4800000 / BYTES_PER_MIB
4.57763671875
```
