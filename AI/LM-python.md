---
title: "LM-python"
date: 2026-02-02
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
            - eg：```
                    a = 5
                    b = a
                    b = 10
                    print(a) #5,b指向新对象10 
        - 可变对象（mutable）
            - list
            - dict
            - set
            - numpy array
            - torch tensor
            - 修改=原地改变
            - eg：```
                    a = [1,2]
                    b = a
                    b.append(3)
                    print(a) #[1,2,3],a和b指向同一个list 
- 引用/拷贝
    - 引用赋值
        - ```b = a```
        - 不是复制是b指向a的对象
        - 修改一个->另一个也改变
    - 浅拷贝
        - ```b = a[:]```或```b= list(a)```
        - 创建新对象，但只拷贝一层
        - eg：```
                a = [[1],[2]]
                b = a[:]
                b[0][0] = 99
                print(a) #[[99],[2]] 
            - 内部list还是共享的（浅拷贝陷阱）