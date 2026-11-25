# Strings

- [Python documentation – String literals, escape sequences and raw strings](https://docs.python.org/3.10/reference/lexical_analysis.html#string-and-bytes-literals)
- [Python documentation – Text sequence type (str)](https://docs.python.org/3/library/stdtypes.html#text-sequence-type-str)
- [Python documentation – Common sequence operations](https://docs.python.org/3/library/stdtypes.html#common-sequence-operations)
- [Python documentation – Membership test operations](https://docs.python.org/3/reference/expressions.html#membership-test-operations)
- [Python documentation – Line endings in text files](https://docs.python.org/3.10/library/functions.html#open)

---

# What is a string?

A string is an ordered sequence of characters that represents text, for example a label, a file name or a message. In Python, the type of a string is `str`.

- A string may contain letters, digits, spaces, punctuation and special characters.
- A string may be empty or contain just one character. Python has no separate character type.
- A string containing digits is still text, not a number.
- Strings are immutable: their contents cannot be changed after creation.

```python
type('10')
<class 'str'>

type(10)
<class 'int'>

''
''

'A'
'A'
```

---

# Creating strings

## String literals and quotation marks

A string literal is text written directly in Python code, enclosed in quotation marks.

- Single quotes (`'...'`) and double quotes (`"..."`) have the same meaning. Choose one style consistently.
- The opening and closing quotation marks must match. They are not part of the string itself.
- Use the other type of quotation mark when the text contains a quote or an apostrophe.

```python
sensor = 'Sentinel-2'

label = "Red band"

'Sentinel-2' == "Sentinel-2"
True

"It's a clear image"
"It's a clear image"

'The label is "Red"'
'The label is "Red"'
```

## Triple quotes and multiline strings

Triple single quotes (`'''...'''`) or triple double quotes (`"""..."""`) allow a string literal to extend across multiple lines. Line breaks and spaces inside the literal become part of the string.

```python
message = """Sensor: Sentinel-2
Band: Red
Resolution: 10 m"""

print(message)
Sensor: Sentinel-2
Band: Red
Resolution: 10 m
```

## Converting other values to strings

Use `str(value)` to create a string from another value.

```python
str(10)
'10'

str(10.5)
'10.5'

str(True)
'True'
```

---

# Escape sequences

Some characters are difficult to type directly in a string literal. An escape sequence starts with a backslash (`\`) and tells Python how to interpret the following character or characters.

| Escape sequence | Name | What it does |
|---|---|---|
| `\n` | Line feed (LF) | Starts a new line in displayed text. |
| `\t` | Horizontal tab (TAB) | Moves to the next tab stop. Useful for separating or aligning text. |
| `\r` | Carriage return (CR) | Moves the cursor back to the beginning of the same line in a terminal, without starting a new line. |
| `\\` | Backslash | Inserts one actual backslash, rather than starting an escape sequence. |
| `\'` | Single quote | Inserts an apostrophe or single quote, even inside a single-quoted string. |
| `\"` | Double quote | Inserts a double quote, even inside a double-quoted string. |

```python
print('Red\nGreen\nBlue')
Red
Green
Blue

print('Band\tValue')
Band	Value

print('It\'s a clear image')
It's a clear image

print("The label is \"Red\"")
The label is "Red"

print('C:\\data\\new\\image.tif')
C:\data\new\image.tif
```

- `\n` and `\t` each represent one character, not two. A tab moves to the next tab stop; the number of displayed spaces depends on the output environment.
- The interpreter normally shows a string's representation (including escape sequences); `print()` displays the actual text.

```python
text = 'A\nB'

text
'A\nB'

print(text)
A
B

len(text)
3
```

## Line endings – Linux, macOS and Windows

Text files use special characters to mark the end of each line (EOL, end of line).

| System | Line ending | Python notation |
|---|---|---|
| Linux / modern macOS | LF (line feed) | `\n` |
| Windows | CRLF (carriage return + line feed) | `\r\n` |
| Classic Mac OS (before Mac OS X) | CR (carriage return) | `\r` |

- LF and CR are different characters. CR traditionally moves the cursor to the beginning of the current line; LF moves it to the next line.
- CRLF consists of two characters.
- These are conventional text-file line endings, not restrictions: a file on any system can contain any of them.

```python
len('\n')
1

len('\r\n')
2
```

> Use `\n` for new lines in Python code on all platforms. By default, when Python reads text files, it converts LF, CRLF and CR to `\n`. When writing text files, it translates `\n` to the operating system's default line ending (CRLF on Windows, LF on Linux and macOS).

---

# Raw string literals

A raw string literal starts with `r` before its opening quote. In an ordinary string literal, Python interprets sequences such as `\n` and `\t`. In a raw string literal, those sequences remain as two characters: a backslash followed by a letter.

## General syntax

```python
r'text'

r"text"
```

Raw strings are useful for Windows paths and regular expressions.

```python
ordinary = 'A\nB'

raw = r'A\nB'

print(ordinary)
A
B

print(raw)
A\nB

len(ordinary)
3

len(raw)
4

ordinary == raw
False

type(raw)
<class 'str'>
```

A Windows path can contain sequences such as `\n` and `\t`, which have a special meaning in an ordinary string literal.

```python
incorrect_path = 'C:\new\test.tif'

print(incorrect_path)
C:
ew	est.tif

escaped_path = 'C:\\new\\test.tif'

raw_path = r'C:\new\test.tif'

print(escaped_path)
C:\new\test.tif

print(raw_path)
C:\new\test.tif

escaped_path == raw_path
True

incorrect_path == raw_path
False
```

In the first path, `\n` and `\t` are interpreted as a newline and a tab. The other two literals create the same correct path. A raw string is not a separate data type; its type is still `str`.

- A raw string literal cannot end with an odd number of backslashes because a backslash can escape a closing quote in the source code.
- To create a path ending in a single backslash, use an ordinary literal with escaped backslashes or concatenate a raw string with a backslash.

```python
path = r'C:\new' + '\\'

print(path)
C:\new\
```

---

# Operators

| Operator | Operation |
|---|---|
| `+` | Concatenation |
| `*` | Repetition |

```python
'Sentinel' + '-2'
'Sentinel-2'

'-' * 5
'-----'
```

---

# Membership operators

| Operator | Meaning for strings |
|---|---|
| `in` | The substring occurs in the string |
| `not in` | The substring does not occur in the string |

- Both operators return a Boolean value.
- Membership tests in strings are case-sensitive.
- Use `substring in string` to test for a character or a sequence of characters.

```python
'2' in sensor
True

'Sentinel' in sensor
True

'sentinel' in sensor
False

'Landsat' not in sensor
True
```

---

# Indexing and slicing

- Indexing starts at zero.
- Negative indices count from the end.
- `len()` returns the number of Unicode code points in a string (characters in these examples).
- In `text[start:stop:step]`, the stop index is excluded.

## General syntax

```python
text[index]

text[start:stop:step]
```

- `index` – position of one character.
- `start` – first position; `stop` – excluded boundary; `step` – distance between positions.
- The slice parameters are optional. A negative step reads backwards.

```python
sensor[0]
'S'

sensor[-1]
'2'

sensor[:8]
'Sentinel'

sensor[9:]
'2'

sensor[::-1]
'2-lenitneS'

len(sensor)
10
```

---

# String methods

- Call methods using dot notation: `object.method()` (see [Objects and methods](07_objects_and_methods.md)).

| Method | Operation |
|---|---|
| `.lower()` | Convert to lowercase |
| `.upper()` | Convert to uppercase |
| `.strip()` | Remove leading and trailing whitespace |
| `.replace(old, new)` | Replace text |
| `.startswith(prefix)` | Test the beginning |
| `.endswith(suffix)` | Test the end |

```python
' RED '.strip().lower()
'red'

'image.tif'.replace('.tif', '.png')
'image.png'

'image.tif'.endswith('.tif')
True
```

- String methods do not modify the original string.

```python
sensor.lower()
'sentinel-2'

sensor
'Sentinel-2'
```
