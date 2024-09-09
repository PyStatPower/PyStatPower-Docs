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

该模块包含一个 `solve` 函数，它可以接受用户传入的 `alpha`，`power`，`p0`，`p1`，`n` 等参数，并返回计算结果。

假设：$\alpha = 0.05, 1-\beta = 0.80, p_0 = 0.80, p_1 = 0.95$，要求计算最小样本量，运行以下代码即可求得结果：

```python
from pystatpower.procedures import one_sample_proportion

result = one_sample_proportion.solve(
    n=None,
    alpha=0.05,
    power=0.80,
    nullproportion=0.80,
    proportion=0.95,
    alternative="two_sided",
    test_type="exact_test",
)

print(result)
```

输出：

```text
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

更多详细用法，请参考 [API 文档](./api/index.md)。
