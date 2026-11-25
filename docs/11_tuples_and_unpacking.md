# Tuples and unpacking

- [Python documentation – Tuples and sequences](https://docs.python.org/3.10/tutorial/datastructures.html#tuples-and-sequences)
- [Python documentation – tuple()](https://docs.python.org/3.10/library/stdtypes.html#tuple)
- [Python documentation – Assignment statements](https://docs.python.org/3.10/reference/simple_stmts.html#assignment-statements)

---

# Creating tuples

A tuple is an ordered collection whose item references cannot be changed after creation. Use tuples for fixed groups of values, such as coordinates or image dimensions.

## Basic creation: tuple literals

```python
(item_1, item_2, ...)
```

- Commas create a tuple; parentheses usually group its items.
- A one-item tuple needs a trailing comma: `(10,)`. `(10)` is an integer.
- Use `()` for an empty tuple.

```python
point = (450000, 5500000)

point
(450000, 5500000)

shape = (800, 1000, 3)

shape
(800, 1000, 3)

(10,)
(10,)

(10)
10

()
()
```

## Other ways to create tuples

### From another object: tuple()

```python
tuple(iterable)

tuple()
```

Use `tuple()` to collect items from another object into a tuple, e.g. to prevent replacing or adding items. Without an argument, it creates an empty tuple.

```python
tuple([10, 20])
(10, 20)

tuple('RGB')
('R', 'G', 'B')

tuple(range(3))
(0, 1, 2)

tuple()
()
```

Use `list()` to convert a tuple to a mutable list.

```python
list(shape)
[800, 1000, 3]
```

### By combining or repeating tuples

```python
(10, 20) + (30,)
(10, 20, 30)

(0,) * 3
(0, 0, 0)
```

---

# Accessing items and tuple operations

Tuples support the same indexing, slicing and membership operations as lists. A slice returns a tuple.

```python
shape[0]
800

shape[-1]
3

shape[:2]
(800, 1000)

len(shape)
3

800 in shape
True

(10, 20, 10).count(10)
2

shape.index(1000)
1
```

Tuples are immutable, but an object inside a tuple can itself be mutable. Choose a list when items need to be replaced or added.

---

# Packing and unpacking

Packing combines values into a tuple. Unpacking assigns items to separate variable names.

## General syntax

```python
name_1, name_2 = iterable

name_1, *remaining = iterable
```

```python
point = 450000, 5500000

x, y = point

x
450000

y
5500000

rows, cols, bands = shape

rows
800
```

Without a starred target, the number of names must equal the number of items. Unpacking works with lists and other iterables as well.

```python
first, *remaining = [10, 20, 30]

first
10

remaining
[20, 30]
```

A starred target receives the remaining items as a list. Only one starred target is allowed at the same unpacking level.

## Swapping values

The right-hand expressions are evaluated before assignment.

```python
x = 10

y = 20

x, y = y, x

x
20

y
10
```

---

# Choosing a list or a tuple

| Property | List | Tuple |
|---|---|---|
| Syntax | `[10, 20]` | `(10, 20)` |
| Ordered and indexed | Yes | Yes |
| Repeated items | Yes | Yes |
| Replace, add or remove items | Yes | No |
| Typical use | Changing collection | Fixed group of values |
