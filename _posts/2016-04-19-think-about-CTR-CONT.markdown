---
layout: post
title:  "简单聊聊CTR（二）"
date:   2016-04-19 15:30:00 +0800
categories: 业务分析
---

## BETA ##

上次聊过我们CTR计算的一些方法，如果我们把曝光点击行为看作是抛硬币，那么很自然我们就会想到：二项分布以及其共轭先验分布－beta分布。

这里采用一张wiki中使用的图：

![](https://upload.wikimedia.org/wikipedia/commons/f/f3/Beta_distribution_pdf.svg)

可以看到beta分布是个“变形金刚”，在我们场景下使用的时候其实很简单。

### 关心 mean 的含义

    a/(a+b)

如果我们把a看作是点击，b看作是不点击。那么mean就是直接计算的CTR。

### 关心 variance 的含义

方差代表了该分布的取值变化。可以看到当a,b取值比较大的时候，variance会降低，分布会更集中在mean。而当a,b比较小的时候，variance会很大，分布很分散。

有了上面的直观感觉，我们能做什么呢？我们可以认为一个商品的CTR服从beta分布，每次计算商品CTR的时候都从beta分布中抽样一个‘ctr’。这样的疑问是商品的CTR就不再是一个value，而是一个random variable。

这样的做法有什么用呢？

可以考虑和online updating和MAB策略结合做商品CTR等特征／分数的估计，通过实时的用户反馈，更新分布参数。这个思想在实际工作中取得了很好的效果。

下一篇我们讨论position bias ctr calculation。今天就说到这里吧。
