变量
取决于如何定义,解释器花费或多或少的时间尝试计算出它们的值.Python在尝试判定变量名时利用动态作用域规则进行处理.当它在代码中找到一个变量时,首先通过查看局部名空间字典考察该变量是不是一个局部变量.如果找到该变量,就抓取该变量的值.否则再在全局名字空间字典中进行搜索,如果需要, 还会搜索内置名字空间.因此,局部变量比其他类型变量的搜索速度要快得多,因而获得它们的值也要快得多.局部变量搜索速度快是因为它们对应于数组中的下标 操作,而全局变量搜索则对应于散列表搜索.一个良好的优化方法是：如果在函数中使用了很多全局变量,把它们的值赋给局部变量可能会有很大帮助.

回到顶部
模块
在一个脚本之中,只需一次导入一个外部模块即可.因此,在代码中不需要多个import语句.实际上,应该避免在程序中尝试再导入模块.根据以往的经验, 应该把所有的import语句放在程序头的最开始部分.然而,对一个模块多次调用import不会真正造成问题,因为它只是一个字典查找.如果必须要对一 个外部模块的某些特定属性进行大量引用,开始编写代码之前,应该考虑将这些元素复制到单个变量中(当然,如果可能的话)－－特另是如果引用在一个循环内部 进行.只要导入模块,解释器就查找该模块的字节编译版.如果未找到,它会自动对模块进行字节编译并生成.pyc文件.因此,当下次尝试导入此模块时,字节 编译文件就在那里.正如读者所体会的那样.pyc文件比常规.py文件执行起来快很多,因为它们在执行之前就已经经解释器解释过.这里的建议是尽量使用字 节编译模块.不论是否拥有.pyc文件Python代码都以相同的速度执行.惟一的区别是如果存在.pyc文件,启动将会有所加快.代码的实际运行速度没 有区别.

回到顶部
字符串
python 中的字符串对象是不可改变的，因此对任何字符串的操作如拼接，修改等都将产生一个新的字符串对象，而不是基于原字符串，因此这种持续的 copy 会在一定程度上影响 python 的性能。对字符串的优化也是改善性能的一个重要的方面，特别是在处理文本较多的情况下。

1. 在字符串连接的使用尽量使用 join() 而不是 +；

2. 当对字符串可以使用正则表达式或者内置函数来处理的时候，选择内置函数。如 str.isalpha()，str.isdigit()，str.startswith(('x', 'yz'))，str.endswith(('x', 'yz'))；

3. 对字符进行格式化比直接串联读取要快，因此要在字符串与其他变量连接时就使用格式化字符串.请查看下面的连接形式：

name="Andre" 
print "Hello " + name 
print "Hello %s" % name

显然与第一个语句相比,第二个print语句更加优化.第三行中的括号是不需要的。

回到顶部
循环
对循环的优化所遵循的原则是尽量减少循环过程中的计算量，有多重循环的尽量将内层的计算提到上一层。

可以在循环中优化大量事件以便它们可平稳运行.下面就是可优化操作的简短清单.在内循环中应该使用内置函数,而不是使用采用Python编写的函数.通过使用运行列表操作的内置函数(例如map(),reduce(),filter())代替直接循环,可以把一些循环开销转移到C代码.向 map,reduce,filter传送内置函数更会使性能得以提高.具有多重循环之时,只有最内层循环值得优化.优化多重循环时,旨在减少内存分配的次数.使最内层循环成为交互作用次数最少者应该有助于性能设计.使用局部变量会大大改善循环内部的处理时间.只要可能,在进入循环前把所有全局变量和属性搜索复制到局部变量.如果在嵌套循环内部使用诸如range(n)之类的结构方法,则在最外层循环外部把值域分配到一个局部变量并在循环定义中使用该变量将快速得多.

yRange=range(500) #优化1 
for xItem in range(100000): 
for yItem in yRange: 
print xItem,yItem

这里的另一种优化是使用xrange作为循环的x，因为100000项列表是一个相当大的列表.

yRange=range(500) 
for xItem in xRange(100000): #优化2 
for yItem in yRange: 
print xItem,yItem

回到顶部
函数
Python的内置函数比采用纯Python语言编写的函数执行速度要快,因为内置函数是采用C语言编写的.map(),filter()以及 reduce就是在性能上优于采用Python编写的函数的内置函数范例.还应了解,Python把函数名作为全局常数加以处理.既然如此,前面我们看到 的名字空间搜索的整个概念同样适用于函数.如果可以选择的话,使用map()函数的隐含循环代替for循环要快得多.我在这里提到的循环的执行时间在很大 程序上取决于传送了什么函数.传送Python函数没有传送内置函数(诸如在operator模块里的那些函数)那么快.

