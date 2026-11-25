# Conditional statements and expressions

- [Python documentation – if statements](https://docs.python.org/3/tutorial/controlflow.html#if-statements)
- [Python documentation – Boolean operations](https://docs.python.org/3/reference/expressions.html#boolean-operations)
- [Python documentation – Conditional expressions](https://docs.python.org/3/reference/expressions.html#conditional-expressions)
- [Python documentation – match statements](https://docs.python.org/3/tutorial/controlflow.html#match-statements)

Conditional statements control which parts of a program are executed. Conditional expressions select a value based on a condition.

- A condition is an expression tested for truth.
- A condition may contain comparisons, logical operators or other expressions.
- Python uses the truth value of an expression; it does not have to be of type `bool`.
- See [Comparison and logical operators](06_comparison_and_logical_operators.md).

---

# Conditional statements

## General syntax

```python
if condition_1:
    statements_1
elif condition_2:
    statements_2
else:
    statements_3
```

- `condition_1`, `condition_2` – expressions tested for truth.
- `statements_1`, `statements_2`, `statements_3` – blocks of one or more statements.
- `if` is required; zero or more `elif` clauses and one optional `else` clause may follow.
- Each clause header ends with a colon (`:`). Its block must be indented.
- `if`, `elif` and `else` headers have the same indentation level.

## `if`

Execute a block of code only if a condition is true.

```python
cloud_cover = 15

if cloud_cover <= 20:
    print('Image accepted')
Image accepted
```

- The condition is followed by a colon (`:`).
- The statements belonging to the block must be indented.
- Use four spaces per indentation level (PEP 8 convention).
- If the condition is false, the block is skipped.
- Execution continues after the `if` statement.

## `if ... else`

Choose between two blocks of code.

```python
if cloud_cover <= 20:
    print('Image accepted')
else:
    print('Image rejected')
Image accepted
```

Exactly one block is executed. `else` has no condition.

## `if ... elif ... else`

Choose between several alternatives.

```python
ndvi = 0.65

if ndvi < 0:
    label = 'Negative'
elif ndvi < 0.2:
    label = 'Low'
elif ndvi < 0.5:
    label = 'Moderate'
else:
    label = 'High'

print(label)
High
```

- Conditions are tested from top to bottom.
- Only the first block with a true condition is executed.
- Any number of `elif` clauses may be used.
- `else` is optional. Without it, no block is executed if all conditions are false.
- The order of conditions matters. In this example, reaching the second condition already means that `ndvi >= 0`.
- The thresholds are illustrative, not universal NDVI classification rules.

## Testing empty collections

Empty collections are false in a Boolean context. Non-empty collections are true, regardless of the truth values of their individual items.

```python
files = []

if not files:
    print('No files to process')
No files to process
```

## Independent `if` statements vs `if ... elif`

Use separate `if` statements when several actions may be needed. Use `elif` when only one alternative should be selected.

```python
cloud_cover = 5

pixel_size = 10

if cloud_cover <= 10:
    print('Low cloud cover')
Low cloud cover

if pixel_size <= 10:
    print('High spatial resolution')
High spatial resolution
```

Both messages are printed. With `elif`, only the first message would be printed.

---

# Combining conditions

Use `and`, `or` and `not` to combine conditions in a single logical expression.

| Operator | Condition is true when |
|---|---|
| `and` | Both conditions are true |
| `or` | At least one condition is true |
| `not` | The condition is false |

## Multiple conditions with `and`

```python
cloud_cover = 15

pixel_size = 10

sensor = 'Sentinel-2'

if cloud_cover <= 20 and pixel_size <= 10 and sensor == 'Sentinel-2':
    print('Image accepted')
Image accepted
```

All three conditions must be true.

## Alternative conditions with `or`

```python
if sensor == 'Sentinel-2' or sensor == 'Landsat 9':
    print('Supported sensor')
Supported sensor
```

At least one comparison must be true. Write a complete comparison on each side of `or`.

```python
# Incorrect: the non-empty string is always truthy.
if sensor == 'Sentinel-2' or 'Landsat 9':
    print('Supported sensor')
Supported sensor
```

## Membership as a condition

Use `in` to test whether a value belongs to a collection. This is often simpler than several equality comparisons joined by `or`.

```python
supported_sensors = ['Sentinel-2', 'Landsat 9']

if sensor in supported_sensors:
    print('Supported sensor')
Supported sensor
```

## Negation with `not`

```python
is_cloudy = False

if not is_cloudy:
    print('Clear image')
Clear image
```

## Combining different logical operators

```python
if (sensor == 'Sentinel-2' or sensor == 'Landsat 9') and cloud_cover <= 20:
    print('Image accepted')
Image accepted
```

- Comparisons are evaluated before `not`, then `and`, then `or` (operator precedence).
- Parentheses group conditions and make the intended logic explicit.
- Parentheses also allow long conditions to be split across multiple lines.

```python
if (
    (sensor == 'Sentinel-2' or sensor == 'Landsat 9')
    and cloud_cover <= 20
    and pixel_size <= 10
):
    print('Image accepted')
Image accepted
```

## Testing a range of values

Use chained comparisons for intervals.

```python
ndvi = 0.65

if ndvi >= -1 and ndvi <= 1:
    print('Valid NDVI')
Valid NDVI

# Equivalent for these simple comparisons:
if -1 <= ndvi <= 1:
    print('Valid NDVI')
Valid NDVI
```

## Short-circuit evaluation

This rule was introduced in [Comparison and logical operators](06_comparison_and_logical_operators.md). The following examples show both possible outcomes.

Python evaluates the operands of `and` and `or` from left to right. It skips the second operand when the first is sufficient to determine the truth of the whole expression.

| Operator | First operand | Second operand |
|---|---|---|
| `and` | False (falsy) | Skipped |
| `and` | True (truthy) | Evaluated |
| `or` | True (truthy) | Skipped |
| `or` | False (falsy) | Evaluated |

### `and`

The second expression contains a division by zero. If it is evaluated, an error occurs.

```python
False and (10 / 0 > 2)
False

True and (10 / 0 > 2)
Traceback (most recent call last):
    ...
ZeroDivisionError: division by zero
```

- In the first example, the result is already false. The division is skipped.
- In the second example, Python must evaluate the division to determine the result.

### `or`

The same division is used to demonstrate the opposite rule.

```python
True or (10 / 0 > 2)
True

False or (10 / 0 > 2)
Traceback (most recent call last):
    ...
ZeroDivisionError: division by zero
```

- In the first example, the result is already true. The division is skipped.
- In the second example, Python must evaluate the division to determine the result.

### Practical use

Use the first condition to check whether the second can be evaluated safely.

```python
correct = 90

total = 0

if total > 0 and correct / total >= 0.9:
    print('Required accuracy reached')

if total == 0 or correct / total < 0.9:
    print('Accuracy unavailable or below threshold')
Accuracy unavailable or below threshold
```

- `and`: `total > 0` is false, so the division and the first block are skipped.
- `or`: `total == 0` is true, so the division is skipped and the second block is executed.
- Reversing the operands in either condition would cause a division-by-zero error.

---

# Nested conditional statements

An `if` statement may contain another `if` statement. Use nesting when the second decision is relevant only after the first condition is satisfied, especially when the inner decision has its own alternatives.

```python
if cloud_cover <= 20:
    if pixel_size <= 10:
        print('Accepted for detailed analysis')
    else:
        print('Accepted for general analysis')
else:
    print('Image rejected')
Accepted for detailed analysis
```

If the only action requires both conditions, prefer a single `if` with `and`.

```python
if cloud_cover <= 20:
    if pixel_size <= 10:
        print('Accepted for detailed analysis')
Accepted for detailed analysis

# Simpler equivalent:
if cloud_cover <= 20 and pixel_size <= 10:
    print('Accepted for detailed analysis')
Accepted for detailed analysis
```

---

# Conditional expression

A conditional expression (also called a ternary expression) selects one of two values. Unlike an `if` statement, it produces a value and can be used inside another expression.

## General syntax

```python
value_if_true if condition else value_if_false
```

- The condition is evaluated first.
- Only the selected value expression is evaluated.
- Both alternatives are required; `else` cannot be omitted.

## Conditional assignment

Use a conditional expression when the purpose is to calculate or select a single value.

```python
cloud_cover = 15

if cloud_cover <= 20:
    status = 'accepted'
else:
    status = 'rejected'
```

The same assignment can be written more concisely:

```python
status = 'accepted' if cloud_cover <= 20 else 'rejected'
```

## Inside another expression

A conditional expression can be used directly as a function argument or as part of a calculation.

```python
print('Accepted' if cloud_cover <= 20 else 'Rejected')
Accepted
```

Select a value only when it can be calculated safely:

```python
correct = 90

total = 100

oa = correct / total if total > 0 else None
```

If `total` is zero, the result is `None`; the division is skipped.

## When to use a conditional expression

| Situation | Preferred form |
|---|---|
| Select one of two values | Conditional expression |
| Use a selected value inside a larger expression | Conditional expression |
| Execute an action only when a condition is true | `if` |
| Execute several statements in a branch | `if ... else` |
| Choose among several alternatives | `if ... elif ... else` |
| Complex conditions or calculations that are hard to read on one line | `if ... else` |

Use a statement when the branches perform different actions, rather than merely select a value.

```python
if cloud_cover <= 20:
    status = 'accepted'
    print('Image accepted')
else:
    status = 'rejected'
    print('Find another image')
Image accepted
```

## Choosing a value vs performing an action

Prefer a conditional expression when selecting a value to use, for example an argument to `print()`.

```python
print('Accepted' if cloud_cover <= 20 else 'Rejected')
Accepted
```

The following is valid Python, but it selects which call to execute rather than a useful return value. Both calls return `None`; the purpose is to display text (a side effect).

```python
print('Accepted') if cloud_cover <= 20 else print('Rejected')
Accepted
```

For selecting actions, prefer an `if` statement.

```python
if cloud_cover <= 20:
    print('Accepted')
else:
    print('Rejected')
Accepted
```

For several alternatives, a nested conditional expression may be difficult to read.

```python
label = 'Low' if ndvi < 0.2 else 'Medium' if ndvi < 0.5 else 'High'
```

Prefer `if ... elif ... else` when it makes the logic clearer.

```python
if ndvi < 0.2:
    label = 'Low'
elif ndvi < 0.5:
    label = 'Medium'
else:
    label = 'High'
```

---

# `match ... case` (Python 3.10+)

The `match` statement tests a value (the subject) against patterns. This is called structural pattern matching. Here we use only simple patterns, such as literal numbers and strings.

- Use `match` to select an action based on specific values.
- Use `if` for general conditions, numerical thresholds and ranges.

## General syntax

```python
match subject:
    case pattern_1:
        statements_1
    case pattern_2:
        statements_2
    case _:
        default_statements
```

- `subject` – an expression whose value is tested.
- `pattern_1`, `pattern_2` – patterns to match against the subject (e.g. literal values).
- `statements_1`, `statements_2` – blocks executed for matching patterns.
- One or more `case` clauses are required. The default case (`case _`) is optional and, if used in this form, must be last.
- The subject is evaluated once. Patterns are tested from top to bottom; only the first matching block is executed.
- No `break` is needed between cases.

## Matching literal values

```python
sensor = 'Sentinel-2'

match sensor:
    case 'Sentinel-2':
        print('Optical sensor')
    case 'Sentinel-1':
        print('Radar sensor')
    case _:
        print('Unknown sensor')
Optical sensor
```

`_` is a wildcard pattern: it matches any value. As the last case, it is executed only if none of the previous cases matches. It works like the final `else` in an `if ... elif ... else` statement. Without it, no block is executed if no pattern matches.

## Alternative patterns (`|`)

Use `|` to match one of several alternative values. It means "or" in a pattern.

```python
match sensor:
    case 'Sentinel-2' | 'Landsat 9':
        print('Optical sensor')
    case 'Sentinel-1':
        print('Radar sensor')
    case _:
        print('Unknown sensor')
Optical sensor
```

For literal values, the first case is equivalent to testing:

```python
if sensor == 'Sentinel-2' or sensor == 'Landsat 9':
    print('Optical sensor')
Optical sensor
```

- `|` is an OR pattern here, not the bitwise OR operator.
- Do not use `and` or `or` to combine patterns after `case`. They combine logical expressions, not patterns.
- For conditions combining comparisons with `and`, `or` or `not`, prefer `if`.
