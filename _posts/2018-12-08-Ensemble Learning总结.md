---
layout:     post
title:      Ensemble Learning 总结
subtitle:   对集成学习做一个总结
date:       2018-12-09
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
## Bagging(Bootstrap Aggregating引导聚集算法)：
### Bagging怎么做：
1. 对于由N个样本的训练集Z，有放回的重复取样N次，得到一个新的训练样本集Z’。这样的步骤称为一次bootstrap，共进行B次。
同一个样本可能会被多次采样到，有些样本也可能不被采样到，在Z样本集中只有63.2%的样本被采集到了Z’中。
2. 对于K中的每一个训练集都训练一个predictor
3. 不用特意设置验证集，利用OOB数据就可以进行数据的验证，整个Ensemble的输出是所有predictor的平均值

### 为什么Bagging可以使模型效果更好：
对于每一个Z’，其实它的分布相对于原训练集Z有了一个偏置bias，Z’和Z的分布不一致，但是由于将多个predictor平均到一起，
bias相互抵消了，所以可以认为对Z’做平均后新训练集的数据分布与原来相同；同时，由于average，我们可以降低预测结果的variance，下面具体看一下。
对于每一个数据$$x_0$$的预测误差其实是由三部分组成：
1. label值和real pattern之间的误差（可以认为是一个白噪声）的方差
2. 预测值与真实值的偏差的平方（打靶平均值离靶心的距离）
3. 预测值自己本身的方差（打靶每一次都会偏离中心，偏离中心的分布）

预测值本身的方差：假设所有预测值是随机变量，方差为$$\sigma^2$$，
它们之间不是相互独立，两两之间相关系数为$$\rho$$，
那么它们平均值的方差为$$\rho\sigma^{2}+\frac{1-\rho}{B}\sigma^2$$，由数理统计知识可以求得。
利用Bagging，我们增大了B值，可以减小方差。

## Random Forest(Bagging+Random Select Feature Set)
由上面的分析我们可以知道，在增大bootstrap的次数B的同时，我们可以通过减小数据之间的相关系数$$\rho$$来减小平均值的方差，Random Forest就是利用了这个想法。
Random Forest中的每个模型都是一棵树，为了尽可能将不同的树解耦，减小它们之间的相关性，
我们在每个结点进行分裂时，针对的feature set不是所有的feature，而是对所有&&p&&个feature进行sample后（一般选择&&\sqrt{p}&&个），
在子feature set中选择信息增益（率）最大的feature以及分裂值。

## Stacking
1. 将所有训练数据分为N份，对于前N-1份，训练一个例如SVM，预测第N份数据的label,

## Boosting


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