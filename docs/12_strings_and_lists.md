# Strings and lists

- [Python documentation – String methods](https://docs.python.org/3.10/library/stdtypes.html#string-methods)

---

# Splitting text

Use `.split()` to create a list of strings from a single string.

## General syntax

```python
text.split(sep=None, maxsplit=-1)
```

- `sep` – separator; omitted or `None` splits on runs of whitespace.
- `maxsplit` – maximum number of splits; `-1` means no limit.
- An explicit separator preserves empty fields between adjacent separators.

```python
'B02,B03,B04'.split(',')
['B02', 'B03', 'B04']

'  Red   Green Blue '.split()
['Red', 'Green', 'Blue']

'B02,,B04'.split(',')
['B02', '', 'B04']

'2026-11-25'.split('-', 1)
['2026', '11-25']
```

Use `.splitlines()` to split text at line boundaries.

```python
'B02\nB03\nB04'.splitlines()
['B02', 'B03', 'B04']
```

---

# Joining strings

Use `.join()` to combine strings with a separator. Call it on the separator, not on the list.

## General syntax

```python
separator.join(iterable_of_strings)
```

```python
bands = ['B02', 'B03', 'B04']

','.join(bands)
'B02,B03,B04'

' '.join(bands)
'B02 B03 B04'

''.join(bands)
'B02B03B04'
```

All items must be strings. Convert numbers to strings before joining them.

```python
'-'.join([str(10), str(20)])
'10-20'
```

---

# Processing file names and labels

Split a simple file name, unpack the parts, and join the selected fields.

```python
filename = 'S2_B04_10m.tif'

stem = filename.removesuffix('.tif')

sensor, band, resolution = stem.split('_')

band
'B04'

'_'.join([sensor, band])
'S2_B04'
```

This works for file names with the specified structure. It does not validate arbitrary file names.
