---
theme: default
class: text-center
highlighter: shiki
lineNumbers: false
transition: slide-left
aspectRatio: 16/9
favicon: /favicon.ico
title: "Unlocking Complete DataFrame Type Hints with Python 3.11's `TypeVarTuple`"

---

# Unlocking Complete DataFrame Type Hints with Python 3.11's `TypeVarTuple`

### Christopher Ariza
### CTO, Research Affiliates

<style>
h1 {font-size: 1.5em;}
</style>


---

# About Me

<Transform :scale="1.5">
<v-clicks>

CTO at Research Affiliates

Python programmer since 2000

PhD in music composition, professor of music technology

Python for algorithmic composition, computational musicology

Since 2012, builder of financial systems in Python

Creator of StaticFrame, an alternative DataFrame library
</v-clicks>
</Transform>


---

# Type Hints Improve our Code

<Transform :scale="1.5">
<v-clicks>

Increase maintainability

Statically verifiable

</v-clicks>
</Transform>


---

# Generic Containers & Nested Data Structures

<Transform :scale="1.5">
<v-clicks depth="3">

- Types can contain other types
- Generic types permit nested specification
    - `list[str]`
    - `tuple[tuple[int, int], tuple[str, str]]`


</v-clicks>
</Transform>


---

# DataFrames are Nested Data Structures

<Transform :scale="1.5">
<v-clicks depth="3">

- Index and column labels have distinct types
- Data values are typed by column
- << diagram? >>
- Interfaces rely on these types
    - Is the index a string or a date?
    - Are values all floats or integers

</v-clicks>
</Transform>


---

# The Common Approach

<Transform :scale="1.5">


```python
import pandas as pd

def process(f: pd.DataFrame) -> pd.Series: ...
```

</Transform>


---
layout: center
---

# There has to be a better way!


---

# Full Generic DataFrame Specification in StaticFrame

<Transform :scale="1.5">

```python
from typing import Any
from static_frame import Frame, Index, TSeriesAny

def process(f: Frame[   # type of the container
        Any,            # type of the index labels
        Index[np.str_], # type of the column labels
        np.int_,        # type of the first column
        np.str_,        # type of the second column
        np.float64,     # type of the third column
        ]) -> TSeriesAny: ...
```

</Transform>


---

# The Problem of Typing DataFrames

<Transform :scale="1.5">
<v-clicks>

- A DataFrame has a variable number of columns (and thus types)
- Requires a variadic generic: `TypeVarTuple`
- Hierarchical indices also require variadic types
- In-place mutation (as in Pandas) negates static typing
    - Adding columns adds types
    - In-place mutation can change a columnar type
- Static typing benefits from immutability

</v-clicks>
</Transform>

<!--
>>> df = pd.DataFrame([[True, 4], [False, 2]])
>>> df.dtypes.values.tolist()
[dtype('bool'), dtype('int64')]
>>> df[2] = (1.2, 5.3)
>>> df.dtypes.values.tolist()
[dtype('bool'), dtype('int64'), dtype('float64')]
>>> df.iloc[0, 0] = -1
>>> df.dtypes.values.tolist()
[dtype('O'), dtype('int64'), dtype('float64')]
-->


---
layout: center
---
# `TypeVarTuple` in Action


---

# How `TypeVarTuple` Works

<Transform :scale="1.5">
<v-clicks>

Type variables permit specifying component types of a type

Like `TypeVar`, `TypeVarTuple` is used in class definition

Variadic generics permit a variable number of type vars

One `TypeVarTuple` can be mixed with zero or more `TypeVar`

</v-clicks>
</Transform>





---
---
# Thank You

<Transform :scale="1.5">


StaticFrame: https://static-frame.dev
</Transform>
