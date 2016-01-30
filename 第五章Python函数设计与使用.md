#2016/1/29学习内容 
#第四章 Python函数设计与使用
之前的几页忘记保存了 很伤心

##变量作用域
>-一个变量已在函数外定义，如果在函数内需要修改这个变量的值，并将这个赋值结果反映到函数之外，可以在函数内用**global**声明这个变量为全局变量，明确声明要使用已定义的同名全局变量


>-在函数内部直接使用**global**关键词将一个变量声明为全局变量，即使在函数外没有定义该全局变量，在调用这个函数之后，将自动增加新的全局变量
>
>     def demo():
	    global a;
	    a=3;
		demo();
		print(a)

#
>也可以这么理解：在函数内如果只引用某个变量的值而没有为其赋新值，该变量为(隐式的)全局变量,如果在变量内任意位置有为变量赋新值的操作，该变量即被认为(隐式的)局部变量，除非使用关键词global进行声明。

###还有这种先斩后奏的用法
>
    
	a=10;
	def demo():
    	a=666  
   		print(a)
    	global a;
	demo();
	print(a)

>实际工程中如果需要在同一个程序的不同模块之间共享全局变量的话，可以编写一个专门的模块来实现这一目的

##lambda表达式
>labmda表达式可以用来声明匿名函数，即没有函数名字的临时使用的小函数


###重要用法.....sorted中做key
	f=lambda x,y,z: x+y+z;
	print(f(1,2,3))
	#6
	g=lambda x,y=2,z=3:x+y+z #含有默认值参数
	print(g(1))
	#6
	print(g(x=2,z=4,y=6))   #关键参数
	#12
	#归根到底函数也是一种变量
	#所以lambda 和 普通函数都可以放到 list 中
	#lambda 也能调用其他函数
	L=[lambda x : x**2,lambda x : x**3]
	import random
	data=[1,2,10,100,1000,10000];
	random.shuffle(data)
	print(data)
	#[10, 10000, 1000, 1, 2, 100]
	data.sort(key=lambda x:x)
	print(data)
	#[1, 2, 10, 100, 1000, 10000]
	data.sort(key=lambda x:-x)
	print(data)
	#[10000, 1000, 100, 10, 2, 1]
	def demo(x):
	    return x
	data.sort(key=demo)     #既然lambda算子可以，那么函数也可以，道理上两者等价 果然
	print(data)
	#[1, 2, 10, 100, 1000, 10000]

##函数高级用法

###map(),reduce(),filter()
>详情已经了解很多了
###用yield语句的函数来创建生成器

	def f():
	    a,b=1,1
	    while True:
	        yield a
	        a , b = b,a+b;
	a=f()
	for i in range(10):
	    print(a.__next__(),end= ' ' )
	#1 1 2 3 5 8 13 21 34 55
	print()
	a=f()
	for i in f():
	    if i > 1000:
	        break;
	    else :
	        print(i,end=' ')
	#1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987 

###使用dis模块的功能可以查看函数的字节码指令


###函数嵌套定义与可调用对象
>在Python中，函数时可以嵌套定义的。另外，任何包含__call__()方法的类的对象都是可以调用的.

	def linear(a,b):
	    def result(x):
	        return  a*x+b
	    return result
	a=linear(1,2)
	print(a(2))
	#4
	
	class linear2:
	    def __init__(self,a,b):
	        self.a,self.b=a,b
	    def __call__(self,x):
	        return self.a*x+self.b
	taxes=linear2(0.3,2)
	print(taxes(5))
	#3.5