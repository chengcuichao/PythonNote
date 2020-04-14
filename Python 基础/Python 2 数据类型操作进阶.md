### 字符串操作

#### 分割字符串

`re.split` 允许你为分隔符指定多个正则模式

```python
import re

line='asdf fjdk; afed, fjek,asdf, foo'
re.split(r'[;,\s]\s*', line)
```

#### 查询匹配

`startswith()` ，`endswith()`匹配字符串开头或结尾，如果你想检查多种匹配可能，只需要将所有的匹配项放入到一个元组中去。

```python
a = 'asdfdfgzxcv'

a.startswith(('as','df'))  #返回True或False
a.find('zxcv')			   #返回匹配到的index
```

#### 字符串对齐

可以使用字符串的`ljust()`，`rjust()`和`center()`方法

```python
text='Hello World'

text.center(20) 	  #两边填充
text.ljust(20,'-')   #右面填充
text.rjust(20,'=')    #左面填充
```

使用format也可以实现，<,>或者^分别相对右面，左面和中间

```python
format(text,'>20')
format(text,'=>20s')
'{:>10s} {:>10s}'.format('Hello','World')  #必须加:号
```

#### 字符串的拼接

想要合并的字符串是在一个序列或者`iterable`中，那么最快的方式就是使用join()方法。

```python
parts=['Is','Chicago','Not','Chicago?']
''.join(parts)
```

如果列表含有非字符串

```python
''.join(str(item) for item inparts)
```

**+=这种写法会比使用join()方法运行的要慢一些，因为每一次执行+=操作的时候会创建一个新的字符串对象。**

#### 字符串的变量替换

`format()` 使用的几种形式

```python
'adas{} {}'.format('cheng','123')
'adas{0} {1}'.format('cheng','123')
'adas{0} {1}'.format('cheng','123')
'adas{name} {pwd}'.format(name='cheng',pwd='123')
```

`format_map()` 如果要被替换的变量能在变量域中找到，那么你可以结合使用`format_map()`和`vars()`，`vars()` 还有一个有意思的特性就是它也适用于对象实例

```python
s='{name} has {n} messages.'

class Info:
    def __init__(self, name, n):
        self.name=name
        self.n=n

a=Info('Guido',37)
s.format_map(vars(a))
```

#### 指定列宽格式化字符串

`textwrap` 模块来格式化字符串的输出

```python
import textwrap

print(textwrap.fill(s,70))
print(textwrap.fill(s,40))
print(textwrap.fill(s,40, initial_indent='    '))  #每行四十个字符，开头缩进

#自动匹配终端大小的时候
import os
os.get_terminal_size().columns #获取终端的大小尺寸
```

### 其他类型

#### 解压可迭代对象赋值给多个变量

以下这种解压赋值可以用在任何可迭代对象上面，而不仅仅是列表或者元组。包括字符串，文件对象，迭代器和生成器。

```python
# 这种必须与可迭代对象数量相同：
data=['ACME',50,91.1, (2012,12,21) ]

name, shares, price, date=data
print(name, shares, price, date)

name, shares, price, (year, mon, day)=data
print(name, shares, price,year, mon, day)

# 也可以使用任意变量名去占位如_,ign（ignore）：
_, shares, price, _ = data

# 如果不确定有多少个可以用*+变量名如：
record=('Dave','dave@example.com','773-555-1212','847-555-1212')
name, email,*phone_numbers=record
print(name, email,phone_numbers)
```

#### 保留最后N个元素

```python
from collections import deque

# 使用deque(maxlen=N)构造函数会新建一个固定大小的队列。当新的元素加入并且这个队列已满的时候，最老的元素会自动被移除掉。

QueueTemp = deque([10],maxlen=10)
QueueTemp.append(1)      #末尾添加
QueueTemp.appendleft(2)  #开头添加
QueueTemp.pop()          #末尾删除并返回
QueueTemp.popleft()      #开头删除并返回
QueueTemp.remove(2)      #移除一个元素返回None

# 在队列两端插入或删除元素时间复杂度都是O(1)，而在列表的开头插入或删除元素的时间复杂度为O(N)
```

