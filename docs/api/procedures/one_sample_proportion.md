---
comments: true
---

# one_sample_proportion

<!-- prettier-ignore-start -->

## Classes

### Alternative

备择假设枚举类。

#### ONE_SIDED

(_str_) : 单侧检验

**Upper**: $H_0: P_1 \leq P_0,\ H_1: P_1 > P_0$

**Lower**: $H_0: P_1 \geq P_0,\ H_1: P_1 < P_0$

#### TWO_SIDED

$H_0: P_1 = P_0,\ H_1: P_1 \neq P_0$

(_str_) : 双侧检验

### TestType

检验类型枚举类。

#### EXACT_TEST

(_str_) : 精确检验

计算公式：

$$
Power_{ET,\ Two-Sided} = \Phi\left( \frac{\sqrt{n}\left( P_0 - P_1 \right) - z_{\alpha / 2} \sqrt{P_0\left( 1 - P_0 \right)}}{\sqrt{P_1\left( 1 - P_1 \right)}} \right)
                        + 1
                        - \Phi\left( \frac{\sqrt{n}\left( P_0 - P_1 \right) + z_{\alpha / 2} \sqrt{P_0\left( 1 - P_0 \right)}}{\sqrt{P_1\left( 1 - P_1 \right)}} \right)
$$

$$
Power_{ET,\ Lower\ One-Sided} = \Phi\left( \frac{\sqrt{n}\left( P_0 - P_1 \right) - z_{\alpha} \sqrt{P_0\left( 1 - P_0 \right)}}{\sqrt{P_1\left( 1 - P_1 \right)}} \right)
$$

$$
Power_{ET,\ Upper\ One-Sided} = 1 - \Phi\left( \frac{\sqrt{n}\left( P_0 - P_1 \right) + z_{\alpha / 2} \sqrt{P_0\left( 1 - P_0 \right)}}{\sqrt{P_1\left( 1 - P_1 \right)}} \right)
$$

#### Z_TEST_USING_S_P0

(_str_) : $Z$ 检验，使用 $S(P_0)$ 作为标准差