在Python中函数调用代价还是很大的。在计算密集的地方，很大次数的循环体中要尽量减少函数的调用及调用层次（能inline最好inline）。

回到顶部
改进算法，选择合适的数据结构
一个良好的算法能够对性能起到关键作用，因此性能改进的首要点是对算法的改进。在算法的时间复杂度排序上依次是：

O(1) -> O(lg n) -> O(n lg n) -> O(n^2) -> O(n^3) -> O(n^k) -> O(k^n) -> O(n!)

因此如果能够在时间复杂度上对算法进行一定的改进，对性能的提高不言而喻。

回到顶部
使用内建函数
你可以用Python写出高效的代码,但很难击败内建函数. 经查证. 他们非常快速.



回到顶部
使用join()连接字符串
你可以使用 "+" 来连接字符串. 但由于string在Python中是不可变的,每一个"+"操作都会创建一个新的字符串并复制旧内容. 常见用法是使用Python的数组模块单个的修改字符;当完成的时候,使用 join() 函数创建最终字符串.

>>> #This is good to glue a large number of strings 
>>> for chunk in input(): 
>>> my_string.join(chunk)

回到顶部
使用Python多重赋值，交换变量
在Python中即优雅又快速: 
>>> x, y = y, x 
这样很慢: 
>>> temp = x 
>>> x = y 
>>> y = temp

回到顶部
尽量使用局部变量
Python 检索局部变量比检索全局变量快. 这意味着,避免 "global" 关键字.

回到顶部
尽量使用 "in"
使用 "in" 关键字. 简洁而快速.

>>> for key in sequence: 
>>> print “found”

回到顶部
使用延迟加载加速
將 "import" 声明移入函数中,仅在需要的时候导入. 换句话说,如果某些模块不需马上使用,稍后导入他们. 例如,你不必在一开使就导入大量模块而加速程序启动. 该技术不能提高整体性能. 但它可以帮助你更均衡的分配模块的加载时间.

回到顶部
为无限循环使用 "while 1"
有时候在程序中你需一个无限循环.(例如一个监听套接字的实例) 尽管 "while true" 能完成同样的事, 但 "while 1" 是单步运算. 这招能提高你的Python性能.

回到顶部
使用 Lazy if-evaluation 的特性
Python 中条件表达式是 lazy evaluation 的，也就是说如果存在条件表达式 if x and y，在 x 为 false 的情况下 y 表达式的值将不再计算。因此可以利用该特性在一定程度上提高程序效率。

回到顶部
使用list comprehension和generator expression
从Python 2.0 开始,你可以使用 list comprehension 取代大量的 "for" 和 "while" 块. 使用List comprehension通常更快，Python解析器能在循环中发现它是一个可预测的模式而被优化.额外好处是，list comprehension更具可读性（函数式编程），并在大多数情况下，它可以节省一个额外的计数变量。列表解析要比在循环中重新构建一个新的 list 更为高效，因此我们可以利用这一特性来提高运行的效率。例如，让我们计算1到10之间的偶数个数：

>>> # the good way to iterate a range 
>>> evens = [ i for i in range(10) if i%2 == 0] 
>>> [0, 2, 4, 6, 8] 
>>> # the following is not so Pythonic 
>>> i = 0 
>>> evens = [] 
>>> while i < 10: 
>>> if i %2 == 0: evens.append(i) 
>>> i += 1 
>>> [0, 2, 4, 6, 8]

生成器表达式则是在 2.4 中引入的新内容，语法和列表解析类似，但是在大数据量处理时，生成器表达式的优势较为明显，它并不创建一个列表，只是返回一个生成器，因此效率较高。例如：代码 a = [w for w in list] 修改为 a = (w for w in list)，运行时间进一步减少，缩短约为 2.98s。

回到顶部
使用Dictionary comprehensions/Set comprehensions
大多数的Python程序员都知道且使用过列表推导(list comprehensions)。如果你对list comprehensions概念不是很熟悉——一个list comprehension就是一个更简短、简洁的创建一个list的方法。

>>> some_list = [1, 2, 3, 4, 5]

>>> another_list = [x + 1 for x in some_list]

