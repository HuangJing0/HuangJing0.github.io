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


>ENO(Essentially Non-Oscillatory)方法是一类求偏微分方程数值解的高分辨率方法(High-resolution scheme)，由[Harten, Engquist, Osher 和 Chakravarthy](https://www.sciencedirect.com/science/article/pii/0021999187900313)在1987年提出. 1994年，[Liu, Chan 和 Osher](https://www.sciencedirect.com/science/article/pii/S0021999184711879?via%3Dihub) 研究了 weighted version of ENO(WENO)。In 1996, [Guang-Sh 与 Chi-Wang Shu](https://www.sciencedirect.com/science/article/pii/S0021999196901308) 发展了新的WENO方法并命名为WENO-JS。

### 有限体积法(FVM)简介


### ENO推导

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
