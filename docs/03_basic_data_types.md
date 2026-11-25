# Basic data types

- [Python documentation – Built-in types](https://docs.python.org/3.10/library/stdtypes.html)
- [Python documentation – Numeric literals](https://docs.python.org/3.10/reference/lexical_analysis.html#numeric-literals)

---

# Types

| Type | Description | Example |
|---|---|---|
| `int` | Integer | `100` |
| `float` | Floating-point number | `10.5` |
| `bool` | Boolean value | `True`, `False` |
| `str` | String (text) | `'Sentinel-2'` |
| `NoneType` | Type of `None` (absence of a meaningful value) | `None` |

---

# Inspecting types

`type()` returns the type of an object.

```python
rows = 800

resolution = 10.0

valid = True

sensor = 'Sentinel-2'

result = None

type(rows)
<class 'int'>

type(resolution)
<class 'float'>

type(valid)
<class 'bool'>

type(sensor)
<class 'str'>

type(result)
<class 'NoneType'>
```

---

# Numeric literals

- Use `_` to group digits for readability.
- Use scientific notation for very small or large floating-point numbers.

```python
1_000_000
1000000

1e6
1000000.0

2.5e-3
0.0025
```

---

# Dynamic typing

- Objects have types.
- A variable name can refer to objects of different types.

```python
x = 10

type(x)
<class 'int'>

x = 10.5

type(x)
<class 'float'>
```