#### 查找最大或最小的N个元素

 Python标准库模块之`heapq`，该模块提供了堆排序算法的实现。`heapq`堆数据结构最重要的特征是heap[0]永远是最小的元素，我们一般使用二叉堆来实现优先级队列。

它的内部调整算法复杂度为l`logN`，`heapq`详细的介绍可参考：https://www.cnblogs.com/chimeiwangliang/p/12431002.html

```python
#拿到nums最小的前五个和最大的前五个，拿到portfolio中price最大的前三个

nums=[1,8,2,23,7,-4,18,23,42,37,2]
portfolio=[
    {'name':'IBM','shares':100,'price':91.1},
    {'name':'AAPL','shares':50,'price':543.22},
    {'name':'FB','shares':200,'price':21.09},
    {'name':'HPQ','shares':35,'price':31.75},
    {'name':'YHOO','shares':45,'price':16.35},
    {'name':'ACME','shares':75,'price':115.65}]

# 1、使用heapq
import heapq

Large = heapq.nlargest(5,nums)
Small = heapq.nsmallest(5,nums)
print(Small,Large)

# 两个函数都能接受一个关键字参数，用于更复杂的数据结构中

def GetData(Data):
    return Data['price']

Large_1 =heapq.nlargest(3,portfolio,key=GetData)
#也可以使用匿名函数,简单快捷
Large_2 =heapq.nlargest(3,portfolio,key=lambda x:x['price'])
print(Large_2)

# 2、可以使用sorted

NewNums = sorted(nums)
print(NewNums[:5],NewNums[-5:])

NewPortfolio = sorted(portfolio,key=lambda x:x['price'])
print(NewPortfolio[:3])

# 3、可以使用sort

nums.sort()
print(nums[:5],nums[-5:])

portfolio.sort(key=lambda x:x['price'])
print(NewPortfolio[:3])

# 以上输出的结果是一样的
'''
[-4, 1, 2, 2, 7] [42, 37, 23, 23, 18]
[{'name': 'AAPL', 'shares': 50, 'price': 543.22}, {'name': 'ACME', 'shares': 75, 'price': 115.65}, {'name': 'IBM', 'shares': 100, 'price': 91.1}]
'''
```

#### 实现一个优先级队列

可以使用`heapq.heappush`和`heapq.heappop`来根据元组的第一个元素进行排序。

```python
import heapq

class PriorityQueue:
    def __init__(self):
        self._queue=[]
        self._index=0
    def push(self, item, priority):
        heapq.heappush(self._queue, (-priority,self._index, item))
        self._index+=1
    def pop(self):
        return heapq.heappop(self._queue)[-1]

class Item:
    def __init__(self, name):
     self.name=name
    def __repr__(self):
        return'Item({!r})'.format(self.name)


q=PriorityQueue()

q.push(Item('foo'),1)
q.push(Item('bar'),5)
q.push(Item('spam'),4)
q.push(Item('grok'),1)

print(q.pop(),q.pop())
>>Item('bar') Item('spam')

另外注意到如果两个有着相同优先级的元素（foo和grok），pop操作按照它们被插入到队列的顺序返回的。
```

#### 字典中的键映射多个值

我们往往向字典里面写入值的时候不知道这个键有没有，所以每次得需要判断下，可以使用collections模块中的`defaultdict`来构造这样的字典。`defaultdict` 的一个特征是它会。

自动初始化每个key刚开始对应的值。

```python
from collections import defaultdict

#一般会先判断是否有这个值
a = {}
for i in range(10):
    if not a.get(i):
        a[i] = []
    a[i].append(i)

#使用defaultdict就不必关心是否有没有这个键了
b = defaultdict(list)
[b[i].append(i) for i in range(10)]

print(a,b)
>>{0: [0], 1: [1], 2: [2], 3: [3], 4: [4], 5: [5], 6: [6], 7: [7], 8: [8], 9: [9]} defaultdict(<class 'list'>, {0: [0], 1: [1], 2: [2], 3: [3], 4: [4], 5: [5], 6: [6], 7: [7], 8: [8], 9: [9]})
```

#### 字典保持排序

为了能控制一个字典中元素的顺序，可以使用collections模块中的`OrderedDict`类。在迭代操作的时候它会保持元素被插入时的顺序。

