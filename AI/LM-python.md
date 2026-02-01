---
title: "LM-python"
date: 2026-01-13
draft: false
---

## LM-python
- python核心
    - python变量不是盒子，是标签
    - 变量只是指向对象的名字
    - 引用语义
- 对象模型
    - python一切都是对象
        - int/list/function/class/tensor
        - 本质都是：对象+引用
    - 可变/不可变
        - 不可变对象（immutable）
            - int
            - float
            - str
            - tuple
            - 修改=创建新对象
        - 可变对象（mutable）
            - list
            - dict
            - set
            - numpy array
            - torch tensor
            - 修改=原地改变