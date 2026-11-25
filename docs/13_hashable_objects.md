# Hashable objects

- [Python documentation – Hashable](https://docs.python.org/3.10/glossary.html#term-hashable)
- [Python documentation – hash()](https://docs.python.org/3.10/library/functions.html#hash)

---

# What is a hash?

A hash is an integer calculated from an object. Dictionaries and sets use hashes to help locate items efficiently, without comparing every stored item.

## General syntax

```python
hash(object)
```

```python
hash(10) == hash(10.0)
True

hash('Red') == hash('Red')
True
```

- A hashable object has a hash that does not change during its lifetime.
- It can be compared for equality. Equal objects must have equal hashes.
- Different objects may have the same hash (a collision); equality is checked as needed.
- When inserting or looking up a dictionary key or a set element, Python uses its hash to find candidate entries, then checks equality when necessary.
- Do not use hash values as persistent identifiers: string hashes may vary between Python processes.

---

# Which objects are hashable?

| Type | Hashable? |
|---|---|
| `int`, `float`, `bool`, `str`, `NoneType` | Yes |
| `tuple` | Only if every item is hashable |
| `list`, `dict`, `set` | No |
| `frozenset` | Yes |

Mutable built-in collections are unhashable because their contents can change. Immutability alone is not sufficient: a tuple containing a list is unhashable.

```python
hash((10, 20)) == hash((10, 20))
True
```

```python
hash([10, 20])
Traceback (most recent call last):
    ...
TypeError: unhashable type: 'list'
```

---

# Why hashability matters

- Dictionary keys must be hashable; dictionary values do not need to be hashable.
- Set elements must be hashable.
- Coordinates such as `(row, col)` can serve as keys or set elements. Lists of coordinates cannot serve directly as individual keys.

See [Dictionaries](14_dictionaries.md) and [Sets](15_sets.md) for examples.
