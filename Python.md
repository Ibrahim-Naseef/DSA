# Python Methods Reference: Strings, Arrays, List, Tuple, Set, Dict

A quick-lookup guide for every built-in method, with what it does, an example, and the result.
Written as prep before starting patterns and DSA in Python.

## Table of Contents

1. [Strings](#1-strings)
2. [Arrays (`array` module)](#2-arrays-array-module)
3. [List](#3-list)
4. [Tuple](#4-tuple)
5. [Set](#5-set)
6. [Dictionary](#6-dictionary)
7. [collections helpers](#7-collections-helpers-dsa-favorites)
8. [Comparison and time complexity](#8-comparison-and-time-complexity)
9. [Common pitfalls](#9-common-pitfalls)

---

## 1. Strings

Strings are **immutable**. Every method returns a **new** string and never changes the original.

### 1.1 Case methods

| Method | What it does | Example | Output |
|---|---|---|---|
| `upper()` | All characters to uppercase | `"hello".upper()` | `'HELLO'` |
| `lower()` | All characters to lowercase | `"HeLLo".lower()` | `'hello'` |
| `capitalize()` | First char upper, rest lower | `"hELLO wORLD".capitalize()` | `'Hello world'` |
| `title()` | First letter of every word upper | `"hello world".title()` | `'Hello World'` |
| `swapcase()` | Flips the case of each char | `"Hello".swapcase()` | `'hELLO'` |
| `casefold()` | Aggressive lowercase for case-insensitive compare | `"Straße".casefold()` | `'strasse'` |

### 1.2 Search methods

| Method | What it does | Example | Output |
|---|---|---|---|
| `find(sub, start, end)` | First index of `sub`, `-1` if missing | `"banana".find("an")` | `1` |
| `rfind(sub, start, end)` | Last index of `sub`, `-1` if missing | `"banana".rfind("an")` | `3` |
| `index(sub, start, end)` | Like `find`, but raises `ValueError` if missing | `"banana".index("z")` | `ValueError` |
| `rindex(sub, start, end)` | Like `rfind`, but raises `ValueError` if missing | `"banana".rindex("a")` | `5` |
| `count(sub, start, end)` | Number of non-overlapping occurrences | `"banana".count("a")` | `3` |
| `startswith(prefix)` | True if string starts with prefix (tuple allowed) | `"banana".startswith(("x","ba"))` | `True` |
| `endswith(suffix)` | True if string ends with suffix (tuple allowed) | `"banana".endswith("na")` | `True` |

### 1.3 Check methods (return `True` / `False`)

All of these return `False` for an empty string.

| Method | What it checks | Example | Output |
|---|---|---|---|
| `isalpha()` | Only letters | `"abc".isalpha()` | `True` |
| `isdigit()` | Only digits (includes superscripts like `²`) | `"123".isdigit()` | `True` |
| `isdecimal()` | Only decimal digits 0-9 style chars (strictest) | `"²".isdecimal()` | `False` |
| `isnumeric()` | Digits, fractions, roman numerals (widest) | `"½".isnumeric()` | `True` |
| `isalnum()` | Only letters or digits | `"abc123".isalnum()` | `True` |
| `isspace()` | Only whitespace (space, tab, newline) | `" \t\n".isspace()` | `True` |
| `isupper()` | All cased chars uppercase (needs at least one) | `"AB1".isupper()` | `True` |
| `islower()` | All cased chars lowercase (needs at least one) | `"ab1".islower()` | `True` |
| `istitle()` | Every word starts with a capital | `"Hello World".istitle()` | `True` |
| `isidentifier()` | Valid Python variable name | `"my_var".isidentifier()` | `True` |
| `isprintable()` | No non-printable chars like `\n` | `"a\nb".isprintable()` | `False` |
| `isascii()` | All chars in ASCII range 0-127 | `"café".isascii()` | `False` |

Hierarchy: `isdecimal` is a subset of `isdigit`, which is a subset of `isnumeric`.

### 1.4 Modify methods

| Method | What it does | Example | Output |
|---|---|---|---|
| `replace(old, new, count)` | Replaces occurrences of `old` with `new` | `"hello".replace("l","L")` | `'heLLo'` |
| `replace` with count | Replace only the first N | `"hello".replace("l","L",1)` | `'heLlo'` |
| `strip(chars)` | Removes chars from both ends (default whitespace) | `"  hi  ".strip()` | `'hi'` |
| `lstrip(chars)` | Removes from the left end only | `"xxhi".lstrip("x")` | `'hi'` |
| `rstrip(chars)` | Removes from the right end only | `"hixx".rstrip("x")` | `'hi'` |
| `removeprefix(p)` | Removes exact prefix once (3.9+) | `"test_a".removeprefix("test_")` | `'a'` |
| `removesuffix(s)` | Removes exact suffix once (3.9+) | `"a.py".removesuffix(".py")` | `'a'` |
| `maketrans(...)` | Builds a translation table (static method) | `str.maketrans("abc","123")` | `{97:49, 98:50, 99:51}` |
| `translate(table)` | Maps/deletes chars using a table | `"aabbcc".translate(str.maketrans("abc","123"))` | `'112233'` |
| `translate` (delete) | Third arg of `maketrans` deletes chars | `"education".translate(str.maketrans("","","aeiou"))` | `'dctn'` |

Note: `strip("abc")` treats the argument as a **set of characters**, not a substring. `removeprefix("abc")` removes the exact string once.

### 1.5 Split and join methods

| Method | What it does | Example | Output |
|---|---|---|---|
| `split(sep, maxsplit)` | Splits into a list (no arg: any whitespace) | `"a b  c".split()` | `['a','b','c']` |
| `split(sep)` | Split on a given separator | `"a,b,c".split(",")` | `['a','b','c']` |
| `split(sep, n)` | Limit number of splits | `"a,b,c,d".split(",",2)` | `['a','b','c,d']` |
| `rsplit(sep, n)` | Same as split but from the right | `"a,b,c,d".rsplit(",",1)` | `['a,b,c','d']` |
| `splitlines()` | Splits on line breaks | `"l1\nl2\r\nl3".splitlines()` | `['l1','l2','l3']` |
| `partition(sep)` | 3-tuple split at the **first** sep | `"k=v=x".partition("=")` | `('k','=','v=x')` |
| `rpartition(sep)` | 3-tuple split at the **last** sep | `"a/b/c.txt".rpartition("/")` | `('a/b','/','c.txt')` |
| `join(iterable)` | Joins strings using the string as separator | `"-".join(["a","b","c"])` | `'a-b-c'` |

Items passed to `join` must be strings: `",".join(str(x) for x in [1,2,3])`.

### 1.6 Align and pad methods

| Method | What it does | Example | Output |
|---|---|---|---|
| `center(w, fill)` | Centers in width `w` | `"hi".center(8,"*")` | `'***hi***'` |
| `ljust(w, fill)` | Left-aligns, pads on the right | `"hi".ljust(5,".")` | `'hi...'` |
| `rjust(w, fill)` | Right-aligns, pads on the left | `"hi".rjust(5,".")` | `'...hi'` |
| `zfill(w)` | Pads with zeros on the left (keeps sign) | `"-42".zfill(5)` | `'-0042'` |
| `expandtabs(n)` | Replaces tabs with spaces (tab size n) | `"a\tb".expandtabs(4)` | `'a   b'` |

If `w` is smaller than the string length, nothing is truncated.


---

## 2. Arrays (`array` module)

Python has no built-in array type. In DSA, a **list** is used as the array. The `array` module gives typed, memory-efficient arrays.

```python
from array import array
a = array('i', [1, 2, 3])
```

Type codes: `'i'` int, `'f'` float, `'d'` double, `'u'` unicode char, `'b'` signed byte, `'l'` long.

| Method / Attribute | What it does | Example | Result |
|---|---|---|---|
| `append(x)` | Add one item at end | `a.append(4)` | `array('i',[1,2,3,4])` |
| `extend(iter)` | Add all items from iterable | `a.extend([5,6])` | `[1,2,3,4,5,6]` |
| `insert(i, x)` | Insert before index `i` | `a.insert(1, 10)` | `[1,10,2,3]` |
| `remove(x)` | Remove first occurrence | `a.remove(10)` | `[1,2,3]` |
| `pop(i)` | Remove and return (default last) | `a.pop()` | `3` |
| `index(x)` | First index of `x` | `a.index(2)` | `1` |
| `count(x)` | Occurrences of `x` | `a.count(2)` | `1` |
| `reverse()` | Reverse in place | `a.reverse()` | `[3,2,1]` |
| `fromlist(list)` | Append items from a list | `a.fromlist([7,8])` | `[1,2,3,7,8]` |
| `tolist()` | Convert to a list | `a.tolist()` | `[1,2,3]` |
| `tobytes()` | Convert to raw bytes | `a.tobytes()` | `b'\x01\x00...'` |
| `frombytes(b)` | Append items from bytes | `a.frombytes(b)` | extends array |
| `byteswap()` | Swap byte order of each item | `a.byteswap()` | in place |
| `buffer_info()` | (memory address, length) | `a.buffer_info()` | `(addr, 3)` |
| `typecode` | Type code attribute | `a.typecode` | `'i'` |
| `itemsize` | Bytes per item | `a.itemsize` | `4` |
| `fromfile` / `tofile` | Read/write to a binary file | `a.tofile(f)` | writes bytes |
| `fromunicode` / `tounicode` | For `'u'` arrays, convert to/from str | `a.tounicode()` | `'abc'` |

### 2D array (matrix using lists)

| Task | Code | Note |
|---|---|---|
| Create `r x c` zero matrix | `[[0]*c for _ in range(r)]` | Correct way |
| Wrong way | `[[0]*c]*r` | All rows share the same list |
| Access | `mat[i][j]` | Row `i`, column `j` |
| Dimensions | `len(mat), len(mat[0])` | rows, cols |
| Transpose | `list(zip(*mat))` | Rows become columns |
| Flatten | `[x for row in mat for x in row]` | 1D list |

---

## 3. List

Mutable, ordered, allows duplicates. Syntax: `[]`.

### 3.1 All 11 methods

| Method | What it does | Example | Result |
|---|---|---|---|
| `append(x)` | Adds one item at the end | `L=[1,2]; L.append(3)` | `[1,2,3]` |
| `extend(iter)` | Adds each item of an iterable | `L=[1,2]; L.extend([3,4])` | `[1,2,3,4]` |
| `insert(i, x)` | Inserts `x` before index `i` | `L=[1,3]; L.insert(1,2)` | `[1,2,3]` |
| `remove(x)` | Removes first occurrence (`ValueError` if absent) | `L=[1,2,2]; L.remove(2)` | `[1,2]` |
| `pop(i)` | Removes and returns item (default last) | `L=[1,2,3]; L.pop()` | returns `3`, `L=[1,2]` |
| `clear()` | Removes all items | `L.clear()` | `[]` |
| `index(x, start, end)` | First index of `x` (`ValueError` if absent) | `[5,6,7].index(6)` | `1` |
| `count(x)` | Number of occurrences | `[1,2,2].count(2)` | `2` |
| `sort(key, reverse)` | Sorts in place, returns `None`, stable | `L=[3,1,2]; L.sort()` | `[1,2,3]` |
| `reverse()` | Reverses in place | `L=[1,2,3]; L.reverse()` | `[3,2,1]` |
| `copy()` | Shallow copy | `B = A.copy()` | new list |

### 3.2 Indexing, slicing, operators

| Operation | Example | Result |
|---|---|---|
| Index | `[10,20,30][0]` | `10` |
| Negative index | `[10,20,30][-1]` | `30` |
| Slice | `[10,20,30,40][1:3]` | `[20,30]` |
| Step slice | `[1,2,3,4,5][::2]` | `[1,3,5]` |
| Reverse slice | `[1,2,3][::-1]` | `[3,2,1]` |
| Concatenate | `[1]+[2]` | `[1,2]` |
| Repeat | `[0]*3` | `[0,0,0]` |
| Membership | `2 in [1,2,3]` | `True` |
| Slice assign | `L=[1,2,3,4]; L[1:3]=[9]` | `[1,9,4]` |
| Delete | `del L[0]` / `del L[1:3]` | removes item(s) |
| Unpack | `a,*rest = [1,2,3]` | `a=1, rest=[2,3]` |
| Swap | `a, b = b, a` | swapped |

### 3.3 Built-in functions used with lists

| Function | What it does | Example | Result |
|---|---|---|---|
| `len(L)` | Number of items | `len([1,2,3])` | `3` |
| `min(L)` / `max(L)` | Smallest / largest | `max([1,5,3])` | `5` |
| `sum(L)` | Total | `sum([1,2,3])` | `6` |
| `sorted(L)` | **New** sorted list | `sorted([3,1,2])` | `[1,2,3]` |
| `sorted(L, key=, reverse=)` | Custom sort | `sorted(["bb","a"], key=len)` | `['a','bb']` |
| `reversed(L)` | Reverse iterator | `list(reversed([1,2,3]))` | `[3,2,1]` |
| `enumerate(L)` | (index, value) pairs | `list(enumerate("ab"))` | `[(0,'a'),(1,'b')]` |
| `zip(A, B)` | Pairs items together | `list(zip([1,2],"ab"))` | `[(1,'a'),(2,'b')]` |
| `any(L)` / `all(L)` | At least one / every truthy | `any([0,1])` | `True` |
| `map(f, L)` | Apply function to each | `list(map(str,[1,2]))` | `['1','2']` |
| `filter(f, L)` | Keep where `f` is true | `list(filter(None,[0,1,2]))` | `[1,2]` |

### 3.4 Comprehensions

| Type | Example | Result |
|---|---|---|
| Basic | `[x*x for x in range(4)]` | `[0,1,4,9]` |
| With condition | `[x for x in range(6) if x%2==0]` | `[0,2,4]` |
| If-else | `["e" if x%2==0 else "o" for x in range(3)]` | `['e','o','e']` |
| Nested | `[[0]*3 for _ in range(2)]` | `[[0,0,0],[0,0,0]]` |

---

## 4. Tuple

Immutable, ordered, allows duplicates. Syntax: `()`. A single-item tuple needs a comma: `(5,)`.

### 4.1 Methods (only 2)

| Method | What it does | Example | Result |
|---|---|---|---|
| `count(x)` | Number of occurrences | `(1,2,2).count(2)` | `2` |
| `index(x, start, end)` | First index (`ValueError` if absent) | `(10,20,30).index(20)` | `1` |

### 4.2 Operations

| Operation | Example | Result |
|---|---|---|
| Index / slice | `(1,2,3)[1:]` | `(2,3)` |
| Concatenate | `(1,2)+(3,)` | `(1,2,3)` |
| Repeat | `(0,)*3` | `(0,0,0)` |
| Unpack | `a,b,c = (1,2,3)` | `a=1,b=2,c=3` |
| Star unpack | `a,*r = (1,2,3)` | `a=1, r=[2,3]` |
| Convert | `tuple([1,2])` / `list((1,2))` | `(1,2)` / `[1,2]` |
| Compare | `(1,2) < (1,3)` | `True` (lexicographic) |
| Assign item | `t[0] = 5` | `TypeError` |

### 4.3 Why use a tuple

| Use | Example |
|---|---|
| Return multiple values | `return min(a), max(a)` |
| Dict key (hashable) | `d[(row, col)] = "x"` |
| Set of coordinates | `visited = {(0,0), (0,1)}` |
| Fixed, safe data | `DAYS = ("Mon","Tue")` |

### 4.4 namedtuple (bonus)

```python
from collections import namedtuple
P = namedtuple("P", ["x", "y"])
p = P(1, 2)
```

| Feature | Example | Result |
|---|---|---|
| Access by name | `p.x` | `1` |
| Access by index | `p[1]` | `2` |
| To dict | `p._asdict()` | `{'x':1,'y':2}` |
| Copy with change | `p._replace(x=10)` | `P(x=10,y=2)` |

---

## 5. Set

Mutable, unordered, unique items only, items must be hashable. Syntax: `{1,2}`. An empty set is `set()`, because `{}` is an empty dict.

### 5.1 All 17 methods

| Method | What it does | Example | Result |
|---|---|---|---|
| `add(x)` | Adds one item | `s={1}; s.add(2)` | `{1,2}` |
| `update(*iters)` | Adds all items from iterables | `s={1}; s.update([2,3])` | `{1,2,3}` |
| `remove(x)` | Removes `x` (`KeyError` if absent) | `{1,2}.remove(2)` | `{1}` |
| `discard(x)` | Removes `x`, no error if absent | `{1,2}.discard(9)` | `{1,2}` |
| `pop()` | Removes and returns an arbitrary item | `{1,2}.pop()` | `1` (arbitrary) |
| `clear()` | Removes all items | `s.clear()` | `set()` |
| `copy()` | Shallow copy | `s.copy()` | new set |
| `union(*o)` | Items in either | `{1,2}.union({2,3})` | `{1,2,3}` |
| `intersection(*o)` | Items in both | `{1,2}.intersection({2,3})` | `{2}` |
| `difference(*o)` | Items in first, not in others | `{1,2}.difference({2,3})` | `{1}` |
| `symmetric_difference(o)` | Items in exactly one | `{1,2}.symmetric_difference({2,3})` | `{1,3}` |
| `update` / `intersection_update` | In-place intersection | `a.intersection_update(b)` | `a` becomes `a & b` |
| `difference_update(o)` | In-place difference | `a.difference_update(b)` | `a` becomes `a - b` |
| `symmetric_difference_update(o)` | In-place symmetric difference | `a.symmetric_difference_update(b)` | `a` becomes `a ^ b` |
| `issubset(o)` | All items of self in `o` | `{1}.issubset({1,2})` | `True` |
| `issuperset(o)` | Self contains all of `o` | `{1,2}.issuperset({1})` | `True` |
| `isdisjoint(o)` | No items in common | `{1}.isdisjoint({2})` | `True` |

### 5.2 Operator equivalents

| Operator | Same as | Meaning |
|---|---|---|
| `a \| b` | `a.union(b)` | Union |
| `a & b` | `a.intersection(b)` | Intersection |
| `a - b` | `a.difference(b)` | Difference |
| `a ^ b` | `a.symmetric_difference(b)` | Symmetric difference |
| `a <= b` | `a.issubset(b)` | Subset |
| `a < b` | none | Proper subset |
| `a >= b` | `a.issuperset(b)` | Superset |
| `a \|= b` | `a.update(b)` | In-place union |
| `a &= b` | `a.intersection_update(b)` | In-place intersection |

Methods accept any iterable (`a.union([1,2])`), while operators need both sides to be sets.

### 5.3 Common uses

| Task | Code |
|---|---|
| Remove duplicates | `list(set(L))` (order lost) |
| Remove duplicates keeping order | `list(dict.fromkeys(L))` |
| Has duplicates? | `len(set(L)) != len(L)` |
| Fast membership | `x in s` is O(1) |
| Common elements | `set(A) & set(B)` |
| Immutable set | `frozenset([1,2,3])` (hashable, can be a dict key) |

---

## 6. Dictionary

Key to value mapping. Keys are unique and hashable, insertion-ordered (3.7+). Syntax: `{k: v}`.

### 6.1 All 11 methods

| Method | What it does | Example | Result |
|---|---|---|---|
| `get(k, default)` | Value for `k`, or default (no error) | `{"a":1}.get("z", 0)` | `0` |
| `keys()` | View of all keys | `{"a":1}.keys()` | `dict_keys(['a'])` |
| `values()` | View of all values | `{"a":1}.values()` | `dict_values([1])` |
| `items()` | View of `(key, value)` pairs | `{"a":1}.items()` | `dict_items([('a',1)])` |
| `update(other)` | Merges, overwriting existing keys | `d={"a":1}; d.update({"a":9,"b":2})` | `{'a':9,'b':2}` |
| `pop(k, default)` | Removes key, returns value | `{"a":1}.pop("a")` | `1` |
| `popitem()` | Removes and returns last inserted pair | `{"a":1,"b":2}.popitem()` | `('b',2)` |
| `setdefault(k, default)` | Returns `d[k]`, inserts default if missing | `d={}; d.setdefault("x",[]).append(1)` | `{'x':[1]}` |
| `clear()` | Removes all items | `d.clear()` | `{}` |
| `copy()` | Shallow copy | `d.copy()` | new dict |
| `dict.fromkeys(keys, val)` | New dict with the same value for all keys | `dict.fromkeys("ab", 0)` | `{'a':0,'b':0}` |

`fromkeys(keys, [])` shares **one** list across all keys. Use a comprehension for separate lists.

### 6.2 Basic operations

| Operation | Example | Result |
|---|---|---|
| Create | `dict(a=1, b=2)` | `{'a':1,'b':2}` |
| From pairs | `dict(zip("ab",[1,2]))` | `{'a':1,'b':2}` |
| Comprehension | `{x: x*x for x in range(3)}` | `{0:0,1:1,2:4}` |
| Access | `d["a"]` | value (`KeyError` if missing) |
| Add / update | `d["c"] = 3` | adds or overwrites |
| Delete | `del d["a"]` | `KeyError` if missing |
| Membership | `"a" in d` | checks **keys** |
| Length | `len(d)` | number of pairs |
| Merge (3.9+) | `d1 \| d2` | new dict, `d2` wins |
| In-place merge | `d1 \|= d2` | updates `d1` |
| Old-style merge | `{**d1, **d2}` | new dict |

### 6.3 Iteration

| Goal | Code |
|---|---|
| Keys | `for k in d:` |
| Values | `for v in d.values():` |
| Key and value | `for k, v in d.items():` |
| With index | `for i, (k, v) in enumerate(d.items()):` |
| Sorted by key | `for k in sorted(d):` |
| Safe delete while looping | `for k in list(d): del d[k]` |

Changing dict size while iterating it raises `RuntimeError`.

### 6.4 Sorting and finding

| Task | Code | Result for `d={"a":3,"b":1,"c":2}` |
|---|---|---|
| Sort by value ascending | `sorted(d.items(), key=lambda x: x[1])` | `[('b',1),('c',2),('a',3)]` |
| Sort by value descending | `sorted(d.items(), key=lambda x: x[1], reverse=True)` | `[('a',3),('c',2),('b',1)]` |
| Back to dict | `dict(sorted(d.items(), key=lambda x: x[1]))` | `{'b':1,'c':2,'a':3}` |
| Key with max value | `max(d, key=d.get)` | `'a'` |
| Minimum value | `min(d.values())` | `1` |
| Invert | `{v: k for k, v in d.items()}` | `{3:'a',1:'b',2:'c'}` |

### 6.5 Frequency count and grouping

```python
s = "hello"

# Manual
freq = {}
for ch in s:
    freq[ch] = freq.get(ch, 0) + 1      # {'h':1,'e':1,'l':2,'o':1}

# Group words by length
groups = {}
for w in ["hi", "yo", "hey"]:
    groups.setdefault(len(w), []).append(w)   # {2:['hi','yo'],3:['hey']}
```

### 6.6 Nested dict

```python
data = {"ravi": {"age": 27, "skills": ["py", "sql"]}}
data["ravi"]["skills"][0]            # 'py'
data.get("amit", {}).get("age")      # None (safe chain)
```

---

## 7. collections helpers (DSA favorites)

```python
from collections import Counter, defaultdict, deque
```

| Tool | What it does | Example | Result |
|---|---|---|---|
| `Counter(iter)` | Frequency dict | `Counter("hello")` | `Counter({'l':2,'h':1,'e':1,'o':1})` |
| `Counter.most_common(n)` | Top `n` by count | `Counter("hello").most_common(1)` | `[('l',2)]` |
| `Counter[x]` for missing | Returns 0, no `KeyError` | `Counter("a")["z"]` | `0` |
| `defaultdict(list)` | Missing key auto-creates `[]` | `dd=defaultdict(list); dd["a"].append(1)` | `{'a':[1]}` |
| `defaultdict(int)` | Missing key auto-creates `0` | `dd=defaultdict(int); dd["x"]+=1` | `{'x':1}` |
| `deque()` | Fast queue, O(1) at both ends | `q=deque([1,2]); q.append(3)` | `deque([1,2,3])` |
| `deque.popleft()` | Remove from front in O(1) | `q.popleft()` | `1` |
| `deque.appendleft(x)` | Add to front in O(1) | `q.appendleft(0)` | `deque([0,2,3])` |

Use `deque` for queues and BFS. Do **not** use `list.pop(0)`, which is O(n).

---

## 8. Comparison and time complexity

### 8.1 Feature comparison

| Feature | str | list | tuple | set | dict |
|---|---|---|---|---|---|
| Syntax | `""` | `[]` | `()` | `{1,2}` | `{k:v}` |
| Mutable | No | Yes | No | Yes | Yes |
| Ordered | Yes | Yes | Yes | No | Yes (insertion) |
| Duplicates | Yes | Yes | Yes | No | Keys no |
| Indexing | Yes | Yes | Yes | No | By key |
| Hashable (can be a key) | Yes | No | Yes | No | No |
| Public methods | 47 | 11 | 2 | 17 | 11 |

### 8.2 Time complexity

| Operation | list | set | dict |
|---|---|---|---|
| Access by index / key | O(1) | n/a | O(1) |
| `x in` (search) | **O(n)** | **O(1)** | **O(1)** |
| append / add / set | O(1) | O(1) | O(1) |
| pop last | O(1) | O(1) | O(1) |
| `pop(0)` / `insert(0, x)` | **O(n)** | n/a | n/a |
| `remove(x)` / delete | O(n) | O(1) | O(1) |
| sort | O(n log n) | n/a | n/a |
| slice | O(k) | n/a | n/a |
| copy | O(n) | O(n) | O(n) |

String notes: concatenating with `+=` in a loop is O(n²). Build a list and use `"".join(parts)` instead.

---

## 9. Common pitfalls

| Pitfall | Wrong | Right |
|---|---|---|
| Sorting returns `None` | `L = L.sort()` | `L.sort()` or `L = sorted(L)` |
| 2D list shared rows | `[[0]*3]*3` | `[[0]*3 for _ in range(3)]` |
| Assignment is not a copy | `B = A` | `B = A.copy()` or `A[:]` |
| Nested copy is shallow | `A.copy()` | `copy.deepcopy(A)` |
| One-item tuple | `(5)` is an int | `(5,)` |
| Empty set | `{}` is a dict | `set()` |
| Missing key | `d["x"]` raises `KeyError` | `d.get("x", 0)` |
| Mutating while iterating | `for x in L: L.remove(x)` | Iterate over a copy `for x in L[:]` |
| Mutable default arg | `def f(a=[])` | `def f(a=None): a = a or []` |
| `strip` is a char set | `"abcHI".lstrip("abc")` removes any of a, b, c | Use `removeprefix` for an exact prefix |
| `fromkeys` shared value | `dict.fromkeys(k, [])` | `{x: [] for x in k}` |
| String is immutable | `s[0] = "x"` raises `TypeError` | `s = "x" + s[1:]` |
| `x in list` inside a loop | O(n²) | Convert to `set` first |

---

## Practice order

1. Run every example in this README yourself.
2. Patterns: stars, then numbers, then alphabets, then hollow shapes, then diamond.
3. String problems: reverse, palindrome, anagram, vowel count, first non-repeating char.
4. List and dict problems: remove duplicates, second largest, rotate, Two Sum, group anagrams.
5. DSA: arrays, hashing, two pointers, recursion, sorting, linked list, stack/queue, trees, graphs, DP.
