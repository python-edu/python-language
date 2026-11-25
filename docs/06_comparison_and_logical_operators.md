# Comparison and logical operators

- [Python documentation – Comparisons](https://docs.python.org/3/reference/expressions.html#comparisons)
- [Python documentation – Boolean operations](https://docs.python.org/3/reference/expressions.html#boolean-operations)
- [Python documentation – Truth value testing](https://docs.python.org/3/library/stdtypes.html#truth-value-testing)
- [Python documentation – Floating-point arithmetic](https://docs.python.org/3/tutorial/floatingpoint.html)

---

# Comparison operators

| Operator | Meaning |
|---|---|
| `==` | Equal to |
| `!=` | Not equal to |
| `<` | Less than |
| `<=` | Less than or equal to |
| `>` | Greater than |
| `>=` | Greater than or equal to |

Comparisons of basic scalar values return `True` or `False`.

```python
10 == 10.0
True

10 != 20
True

10 < 20
True

10 <= 10
True

10 > 20
False

10 >= 10
True
```

## Assignment vs comparison

- `=` assigns a value.
- `==` compares two values.

```python
resolution = 10

resolution == 10
True
```

---

# Logical operators

| Operator | Meaning (for Boolean operands) |
|---|---|
| `and` | Both operands are true |
| `or` | At least one operand is true |
| `not` | Reverses the truth value |

```python
True and False
False

True or False
True

not True
False
```

## Combining comparisons

```python
slope = 15

cloud_cover = 20

slope >= 10 and slope <= 30
True

cloud_cover < 10 or slope > 10
True

not (cloud_cover > 50)
True
```

## Operator precedence

Comparisons are evaluated before `not`, then `and`, then `or`.

- Use parentheses to group conditions when needed.

```python
True or False and False
True

(True or False) and False
False
```

## Chained comparisons

Use chained comparisons to test whether a value is within a range.

```python
slope >= 10 and slope <= 30
True

10 <= slope <= 30
True

10 < slope < 15
False
```

---

# Assigning values based on conditions

## Assigning Boolean values

Assign the result of a comparison or a logical expression directly to a variable.

```python
valid_slope = 0 <= slope <= 90

valid_slope
True

suitable = valid_slope and cloud_cover < 30

suitable
True

cloudy = cloud_cover > 50

cloudy
False
```

Conditional selection of a non-Boolean value is covered in [Conditional statements and expressions](16_conditions.md).

---

# Truth values

- Zero, an empty string and `None` are false in a Boolean context.
- Non-zero numbers and non-empty strings are true.
- `and` and `or` return one of their operands, not necessarily a Boolean value.
- `not` always returns a Boolean value.

```python
0 or 10
10

5 and 20
20

not 0
True

bool(5 and 20)
True
```

---

# Short-circuit evaluation

- `and` stops when the first operand is false.
- `or` stops when the first operand is true.
- The second operand is evaluated only if necessary.

```python
x = 0

x != 0 and 10 / x > 2
False

x == 0 or 10 / x > 2
True
```

Neither expression divides by zero. The second operand is skipped.

If the first operand does not determine the result, Python evaluates the second operand. These examples deliberately cause an error:

```python
True and (10 / 0 > 2)
Traceback (most recent call last):
    ...
ZeroDivisionError: division by zero

False or (10 / 0 > 2)
Traceback (most recent call last):
    ...
ZeroDivisionError: division by zero
```

---

# Identity and None

- Use `is` and `is not` to test object identity.
- Use `is None` and `is not None` to test for `None`.
- Use `==` for equality of values, not `is`.

```python
result = None

result is None
True

result is not None
False
```

---

# Floating-point comparisons

## The problem

- Some decimal numbers, such as `0.1` and `0.2`, cannot be represented exactly as binary floating-point numbers.
- Calculations with these numbers can produce small rounding errors.
- Two mathematically equal values may therefore compare as unequal.

```python
calculated = 0.1 + 0.2

expected = 0.3

calculated
0.30000000000000004

expected
0.3

calculated == expected
False
```

## Comparing with a tolerance

- Calculate the absolute difference between the same two values.
- Define a tolerance: the maximum acceptable absolute difference.
- Treat the values as equal for the purpose of the calculation if the difference is less than or equal to the tolerance.

```python
difference = abs(calculated - expected)

difference
5.551115123125783e-17

tolerance = 1e-12

difference <= tolerance
True
```

The difference is smaller than the tolerance (`0.000000000001`). The values are sufficiently close, although they are not exactly equal.

The same comparison in a single expression:

```python
abs(calculated - expected) <= tolerance
True
```

- Choose the tolerance according to the required accuracy of the calculation.
- `1e-12` is an example of an absolute tolerance, not a universal value.
