#2016/1/27学习内容 
#第二章 Python序列-复杂的数据结构

##堆
	import heapq
	#添加元素进堆
	heapq.heappush(heap,n)
	#小根堆堆顶
	heapq.heappop(heap)
	#列表转换为堆
	heapq.heapify(myheap)
	#替换堆顶元素
	heapq.heapreplace(myheap,6)
	#返回前三个最大最小的元素
	heapq.nlargest(3,myheap)
	heapq.nsmallest(3,myheap)
	#更多请查阅资料
##队列
	import Queue
	#初始化
	q=Queue.Queue()	
	#入队	
	q.put(1)
	#出队并返回值
	q.get()
###还有更多的扩展
- 后进先出队列
- 优先队列
- collections模块的双端队列
- 以后使用时查询
##栈
	直接利用列表就好..
	只用append和pop...