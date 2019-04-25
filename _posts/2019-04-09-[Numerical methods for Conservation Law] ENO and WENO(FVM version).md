---
layout:     post
title:      Numerical methods - ENO and WENO(FVM version)
subtitle:   ENO/WENO 的原理和推导
date:       2019-04-09
author:     Jing
header-img: img/post-bg-CL.png
catalog: true
export_on_save:
html: true
tags:
    - Numerical methods
    - Conservation Law
---


>ENO(Essentially Non-Oscillatory)方法是一类求偏微分方程数值解的高分辨率方法(High-resolution scheme),由[Harten, Engquist, Osher 和 Chakravarthy](https://www.sciencedirect.com/science/article/pii/0021999187900313)在1987年提出. 1994年，[Liu, Chan 和 Osher](https://www.sciencedirect.com/science/article/pii/S0021999184711879?via%3Dihub) 研究了 weighted version of ENO(WENO). In 1996, [Guang-Sh 与 Chi-Wang Shu](https://www.sciencedirect.com/science/article/pii/S0021999196901308) 发展了新的WENO方法并命名为WENO-JS。

### 有限体积法(FVM)简介
Given cell average ${\bar{u}}_j$, compute point values $u_{j+\frac{1}{2}}^-$.

### ENO推导
ENO: adaptively choose stencil to reduce oscillation. Given the cell average Find a $k$-th order accurate estimates for the values of $u(x)$ at the cell boundaries. Particularly the basis of this approximation is formed by polynomials of degree at most k − 1.
#### 1st order
$u_{j+\frac{1}{2}}^- = \bar{u}_j$: 直接用平均值代替点值。
#### 2nd order
在stencil$[\bar{u}_{j-1},\bar{u}_{j}]$或$[\bar{u}_{j},\bar{u}_{j+1}]$上计算 $u_{j+\frac{1}{2}}^-$:
$$u^-_{j+\frac{1}{2}} = ss$$

### WENO推导

**在_includes/head.html中添加:**
```
<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    tex2jax: {
      skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
      inlineMath: [['$','$']]
    }
  });
</script>
```

[Reference](https://stackoverflow.com/questions/26275645/how-to-support-latex-in-github-pages)
