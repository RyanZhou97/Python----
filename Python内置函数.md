#Python 常用内建函数
##比较基础的列表
###abs(x)
> 求绝对值
###pow(x,y)
> 返回x的y次方，等同于x**y
###round(x[,小数位数])
> 对x进行四舍五入，若不指定位数，则返回整数
###chr(x)
> 返回ASCII编码为x的字符，str类型
###ord(x)
> 返回一个字符x的编码　chr的逆操作
###float(x)
> 把数字或字符串x 转换成浮点型并输出
###int(x)
> 把浮点数或整数 转换为整数
###str(object)
> 把对象x转换为字符串
###list([x]),set([x]),tuple([x]),dict([x])
> 把对象转换为列表，集合，元组，字典并返回
###bin（x)
> 把数字x转换为二进制字符串    0bxxxx
###oct(x)
> 把数字x转换为八进制字符串    0oxxxx
###hex(x)
> 把数字x转换为十六进制字符串  0xxxxx
###cmp(x,y)
> Python 3.X已经不支持
###bool(x）
> x为0，或者''，或者False时 返回False，否则返回Ture
###max(x),min(x),sum(x)
> 返回序列中的最大值，最小值，或数值元素之和



##比较复杂的列表
###eval(s)
> 计算字符串中表达式的值并返回
###filter(Function or None,sequence)
> 返回序列中使得函数值为Ture的那些元素，如果函数为None则返回那些值等价于Ture的元素，如果序列为元组或字符串则返回相同类型结果，其他则返回列表
###map(Function,Sequence)
> 将单参数函数映射到序列中每个元素，返回结果列表
###reduce(Function,Sequence)
> 将接收2个参数的函数以累计的方式从左到右依次应用至序列的每个元素，最终返回单个值作为结果
###zip(seq1[,seq2[...]])
> 返回[(seq1[0],seq2[0],seq3[0],...),(seq1[1],seq2[1],seq3[1]..),...] 以最短的那个list的长度为基准
###open()			//暂时不会使用
> 以指定模式打开文件并返回文件对象
###range([start,]end[,step])
> 返回一个等差数列，不包括终值，Python 3.x中返回一个range对象
###reversed(列表或元组)
> 返回逆序后的迭代器对象
###sorted(列表) 
> 返回排序后的参数

##信息列表
###dir(object)
> 返回指定对象的成员列表
###help(object)
> 返回对象obj的帮助信息
###callable(object)
> 测试对象是否可调用。比如类和函数式可调用的，包含\_\_\_call___()方法的类的对象也是可调用的
###id(object)		
> 返回对象的标识(地址),类似C中的取地址符号
###type(object)
> 返回obj的类型
###all(iterable)
> 如果对于可迭代对象所有元素满足bool(x) 为Ture，则返回Ture,否则返回Flase。对于空的迭代对象返回Ture。
###any(iterable)
> 如果对于可迭代对象存在元素满足bool(x) 为Ture，则返回Ture,否则返回Flase.对于空的迭代对象返回False。
###isinstance(object,class or type or tuple)
>测定对象是否是指定类型的实例
###len(object)
>返回对象obj所含的元素个数，适用于列表，元组，集合，字典，字符串等类型的对象。
