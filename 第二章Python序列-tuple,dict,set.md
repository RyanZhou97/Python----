#2016/1/27学习内容 
#第二章 Python序列-tuple
##tuple创建的tips
- a\_tuple=('a',)，要这样创建，而不是a\_tuple=('a'),后者是一个创建了一个字符
##tuple常用操作
- 类似list，但是不能进行修改.能作为字典的key值
- 当然如果tuple中的元素有list，要另当别论

##序列解包
>
- 可以用序列解包对多个变量同时进行赋值
- 序列解包也可以用于列表和字典。字典默认是对key操作，如果需要key-value操作，需要items()方法，如果仅对value操作，需要用values()方法明确指定
- 在调用函数时，在实参面前加入一个星号"*"也可以进行序列解包，从而实现将序列中的元素值一次传递给相同数量的形参，详情见之后.

##生成器推倒式
> 
> - 生成器推导式和列表推倒式非常接近.
> - 生成器推导式的结果是一个生成器对象。不是列表，也不是元组，而是一种迭代器(惰性计算).
> - 利用next或者作为迭代器使用
> - 当所有元素访问结束以后，如果需要重新访问其中的元素，必须重新创建该生成器对象。

	g=(i**2 for i in range(0,10))
	print(g)
	#<generator object <genexpr> at 0x0000000002307CF0>
	print(tuple(g)) #转换为列表	
	#(0, 1, 4, 9, 16, 25, 36, 49, 64, 81)
	print(tuple(g)) #元素已经遍历结束，所以会为空
	#() 
	g=(i**2 for i in range(0,10))
	print(g.__next__())
	# 0
	print(g.__next__())
	# 1	
	print(g.__next__())
	# 4
	g=(i**2 for i in range(0,10))
	for i in g:
	print (i,end=' ');
	#0 1 4 9 16 25 36 49 64 81
#第二章 Python序列-dict
##定义
>- 字典是”键-值对“的无序可变序列，字典中的每个元素包含两个部分：”键“和"值"。定义字典时，每个元素的“键”和“值”用冒号分隔，相邻元素之间用逗号分隔，所有的元素放在一堆大括号“{”和“}”中。
- 字典的“键”可以是Python 中任意不可变的数据，不能是列表，集合，字典
- 键不能重复 ，值能重复
##内置函数globals() locals()
>- globals()返回当前作用域的所有全局变量和值的字典
>- locals() 返回当前作用域的所有局部变量和值得字典 

##字典创建与删除
- 使用内置函数dict()通过已有数据快速创建字典
	
		x=dict(zip(keys,values))
- 使用内置函数dict()根据给点的“键值对”来创建字典

		d=dict(name='Zhou Yong',age=18)

###**formkeys(list)**	
- 还可以给定内容为键，创建值为空的字典

		adict=dict.fromkeys(['name','age','sex'])
- 使用del删除


##字典元素的读取
- 下标：直接使用下标，若指定的键不存在会抛出异常

		Dict['name2']
- .get(dict[,指定值]):比较推荐的也是更安全的字典语速访问方法是用字典对象的get()方法，当键不存在的时候返回指定值，若不指定值，则返回None。

- .items():返回字典的键值对列表

- .values()： 返回字典的值列表

##字典元素的添加，修改
- 指定键为下标赋值时，若键已经存在就修改，不存在就赋值。
- 可以用对象的方法.updata(dict),用另一个字典批量更新当前字典，原则同上
- .clear()
- .pop(key) 删除并返回指定键的元素
- .popitem() 删除并返回字典中的一个元素 类似随机了。感觉没什么卵用7 

##扩展
###collections模块下的defaultdict
>类似于C++STL中的MAP
>可以规定好值的类型。

	from collections import defaultdict
	frequences=defaultdict(str);
	for item in z :
  		frequences[item]+='a';
	print(frequences.items())

	from collections import defaultdict
	frequences=defaultdict(1);
	from item in z :
    	frequences[item]+=1;
	print(frequences.items())

###collections模块下的Counter类
>计数的扩展类，统计各元素出现的次数，本质为一个dict
>还有方法可以查找出现最多的元素等功能

###collections模块下的OrderedDict
>字典按照插入顺序排序

#Python序列-set
##集合的创建与删除
###set()
>set中不支持嵌套列表

###del
>只能删除整个集合

###pop()
>删除并返回第一个，不接受参数

###add(x)
>增加元素x 不是append

###remove(x)
>删除指定元素x

##集合操作
###并集
>- set\_a|set\_b
>- set\_a.union(set\_b)
###交集
>- set\_a&set\_b
>- set\_a.intersection(set\_b)
###差集
>- set\_a-set\_b
>- set\_a.difference(set\_b)

###对称差
>- set\_a^set\_b
>- set\_a.symmetric_difference(b_set)

###子集
>- x.issubstr(y)

