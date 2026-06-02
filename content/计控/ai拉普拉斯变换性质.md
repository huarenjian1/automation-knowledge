---
math: true
title: ai拉普拉斯变换性质
---

好的，我们来分别推导拉普拉斯变换中的**频移性质**（s 域平移）和**时移性质**（t 域平移）。

---

## 一、频移性质（s 域平移 / 复指数调制）

**定理**：

若

$$ L[f(t)] = F(s) $$

则

$$ L[e^{at}f(t)] = F(s-a) $$

其中 $a$ 可以是实数或复数。

**推导**：

由拉普拉斯变换的定义：

$$ L[e^{at}f(t)] = \int_0^\infty e^{at}f(t)e^{-st}dt $$

将指数合并：

$$ = \int_0^\infty f(t)e^{-(s-a)t}dt $$

根据 $F(s)$ 的定义 $F(s) = \int_0^\infty f(t)e^{-st}dt$，可知上式就是

$$ = F(s-a) $$

**收敛域**：若 $F(s)$ 的收敛域是 $\operatorname{Re}(s) > \sigma_0$，则 $F(s-a)$ 的收敛域是 $\operatorname{Re}(s-a) > \sigma_0$，即 $\operatorname{Re}(s) > \sigma_0 + \operatorname{Re}(a)$。

---

**例子**：

已知 $L[\cos(\omega t)] = \dfrac{s}{s^2+\omega^2}$，求 $L[e^{-2t}\cos(\omega t)]$。

由频移性质，$a = -2$，$F(s) = \dfrac{s}{s^2+\omega^2}$，则

$$ L[e^{-2t}\cos(\omega t)] = F(s+2) = \frac{s+2}{(s+2)^2+\omega^2}. $$

---

## 二、时移性质（t 域平移 / 延迟）

**定理**：

若

$$ L[f(t)] = F(s) $$

则对 $T > 0$，

$$ L[f(t-T) u(t-T)] = e^{-sT}F(s) $$

其中 $u(t)$ 是单位阶跃函数。

**推导**：

由定义：

$$ L[f(t-T) u(t-T)] = \int_0^\infty f(t-T) u(t-T) e^{-st} dt $$

因为 $u(t-T) = 0$ 当 $t < T$，所以：

$$ = \int_T^\infty f(t-T) e^{-st} dt $$

做变量代换 $\tau = t - T$，则 $t = \tau + T$，$dt = d\tau$，当 $t = T$ 时 $\tau = 0$：

$$ = \int_0^\infty f(\tau) e^{-s(\tau+T)} d\tau $$

提取与 $\tau$ 无关的因子 $e^{-sT}$：

$$ = e^{-sT} \int_0^\infty f(\tau) e^{-s\tau} d\tau $$

而积分正是 $F(s)$，所以：

$$ = e^{-sT} F(s) $$

**收敛域**：和 $F(s)$ 相同，因为只是乘了一个 $e^{-sT}$，不改变绝对可积的条件在 $\operatorname{Re}(s)$ 上的要求。

---

**注意**：

- 时移性质必须写成 $f(t-T)u(t-T)$，而不能直接写 $f(t-T)$，因为 $t < T$ 时 $f(t-T)$ 可能被定义，但单边拉普拉斯变换从 $t = 0$ 开始积分，为了体现延迟 $T$ 后信号在 $t < T$ 为零，需要乘上 $u(t-T)$。
- 如果 $f(t)$ 本身就是因果信号，则 $f(t)u(t)$ 是原信号，此时 $f(t-T)u(t-T)$ 表示延迟 $T$ 的同一个因果信号。

---

**例子**：

已知 $L[u(t)] = \dfrac{1}{s}$，则：

$$ L[u(t-3)] = e^{-3s} \cdot \frac{1}{s}. $$

---

## 三、两者对比

| 性质名称 | 时域操作 | s 域效果 | 主要用途 |
|---|---|---|---|
| **频移性质** | $e^{at}f(t)$ | $F(s-a)$ | 调制、衰减/增幅指数因子、求解含 $e^{at}$ 的微分方程 |
| **时移性质** | $f(t-T)u(t-T)$ | $e^{-sT}F(s)$ | 延时系统、分段函数变换、初始条件处理 |

---

这两个性质是拉普拉斯变换在系统分析、电路、控制理论中最基本且常用的工具。