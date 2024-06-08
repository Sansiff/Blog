---
title: CSAPP Chapter 1 A Tour of Computer Systems
typora-root-url: csappchapter1
date: 2024-06-04 20:27:38
categories: CSAPP
tags: CSAPP
mathjax: true
---

## Amdahl's Law

Amdahl‘ Law的主要思想是：当我们对系统的某个部分加速时，其对系统整体性能的影响取决于该部分的重要性和加速程度。假设系统执行某个任务所需时间为$T_{old}$，对占系统运行时间比例为$\alpha$的部分进行优化，并且这个部分的性能提升比例为$k$，则有现在系统执行这个任务所需时间

$T_{new}=(1-\alpha)T_{old}+ \alpha T_{old} / k = T_{old}[(1-\alpha)+\alpha/k]$

优化这个部分对系统的加速比

$S=\frac{1}{1-\alpha+\alpha/k}$

因此，Amdahl's Law的主要观点是：想要显著加速整个系统，必须提升系统中相当大的部分的速度。

## Concurrency & Parallelism

We use the term *concurrency* to refer to the general concept of a system with multiple, simultaneous activities, and the term *parallelism* to refer to the use of concurrency to make a system run faster. 

并发指的是一个同时具有多个活动的系统，并行指的是使用并发来使一个系统运行的更快
