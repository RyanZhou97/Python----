#2016/1/27学习内容 
#第一章 Python基础
###Python内置函数
> 见Python内置函数.md
###del命令
> 显式删除操作,列表中也可以使用。
###基本输入输出
####input()
>读入进来永远是字符串
####print
>文件重定向

    fp=open(r'D:\mytest.txt','a+') 
    print(type(fp),file=fp);
    fp.close();
>输出不换行

    for i in range(10):
    print(i,end=' ');
    0 1 2 3 4 5 6 7 8 9
    for i in range(10):
    print(i,end='');
    0123456789

###模块导入和使用
	`import math
	 import math as mt
	 from math import sin`
###缩进
	 Ctrl+[ Ctrl+]
###注释
	
- #
- '''注释内容'''
- Ctrl-3,Ctrl-4 集体注释or 解除注释
###续行
> 可以使用\ 但更推荐使用括号
###split
> 将字符串按指定字符切割成列表