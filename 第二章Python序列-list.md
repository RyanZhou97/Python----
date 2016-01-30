#2016/1/27学习内容 
#第二章 Python序列-list
##list常用操作
###list.append(x)
###list.extend(L)
###list.insert(index,x)
###list.remove(x)
>删除在列表中首次出现的指定元素x
###list.pop([index])
>删除并返回列表对象指定位置的元素，默认为最后一个元素
###list.clear()
###list.index(x)
>返回第一个值为x的元素的下标，若不存在值为x的元素则抛出异常
###list.count(x)
>返回指定元素x在列表中出现的次数
###list.reverse()
>对列表元素进行原地翻转
###list.sort()
>对列表元素进行原地排序
###list.copy()
>对列表对象的浅复制.

###append比'+'运算快很多

###使用乘法扩展列表对象
>**千万要小心**
>当使用*运算符将**包含列表的列表**进行重复并创建新列表时，并不创建元素的复制，而是创建已有对象的引用。因此，当修改其中一个值时，对应的引用也会被修改。

例如：

	 x=[[1,2,3]]*3;
	 x[0][0]=10;
	 print(x);
	 [[10, 2, 3], [10, 2, 3], [10, 2, 3]]

##成员资格判断
###in
###not in

##切片
###浅赋值
是切割后创建一片新的内存放置
###利用切片原地操作
	x=[1,2,3]*3;
	x[1:2:]=[10];
	print(x);
	x[::2]=[0]*((len(x)+1)//2);
	print(x);
	[1, 2 , 3, 1, 2, 3, 1, 2, 3]
	[1, 10, 3, 1, 2, 3, 1, 2, 3]
	[0, 10, 0, 1, 0, 3, 0, 2, 0]
###也可以结合del操作

	x=[1,2,3]*3;
	del x[::2];
	print(x);

##列表排序
###random.shuffle(list)
>打乱lsit顺序
###逆序
>list.sort(reverse=Ture)
###自定义排序 以后学习

###sorted(list,reverse=Ture)
>内联的逆序排序

###enumerate(列表）
>枚举列表，元组或其他可迭代对象的元素，返回枚举类型，枚举对象中每个元素是包含下标和元素值的元组。对字典得到的是建值。
	
	x=[1,2,3,4,5,6,7];
	for i,value in enumerate(x):
	    print(i,value);

##列表推倒式
- [Expression for Variable in  list]
- 也就是：[ 表达式  for  变量 in 列表]
- 如果需要加入if条件语句则是：[表达式 for 变量 in 列表 if 条件]
- 如果表达式中需要if else 语句则是 [表达式 if 条件 else 表达式 for 变量 in 列表 if 条件]
- 如果表达式有两个元素  语句则是[(表达式,表达式) for x in 列表 for y in 列表 if 条件]


几个精彩的用法

列表推导实现嵌套列表的平铺
  
	vec = [[1,2,3],[4,5,6],[7,8,9]]	
	a=[num for elem in vec for num in elem]
	print(a)
	[1, 2, 3, 4, 5, 6, 7, 8, 9]

列表推倒实现矩阵转置

	matrix=[[1,2,3,4],[5,6,7,8],[9,10,11,12]];
	[[row[i] for row in matrix] for i in range(4)]
	[[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]

使用列表推导式生成100以内的所有素数

	import math
	[p for p in range(2,100) if 0 not in [p%d for d in range(2,int(math.sqrt(p))+1)]]
	[2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97]