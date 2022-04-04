---
layout: article
title: OMSCS-DL课程笔记18-Unsupervised and Semi-Supervised Learning
tags: ["OMSCS", "CS7643-DL"]
key: OMSCS-DL-18
aside:
  toc: true
sidebar:
  nav: OMSCS-DL
---

> 这个系列是Gatech OMSCS 深度学习课程([CS 7643: Deep Learning](https://omscs.gatech.edu/cs-7643-deep-learning))的同步课程笔记。课程内容涉及深度学习的基本理论方法以及它在计算机视觉、自然语言处理以及决策理论等领域中的应用，本节主要介绍无监督学习和半监督学习。
<!--more-->

## Introduction

目前我们课程中主要介绍了深度神经网络在监督学习中的应用。在监督学习中我们需要为每一个数据赋予标签，然后学习到这个映射函数来实现不同的功能。与监督学习对应的学习任务称为**无监督学习(unsupervised learning)**，此时我们没有任何标签的信息当仍然希望可以从数据中进行学习。在监督学习和无监督学习之间还存在着**半监督学习(semi-supervised learning)**和**自监督学习(self-supervised learning)**等类型，在这样的任务中我们则需要同时处理包含标签和无标签的数据。

<div align=center>
<img src="https://i.imgur.com/lU4SFnI.png" width="80%">
</div>

无监督学习的目标是学习到数据自身分布的特征，一般来说可以分为**建模(modeling)**、**聚类(clustering)**和**表征(representation)**几种不同类型的任务。在深度学习时代我们也有使用深度学习来解决这些问题的方法，比如说深度生成模型、度量学习以及表征学习等等。

<div align=center>
<img src="https://i.imgur.com/jaYlh9F.png" width="80%">
</div>

无监督学习的难点在于如何处理没有标签的数据。在监督学习中我们可以使用各种损失函数来训练网络，但在无监督学习中我们可能无法使用监督学习中常用的那些损失函数进行训练。同时如何设计训练过程、网络架构同样也是无监督学习的难点。

<div align=center>
<img src="https://i.imgur.com/OircGL2.png" width="80%">
</div>

为了解决这些问题人们设计了不同的训练策略。常用的方法包括使用伪标签来标记数据、利用数据增强来提升模型性能、通过元学习的方法来进行模型初始化以及使用代理任务来辅助训练。

<div align=center>
<img src="https://i.imgur.com/SO25loa.png" width="80%">
</div>

## Semi-Supervised Learning

在现实的机器学习任务中往往有着大量的无标签数据，而半监督学习的目标是把这些无标签的数据和有标签的数据结合起来并提升模型的性能。

<div align=center>
<img src="https://i.imgur.com/4byayB2.png" width="80%">
</div>

近期的一些研究指出，我们甚至可以通过半监督学习的方法来获得比监督学习更好的性能。

<div align=center>
<img src="https://i.imgur.com/IhXSa5E.png" width="80%">
</div>

### An Old Idea: Predictions of Multiple Views

半监督学习的一种经典思想是使用模型在未标记的数据上进行预测，然后把预测的结果作为新的带标签数据进行训练。这种方法并不是一个很新的方法，实际上90年代人们就提出过类似的思想来训练数据。

<div align=center>
<img src="https://i.imgur.com/OhP6jHJ.png" width="80%">
</div>

### Pseudo-Labeling

更加现代的做法是把数据集划分为有标签数据和无标签数据两类，对于有标签的数据按照通常的监督学习进行训练，而对于无标签数据则为它们赋予伪标签进行训练。在训练伪标签数据时我们需要结合数据增强的方法，通过最小化无标签数据在不同数据增强方法下模型输出的交叉熵来实现无标签数据的训练。

<div align=center>
<img src="https://i.imgur.com/b25fwFK.png" width="80%">
</div>

在实际训练时我们可以把标签数据和无标签数据放在一起同时进行训练。这样整个训练流程可以分成标签数据和无标签数据两个分支并且有着各自的损失函数，而把两个分支合并到一起就可以实现端到端的训练了。

<div align=center>
<img src="https://i.imgur.com/2rXMeNt.png" width="80%">
</div>

当然这种训练方法还有很多技巧，比如说合理地设计标签数据和无标签数据在一个batch中的比例、如何选取生成伪标签的阈值、如何设计学习率策略、利用滑动平均来更新模型参数等等。

<div align=center>
<img src="https://i.imgur.com/GYW8qrE.png" width="80%">
</div>

试验结果表明，使用半监督学习的方法可以提升分类模型的性能

<div align=center>
<img src="https://i.imgur.com/BAvj6NS.png" width="80%">
<img src="https://i.imgur.com/JLepsLZ.png" width="80%">
</div>

### Other Methods

除了上面介绍过的伪标签方法，在无监督学习中还可以使用对抗样本、知识蒸馏、label propagation等不同方法进行训练。

<div align=center>
<img src="https://i.imgur.com/fW7NY2L.png" width="80%">
<img src="https://i.imgur.com/oEaubFz.png" width="80%">
</div>

<div align=center>
<img src="https://i.imgur.com/sm7iBzC.png" width="80%">
</div>

## Few-Shot Learning

**少样本学习(few-shot learning)**的目的在于解决数据集上样本分布极不均衡的问题。很多常见的标签都有大量的数据，但是一些罕见的标签则通常只有很少的数据作为支持。因此我们希望可以通过在有着大量数据的标签上进行训练从而提升在这些罕见标签上模型的性能。

<div align=center>
<img src="https://i.imgur.com/R0QMacJ.png" width="80%">
</div>

### Finetuning

少样本学习最直接的思路是使用fine-tuning的方式先在常见标签的数据上进行训练，然后在罕见标签数据上进行微调。

<div align=center>
<img src="https://i.imgur.com/RljWp6H.png" width="80%">
</div>

一些研究表明使用余弦相似度的分类模型要比神经网络更适合这样的训练模式。

<div align=center>
<img src="https://i.imgur.com/VuyAGZ2.png" width="80%">
</div>

实践中发现fine-tuning的方式并不完全适合少样本学习的问题，这主要是由于训练过程和微调过程是完全割裂的，我们无法直接利用常见标签数据的信息来指导少样本学习过程。

<div align=center>
<img src="https://i.imgur.com/CPsKuzN.png" width="80%">
</div>

### Meta-Training

meta-training的思路是利用常见样本的数据来模拟少样本学习的过程。我们可以把训练数据假装成少样本数据，每次训练时从选择常见标签的几个样本分别作为训练数据和查询数据，这样训练过程和最终的测试过程是完全一致的。

<div align=center>
<img src="https://i.imgur.com/nZzVmvG.png" width="80%">
</div>

通过meta-training的学习过程，我们可以获得MatchingNet、ProtoNet以及RelationNet等不同形式的模型。

<div align=center>
<img src="https://i.imgur.com/IdPGsAX.png" width="80%">
</div>

从一个更高的层次来看，meta-training的本质是利用学习的方式来设计学习算法，也就是说我们可以通过学习来改进模型的初始化和训练方式从而更适应少样本学习的任务。

<div align=center>
<img src="https://i.imgur.com/ZuQKD4Z.png" width="80%">
</div>

本节课中我们主要介绍改进梯度下降以及模型初始化方式这两种meta-training方法。

<div align=center>
<img src="https://i.imgur.com/ViASPb8.png" width="80%">
</div>

### Meta-Learner LSTM

回忆梯度下降法的参数更新方法，不难发现它和LSTM中cell的更新方法有一些类似之处。因此meta-learner LSTM的思路是把LSTM的训练方法引入到梯度下降中，这样就可以自适应地修正学习率和遗忘率。

<div align=center>
<img src="https://i.imgur.com/EovD0UH.png" width="80%">
</div>

使用LSTM训练方法的另一个好处是整个训练过程是可微的，我们可以把meta-learner LSTM展开成类似于LSTM的计算图这样就可以使用常用的网络模型进行训练。

<div align=center>
<img src="https://i.imgur.com/uUbTkpv.png" width="80%">
</div>

### Model-Agnostic Meta-Learning (MAML)

MAML的思路是直接学习模型的初始化，整个模型的训练过程仍是基于SGD。

<div align=center>
<img src="https://i.imgur.com/lIeuy2n.png" width="80%">
<img src="https://i.imgur.com/ovMIHj1.png" width="80%">
</div>

和meta-learner LSTM相比，MAML往往有着更好的理论保证。

<div align=center>
<img src="https://i.imgur.com/AiKXBSH.png" width="80%">
</div>

## Unsupervised and Self-Supervised Learning
