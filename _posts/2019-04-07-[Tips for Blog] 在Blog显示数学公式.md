---
layout:     post
title:      Tips - 在Blog中显示数学公式
subtitle:   让GitHub Page支持Latex公式
date:       2019-04-07
author:     Jing
header-img: img/post-bg-tips.jpg
catalog: true
export_on_save:
html: true
tags:
    - Tips
---


>在博客中显示数学公式

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
**或者：**
```
<script type="text/javascript" src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"> </script>
 <script type="text/x-mathjax-config">
   MathJax.Hub.Config({
     tex2jax: {
       inlineMath: [['$','$'], ['\\(','\\)']],
       displayMath: [['$$','$$'], ['\[','\]']],
       processEscapes: true,
       processEnvironments: true,
       skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
       TeX: { equationNumbers: { autoNumber: "AMS" },
       extensions: ["AMSmath.js", "AMSsymbols.js"] } } });
  </script>
```

[Reference](https://stackoverflow.com/questions/26275645/how-to-support-latex-in-github-pages)
