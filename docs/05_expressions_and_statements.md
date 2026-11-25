# Expressions and statements

- [Python documentation – Expressions](https://docs.python.org/3/reference/expressions.html)
- [Python documentation – Simple statements](https://docs.python.org/3/reference/simple_stmts.html)
- [Python documentation – Compound statements](https://docs.python.org/3/reference/compound_stmts.html)

---

# Expressions

An expression is evaluated to produce a value (an object).

```python
10
10

2 + 3
5

abs(-5)
5

float('10.5')
10.5
```

Expressions can be used on the right-hand side of an assignment or as function arguments.

```python
area = 10 * 10

print(round(3.14159, 2))
3.14
```

---

# Statements

A statement is an instruction in a program. An assignment statement binds a name to a value.

```python
rows = 800

cols = 1000

pixels = rows * cols
```

| Code | Classification |
|---|---|
| `rows * cols` | Expression |
| `pixels = rows * cols` | Assignment statement |
| `pixels += 1` | Augmented assignment statement |
| `print(pixels)` | Function call expression used as a statement |

An assignment statement cannot be passed to a function as an expression.

---

# Return value and output

A function call is an expression even if the function returns `None`.

```python
result = print('Example')
Example

result is None
True
```

- `print()` produces visible output.
- Its return value is `None`.
