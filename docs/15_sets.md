# Sets

- [Python documentation – Set types](https://docs.python.org/3.10/library/stdtypes.html#set-types-set-frozenset)
- [Python documentation – Sets](https://docs.python.org/3.10/tutorial/datastructures.html#sets)

---

# Creating sets

A set is a collection of unique, hashable elements. Use it to remove duplicates, test membership or compare groups of values. Sets do not have positional indices or a guaranteed iteration order.

## Basic creation: set literals

```python
{item_1, item_2, ...}
```

Place items inside curly braces, separated by commas. Unlike a dictionary, a set contains individual items, not key-value pairs.

```python
bands = {'B02', 'B03', 'B04'}

bands
{'B02', 'B03', 'B04'}

{10, 10}
{10}
```

Set representations may display elements in a different order from the examples. The order is not part of the set's value.

Use `set()` for an empty set; `{}` creates an empty dictionary.

```python
set()
set()

type({})
<class 'dict'>
```

## Other ways to create sets

### From another object: set()

```python
set(iterable)
```

Use `set()` to collect unique elements from another iterable. Repeated items are removed. All items must be hashable.

```python
set([10, 20, 10])
{10, 20}

set(('B02', 'B02'))
{'B02'}

set('RRR')
{'R'}

set({'B02': 10, 'B11': 20})
{'B02', 'B11'}
```

When a dictionary is passed directly to `set()`, its keys are used. To collect unique dictionary values, use `.values()`.

```python
resolution = {'B02': 10, 'B03': 10, 'B11': 20}

set(resolution.values())
{10, 20}
```

### From another set

Use `set(existing_set)` or `.copy()` to create a separate set.

```python
original = {10}

separate = original.copy()

separate.add(20)

separate
{10, 20}

original
{10}
```

Set operations also create new sets (see below). [Set comprehensions](20_dictionary_and_set_comprehensions.md) create sets from expressions.

---

# Testing membership and counting elements

```python
len(bands)
3

'B02' in bands
True

'B11' in bands
False
```

Sets do not support indexing or slicing. Use a list or tuple when positional access is needed.

---

# Changing sets

| Method | Operation |
|---|---|
| `.add(item)` | Add an element |
| `.update(iterable)` | Add several elements |
| `.remove(item)` | Remove an element; error if absent |
| `.discard(item)` | Remove an element if present |
| `.pop()` | Remove and return an arbitrary element |
| `.clear()` | Remove all elements |
| `.copy()` | Create a separate set |

```python
bands.add('B08')

bands
{'B02', 'B03', 'B04', 'B08'}

bands.update(['B11', 'B12'])

bands
{'B02', 'B03', 'B04', 'B08', 'B11', 'B12'}

bands.discard('B99')

bands
{'B02', 'B03', 'B04', 'B08', 'B11', 'B12'}

bands.remove('B03')

'B03' in bands
False

bands
{'B02', 'B04', 'B08', 'B11', 'B12'}

bands.clear()

bands
set()
```

`.remove()` raises `KeyError` if the item is absent; `.discard()` leaves the set unchanged. `.pop()` removes an arbitrary item, not the first or last item.

---

# Set operations

Let `available` contain existing bands and `required` contain bands needed for an analysis.

```python
available = {'B02', 'B03', 'B04'}

required = {'B04', 'B08'}
```

| Operator | Method | Meaning |
|---|---|---|
| `\|` | `.union()` | Elements in either set |
| `&` | `.intersection()` | Elements in both sets |
| `-` | `.difference()` | Elements only in the left set |
| `^` | `.symmetric_difference()` | Elements in exactly one set |

```python
available | required
{'B02', 'B03', 'B04', 'B08'}

available & required
{'B04'}

required - available
{'B08'}

available ^ required
{'B02', 'B03', 'B08'}
```

Operators require set operands; the corresponding methods also accept other iterables. Augmented forms `|=`, `&=`, `-=`, `^=` update the set in place.

## Relationships

```python
# Is required a subset of available?
required <= available
False

# Is available a superset of {'B02'}?
available >= {'B02'}
True

available.isdisjoint(required)
False
```

## Set operations on dictionary views

Dictionary key views support set-like operations without converting them to sets. Item views also support these operations when their pairs are hashable. The result of `&`, `|`, `-` or `^` is a new set, not a view.

```python
first = {'B02': 10, 'B04': 10}

second = {'B04': 20, 'B08': 10}

first.keys() & second.keys()
{'B04'}

first.keys() - second.keys()
{'B02'}

first.items() & second.items()
set()
```

---

# Immutable sets

`frozenset()` creates an immutable, hashable set. Use it when a set of values must serve as a dictionary key or as an element of another set.

```python
required = frozenset(['B04', 'B08'])

required
frozenset({'B04', 'B08'})

type(required)
<class 'frozenset'>
```

---

# Choosing a data structure

| Type | Order | Access | Repeated values | Mutable |
|---|---|---|---|---|
| `list` | Insertion order | Index | Yes | Yes |
| `tuple` | Item order | Index | Yes | No |
| `dict` | Insertion order | Key | Values: yes; keys: no | Yes |
| `set` | Not guaranteed | Membership | No | Yes |

Use a list for a sequence of changing items, a tuple for fixed groups of values, a dictionary for key-value associations, and a set for unique elements.
