---
comments: true
---

# Interval

定义一个区间，可指定是否包含上下限，不支持单点区间（例如：[1, 1]）。

`Interval` 是一个不可变的数据类，这意味着一旦实例化一个区间，就不能再修改区间的大小和边界。

## Parameters

<!-- prettier-ignore-start -->

### lower

_Any_ : 区间下限

### upper

_Any_ : 区间上限

### lower_inclusive

_bool_ : 是否包含区间下限

### upper_inclusive

_bool_ : 是否包含区间上限

<!-- prettier-ignore-end -->

## Methods

### pseudo_lbound

(_eps_ : _float_ = 1e-10) -> _int_ | _float_

返回区间的伪下界，用于数值计算。

```python linenums="1"
>>> Interval(0, 1).pseudo_lbound()
1e-10
```

### pseudo_ubound

(_eps_ : _float_ = 1e-10) -> _int_ | _float_

返回区间的伪上界，用于数值计算。

```python linenums="1"
>>> Interval(0, 1).pseudo_ubound()
0.9999999999
```

### pseudo_bound

(_eps_ : _float_ = 1e-10) -> _int_ | _float_

返回区间的伪上下界，用于数值计算。

```python linenums="1"
>>> Interval(0, 1).pseudo_bound()
(1e-10, 0.9999999999)
```

### \_\_contains\_\_

(_value_: _int_|_float_) -> _bool_

判断给定的值是否在区间内。

```python linenums="1"
>>> interval = Interval(0, 1, lower_inclusive=True, upper_inclusive=False)
>>> 0.5 in interval
True
>>> 1 in interval
False
>>> 0 in interval
False
```

### \_\_eq\_\_

(_value_: _int_|_float_) -> _bool_

判断两个区间是否相等。

```python linenums="1"
>>> Interval(0, 1) == Interval(0, 1)
True
>>> Interval(0, 1) == Interval(1, 2)
False
>>> Interval(0, 1) == Interval(0, 1, lower_inclusive=False)
False
>>> Interval(0, 1) == Interval(0, 1, upper_inclusive=False)
False
```

### \_\_repr\_\_

() -> _str_

返回区间的表示形式。

```python linenums="1"
>>> Interval(0, 1, lower_inclusive=True, upper_inclusive=False)
[0, 1)
```