```python
from collections import OrderedDict
import json

d = OrderedDict()
d['foo']=1
d['bar']=2
d['spam']=3
d['grok']=4

print(d)
print(json.dumps(d))
>>OrderedDict([('foo', 1), ('bar', 2), ('spam', 3), ('grok', 4)])
>>{"foo": 1, "bar": 2, "spam": 3, "grok": 4}
```

#### 字典数据的排序

```python
#将下面以value排序并取出最大最小值
prices={'ACME':45.23,
        'AAPL':612.78,
        'IBM':205.55,
        'HPQ':37.20,
        'FB':10.75}

# 1、使用sorted
a = sorted(prices.items(),key=lambda x:x[1])
print(a[0],a[-1])
>>('FB', 10.75) ('AAPL', 612.78)

# 2、使用heapq
import heapq

b = heapq.nsmallest(len(prices),prices.items(),key=lambda x:x[1])
print(b[0],b[-1])
>>('FB', 10.75) ('AAPL', 612.78)

# 取出最大最小值也可以用
max(zip(prices.values(),prices.keys()),key=lambda x:x[0])
min(zip(prices.values(),prices.keys()),key=lambda x:x[0])
```

#### 命名切片

一般来讲，代码中如果出现大量的硬编码下标值会使得可读性和可维护性大大降低。比如，如果你回过来看看一年前你写的代码，你会摸着脑袋想那时候自己到底想干嘛啊。这里的解决方案是一个很简单的方法让你更加清晰的表达代码到底要做什么。

```python
items=[0,1,2,3,4,5,6]
s = slice(2,30)
print(items[s])
print(items[2:30])

'''
	你还能通过调用切片的indices(size)方法将它映射到一个确定大小的序列上，这个方法返回一个三元组(start, stop, step)，所有值都会被合适的缩小以满足边界限制，从而使用的时候避免出现IndexError异常你还能通过调用切片的indices(size)方法将它映射
'''
到一个确定大小的序列上。
a=slice(5,50,2)
s='HelloWorld'
a.indices(len(s))
for i in range(*a.indices(len(s))):
    print(s[i])
```

#### 列表中出现次数最多的元素

`collections.Counter`类就是专门为这类问题而设计的，它甚至有一个有用的most_common()方法直接给了你答案。

```python
from collections import Counter


words=['look','into','my','eyes','look','into','my',
       'eyes','the','eyes','the','eyes','the','eyes',
       'not','around','the','eyes',"don't",'look','around',
       'the','eyes','look','into','my','eyes',"you're",'under']


WordCounter = Counter(words)

TopThree = WordCounter.most_common(3)
#作为输入，Counter对象可以接受任意的由可哈希（hashable）元素构成的序列对象。在底层实现上，一个Counter对象就是一个字典，将元素映射到它出现的次数上。

#Counter实例一个鲜为人知的特性是它们可以很容易的跟数学运算操作相结合

morewords=['why','are','you','not','looking','in','my','eyes']

MoreWordCounter = Counter(morewords)

print(WordCounter - MoreWordCounter)
print(WordCounter + MoreWordCounter)

>>Counter({'eyes': 7, 'the': 5, 'look': 4, 'into': 3, 'my': 2, 'around': 2, "don't": 1, "you're": 1, 'under': 1})
>>Counter({'eyes': 9, 'the': 5, 'look': 4, 'my': 4, 'into': 3, 'not': 2, 'around': 2, "don't": 1, "you're": 1, 'under': 1, 'why': 1, 'are': 1, 'you': 1, 'looking': 1, 'in': 1})
```

#### 映射名称到序列元素

 `collections.namedtuple()`函数通过使用一个普通的元组对象来帮你解决这个问题。这个函数实际上是一个返回Python中标准元组类型子类的一个工厂方法。你需要传递一个类型名和你需要的字段给它，然后它就会返回一个类，你可以初始化这个类，为你定义的字段传递值等。

```python
from collections import namedtuple

Subscriber=namedtuple('Subscriber', ['addr','joined'])
sub=Subscriber('jonesy@example.com','2012-10-19')

#但是需要注意的是，不像字典那样，一个命名元组是不可更改的
print(sub.addr)
print(sub.joined)
```

****

**以上内容为Python Cookbook所记的笔记**