#1月29日学习内容
#Python面向对象程序设计

##类的定义与使用

###类定义语法
>使用class关键词
	
	class Car:
    	def infor(self):
    	    print("This is car")
###self参数
>类的所有实例方法都必须至少有一个名为self的参数,并且必须是方法的第一个形参

>self参数代表将来要创建的对象本身

>实际上也没可以不用self 而取别的名字，但这是约定俗成的事
	
	
	class A:
	    def __init__(hahaha, v):
	        hahaha.value=v
	    def show(hahaha):
	        return hahaha.value
	a=A(3)
	a.show()

###类成员与实例成员
实例属性
>实例属性一般是指在构造函数__init()__中定义的,定义与使用必须以self作为前缀;

类属性
>是在类中所有方法以外定义的数据成员

两者区别
>在主程序中
>
>实例属性属于实例，只能通过对象名访问
>
>而类属性属于类  ,可以通过类名和对象名访问

####Python优点
>可以动态的为类对象增加成员	        

###私有成员和公有成员
私有属性
> 如果属性名以两个下划线"__"(中间无空)开头则表示是私有属性

>大多数跟其他语言一样,但是Python支持的特殊方式访问 对象.\_类名__xxx

- _xxx
>这样的对象叫做保护成员，不能用”from module import *"导入，只有类对象和子类对象能访问这些成员

- \_\_xxx\_\_
> 系统定义的特殊成员,非私有成员

- __xxx
>只有类对象自己能访问，子类对象也不能访问到这个成员，但可以用对象名.\_类名__xxx这样的特殊方式访问.



##方法

###共有方法
>通过对象名直接调用,在方法中也要用self

>如果通过类名来调用属于对象的共有方法，需要显示为改方法的self参数传递一个对象名，用来明确指定访问那个对象的数据成员


###公有方法
>__来命名

>不能通过对象名直接调用，只能在属于对象的方法中通过self调用或在外部通过特殊方法调用

###静态方法和类方法
>都可以通过类名和对象名来调用

>但只能访问属于类的成员，而不能访问属于对象的成员

类方法

>一般将cls作为类方法的第一个参数名称.

>需要在前面加一个@classmethod的修饰符 表示下一个方法为类方法

    @classmethod
    def classShowTotal(cls):
        print(cls.__value)

静态方法
>不需要参数名

>需要在前面加一个@staticmethod的修饰符 表示下一个方法为静态方法

	class Root:
	    __total=0;
	    def __init__(self,v):
	        self.__value=v
	        Root.__total+=1
	
	    def show(self):
	        print('self.__value:',self.__value)
	        print('Root.__total:',Root.__total)
	
	    @classmethod        #修饰符
	    def classShowTotal(cls):    #类方法
	        print(cls.__total)
	
	    @staticmethod       #修饰符
	    def staticShowTotal():
	        print(Root.__total)
	r=Root(3)
	r.classShowTotal()          ##类方法可以用对象调用
	#1
	r.staticShowTotal()         ##静态方法也可以用对象调用
	#1
	r.show()
	#self.__value: 3
	#Root.__total: 1
	rr=Root(5)
	Root.classShowTotal()      ##类方法可以用类调用
	#2
	Root.staticShowTotal()     ##静态方法也可以用类调用
	#2
	Root.show(r)        ##为self显示传递对象名
	#self.__value: 3
	#Root.__total: 2    证明__total只有一个
	
	r.show()
	#self.__value: 3
	#Root.__total: 2

##属性
>python2.X的属性没有实质的意义 无法起到保护的作用。当建立一个只读的属性时
>如果修改其值，虽然并不会真正的修改，修改的时候其实是新建了一个变量会把这个属性隐藏。所以十分鸡肋

>python 3.X中 得到较为完整的实现

>用@property 标识符表示下一个方法是 属性方法


>用property(\_\_get,\_\_set\_\_del)的方法设置 ,不需要的参数可以用None

>具体看以下代码

只读属性

	class Test:
	    def __init__(self,value):
	        self.__value=value
	    @property
	    def value(self):
	        return self.__value
	
	t=Test(3);
	print(t.value)
	#3
	t.value=5;
	#AttributeError: can't set attribute

可读可修改

	class Test:
	    def __init__(self,value):
	        self.__value=value
	    def __get(self):
	        return self.__value
	    def __set(self,v):
	        self.__value=v;
	    value=property(__get,__set)
	
	t=Test(3)
	print(t.value)
	#3
	t.value=5;
	print(t.value)
	#5

可读可修改可删除

	class Test:
	    def __init__(self,value):
	        self.__value=value
	    def __get(self):
	        return self.__value
	    def __set(self,v):
	        self.__value=v;
	    def __del(self):
	        del self.__value
	    value=property(__get,__set,__del)
	
	t=Test(3)
	print(t.value)
	#3
	t.value=5;
	print(t.value)
	#5
	del t.value

系统自己补出的代码 有待研究 很厉害的样子

	class Test:
	    def __init__(self,value):
	        self.__value=value
	    def value():
	        doc = "The value property."
	        def fget(self):
	            return self.__value
	        def fset(self, value):
	            self.__value = value
	        def fdel(self):
	            del self.__value
	        return locals()
	    value = property(**value())

##特殊方法于运算符重载
###常用特殊方法
-  构造函数\_\_init()__ 
-  析构函数\_\_del()__
-  \_\_add__() , \_\_radd__()
>左+，右+

-  \_\_sub__

> \-

- \_\_mul__
> *

- \_\_div()__ ,\_\_truediv__()
> Python 2.x使用div()，Python3.X使用turediv()

- \_\_floordiv__()
> 整除

- \_\_mod__()
> 取余

- \_\_pow__()
> **

- \_\_cmp__()

- \_\_repr__()
> 打印 转换

- \_\_setitem__()
> 按照索引赋值

- \_\_getitem__()
> 按照索引获取值

- \_\_len__()
> 计算长度

- \_\_call__()
> 函数调用

- \_\_contains__()
> 测试是否包含某个元素

- \_\_eq\_\_() ,\_\_ne\_\_() ,\_\_lt\_\_() ,\_\_le\_\_() ,\_\_gt\_\_() ,\_\_ge\_\_() 
> ==,!=,<,<=,>,>=

- \_\_str__()
> 转化为字符串

- \_\_lshift\_\_()  ,\_\_lshift__() 
> <<,>>

- \_\_and\_\_()  ,\_\_or\_\_() ,\_\_invert\_\_()
> &,|,~


- \_\_iadd\_\_()  ,\_\_isub__() 
> +=,-=




##继承
	class 类名(继承的类名):
		pass
有时间补充
	