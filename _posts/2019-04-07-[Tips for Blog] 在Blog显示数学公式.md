---
layout:     post
title:      Tips for Blog - 显示数学公式
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


> 在GitHub Page中显示数学公式

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
