# List comprehensions

- [Python documentation – List comprehensions](https://docs.python.org/3.10/tutorial/datastructures.html#list-comprehensions)
- [Python documentation – Displays for lists, sets and dictionaries](https://docs.python.org/3.10/reference/expressions.html#displays-for-lists-sets-and-dictionaries)

---

# Creating a list from another iterable

A list comprehension builds a new list by evaluating an expression for successive items. It is an alternative to a `for` loop that fills a list with `.append()`.

## General syntax

```python
[expression for item in iterable]

[expression for item in iterable if condition]
```

- `iterable` – source of items.
- `item` – name receiving each item.
- `expression` – value added to the new list.
- `if condition` – optional filter; only items satisfying it are used.

## Transforming values

Convert pixel sizes in metres to areas in square metres.

```python
sizes = [10, 20, 30]

areas = []

for size in sizes:
    areas.append(size**2)

areas
[100, 400, 900]
```

The equivalent comprehension:

```python
areas = [size**2 for size in sizes]

areas
[100, 400, 900]
```

The original list is unchanged.

---

# Filtering and transforming

```python
ndvi = [-0.2, 0.1, 0.4, 0.7]

positive = [value for value in ndvi if value > 0]

positive
[0.1, 0.4, 0.7]

percent = [value * 100 for value in ndvi if value > 0]

percent
[10.0, 40.0, 70.0]
```

Python takes each item, checks the optional condition and evaluates the expression only for accepted items.

---

# Filtering vs conditional expression

A filter changes which items are included. A conditional expression chooses the value for each included item.

```python
[value for value in ndvi if value >= 0.3]
[0.4, 0.7]

[1 if value >= 0.3 else 0 for value in ndvi]
[0, 0, 1, 1]
```

Use a normal `for` loop when several statements, complex decisions or actions other than building a list are needed.
