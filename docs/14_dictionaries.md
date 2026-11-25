# Dictionaries

- [Python documentation – Mapping types – dict](https://docs.python.org/3.10/library/stdtypes.html#mapping-types-dict)
- [Python documentation – Dictionary view objects](https://docs.python.org/3.10/library/stdtypes.html#dictionary-view-objects)
- [Python documentation – zip()](https://docs.python.org/3.10/library/functions.html#zip)
- [Python documentation – Dictionaries](https://docs.python.org/3.10/tutorial/datastructures.html#dictionaries)

---

# Creating dictionaries

A dictionary maps unique keys to values. Unlike a list, a value is accessed by its key rather than by its position.

- Keys must be [hashable](13_hashable_objects.md); values may be any object.
- A key appears only once. If a key occurs more than once, the last value is used.
- Dictionaries are mutable and preserve insertion order (language guarantee since Python 3.7).

## Basic creation: dictionary literals

```python
{key_1: value_1, key_2: value_2, ...}
```

A colon separates a key from its value. Commas separate key-value pairs. Use `{}` for an empty dictionary.

```python
resolution = {'B02': 10, 'B03': 10, 'B11': 20}

resolution
{'B02': 10, 'B03': 10, 'B11': 20}

empty = {}

empty
{}

{'B02': 10, 'B02': 20}
{'B02': 20}
```

## Other ways to create dictionaries

### From named arguments: dict()

```python
dict(name_1=value_1, name_2=value_2, ...)
```

Use this form when keys are strings that can be written as Python argument names. Unlike a literal, the names are not quoted. This form cannot directly express arbitrary keys, e.g. integers or strings containing spaces.

```python
metadata = dict(rows=800, cols=1000)

metadata
{'rows': 800, 'cols': 1000}

dict()
{}
```

### From key-value pairs: dict()

```python
dict(iterable_of_pairs)
```

Use this form when the data are already grouped into pairs. Each item must contain exactly two elements: the key and its value.

```python
pairs = [('B02', 10), ('B11', 20)]

dict(pairs)
{'B02': 10, 'B11': 20}
```

### From separate collections of keys and values: dict(zip())

```python
dict(zip(keys, values))
```

Use this form when keys and values are stored in two separate sequences. `zip()` pairs items at corresponding positions. `dict()` converts the pairs into dictionary entries.

```python
bands = ['B02', 'B04', 'B11']

sizes = [10, 10, 20]

list(zip(bands, sizes))
[('B02', 10), ('B04', 10), ('B11', 20)]

dict(zip(bands, sizes))
{'B02': 10, 'B04': 10, 'B11': 20}
```

By default, `zip()` stops at the end of the shortest input. Use `strict=True` (Python 3.10+) when both inputs must have the same length.

```python
dict(zip(bands, sizes, strict=True))
{'B02': 10, 'B04': 10, 'B11': 20}
```

See [Parallel iteration](21_parallel_iteration.md) for further uses of `zip()`.

### From keys with a common initial value: dict.fromkeys()

```python
dict.fromkeys(keys, value=None)
```

Use this method to initialise several keys with the same value, for example counters or missing results. If the value is omitted, each key is associated with `None`.

```python
dict.fromkeys(bands, 0)
{'B02': 0, 'B04': 0, 'B11': 0}

dict.fromkeys(bands)
{'B02': None, 'B04': None, 'B11': None}
```

All keys refer to the same initial object. Use immutable values such as `0` or `None` rather than a shared mutable list.

### From an existing dictionary

Use `dict(existing_dict)` or `.copy()` to create a separate dictionary (a shallow copy). Changing a top-level entry in the copy does not change the original entry.

```python
metadata_copy = dict(metadata)

metadata_copy['rows'] = 900

metadata_copy
{'rows': 900, 'cols': 1000}

metadata
{'rows': 800, 'cols': 1000}
```

See [References and copies](29_references_and_copies.md) for nested objects and [Dictionary and set comprehensions](20_dictionary_and_set_comprehensions.md) for creating dictionaries from expressions.

---

# Accessing and modifying values

```python
resolution['B02']
10

resolution['B04'] = 10  # add a new key

resolution
{'B02': 10, 'B03': 10, 'B11': 20, 'B04': 10}

resolution['B11'] = 30  # replace a value

resolution
{'B02': 10, 'B03': 10, 'B11': 30, 'B04': 10}

len(resolution)
4

'B02' in resolution
True

10 in resolution
False
```

Membership tests keys, not values. An absent key raises `KeyError` with bracket access. Use `.get(key, default)` when a missing key is expected.

```python
resolution.get('B99') is None
True

resolution.get('B99', -1)
-1
```

## Dictionary methods

| Method | Operation |
|---|---|
| `.get(key, default)` | Read a value or return a default |
| `.update(other)` | Add or replace entries |
| `.pop(key)` | Remove a key and return its value |
| `.clear()` | Remove all entries |
| `.copy()` | Create a shallow copy |

```python
resolution.update({'B08': 10, 'B11': 20})

resolution
{'B02': 10, 'B03': 10, 'B11': 20, 'B04': 10, 'B08': 10}

removed = resolution.pop('B03')

removed
10

'B03' in resolution
False

resolution
{'B02': 10, 'B11': 20, 'B04': 10, 'B08': 10}
```

Use `del` to remove an entry without returning its value.

```python
del resolution['B04']

resolution
{'B02': 10, 'B11': 20, 'B08': 10}

resolution.clear()

resolution
{}
```

---

# Dictionary views

## What is a view?

A view is an object that provides access to selected parts of a dictionary: its keys, values or key-value pairs.

It is called a view because it shows the contents of the original dictionary without creating a separate list of those contents. When the dictionary changes, an existing view shows the updated contents automatically.

| Method | Object type | Provides access to |
|---|---|---|
| `.keys()` | `dict_keys` | Keys |
| `.values()` | `dict_values` | Values |
| `.items()` | `dict_items` | Key-value pairs (tuples) |

```python
resolution = {'B02': 10, 'B11': 20}

keys = resolution.keys()

values = resolution.values()

items = resolution.items()

keys
dict_keys(['B02', 'B11'])

values
dict_values([10, 20])

items
dict_items([('B02', 10), ('B11', 20)])

type(keys)
<class 'dict_keys'>

type(values)
<class 'dict_values'>

type(items)
<class 'dict_items'>
```

The square brackets in the displayed representation do not mean that the view is a list. Views have their own types.

## Views vs the original dictionary vs lists

| Property | Dictionary | View | List |
|---|---|---|---|
| Contents | Key-value pairs | Selected parts of a dictionary | Items |
| Access by key | Yes | No | No |
| Access by position | No | No | Yes |
| Modify contents directly | Yes | No | Yes |
| Reflect changes in the original dictionary | Original object | Yes | No (for a list created from a view) |

A view cannot be indexed or edited directly. Change the dictionary itself to update its contents.

## Dynamic views and independent snapshots

Create a view and a list before changing the dictionary. Compare them after adding, replacing and removing entries.

```python
snapshot = list(keys)

snapshot
['B02', 'B11']

resolution['B04'] = 10

keys
dict_keys(['B02', 'B11', 'B04'])

snapshot
['B02', 'B11']

resolution['B11'] = 30

values
dict_values([10, 30, 10])

items
dict_items([('B02', 10), ('B11', 30), ('B04', 10)])

del resolution['B02']

keys
dict_keys(['B11', 'B04'])

snapshot
['B02', 'B11']
```

- A view reflects additions, replacements and removals in the original dictionary.
- `list(view)` creates a separate list of the current items. Later additions, removals or replacements of dictionary entries do not update the list.
- The conversion is shallow: mutable objects inside the list can still be shared with the dictionary.

## When to use a view or a list

Use views when checking membership, counting items, or processing dictionary contents without creating a separate collection. Use a list when positional access, sorting into a separate list, or a snapshot is needed.

```python
'B11' in keys
True

30 in values
True

('B04', 10) in items
True

len(keys)
2

list(keys)[0]
'B11'

list(values)
[30, 10]

list(items)
[('B11', 30), ('B04', 10)]
```

- Key views and item views with hashable pairs also support set-like operations (see [Sets](15_sets.md)). Value views do not support these operations because values may repeat or be unhashable.
- Views provide the items for a `for` loop (see [For loops](17_for_loops.md)). Avoid adding or removing dictionary keys during iteration.

---

# Combining dictionaries (Python 3.9+)

`|` creates a new dictionary; `|=` updates the left dictionary. For shared keys, the right-hand value wins.

```python
base = {'sensor': 'S2', 'resolution': 10}

updates = {'resolution': 20, 'band': 'B11'}

base | updates
{'sensor': 'S2', 'resolution': 20, 'band': 'B11'}

base
{'sensor': 'S2', 'resolution': 10}

base |= updates

base
{'sensor': 'S2', 'resolution': 20, 'band': 'B11'}
```

---

# Nested dictionaries and tuple keys

```python
metadata = {'shape': {'rows': 800, 'cols': 1000}, 'bands': ['B02', 'B03']}

metadata['shape']['rows']
800

metadata['bands'][0]
'B02'

pixels = {(0, 0): 15, (0, 1): 20}

pixels[(0, 1)]
20
```

The tuple key identifies one pixel by row and column.
