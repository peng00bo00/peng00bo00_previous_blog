---
layout: article
title: OMSCS-SIM课程笔记01-Whirlwind Tour of Simulation
tags: ["OMSCS", "ISYE6644-SIM"]
key: OMSCS-SIM-01
aside:
  toc: true
sidebar:
  nav: OMSCS-SIM
---

> 这个系列是Gatech OMSCS 仿真和建模课程([ISYE 6644: Simulation and Modeling for Engineering and Science](https://omscs.gatech.edu/isye-6644-simulation-and-modeling-engineering-and-science))的同步课程笔记。课程内容涉及计算机模拟在统计分析和建模中的应用，本节主要介绍计算机模拟的基本概念。
<!--more-->

## Models

目前计算机仿真在各行各业都有大量的应用，要进行计算机仿真我们需要一个**模型(model)**。所谓"模型"是对客观现实世界某个过程的抽象，根据过程的特点我们可以把模型分为离散和连续模型(discrete vs. continuous)、随机和确定模型(stochastic vs. deterministic)以及动态和静态模型(dynamic vs. static)。在本课程中我们会重点关注**离散、随机而且动态**的模型。

同时要求解一个模型可以考虑使用**解析解(analytic methods)**、**数值解(numerical methods)**或是**仿真解(simulation methods)**等不同方法。对于确定性的模型，解析解和数值解都有非常多的应用。但对于有随机性的模型则只能通过仿真的方式进行求解。

## Simulation

计算机仿真是对现实世界某个过程进行模拟，对于动态的系统还往往需要生成人工的历史数据才能进行后面的推断。目前计算机仿真在工业工程、运筹学、管理科学等领域都有着重要的应用。研究者和管理人员会通过计算机仿真来求解复杂系统下的各种问题。

和传统方法相比，计算机仿真更便于去回答各种"如果"问题，因此它在系统设计和优化中有着大量的应用。当然计算机仿真也具有一些缺陷，比如说对系统进行建模往往不是那么的容易，而且仿真过程一般会比较费时，更重要的是仿真的结果都具有随机性，如何去理解和解释仿真的结果对于解答生产生活中的问题是十分重要的。