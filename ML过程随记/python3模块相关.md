# Python3 模块相关内容笔记

## Python3 multiprocessing 多进程
利用pool模块是的map方法只能传递一个参数，而在全面搭配寻找最优参数时的全面搭配实验
需要多个维度的参数

可以利用`starmap_async()`函数来解决

同时掌握一种快速生成多维数据的方式

```
[(x,y) for x in range(1,5) for y in range(5,8)]

```
