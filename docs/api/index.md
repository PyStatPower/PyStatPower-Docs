# API

## 说明

以下部分模块提供了别名，以简化调用。

<!-- prettier-ignore-start -->
??? note "有关“别名”的解释"
    别名提供了一个更简洁的调用模块的方式，这意味着你可以使用别名引用对应模块，而无需使用完整的模块名称（通常长达十几个字母）。例如，以下两段代码是等价的：
    ```python
    from pystatpower.procedures import one_sample_proportion
    result = one_sample_proportion.solve(
        n=None,
        alpha=0.05,
        power=0.80,
        nullproportion=0.80,
        proportion=0.95,
    )
    ```

    ```python
    from pystatpower.procedures import ospp
    result = ospp.solve(
        n=None,
        alpha=0.05,
        power=0.80,
        nullproportion=0.80,
        proportion=0.95,
    )
    ```
<!-- prettier-ignore-end -->

## 核心模块

| 模块                      | 描述         |
| ------------------------- | ------------ |
| [interval](interval.md)   | 区间类       |
| [exception](exception.md) | 自定义异常类 |

## 实用模块

| 模块                                                           | 别名 | 描述               |
| -------------------------------------------------------------- | ---- | ------------------ |
| [one_sample_proportion](./procedures/one_sample_proportion.md) | ospp | 单样本率差异性检验 |