计算公式：同 [EXACT_TEST](#exact_test)

#### Z_TEST_USING_S_P0_CC

(_str_) : $Z$ 检验，使用 $S(P_0)$ 作为标准差，使用连续性校正

计算公式：

$$
Power_{ZS\left( P_0 \right)CC,\ Two-Sided} = \Phi\left( \frac{\sqrt{n}\left( P_0 - P_1 \right) - z_{\alpha / 2} \sqrt{P_0\left( 1 - P_0 \right)} - c}{\sqrt{P_1\left( 1 - P_1 \right)}} \right)
                                             + 1
                                             - \Phi\left( \frac{\sqrt{n}\left( P_0 - P_1 \right) + z_{\alpha / 2} \sqrt{P_0\left( 1 - P_0 \right)} + c}{\sqrt{P_1\left( 1 - P_1 \right)}} \right)
$$

其中，

$$
c =
\begin{cases}
\frac{1}{2\sqrt{n}}, & \text{if } \left| P_1 - P_0 \right| \lt \frac{1}{2n} \\
0, & \text{otherwise}
\end{cases}
$$

$$
Power_{ZS\left( P_0 \right)CC,\ Lower\ One-Sided} = \Phi\left( \frac{\sqrt{n}\left( P_0 - P_1 \right) - z_{\alpha} \sqrt{P_0\left( 1 - P_0 \right)} - c}{\sqrt{P_1\left( 1 - P_1 \right)}} \right)
$$

$$
Power_{ZS\left( P_0 \right)CC,\ Upper\ One-Sided} = 1 - \Phi\left( \frac{\sqrt{n}\left( P_0 - P_1 \right) + z_{\alpha} \sqrt{P_0\left( 1 - P_0 \right)} + c}{\sqrt{P_1\left( 1 - P_1 \right)}} \right)
$$

#### Z_TEST_USING_S_PHAT

(_str_): $Z$ 检验，使用 $S(\hat{P})$ 作为标准差

计算公式：

$$
Power_{ZS\left( P_1 \right),\ Two-Sided} = \Phi\left( \frac{\sqrt{n}\left( P_0 - P_1 \right) - z_{\alpha / 2} \sqrt{P_1\left( 1 - P_1 \right)}}{\sqrt{P_1\left( 1 - P_1 \right)}} \right)
                        + 1
                        - \Phi\left( \frac{\sqrt{n}\left( P_0 - P_1 \right) + z_{\alpha / 2} \sqrt{P_1\left( 1 - P_1 \right)}}{\sqrt{P_1\left( 1 - P_1 \right)}} \right)
$$

$$
Power_{ZS\left( P_1 \right),\ Lower\ One-Sided} = \Phi\left( \frac{\sqrt{n}\left( P_0 - P_1 \right) - z_{\alpha} \sqrt{P_1\left( 1 - P_1 \right)}}{\sqrt{P_1\left( 1 - P_1 \right)}} \right)
$$

$$
Power_{ZS\left( P_1 \right),\ Upper\ One-Sided} = 1 - \Phi\left( \frac{\sqrt{n}\left( P_0 - P_1 \right) + z_{\alpha} \sqrt{P_1\left( 1 - P_1 \right)}}{\sqrt{P_1\left( 1 - P_1 \right)}} \right)
$$

#### Z_TEST_USING_S_PHAT_CC

(_str_) : $Z$ 检验，使用 $S(\hat{P})$ 作为标准差，使用连续性校正

计算公式：

$$
Power_{ZS\left( P_1 \right)CC,\ Two-Sided} = \Phi\left( \frac{\sqrt{n}\left( P_0 - P_1 \right) - z_{\alpha / 2} \sqrt{P_1\left( 1 - P_1 \right)} - c }{\sqrt{P_1\left( 1 - P_1 \right)}} \right)
                        + 1
                        - \Phi\left( \frac{\sqrt{n}\left( P_0 - P_1 \right) + z_{\alpha / 2} \sqrt{P_1\left( 1 - P_1 \right)} + c }{\sqrt{P_1\left( 1 - P_1 \right)}} \right)
$$

其中，

$$
c =
\begin{cases}
\frac{1}{2\sqrt{n}}, & \text{if } \left| P_1 - P_0 \right| \lt \frac{1}{2n} \\
0, & \text{otherwise}
\end{cases}
$$

$$
Power_{ZS\left( P_1 \right)CC,\ Lower\ One-Sided} = \Phi\left( \frac{\sqrt{n}\left( P_0 - P_1 \right) - z_{\alpha} \sqrt{P_1\left( 1 - P_1 \right)} - c }{\sqrt{P_1\left( 1 - P_1 \right)}} \right)
$$

$$
Power_{ZS\left( P_1 \right)CC,\ Upper\ One-Sided} = 1 - \Phi\left( \frac{\sqrt{n}\left( P_0 - P_1 \right) + z_{\alpha} \sqrt{P_1\left( 1 - P_1 \right)} + c }{\sqrt{P_1\left( 1 - P_1 \right)}} \right)
$$

### SearchDirection

搜索方向枚举类。

#### LOWER

(_str_) : 向下搜索

#### UPPER

(_str_) : 向上搜索

!!! note
    仅当求解目标为 [nullproportion](#nullproportion) 或 [proportion](#proportion) 时，该枚举类才会起作用。

## Functions

### solve

#### Parameters

##### n

_int_ : 样本量

##### alpha

_float_ : 显著性水平

##### nullproportion

_float_ : 零假设的概率

##### proportion

_float_ : 备择假设的概率

##### alternative

_Alternative_ : 检验方法，可选值为 `'ONE_SIDED'`, `'TWO_SIDED'`

##### test_type

_Test\_Type_ : 检验类型，可选值为 `'EXACT_TEST'`, `'Z_TEST_USING_S_P0'`, `'Z_TEST_USING_S_P0_CC'`, `'Z_TEST_USING_S_PHAT'`, `'Z_TEST_USING_S_PHAT_CC'`

##### search_direction

_Search\_Direction_ : 搜索方向，可选值为 `'LOWER'`, `'UPPER'`

!!! note
    仅当求解目标为 [nullproportion](#nullproportion) 或 [proportion](#proportion) 时，该参数才会起作用。

### Returns

_int_ | _float_ : 目标参数的解

### Examples

#### 计算样本量

```python linenums="1"
from pystatpower.procedures import one_sample_proportion

result = one_sample_proportion.solve(
    n=None,
    alpha=0.05,
    power=0.80,
    nullproportion=0.80,
    proportion=0.95,
)

print(result)
```

#### 计算检验效能

```python linenums="1"
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

#### 计算备择假设的概率

```python linenums="1"
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

<!-- prettier-ignore-end -->
