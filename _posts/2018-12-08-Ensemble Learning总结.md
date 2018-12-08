---
layout:     post
title:      Ensemble Learning 总结
subtitle:   对集成学习做一个总结
date:       2018-12-08
author:     BS
header-img: img/post-bg-hacker.jpg
catalog: true
tags:
    - Machine Learning
    - Ensemble Learning
---


> “昨夜西风凋碧树。独上高楼，望尽天涯路。”
> 
> [我的博客](http://bishengsjtu.github.io)
>
> 

# 为什么要进行集成学习？
我们知道，不同的模型有着不同的优缺点：预测能力，预测效果，和一些其它不同的特点。
如果我们得到了一系列predictor set $$\lbrace\cal{f_1,...,f_n}\rbrace$$，如何将最终的预测效果进行提升呢，就要进行集成学习。
集成学习有如下优势：
- 1.可以利用投票的方式减小预测误差，前提是每一个predictor的预测能力已经较好，ensemble往往能进一步提升预测效果
- 2.在数据空间的不同区域可以用不同predictor进行预测

简单的集成学习方法：
- Averaging，取模型的平均
- Weighted Averaging，取模型加权平均
- Gating，加权平均，权值是由输入特征通过学习得到，注意：利用梯度下降更新权值时，模型参数不会改变
- Multi Layer，利用神经网络进行Ensemble
- Tree Model，利用树模型进行Ensemble

# 集成学习：**Diversity For Ensemble Input Is Important!**
映射的pattern可能很复杂$$\mapsto$$需要我们尝试的模型具有Diversity
可能会出现过拟合的情况$$\mapsto$$需要我们输入的Trainning Set具有Diversity
输入的数据可能会有噪声$$\mapsto$$需要我们选择的Feature Set具有Diversity

# 集成学习的主要方法
- Bagging(Bootstrap Aggregating)



<head>
    <script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
    <script type="text/x-mathjax-config">
        MathJax.Hub.Config({
            tex2jax: {
            skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
            inlineMath: [['$','$']]
            }
        });
    </script>
</head>