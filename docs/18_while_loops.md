# While loops

- [Python documentation – The while statement](https://docs.python.org/3.10/reference/compound_stmts.html#the-while-statement)
- [Python documentation – Loop control](https://docs.python.org/3.10/reference/simple_stmts.html#the-break-statement)

---

# The `while` statement

A `while` loop repeats a block of code as long as a condition is true. Unlike a `for` loop, the number of iterations does not need to be known in advance.

## General syntax

```python
while condition:
    statements
```

- `condition` – an expression tested before each iteration.
- `statements` – the indented loop body.
- If the condition is false at the beginning, the body is never executed.
- Something must eventually make the condition false, or the loop must be stopped with `break`.

```python
remaining = 3

while remaining > 0:
    print(remaining)
    remaining -= 1
3
2
1

print('Finished')
Finished
```

The condition is tested again after every iteration. When `remaining` reaches zero, execution continues after the loop.

---

# Condition-controlled calculations

Find the smallest power of two that is at least as large as an image width.

```python
width = 1000

size = 1

while size < width:
    size *= 2

size
1024
```

The loop stops when `size >= width`. The number of doublings depends on the input.

---

# `break` and `continue`

These statements work as in a `for` loop. `break` exits the loop; `continue` starts the next condition test. Update the loop state before `continue` if the update is needed for termination.

```python
attempt = 0

while attempt < 5:
    attempt += 1
    if attempt == 2:
        continue
    if attempt == 4:
        break
    print(attempt)
1
3
```

---

# Choosing `for` or `while`

| Situation | Preferred loop |
|---|---|
| Process items of a collection | `for` |
| Repeat a known number of times | `for` with `range()` |
| Repeat until a condition changes | `while` |

Avoid a `while` loop with a condition that cannot become false unless a reliable `break` is provided.
