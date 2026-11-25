# String formatting

- [Python tutorial – Fancier output formatting](https://docs.python.org/3.10/tutorial/inputoutput.html#fancier-output-formatting)
- [Python documentation – Format specification mini-language](https://docs.python.org/3.10/library/string.html#format-specification-mini-language)
- [Python documentation – Format string syntax](https://docs.python.org/3.10/library/string.html#format-string-syntax)
- [Python documentation – Built-in format()](https://docs.python.org/3.10/library/functions.html#format)
- [Python documentation – printf-style string formatting](https://docs.python.org/3.10/library/stdtypes.html#printf-style-string-formatting)

---

# What is string formatting?

String formatting is the process of representing values as text in a specified form, often as part of a larger string.

- **String interpolation** – inserting values into text.
- **Format specification** – controlling how a value is represented, e.g. decimal places, width or alignment.
- Formatting produces a string; it does not change the original value or its type.

```python
accuracy = 0.94638

str(accuracy)
'0.94638'

format(accuracy, '.2f')
'0.95'

format(accuracy, '.2%')
'94.64%'

accuracy
0.94638
```

---

# Formatting methods

| Method or approach | Usage | Mini-language |
|---|---|---|
| [F-strings](#f-strings-formatted-string-literals) | Common; preferred for new code | Yes |
| [str.format()](#strformat) | Common; useful for reusable templates | Yes |
| [format()](#format) | Less common; useful for single values | Yes |
| [% operator](#percent-operator) | Older style; still common in existing code and logging | No |
| [string.Template](#stringtemplate) | Less common; simple substitution | No |
| [Manual formatting](#manual-formatting) | Common for simple operations | No |

- Focus on the first three methods: f-strings, `str.format()` and `format()`.
- Usage indicates practical learning priorities, not measured popularity.
- The older `%` style is still supported; it is not deprecated.

---

# Format specification mini-language

Python uses a dedicated mini-language to control the textual representation of values. It is shared by f-strings, `str.format()` and `format()` for standard types such as `int`, `float` and `str`.

## General syntax

Full standard format specification (Python 3.10):

```text
[[fill]align][sign][#][0][width][grouping_option][.precision][type]
```

Common options (without the less common `#` option):

```text
[[fill]align][sign][0][width][grouping][.precision][type]
```

- Square brackets mark optional parts; do not type the brackets.
- Write the selected options in the specified order, from left to right.
- Omit any unused option completely: no placeholder or separator is needed.
- Python uses default settings for omitted options, depending on the value's type.
- Not all combinations are valid for every data type.

## How to read a format specification

Python recognises each option by its syntax and position in the sequence. The options do not all have the same form.

| Option | How to recognise it | Example |
|---|---|---|
| `fill` | One character immediately before an alignment symbol | `*` |
| `align` | One of `<`, `>`, `^`, `=` | `>` |
| `sign` | `+`, `-` or a space | `+` |
| `#` | The alternate-form flag | `#` |
| `0` | A zero-padding flag before the width | `0` |
| `width` | An integer (minimum total number of characters) | `14` |
| `grouping` | `,` or `_` (digit separator) | `,` |
| `.precision` | A dot followed by an integer | `.2` |
| `type` | A presentation code at the end | `f` |

For example, in `08.2f`:

- `0` is the zero-padding flag.
- `8` is the width; it ends where the dot begins.
- `.2` is the precision; the dot marks its beginning.
- `f` is the presentation type.

In `8.2f`, the zero-padding flag is omitted. In `.2f`, both zero padding and width are omitted. Their absence does not change the meaning of the remaining options.

Position matters: in `0>8`, the first `0` is a fill character because it is followed by `>`, not a zero-padding flag. Changing the required order, e.g. `f8.2`, produces a `ValueError`.

## Examples: from a complete to an empty specification

Use `format(value, format_spec)` to explore the mini-language independently of string interpolation.

```python
value = 1234.5678
```

Each example removes one option from the preceding example.

- The option names are aligned above their values; `·` marks an omitted option in the diagram only.
- Join the selected characters without spaces or omission markers. Keep the dot in `.precision`.

```text
 fill  align  sign  #  zero  width  grouping  precision  type
-------------------------------------------------------------
  *      >     +    #   0      14      ,          .2      f
format(value, '*>+#014,.2f')
'*****+1,234.57'

  *      >     +    #   ·      14      ,          .2      f
format(value, '*>+#14,.2f')
'*****+1,234.57'

  *      >     +    ·   ·      14      ,          .2      f
format(value, '*>+14,.2f')
'*****+1,234.57'

  ·      >     +    ·   ·      14      ,          .2      f
format(value, '>+14,.2f')
'     +1,234.57'

  ·      ·     +    ·   ·      14      ,          .2      f
format(value, '+14,.2f')
'     +1,234.57'

  ·      ·     ·    ·   ·      14      ,          .2      f
format(value, '14,.2f')
'      1,234.57'

  ·      ·     ·    ·   ·      ·       ,          .2      f
format(value, ',.2f')
'1,234.57'

  ·      ·     ·    ·   ·      ·       ·          .2      f
format(value, '.2f')
'1234.57'

  ·      ·     ·    ·   ·      ·       ·          ·       f
format(value, 'f')
'1234.567800'

  ·      ·     ·    ·   ·      ·       ·          ·       ·
format(value, '')
'1234.5678'
```

- In the first example, `0` has no effect because `*` is the explicit fill character. The `#` flag also has no visible effect with `.2f`.
- Removing `>` does not change the output: numbers are right-aligned by default.
- Removing `.2` gives the default precision of `f` (six decimal places).
- An empty specification uses the default string representation for this value.

---

# Format options

## Fill and alignment

- `fill` – padding character (space by default); must be followed by an alignment symbol.
- `align` – `<` left, `>` right, `^` centre, `=` between the sign and digits (numbers only).
- Strings are left-aligned and numbers are right-aligned by default. Padding is added only if the specified width exceeds the length of the formatted value.

```python
format('Red', '<8')
'Red     '

format('Red', '>8')
'     Red'

format('Red', '^8')
'  Red   '

format('Red', '-^8')
'--Red---'

format(-42, '*=8')
'-*****42'
```

## Sign

- `+` – always show the sign; `-` – show the sign only for negative numbers (default); space – add a leading space to non-negative numbers.

```python
format(42, '+')
'+42'

format(-42, '+')
'-42'

format(42, '-')
'42'

format(42, ' ')
' 42'
```

## Alternate form (`#`)

A less common option: retain the decimal point in fixed-point notation or add a base prefix to binary or hexadecimal integers.

```python
format(12.0, '#.0f')
'12.'

format(255, '#x')
'0xff'
```

## Zero padding

Use `0` before the width to pad numbers with zeros (after the sign, if present, when no explicit alignment is specified).

```python
format(7, '04d')
'0007'

format(-7, '04d')
'-007'
```

## Width

Width is the minimum total number of characters, including signs, decimal points and separators. Longer values are not truncated.

```python
format(42, '8')
'      42'

format(12345, '3')
'12345'
```

## Grouping

- `,` – comma separator; `_` – underscore separator; omitted – no grouping.
- For decimal numbers, digits before the decimal point are grouped in threes, starting from the right. Grouping changes only the text representation, not the numeric value.

```python
format(1234567, ',')
'1,234,567'

format(1234567, '_')
'1_234_567'

format(1234567.89, ',.2f')
'1,234,567.89'
```

## Precision

The meaning of `.precision` depends on the presentation type:

- `f`, `e`, `%` – number of decimal places in the displayed number.
- `g` – number of significant digits.
- `s` – maximum number of characters.
- Integer presentation types (`d`, `b`, `x`) do not support precision.

```python
format(3.14159, '.2f')
'3.14'

format(12345, '.3g')
'1.23e+04'

format('Sentinel-2', '.8s')
'Sentinel'
```

## Presentation type

The table shows the value, the format specification and the resulting string, e.g. `format(42, 'd')`.

| Type | Meaning | Value | Specification | Result |
|---|---|---|---|---|
| `d` | Decimal integer | `42` | `d` | `'42'` |
| `f` | Fixed-point notation | `3.14159` | `.2f` | `'3.14'` |
| `e` | Scientific notation | `12345` | `.2e` | `'1.23e+04'` |
| `g` | General notation | `12345` | `.3g` | `'1.23e+04'` |
| `%` | Multiply by 100 and add `%` | `0.94638` | `.2%` | `'94.64%'` |
| `s` | String | `'Red'` | `s` | `'Red'` |
| `b` | Binary integer | `10` | `b` | `'1010'` |
| `x` | Hexadecimal integer | `255` | `x` | `'ff'` |

- For `float` values, `f`, `e` and `%` use six decimal places by default.
- `g` selects fixed-point or scientific notation according to the magnitude and precision.
- If the type is omitted, Python uses the default presentation for the value's data type.

---

# F-strings (formatted string literals)

## General syntax

```python
f'{expression}'

f'{expression:format_spec}'
```

- Prefix a string literal with `f`.
- Use `{expression}` to insert the value of an expression.
- Use `{expression:format_spec}` to control its presentation.
- Prefer f-strings for most new code when the values are available at the point of formatting.

```python
sensor = 'Sentinel-2'

accuracy = 0.94638

f'{sensor}: {accuracy:.2%}'
'Sentinel-2: 94.64%'

f'Error: {1 - accuracy:.2%}'
'Error: 5.36%'

f'{accuracy=:.3f}'
'accuracy=0.946'

f'{{{sensor}}}'
'{Sentinel-2}'
```

- `=` after an expression includes the expression itself and its value (useful for debugging).
- Use `{{` and `}}` to include literal braces.

---

# str.format()

The string method `str.format()` uses replacement fields `{}` with optional argument positions or names. Arguments are supplied separately to the method.

## General syntax

```python
'{field:format_spec}'.format(arguments)
```

- `field` – an argument position or name; may be empty for automatic numbering.
- `format_spec` – optional format specification, introduced by `:`.

```python
'{}: {:.2%}'.format(sensor, accuracy)
'Sentinel-2: 94.64%'

'{1}: {0:.2%}'.format(accuracy, sensor)
'Sentinel-2: 94.64%'

'{name}: {oa:.2%}'.format(name=sensor, oa=accuracy)
'Sentinel-2: 94.64%'
```

> **F-strings vs `str.format()`**
>
> - An f-string is evaluated immediately. The variables used in its expressions must already exist. The result is a completed string, not a template for later use.
> - With `str.format()`, an ordinary string containing replacement fields can be created before the values are available. The values are supplied later, when `.format()` is called. The same template can be reused without changing it.
> - F-strings allow Python expressions inside the braces, e.g. `{1 - accuracy:.2%}`. In `str.format()`, fields refer to arguments rather than arbitrary expressions: calculate the expression before passing it to `.format()`.

The following examples are independent. Start with no variable named `oa`.

```python
f'Accuracy: {oa:.2%}'
Traceback (most recent call last):
    ...
NameError: name 'oa' is not defined
```

With `str.format()`, define the template first and supply values later:

```python
template = 'Accuracy: {oa:.2%}'

template.format(oa=0.94638)
'Accuracy: 94.64%'

template.format(oa=0.91234)
'Accuracy: 91.23%'

template
'Accuracy: {oa:.2%}'
```

An f-string works once the value is available, but the resulting string does not change when the variable is reassigned:

```python
oa = 0.94638

message = f'Accuracy: {oa:.2%}'

oa = 0.91234

message
'Accuracy: 94.64%'

f'Accuracy: {oa:.2%}'
'Accuracy: 91.23%'
```

An expression inside an f-string and the equivalent expression passed as an argument to `str.format()`:

```python
f'Error: {1 - accuracy:.2%}'
'Error: 5.36%'

'Error: {:.2%}'.format(1 - accuracy)
'Error: 5.36%'
```

---

# format()

Use `format(value, format_spec)` to format a single value without surrounding text. Unlike f-strings and `str.format()`, it requires neither braces nor a colon.

```python
format(accuracy, '.2%')
'94.64%'

format(7, '04d')
'0007'
```

---

# Other formatting methods

## Percent operator

Older printf-style formatting, still supported and used in existing code and logging. Uses its own placeholders (`%s`, `%d`, `%.2f`, etc.), not the mini-language. The pair of values in the example is a tuple, covered in [Tuples and unpacking](11_tuples_and_unpacking.md).

```python
'%s: %.2f%%' % (sensor, accuracy * 100)
'Sentinel-2: 94.64%'
```

## string.Template

[`string.Template`](https://docs.python.org/3.10/library/string.html#template-strings) uses `$name` placeholders for simple substitution, without format specifications. This example previews importing a standard-library object; the focus here is the placeholder syntax.

```python
from string import Template

Template('Sensor: $name').substitute(name=sensor)
'Sensor: Sentinel-2'
```

## Manual formatting

Use string concatenation (`+` with `str()`) or padding methods (`.ljust()`, `.rjust()`, `.center()`, `.zfill()`) for simple operations without the mini-language.

```python
'Sensor: ' + sensor
'Sensor: Sentinel-2'
```

---

# Practical examples

## File names and identifiers

```python
band = 4

f'band_{band:02d}.tif'
'band_04.tif'
```

## Numeric results and units

```python
gsd = 10.1234

f'GSD: {gsd:.2f} m'
'GSD: 10.12 m'
```

## Aligned columns

```python
print(f'{"Sensor":<12}{"Accuracy":>10}')
Sensor        Accuracy

print(f'{sensor:<12}{accuracy:>10.2%}')
Sentinel-2      94.64%
```

- Formatting and displaying are separate operations. Formatting returns a string; `print()` displays it.
