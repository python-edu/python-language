# Basic built-in functions

- [Python documentation – Built-in functions](https://docs.python.org/3.10/library/functions.html)
- [Python documentation – print()](https://docs.python.org/3.10/library/functions.html#print)

---

# Calling functions

- Built-in functions are available without importing modules.
- A function performs an operation and returns a result (possibly `None`).

## General syntax

```python
function_name(argument_1, argument_2, ...)
```

- `function_name` – name of the function.
- Arguments – values passed to the function, separated by commas.
- Depending on the function, a call may require no arguments, one argument or multiple arguments.

---

# Displaying values – print()

Use `print()` to display text, variable values and calculation results.

```python
resolution = 10

print('Resolution:', resolution, 'm')
Resolution: 10 m

print(10 * 20)
200
```

- `print()` converts its arguments to text for display.
- By default, arguments are separated by a space and each call ends with a newline (`\n`).
- `sep` changes the separator between arguments; `end` changes what is printed after the last argument.

```python
print('Red', 'Green', 'Blue', sep=', ')
Red, Green, Blue

print('Resolution:', resolution, end=' m\n')
Resolution: 10 m
```

- Use `end=''` to suppress the final newline. The next output then starts on the same line.
- `print()` displays values but returns `None`, not the displayed text.

```python
result = print('Red')
Red

result is None
True
```

---

# Converting values between data types

| Function | Operation | Example | Result |
|---|---|---|---|
| `int()` | Convert to integer | `int('10')` | `10` |
| `float()` | Convert to float | `float('10.5')` | `10.5` |
| `str()` | Convert to string | `str(10)` | `'10'` |
| `bool()` | Convert to Boolean | `bool(0)` | `False` |

```python
int(3.9)
3

int(-3.9)
-3

float(10)
10.0

bool(-5)
True

bool('')
False

bool('False')
True
```

- `int()` truncates a floating-point number towards zero.
- `bool()` returns `False` for zero, an empty string and `None`.
- A non-empty string is true, regardless of its text.

---

# Performing numeric calculations

| Function | Purpose |
|---|---|
| `abs()` | Calculate an absolute value |
| `round()` | Round a number |
| `pow()` | Raise a number to a power |
| `divmod()` | Calculate the floor quotient and remainder |

```python
abs(-2.5)
2.5

round(12.3456, 2)
12.35

round(12.3456)
12

pow(2, 3)
8

divmod(17, 5)
(3, 2)
```

`divmod()` returns the floor quotient and remainder together as a pair (a tuple; see [Tuples and unpacking](11_tuples_and_unpacking.md)).

`round()` rounds exact halfway cases to the nearest even value. Floating-point representation can affect rounding.

```python
round(2.5)
2

round(3.5)
4
```
