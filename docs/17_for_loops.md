# For loops

- [Python documentation – The for statement](https://docs.python.org/3.10/reference/compound_stmts.html#the-for-statement)
- [Python tutorial – for statements and loop control](https://docs.python.org/3.10/tutorial/controlflow.html#for-statements)
- [Python documentation – range](https://docs.python.org/3.10/library/stdtypes.html#ranges)
- [Python documentation – enumerate](https://docs.python.org/3.10/library/functions.html#enumerate)

---

# The `for` statement

A loop repeats a block of code. A `for` loop takes successive items from an object and executes the same block for each item. This process is called iteration.

## General syntax

```python
for target in iterable:
    statements
```

- `target` – usually a variable name that receives the current item.
- `iterable` – an object that provides successive items, e.g. a string, list, tuple, dictionary, set or range of integers.
- `statements` – one or more indented instructions (the loop body).
- `for` and `in` are keywords; the colon and indentation are required.

Python takes the first item, assigns it to the target and executes the loop body. It repeats these steps for each remaining item. When no more items are available, execution continues after the loop.

## Iterating over a string

A string provides its characters one at a time, in order.

```python
for band in 'RGB':
    print(band)
R
G
B
```

The variable `band` receives `R`, then `G`, then `B`. The same `print()` instruction is executed three times.

## Iterating over collections

Lists and tuples provide items in order. A dictionary provides keys by default; `.items()` provides key-value pairs. A set has no guaranteed iteration order.

```python
bands = ['Red', 'Green', 'Blue']

for band in bands:
    print(band)
Red
Green
Blue
```

```python
resolutions = {'B02': 10, 'B11': 20}

for band, resolution in resolutions.items():
    print(band, resolution)
B02 10
B11 20
```

## Filtering items in a loop

Create an empty list before the loop, then append only items that satisfy a condition. The original collection remains unchanged.

```python
cloud_cover = [5, 15, 30]

accepted = []

for value in cloud_cover:
    if value <= 20:
        accepted.append(value)

accepted
[5, 15]
```

Avoid adding or removing items from the list being iterated over.

## Loop body and indentation

All instructions at the same indentation level inside the loop belong to its body. An instruction outside the loop runs after the loop finishes.

```python
for band in 'RGB':
    print(f'Band: {band}')
    print('Processing')
Band: R
Processing
Band: G
Processing
Band: B
Processing

print('Finished')
Finished
```

---

# `range()`

`range()` creates a sequence of integers. Use it to repeat an operation a specified number of times or to work with successive integer values.

## General syntax

```python
range(stop)

range(start, stop)

range(start, stop, step)
```

- `start` – first value (default: `0`).
- `stop` – excluded boundary; the sequence stops before reaching or passing it.
- `step` – difference between consecutive values (default: `1`); it cannot be zero.
- All three arguments are integers. Use a negative step to obtain decreasing values.

`range()` creates a `range` object, not a list. It does not store all the integers separately.

## Examples

| Expression | Successive values |
|---|---|
| `range(4)` | `0, 1, 2, 3` |
| `range(1, 5)` | `1, 2, 3, 4` |
| `range(0, 10, 3)` | `0, 3, 6, 9` |
| `range(5, 0, -1)` | `5, 4, 3, 2, 1` |
| `range(5, 5)` | No values |
| `range(5, 0)` | No values |

```python
for number in range(1, 5):
    print(number)
1
2
3
4
```

## Indexing a list with `range()`

Use a range of indices when you need to update items by position. For reading items, direct iteration is usually simpler.

```python
values = [10, 20, 30]

for index in range(len(values)):
    values[index] *= 2

values
[20, 40, 60]
```

## Calculations in a loop

To calculate the total area of five square pixels with a side length of 10 m, start with zero and add the area of one pixel in each iteration.

```python
pixel_size = 10

total_area = 0

for pixel in range(5):
    total_area += pixel_size**2

print(total_area)
500
```

The value of `total_area` changes from `0` to `100`, `200`, `300`, `400` and `500`.

## Repetition without using the loop variable

Use `_` when the current item is not needed in the loop body.

```python
for _ in range(3):
    print('Processing')
Processing
Processing
Processing
```

`_` is an ordinary variable name. Using it for an unused value is a convention, not a special rule of the `for` statement.

---

# `enumerate()`

Use `enumerate()` when both an item and its position or sequence number are needed. It provides two values in each iteration: a counter and the current item.

## General syntax

```python
enumerate(iterable, start=0)

for counter, item in enumerate(iterable):
    statements
```

- `iterable` – an object to iterate over.
- `start` – initial counter value (default: `0`).
- `counter` – receives the current counter value.
- `item` – receives the current item.

The counter increases by one after each item. Changing `start` changes the numbering, not the items selected. Each pair is unpacked into two names (see [Tuples and unpacking](11_tuples_and_unpacking.md)).

## Index and item

```python
for index, band in enumerate('RGB'):
    print(index, band)
0 R
1 G
2 B
```

## Numbering from one

```python
for number, band in enumerate('RGB', start=1):
    print(number, band)
1 R
2 G
3 B
```

## Choosing between direct iteration, `range()` and `enumerate()`

| What is needed? | Example |
|---|---|
| Only the items | `for band in 'RGB':` |
| Integers or a fixed number of repetitions | `for i in range(3):` |
| Both the index and the item | `for i, band in enumerate('RGB'):` |

It is also possible to use `range()` and string indexing:

```python
bands = 'RGB'

for index in range(len(bands)):
    print(index, bands[index])
0 R
1 G
2 B
```

This produces the same output as `enumerate(bands)`. Prefer `enumerate()` when both the index and the item are needed.

---

# `break` and `continue`

By default, a `for` loop processes all items. These two statements change its execution.

## `break` – stop the loop

```python
for item in iterable:
    if condition:
        break
    statements
```

When `break` is executed, the loop ends immediately. The remaining instructions in its body and all remaining iterations are skipped. Execution continues after the loop.

```python
for number in range(1, 6):
    if number == 3:
        break
    print(number)
1
2

print('Finished')
Finished
```

## `continue` – skip the rest of the current iteration

```python
for item in iterable:
    if condition:
        continue
    statements
```

When `continue` is executed, the remaining instructions in the current iteration are skipped. The loop proceeds to the next item, if one is available.

```python
for number in range(1, 6):
    if number == 3:
        continue
    print(number)
1
2
4
5

print('Finished')
Finished
```

Both statements affect only the innermost enclosing loop.

Compare the two examples: `break` stops at `3`; `continue` skips `3` and proceeds to `4`.
