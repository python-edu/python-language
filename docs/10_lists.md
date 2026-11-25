# Lists

- [Python documentation – Lists](https://docs.python.org/3.10/tutorial/introduction.html#lists)
- [Python documentation – Mutable sequence operations](https://docs.python.org/3.10/library/stdtypes.html#mutable-sequence-types)
- [Python documentation – list()](https://docs.python.org/3.10/library/stdtypes.html#list)
- [Python documentation – range()](https://docs.python.org/3.10/library/stdtypes.html#range)
- [Python documentation – More on lists](https://docs.python.org/3.10/tutorial/datastructures.html#more-on-lists)

---

# Creating lists

A list is an ordered collection of objects. Use a list when the number of items or their values may change.

- Items may have different types; related data usually use a consistent type.
- Repeated values are allowed. A list is mutable: its contents can be changed.

## Basic creation: list literals

```python
[item_1, item_2, ...]
```

Place items inside square brackets, separated by commas. Use `[]` for an empty list.

```python
bands = ['Red', 'Green', 'Blue']

bands
['Red', 'Green', 'Blue']

values = [10, 20, 10]

values
[10, 20, 10]

empty = []

empty
[]
```

## Other ways to create lists

### From another object: list()

```python
list(iterable)

list()
```

An iterable is an object that can provide its items one at a time. `list()` collects those items into a new list. Without an argument, it creates an empty list.

```python
list('RGB')
['R', 'G', 'B']

list([10, 20])
[10, 20]

list()
[]
```

Use `range()` to represent a sequence of integers. The stop value is excluded (see [For loops](17_for_loops.md) for more options).

```python
list(range(5))
[0, 1, 2, 3, 4]

list(range(2, 6))
[2, 3, 4, 5]
```

### By combining or repeating lists

`+` joins lists to create a new list. `*` repeats the items; it does not make independent copies of the items.

```python
['Red', 'Green'] + ['Blue']
['Red', 'Green', 'Blue']

[0] * 4
[0, 0, 0, 0]
```

### From parts of a string or another list

A string's `.split()` method returns a list of parts (see [Strings and lists](12_strings_and_lists.md)). A list slice creates a new list containing selected items.

```python
'B02,B03,B04'.split(',')
['B02', 'B03', 'B04']

bands[:2]
['Red', 'Green']
```

[Tuple conversion](11_tuples_and_unpacking.md) and [list comprehensions](19_list_comprehensions.md) provide further ways to create lists.

---

# Accessing items

As with strings, indices start at zero. A slice excludes its stop index and creates a new list.

## General syntax

```python
items[index]

items[start:stop:step]
```

```python
bands[0]
'Red'

bands[-1]
'Blue'

bands[:2]
['Red', 'Green']

bands[::-1]
['Blue', 'Green', 'Red']

len(bands)
3

'Green' in bands
True
```

An invalid single index raises `IndexError`.

---

# Changing lists

Assign a value to an index to replace an item. Assign a sequence to a slice to replace several items.

```python
bands[0] = 'NIR'

bands
['NIR', 'Green', 'Blue']

bands[1:3] = ['Red']

bands
['NIR', 'Red']
```

## List methods

| Method | Operation |
|---|---|
| `.append(item)` | Add one item at the end |
| `.extend(iterable)` | Add all items from another iterable |
| `.insert(index, item)` | Insert before the index |
| `.remove(item)` | Remove the first matching item |
| `.pop(index)` | Remove and return the item (last by default) |
| `.clear()` | Remove all items |
| `.index(item)` | Find the index of the first match |
| `.count(item)` | Count occurrences |

```python
bands.append('Blue')

bands
['NIR', 'Red', 'Blue']

bands.extend(['SWIR1', 'SWIR2'])

bands
['NIR', 'Red', 'Blue', 'SWIR1', 'SWIR2']

bands.insert(0, 'Green')

bands
['Green', 'NIR', 'Red', 'Blue', 'SWIR1', 'SWIR2']

bands.remove('Blue')

bands
['Green', 'NIR', 'Red', 'SWIR1', 'SWIR2']

last = bands.pop()

last
'SWIR2'

bands
['Green', 'NIR', 'Red', 'SWIR1']
```

- `.remove()` and `.index()` raise `ValueError` if the value is absent.
- `.append()` and `.extend()` modify the list and return `None`, not the modified list.
- Use `del` to remove an item by index.

```python
del bands[0]

bands
['NIR', 'Red', 'SWIR1']

bands.clear()

bands
[]
```

---

# List operations and built-in functions

Use `len()` to count items, `sum()` to add numbers and `min()` / `max()` to find the smallest / largest item.

```python
values = [20, 10, 30, 10]

len(values)
4

sum(values)
70

min(values)
10

max(values)
30

values.count(10)
2

values.index(10)
1
```

## Sorting and reversing

```python
sorted(values)
[10, 10, 20, 30]

values
[20, 10, 30, 10]

values.sort()

values
[10, 10, 20, 30]

values.reverse()

values
[30, 20, 10, 10]
```

`sorted()` returns a new list. `.sort()` and `.reverse()` change the existing list and return `None`.

---

# Nested lists and references

A list may contain other lists. Two successive indices access an inner item.

```python
pixels = [[1, 2], [3, 4]]

pixels[1][0]
3
```

Assignment does not copy a list. Use `.copy()`, `list(original)` or `original[:]` for a separate outer list (a shallow copy); nested objects are still shared (see [References and copies](29_references_and_copies.md)).

```python
original = [10, 20]

alias = original

copy = original.copy()

alias[0] = 99

original
[99, 20]

copy
[10, 20]
```

Avoid changing the length of a list while iterating over it (covered in [For loops](17_for_loops.md)).
