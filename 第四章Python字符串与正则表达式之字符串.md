#2016/1/28学习内容 
#第四章 Python字符串与正则表达式之字符串
##编码规则
###UTF-8
>以1个字节表示英语字符(兼容ASCII),以3个字节表示中文及其他语言，UTF-8对全世界所有国家需要用到的字符进行了编码
###GB2312->GBK->CP936
>用2个字节表示中文
###Unicode

###常用指定方法
	#coding=utf-8
	#coding:GBK
	#-*-coding:utf-8-*-
###2.x与3.x区别
>2.x没有很好的支持,len(中文)=2或3

>3.x很好的支持了，len(中文)=1

##字符串
>是不可变序列，修改生成的字符串

###字符串格式化

- 最基本的
		
		a1=1
		a2=1	
		a3=1
		"%d%d%d"%(a1,a2,a3)

- 更推荐的.format()方法

		print("The number {0:,} in hex is : {0:#10.4f},the number {1} is oct is {1:#o}".format(5555,55))
		#The number 5,555 in hex is :  5555.0000,the number 55 is oct is 0o67
		print("The nuber  {1:,} in hex is : {1:#x}, the nuber {0} in oct is {0:#o}".format(55,5555))    #与位置无关
		#The nuber  5,555 in hex is : 0x15b3, the nuber 55 in oct is 0o67
		print("my name is {name},my age is {age},and my QQ is {qq}".format(name="zhou",qq="111",age=18)) #还能利用变量
		#my name is zhou,my age is 18,and my QQ is 111
		position=(5,8,13)
		print("X:{0[0]} Y:{0[1]} Z:{0[2]}".format(position)) #能利用列表
		#X:5 Y:8 Z:13
	
		#更厉害的是 能把format参数留空，当做一个函数用
		weather=[("Monday","rain")]
		formatter="Weather of '{0[0]}',is '{0[1]}' ".format
		print(formatter(weather[0]))
		#Weather of 'Monday',is 'rain' 
		
##字符串常用方法

###查找统计类 find(),rfind(),index(),rindex(),count()

- find(string[,start[,end]])
>从开始到结尾查找string第一次出现的位置 没找到输出-1

>end的位置实际是闭区间，实际查找为end-1

- rfind(string[,start[,end]])
> 从结尾到开始查找string第一次出现的位置 没找到输出-1

> end的位置实际是闭区间，实际查找为end-1

- index和rindex

> 同上，但是如果没有找到，抛出异常

- count(substr)

> 统计子字符串出现的次数


###切割类 split(),rsplit(),partition(),rpartion()

- split([分隔符[,最大分隔次数]])
> 依照分隔符从左端开始分隔多个字符串，返回一个列表
> 如果为参数为空的话，分隔符就是所有的空白符号(包括空格，换行，制表符等)

- rsplit

- partition(分割符)
> 分隔三个部分，依次为 分隔符前的字符串 分隔符，分隔符后的字符串

- rpartition

- qustion?怎么指定多个分隔符
> 网上说 用别的模块的split即可

###合并类 join()

- join(list)

>将一组列表合并成一个字符串，并在其中插入指定字符，即调用这个方法的字符


###转换大小写类 lower() upper() capitalize() title() swapcase()

-lower()
>全部转小写

-upper()
>全部转大写

-capitalize()
>首字母大写，其余全部小写

-title()
>其余字符以后的第一个字母大写

-swapcase()
>大小写互换

###替换类 replace()

-replace(指定串，替换串)
>把所有字符串中的指定串替换成替换串

###映射类 maketrans() translate()

###删除类 strip(),rstrip(),lstrip()
>删除两端，右端或左端的空白字符，或连续指定字符

	s="aaassssfffff"
	print(s.strip("af"))
	#ssss

###eval()

>内置函数eval()尝试把任意字符串转换为Python表达式并执行并返回值
>黑客可以利用这一个代码进行入侵

>很重要很强大的功能

###关键词 in , not in 
>判断一个字符串是否出现在另一个字符串中，返回True 或 False。


###开头结尾检验 startswith() endswith()
>能接受一个tuple来批量检验多个参数

>能接受一个开头 结尾 指定范围

>常见例子 ：检验文件后缀名.


	import os
	[filename for filename in os.listdir(r'D:\\') if filename.endswith(('.bmp'),('.jpg'),('.gif'))]

###判断字符的类型 isalnum(),isalpha(),isdigit,isspace(),isupper(),islower()

###字符串对齐 center(),ljust,rjust
>返回指定宽度的新字符串，原字符串居中，左对齐，右对齐出现在新字符串中，如果宽度大于字符串长度，则使用指定的字符（默认为空格）进行填充

##字符串常量
>在string模块中定义了多个字符串常量，包括数字字符，标点字符，英文字母，大写字母，小写字母
>用户可以直接使用这些常量

	import string
	print(string.digits)
	#0123456789
	print(string.punctuation)
	#!"#$%&'()*+,-./:;<=>?@[\]^_`{|}~
	print(string.ascii_letters)
	#abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ
	print(string.printable)
	#0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ!"#$%&'()*+,-./:;<=>?@[\]^_`{|}~     
	

##可变字符串
>在Python中，字符串属于不可变对象，不支持原地修改，如果需要修改其中的值，只能重新创建一个新的字符串对象，然而，如果确实需要一个支持原地修改的unicode数据对象，可以使用io.StringIO对象或array模块

	import io 
	s="Hello,world"
	sio=io.StringIO(s)
	print(sio.getvalue())
	#Hello, world
	print(id(sio))
	#36748456
	sio.seek(6)
	sio.write("there!")
	print(sio.getvalue())
	#Hello,there!
	print(id(sio))
	#36748456

array

	s="Hello,world"
	import array
	a=array.array('u',s)
	print(a)
	a[0]='y'
	print(a)
	
	print(a.tounicode())
	
	#array('u', 'Hello,world')
	#array('u', 'yello,world')
	#yello,world


