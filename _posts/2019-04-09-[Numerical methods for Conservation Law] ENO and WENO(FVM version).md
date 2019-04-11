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


>The first ENOENO(Essentially Non-Oscillatory) scheme was developed by Harten, Engquist, Osher and Chakravarthy in [1987](https://www.sciencedirect.com/science/article/pii/0021999187900313). The first weighted version of ENO(WENO) was developed in [1994](https://www.sciencedirect.com/science/article/pii/S0021999184711879?via%3Dihub).

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
