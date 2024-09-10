---
comments: true
---

# 使用

PyStatPower 对于每一种假设检验场景均提供了一个单独的模块用于处理功效分析问题，下面以单组率差异性检验为例介绍如何使用 PyStatPower。

## 试验假设

单组率差异性检验的统计假设为：

\begin{align}
H_0: p_1 = p_2 \\
H_1: p_1 \neq p_2
\end{align}

该统计假设场景中包含的变量如下：

- $\alpha$: 显著性水平
- $1-\beta$: 检验效能，即 power
- $p_0$: 原假设的概率
- $p_1$: 备择假设的概率
- $n$: 样本量

实际应用中，可能会根据其中一些变量的值来求解剩下的变量，例如：试验开始前计算所需的最小样本量、试验结束后计算检验效能、根据参数反推备择假设的概率等。

## 模块调用

对于这个场景，PyStatPower 提供了 `one_sample_proportion` 模块用于功效分析。

该模块包含一个 `solve` 函数，它可以接受用户传入的 `n`，`alpha`，`power`，`p0`，`p1`，等参数，并返回计算结果。

### 计算样本量

假设某次试验开始前，设定参数：$\alpha = 0.05$, $1-\beta = 0.80$, $p_0 = 0.80$, $p_1 = 0.95$，要求计算最小样本量，运行以下代码即可求得结果：

```python linenums="1" hl_lines="4"
from pystatpower.procedures import one_sample_proportion

result = one_sample_proportion.solve(
    n=None,
    alpha=0.05,
    power=0.80,
    nullproportion=0.80, # (1)!
    proportion=0.95,
)

print(result)
```

1. `nullproportion` 为原假设的概率 $p_0$ ，`proportion` 为备择假设的概率 $p_1$ 。

输出：

```text linenums="1"
41.594991602280594
```

实际应用中，需向上取整，得到最小样本量为 42。

如需考虑脱落率，可使用以下公式计算：

$$
n' = \frac{n}{1 - \ell}
$$

其中，$n$ 为不考虑脱落率的样本量，$\ell$ 为脱落率，$n'$ 为考虑脱落率的样本量。

在上述例子中，假设脱落率为 10%，则最终需要的最小样本量为：

$$
n' = \lceil\frac{42}{0.9}\rceil = 47
$$

### 计算检验效能

试验结束后，实际入组 47 例样本，脱落 2 例，43 例样本呈现阳性结果，求本次试验的检验效能。

```python linenums="1" hl_lines="6"
from pystatpower.procedures import one_sample_proportion

result = one_sample_proportion.solve(
    n=45,
    alpha=0.05,
    power=None,
    nullproportion=0.80,
    proportion=43 / 45,
)

print(result)
```

输出：

```text linenums="1"
0.8960352663192755
```

可以看到本次试验的检验效能约为 0.8960，高于试验开始前设定的 0.80。

### 反推备择假设的概率

假设固定样本量 30（不考虑脱落率），试验结束后，阳性结果的概率需达到多少，才能在设定的显著性水平下，仍然达到 0.80 的检验效能？

```python linenums="1" hl_lines="8"
from pystatpower.procedures import one_sample_proportion

result = one_sample_proportion.solve(
    n=30,
    alpha=0.05,
    power=0.80,
    nullproportion=0.80,
    proportion=None,
)

print(result)
```

输出：

```text linenums="1"
0.9695411322879357
```

因此，在设定的显著性水平下，要达到 0.80 的检验效能，阳性结果的概率至少需要达到 97%。

## 更多用法

请参考 [API 文档](./api/index.md)。
