# Objects and methods

- [Python documentation – Objects, values and types](https://docs.python.org/3/reference/datamodel.html#objects-values-and-types)
- [Python documentation – Attribute references](https://docs.python.org/3/reference/expressions.html#attribute-references)
- [Python documentation – Built-in types](https://docs.python.org/3/library/stdtypes.html)

---

# What is an object?

In the real world, things have properties, and we can perform operations on them.

Consider a digital image:

- Properties: width, height, number of bands.
- Operations: resize, rotate, crop.

In programming, we can represent such a thing as an object. An object combines data and operations related to that data.

---

# Objects in Python

Python uses the same idea to represent data, including numbers, strings and collections.

- Each object has a type, a value and an identity.
- A variable name refers to an object.
- Attributes provide access to information about an object.
- Methods perform operations associated with an object.
- The object type determines which attributes and methods are available.

```python
x = 10

type(x)
<class 'int'>

x = 10.5

type(x)
<class 'float'>

x = 'Sentinel-2'

type(x)
<class 'str'>
```

---

# Attributes, methods and dot notation

Python uses dot notation (`.`) to access attributes and methods.

- `object.attribute` – access an attribute.
- `object.method()` – call a method without arguments.
- `object.method(argument)` – call a method with an argument.

For a floating-point number, `real` and `imag` provide its real and imaginary parts. The `is_integer()` method checks whether its value is a whole number.

```python
x = 12.5

x.real
12.5

x.imag
0.0

x.is_integer()
False
```

- `x` – a name referring to an object.
- `real`, `imag` – attributes.
- `is_integer()` – method call.
- `float` – object type.

```python
x = 12.0

x.is_integer()
True
```

A method can return a result, modify an object, or do both, depending on the method and object type.

---

# Functions and methods

| Syntax | Example | Meaning |
|---|---|---|
| `function(object)` | `round(value)` | Pass an object to a function |
| `object.attribute` | `value.real` | Access an attribute |
| `object.method()` | `value.is_integer()` | Call a method on an object |
