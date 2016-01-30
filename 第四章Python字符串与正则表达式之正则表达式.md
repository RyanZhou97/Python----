#2016/1/28学习内容 
#第四章 Python字符串与正则表达式之正则表达式
>正则表达式是字符串处理的有力工具和技术，正则表达式使用预定义的特定模式去匹配一类具有共同特征的字符串，主要用于字符串处理，可以快速，准确地完成复杂的查找，替换等处理要求。

>Python中，re模块提供了正则表达式操作所需要的基本功能

##正则表达式元字符
###元字符:   .
>匹配除换行符意外的任意单个字符

###元字符:   *
>匹配位于*之前的0个或多个字符

###元字符：  +
>匹配位于+之前的1个或多个字符

###元字符:   |
>匹配位于|之前或之后的字符

###元字符:   ^
>匹配行首，匹配以^后面的字符开头的字符串

###元字符:   $
>匹配行尾，匹配以$之前的字符结束的字符串

###元字符:   ?
>匹配位于?之前的0个或1个字符

###元字符:	 \
>表示位于\之后的为转义字符

###元字符: []
>匹配位于[]中的任意一个字符

###元字符: -
>用在[]之内用来表示范围

###元字符：()
>将位于()内的内容作为一个整体对待

###元字符: {}
>按{}中的次数进行匹配

###元字符: \b	\B
>匹配单词头或单词尾 \\\不明意义

>非单词头，单词尾

###元字符： \d  \D
>匹配任何数字 相当于[0-9]

>相反


###元字符: \s \S
>匹配任何空白字符 

>相反

###元字符:  \w \W
>匹配任何字母，数字，下划线，相当于[a-zA-Z0-9_]

>相反

- 如果原字符串中有\d出现，想查找它，需要在正则中用\\\\\d
- 如果原子符串中有+[]等符号出现，想查找他，需要在正则前加一个\即可

##注意事项
###数量词的贪婪模式与非贪婪模式
>正则表达式通常用于在文本中查找匹配的字符串。Python里数量词默认是贪婪的（在少数语言里也可能是默认非贪婪），总是尝试匹配尽可能多的字符；非贪婪的则相反，总是尝试匹配尽可能少的字符。例如：正则表达式"ab*"如果用于查找"abbbc"，将找到"abbb"。

>而如果使用非贪婪的数量词"ab*?"，将找到"a",加个问号代表尽可能少的匹配。

>除非结尾有特定要求，一般都是贪婪的。
###反斜杠的困扰
>与大多数编程语言相同，正则表达式里使用"\"作为转义字符，这就可能造成反斜杠困扰。假如你需要匹配文本中的字符"\"，那么使用编程语言表示的正则表达式里将需要4个反斜杠"\\\\"：前两个和后两个分别用于在编程语言里转义成反斜杠，转换成两个反斜杠后再在正则表达式里转义成一个反斜杠。Python里的9原生字符串很好地解决了这个问题，这个例子中的正则表达式可以使用r"\\"表示。同样，匹配一个数字的"\\d"可以写成r"\d"。有了原生字符串，你再也不用担心是不是漏写了反斜杠，写出来的表达式也更直观。




##re模块主要方法
###compile(pattern,string[,flags])		//??
>创建模式对象

###search(pattern,string[,flags])		//??
>在整个字符串中寻找模式，返回match对象或None
>从全部
###match(pattern，string[,flags])		//??
>从字符串的开始出匹配模式，返回match对象或None
>只是从开头

###findall(pattern,string[,flags])
>列出字符串中模式的所有匹配项

###split(pattern,string[,maxsplit=0])
>根据模式匹配项分割字符串

###sub(pattern,repl,string[,count=0])
>将字符串中所有pat的匹配项用repl替换

###escape(string)
>将字符串中所有特殊正则表达式字符转义