>>> another_list

>>> [2, 3, 4, 5, 6]

自从python 3.1 (甚至是Python 2.7)起，我们可以用同样的语法来创建集合和字典表：

>>>#Se Comprehensions

>>> some_list = [1, 2, 3, 4, 5, 2, 5, 1, 4, 8]

>>> even_set = { x for x in some_list if x % 2 == 0 }

>>> even_set set([8, 2, 4])

>>> # Dict Comprehensions

>>> d = {x: x % 2 == 0 for x in range(1, 11)}

>>> d {1: False, 2: True, 3: False, 4: True, 5: False, 6: True, 7: False, 8: True, 9: False, 10: True}

在第一个例子里，我们以some_list为基础，创建了一个具有不重复元素的集合，而且集合里只包含偶数。而在字典表的例子里，我们创建了一个key是不重复的1到10之间的整数，value是布尔型，用来指示key是否是偶数。

这里另外一个值得注意的事情是集合的字面量表示法。我们可以简单的用这种方法创建一个集合：

>>> my_set ={1, 2, 1, 2, 3, 4}

>>> my_set

set([1, 2, 3, 4])

而不需要使用内置函数set()。

回到顶部
集合 (set) 与列表 (list)
set 的 union， intersection，difference 操作要比 list 的迭代要快。因此如果涉及到求 list 交集，并集或者差的问题可以转换为 set 来操作。

set(list1) | set(list2)

union

包含list1和list2所有数据的新集合

set(list1) & set(list2)

intersection

包含list1和list2中共同元素的新集合

set(list1) - set(list2)

difference

在list1中出现但不在list2中出现的元素的集合

回到顶部
使用dict 和 set 测试成员
Python dict中使用了 hash table，因此查找操作的复杂度为 O(1)，因此对成员的查找访问等操作字典要比 list 更快。

检查一个元素是在dicitonary或set是否存在，这在Python中非常快的。这是因为dict和set使用哈希表来实现，查找效率可以达到O(1)，而 list 实际是个数组，在 list 中，查找需要遍历整个 list，其复杂度为 O(n)，因此，如果您需要经常检查成员，使用 set 或 dict做为你的容器。

>>> mylist = ['a', 'b', 'c'] #Slower, check membership with list: 
>>> ‘c’ in mylist 
>>> True 
>>> myset = set(['a', 'b', 'c']) # Faster, check membership with set: 
>>> ‘c’ in myset: 
>>> True

回到顶部
计数时使用Counter计数对象
这听起来显而易见，但经常被人忘记。对于大多数程序员来说，数一个东西是一项很常见的任务，而且在大多数情况下并不是很有挑战性的事情——这里有几种方法能更简单的完成这种任务。

Python的collections类库里有个内置的dict类的子类，是专门来干这种事情的：

>>>from collections import Counter

>>>c = Counter('hello world')

>>>c

Counter({'l': 3, 'o': 2, ' ': 1, 'e': 1, 'd': 1, 'h': 1, 'r': 1, 'w': 1})

>>>c.most_common(2)

[('l', 3), ('o', 2)]

回到顶部
使用xrange()处理长序列
这样可为你节省大量的系统内存，因为xrange()在序列中每次调用只产生一个整数元素。而相反 range()，它將直接给你一个完整的元素列表，用于循环时会有不必要的开销。

回到顶部
使用 Python generator
这也可以节省内存和提高性能。例如一个视频流，你可以一个一个字节块的发送，而不是整个流。例如：

>>> chunk = ( 1000 * i for i in xrange(1000)) 
>>> chunk 
>>> chunk.next() 
0 
>>> chunk.next() 
1000 
>>> chunk.next() 
2000

回到顶部
了解itertools模块
该模块对迭代和组合是非常有效的。让我们生成一个列表[1，2，3]的所有排列组合,仅需三行Python代码：

>>> import itertools 
>>> iter = itertools.permutations([1,2,3]) 
>>> list(iter) 
[(1, 2, 3), (1, 3, 2), (2, 1, 3), (2, 3, 1), (3, 1, 2), (3, 2, 1)]

回到顶部
学习bisect模块保持列表排序
这是一个免费的二分查找实现和快速插入有序序列的工具。也就是说，你可以使用：

>>> import bisect 
>>> bisect.insort(list, element) 
你已將一个元素插入列表中, 而你不需要再次调用 sort() 来保持容器的排序, 因为这在长序列中这会非常昂贵.

