---
title: BLEU 算法计算相似度
authors: Ethan Lin
year: 2024-04-26
tags:
  - 类型/笔记
  - 日期/2024-04-26
  - 内容/相似度计算
aliases:
  - BLEU 算法
---

# BLEU 算法计算相似度


相关介绍：[BLEU详解 - 知乎](https://zhuanlan.zhihu.com/p/223048748)


总体思想就是准确率，假如给定标准译文reference，神经网络生成的句子是candidate，句子长度为n，candidate中有m个单词出现在reference，m/n就是bleu的1-gram的计算公式。