###flags的值
>其中函数参数flags的值可以是re.I(忽略大小写),re.L，re.M(多行匹配模式)，re.S(使元字符“.”匹配任意字符，包括换行),re.U(匹配Unicode),re.X(忽略模式中的空格,并可以使用#注释)的不同组合（使用“|"进行组合
##直接使用re模块方法

	import re
	text='alpha. beta....gamma delta'
	print(re.split('[\. ]+',text))
	#['alpha', 'beta', 'gamma', 'delta']
	print(re.split('[\. ]+',text,2))  #分隔两次
	#['alpha', 'beta', 'gamma delta']
	print(re.split('[\. ]+',text,1))  #分隔一次
	#['alpha', 'beta....gamma delta']
	pat='[a-zA-Z]+'
	print(re.findall(pat,text))     #查找所有单词
	#['alpha', 'beta', 'gamma', 'delta']
	pat='{name}'
	text='Dear {name}...'
	print(re.sub(pat,'zhou yong',text)) #字符串替换
	#Dear zhou yong...
	s='a s d'
	print(re.sub('a|s|d','good',s)) #字符串替换
	#good good good
	print(re.escape('http://www.python.org'))
	#http\:\/\/www\.python\.org
	print(re.match('done|quit','done'))
	#<_sre.SRE_Match object; span=(0, 4), match='done'>
	print(re.match('done|quit','don!'))
	#None
	print(re.search('done|quit','dddone'))
	#<_sre.SRE_Match object; span=(2, 6), match='done'>

下面的代码使用不同的方法删除字符串中多余的空格，如果遇到连续多个空格则只保留一个
	
	import re
	s='aaa   \t  bb     c d e ffff   '
	#直接使用re模块的字符串替换方法
	print(re.sub('\s+',' ',s))
	#删除两顿的字符
	print(' '.join(re.split('\s+',s.strip())))



下面的代码使用以"\"开头的元字符来实现字符串的特定搜索
	
    import re
	example="ShanDong Institute of Business and Technology is a very beautiful school. o "
	print(re.findall(r'\ba.+?   \b',example))
	#['and', 'a ']
	#因为用的是+号一定要选择一个所以是'a '
	print(re.findall(r'\ba.*?\b',example))  #以a开头的完整单词  .*?代表非贪婪匹配
	#['and', 'a']
	print(re.findall(r'\Bo.*?\b',example))  #不以o开头且含有o字母的单词剩余部分
	#['ong', 'ology', 'ool']
	print(re.findall(r'\b\w.*?\b',example)) #所有单词
	#['ShanDong', 'Institute', 'of', 'Business', 'and', 'Technology', 'is', 'a', 'very', 'beautiful', 'school', 'o']
	print(re.split('\s',example.strip()))   #使用空白字符分割字符
	#['ShanDong', 'Institute', 'of', 'Business', 'and', 'Technology', 'is', 'a', 'very', 'beautiful', 'school.', 'o']
	example="Python 2.7.8,Python 3.4.2" #查找并返回x.x.x形式的数字
	print(re.findall(r"\d\.\d\.\d",example))
	#['2.7.8', '3.4.2']


##使用正则表达式对象
>首先使用re模块的compile()方法将正则表达式编译生成正则表达式对象，然后再使用正则表达式对象提供的方法进行字符串处理，可以提高速度。

>类似直接使用

	import re
	example='BBB'
	pattern=re.compile(r'\bB\w+\b')
	pattern.findall(example)
	pattern.match(example)
	pattern.search(example)
	pattern.sub("*",example)
	pattern.split(example)
	
##子模式与match对象

###子模式
>使用圆括号"()"表示一个子模式，园括号内的内容作为一个整体出现，例如（red)+

>小心使用圆括号，不要以为他是[]的替代品，注意代码的最后

>无捕获分组..(?:string)
	
	import re
	telNumber="0535-1234567 010-12345678 025-87654321"
	pattern=re.compile(r'\d{3,4}-\d{7,8}')
	print(pattern.findall(telNumber))
	#['0535-1234567', '010-12345678', '025-87654321']
	pattern=re.compile(r'(\d{3,4})-(\d{7,8})')
	print(pattern.findall(telNumber))           #用括号会输出一个tuple
	#[('0535', '1234567'), ('010', '12345678'), ('025', '87654321')]
	
	#
	print(re.findall(r"[red]+","redredred"))
	#['redredred']
	
	print(re.findall(r"(red)+","redredred"))            #小心使用分组，输出结果只输出分组中的一部分
	#['red']

	#让正则把red看做一个整体，但又不分组.要用无捕获分组
	print(re.findall(r"(?:red)+","redredred"))           
	#['redredred']

###match对象
>正则表达式模块或正则表达式对象的match()和search()方法匹配成功后都会返回match对象。match

对象的主要方法有

group()
>返回匹配的一个或多个子模式内所有命名子模式内容的字典

groups() 
>返回所有子模式构建的元组

groupdict() 
>返回包含所有命名子模式内容的字典

start()
>子模式内容的起始位置

end()
>返回指定子模式内容的结束位置的前一个位置

span()
>起始位置，结束位置的元组

##子模式扩展语法

###(?P<groupname\>)
>为子模式命名

###(?iLmsux)	
>设置匹配标志，可以是几个字母的组合，每个字母的含义与编译标志相同

>例如忽略大小写之类
###(?:...)
>匹配但不捕获该匹配的子表达式

###(?P=groupname)
>表示在此之前的命名为groupname的子模式

>用于表示查找结果相同的，见下面代码例子

###(?#...)		不知道怎么用
>表示注释 

###(?=...)
>用于正则表达式之后，表示如果=后的内容在字符串中出现则匹配，但不返回=之后的内容
###(?!...)
>用于正则表达式之后，表示如果！后的内容在字符串中不出现则匹配，但不反回！之后的内容

###(?<=...)
>用于正则表达式之前，与(?=...)含义相同

>前向界定必须用常数
###(?<!...)
>用于正则表达式之前，与(?!...)含义相同

>前向界定必须用常数
###下面通过几个示例来演示子模式扩展语法的应用

	pattern=re.compile(r'(?<=\w\s)way(?=\s\w)')   #查找不在句子开头和结尾的单词way是待查找单词
	# 字母符号way符号字母 满足\w\sway\s\w，一定在句子中间
	pattern=re.compile(r'\b(?i)n\w+\b')#查找以n或N字母开头的所有单词
	pattern=re.compile(r'(\b\w*(?P<f>\w+)(?P=f)\w*\b)') #查找具有连续相同字母的单词
	