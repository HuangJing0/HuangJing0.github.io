---
layout:     post
title:      Numerical methods - Spectral Method
subtitle:   ENO/WENO 的原理和推导
date:       2019-04-19
author:     Jing
header-img: img/post-bg-CL.png
catalog: true
export_on_save:
html: true
tags:
    - Numerical methods
    - Conservation Law
---


>Spectral method(谱方法)

### 连续变换
<!-- 给定区域均值 -->
$\bar{u}_j$, 计算点值$u_{j+\frac{1}{2}}^-$.

### 间断变换
ENO: adaptively choose stencil to reduce oscillation. Given the cell average Find a $k$-th order accurate estimates for the values of $u(x)$ at the cell boundaries. Particularly the basis of this approximation is formed by polynomials of degree at most $k − 1$.
#### 1st order
$u_{j+\frac{1}{2}}^- = \bar{u}_j$: 直接用平均值代替点值。
#### 2nd order
在stencil$[\bar{u}_{j-1},\bar{u}_{j}]$或$[\bar{u}_{j},\bar{u}_{j+1}]$上计算 $u_{j+\frac{1}{2}}^-$:
\[u^-_{j+\frac{1}{2}} = \]

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
