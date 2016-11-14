title: django初探
date: 2015-12-09 21:05:44
tags: [python,django]
categories: 辅助攻击技能 
description: 学习django的时候想到了一些比较好玩的总结，可能就我觉得好玩吧
---

对linux/unix的世界，万物皆文件，这一点都没错的。

``python3 -m venv myvenv``说是创建了一个虚拟环境，其实就是一个文件夹（里面有所需文件）罢了。

<br>
执行``django-admin startproject mysite .``之后，产生的文件结构就是这样的

```
djangogirls
├───manage.py
└───mysite
        settings.py
        urls.py
        wsgi.py
        __init__.py
```
所以其实还是文件啦～

<br>

这意味着什么？
---
不正意味着搞丢了什么django的文件随便加个格式一模一样的就好了吗～