回到顶部
理解Python列表，实际上是一个数组
Python中的列表实现并不是以人们通常谈论的计算机科学中的普通单链表实现的。Python中的列表是一个数组。也就是说，你可以以常量时间O(1) 检索列表的某个元素，而不需要从头开始搜索。这有什么意义呢？ Python开发人员使用列表对象insert()时, 需三思.

例如：>>> list.insert（0，item）

在列表的前面插入一个元素效率不高, 因为列表中的所有后续下标不得不改变. 然而，您可以使用list.append()在列表的尾端有效添加元素. 优先选择deque，如果你想快速的在插入或删除时。它是快速的，因为在Python中的deque用双链表实现。

回到顶部
使用Schwartzian Transform 的 sort()
原生的list.sort（）函数是非常快的。 Python会按自然顺序排序列表。有时，你需要非自然顺序的排序。例如，你要根据服务器位置排序的IP地址。 Python支持自定义的比较，你可以使用list.sort（CMP（）），这会比list.sort（）慢，因为增加了函数调用的开销。如果性能有问 题，你可以申请Guttman-Rosler Transform,基于Schwartzian Transform. 它只对实际的要用的算法有兴趣，它的简要工作原理是，你可以变换列表，并调用Python内置list.sort（） - > 更快，而无需使用list.sort（CMP（） ）->慢。



回到顶部
Python装饰器缓存结果
“@”符号是Python的装饰语法。它不只用于追查，锁或日志。你可以装饰一个Python函数，记住调用结果供后续使用。这种技术被称为memoization的。下面是一个例子：

>>> from functools import wraps 
>>> def memo(f): 
>>> cache = { } 
>>> @wraps(f) 
>>> def wrap(*arg): 
>>> if arg not in cache: cache['arg'] = f(*arg) 
>>> return cache['arg'] 
>>> return wrap 
我们也可以对 Fibonacci 函数使用装饰器: 
>>> @memo 
>>> def fib(i): 
>>> if i < 2: return 1 
>>> return fib(i-1) + fib(i-2)

这里的关键思想是:增强函数(装饰)函数,记住每个已经计算的Fibonacci值;如果它们在缓存中,就不需要再计算了.

回到顶部
理解Python的GIL（全局解释器锁）
GIL是必要的，因为CPython的内存管理是非线程安全的。你不能简单地创建多个线程，并希望Python能在多核心的机器上运行得更快。这是因为 GIL將会防止多个原生线程同时执行Python字节码。换句话说，GIL將序列化您的所有线程。然而，您可以使用线程管理多个派生进程加速程序，这些程 序独立的运行于你的Python代码外。

回到顶部
使用multiprocessing模块实现真正的并发
因为GIL会序列化线程, Python中的多线程不能在多核机器和集群中加速. 因此Python提供了multiprocessing模块, 可以派生额外的进程代替线程, 跳出GIL的限制. 此外, 你也可以在外部C代码中结合该建议, 使得程序更快.

注意, 进程的开销通常比线程昂贵, 因为线程自动共享内存地址空间和文件描述符. 意味着, 创建进程比创建线程会花费更多, 也可能花费更多内存. 这点在你计算使用多处理器时要牢记.



 

回到顶部
本地代码
好了, 现在你决定为了性能使用本地代码. 在标准的ctypes模块中, 你可以直接加载已编程的二进制库(.dll 或 .so文件)到Python中, 无需担心编写C/C++代码或构建依赖. 例如, 我们可以写个程序加载libc来生成随机数。

然而, 绑定ctypes的开销是非轻量级的. 你可以认为ctypes是一个粘合操作系库函数或者硬件设备驱动的胶水. 有几个如 SWIG, Cython和Boost 此类Python直接植入的库的调用比ctypes开销要低. Python支持面向对象特性, 如类和继承. 正如我们看到的例子, 我们可以保留常规的C++代码, 稍后导入. 这里的主要工作是编写一个包装器 (行 10~18).



回到顶部
像熟悉文档一样的熟悉Python源代码
Python有些模块为了性能使用C实现。当性能至关重要而官方文档不足时，可以自由探索源代码。你可以找到底层的数据结构和算法。

回到顶部
其他优化技巧
1. 如果需要交换两个变量的值使用 a,b=b,a 而不是借助中间变量 t=a;a=b;b=t；

>>> from timeit import Timer

>>> Timer("t=a;a=b;b=t","a=1;b=2").timeit()

