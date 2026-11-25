# Arithmetic operators

- [Python documentation – Arithmetic operations](https://docs.python.org/3.10/reference/expressions.html#binary-arithmetic-operations)
- [Python documentation – Operator precedence](https://docs.python.org/3.10/reference/expressions.html#operator-precedence)

---

# Operators

| Operator | Operation | Example | Result |
|---|---|---|---|
| `+` | Addition | `7 + 3` | `10` |
| `-` | Subtraction | `7 - 3` | `4` |
| `*` | Multiplication | `7 * 3` | `21` |
| `/` | Division | `7 / 2` | `3.5` |
| `//` | Floor division | `7 // 2` | `3` |
| `%` | Modulo (remainder) | `7 % 2` | `1` |
| `**` | Exponentiation | `2 ** 3` | `8` |

---

# Examples

```python
12 + 5
17

12 - 5
7

12 * 5
60

12 / 5
2.4

12 // 5
2

12 % 5
2

12 ** 2
144
```

- For `int` and `float` operands, `/` returns a floating-point number, even when the division is exact.
- `//` rounds the quotient down towards negative infinity. With integer operands, the result is an integer.
- `%` gives the remainder associated with floor division.

```python
12 / 3
4.0

-7 // 2
-4

-7 % 2
1
```

---

# Operator precedence

- Parentheses control the order of operations.
- Exponentiation precedes multiplication and division.
- Multiplication, division, floor division and modulo precede addition and subtraction.

```python
2 + 3 * 4
14

(2 + 3) * 4
20

2 * 3 ** 2
18

(-2) ** 2
4

-2 ** 2
-4
```