0.25154118749729365

>>> Timer("a,b=b,a","a=1;b=2").timeit()

0.17156677734181258

>>>

2. 在循环的时候使用 xrange 而不是 range；使用 xrange 可以节省大量的系统内存，因为 xrange() 在序列中每次调用只产生一个整数元素。而 range() 將直接返回完整的元素列表，用于循环时会有不必要的开销。在 python3 中 xrange 不再存在，里面 range 提供一个可以遍历任意长度的范围的 iterator。

3. 使用局部变量，避免"global" 关键字。python 访问局部变量会比全局变量要快得多，因此可以利用这一特性提升性能。

4. if done is not None 比语句 if done != None 更快，读者可以自行验证；

5. 在耗时较多的循环中，可以把函数的调用改为内联的方式；

6. 使用级联比较 "x < y < z" 而不是 "x < y and y < z"；

7. while 1 要比 while True 更快（当然后者的可读性更好）；

8. build in 函数通常较快，add(a,b) 要优于 a+b。

结论

这些不能替代大脑思考. 打开引擎盖充分了解是开发者的职责,使得他们不会快速拼凑出一个垃圾设计. 以上的Python建议可以帮助你获得好的性能. 如果速度还不够快, Python將需要借助外力:分析和运行外部代码。

回到顶部
工具优化
有益的提醒,静态编译的代码仍然重要. 仅例举几例, Chrome,Firefox,MySQL,MS Office 和 Photoshop都是高度优化的软件,我们每天都在使用. Python作为解析语言,很明显不适合. 不能单靠Python来满足那些性能是首要指示的领域. 这就是为什么Python支持让你接触底层裸机基础设施的原因, 将更繁重的工作代理给更快的语言如C. 这高性能计算和嵌入式编程中是关键的功能.

 

回到顶部
首先 拒绝调优诱惑


调优给你的代码增加复杂性. 集成其它语言之前, 请检查下面的列表. 如果你的算法是"足够好", 优化就没那么迫切了.

1. 你做了性能测试报告吗? 
2. 你能减少硬盘的 I/O 访问吗? 
3. 你能减少网络 I/O 访问吗? 
4. 你能升级硬件吗? 
5. 你是为其它开发者编译库吗? 
6. 你的第三方库软件是最新版吗?

对代码优化的前提是需要了解性能瓶颈在什么地方，程序运行的主要时间是消耗在哪里，对于比较复杂的代码可以借助一些工具来定位，python内置了丰富的性能分析工具，如 profile,cProfile 与 hotshot 等。其中 Profiler是python 自带的一组程序，能够描述程序运行时候的性能，并提供各种统计帮助用户定位程序的性能瓶颈。Python 标准模块提供三种 profilers:cProfile,profile 以及 hotshot。

回到顶部
使用工具监控代码 而不是直觉
速度的问题可能很微妙, 所以不要依赖于直觉. 感谢 "cprofiles" 模块, 通过简单的运行你就可以监控Python代码.

1. “python -m cProfile myprogram.py”



2. 使用import profile模块

import profile

def profileTest():

Total =1;

for i in range(10):

Total=Total*(i+1)

print Total

return Total

if __name__ == "__main__":

profile.run("profileTest()")

程序的运行结果如下：



其中输出每列的具体解释如下：

ncalls：表示函数调用的次数；

tottime：表示指定函数的总的运行时间，除掉函数中调用子函数的运行时间；

percall：（第一个 percall）等于 tottime/ncalls；

cumtime：表示该函数及其所有子函数的调用运行的时间，即函数开始调用到返回的时间；

percall：（第二个 percall）即函数运行一次的平均时间，等于 cumtime/ncalls；

filename:lineno(function)：每个函数调用的具体信息；

如果需要将输出以日志的形式保存，只需要在调用的时候加入另外一个参数。如 profile.run("profileTest()","testprof")。

对于大型应用程序，如果能够将性能分析的结果以图形的方式呈现，将会非常实用和直观，常见的可视化工具有 Gprof2Dot，visualpytune，KCacheGrind 等，读者可以自行查阅相关官网。

回到顶部
审查时间复杂度
控制以后, 提供一个基本的算法性能分析. 恒定时间是理想值. 对数时间复度是稳定的. 阶乘复杂度很难扩展.

O(1) -> O(lg n) -> O(n lg n) -> O(n^2) -> O(n^3) -> O(n^k) -> O(k^n) -> O(n!)

