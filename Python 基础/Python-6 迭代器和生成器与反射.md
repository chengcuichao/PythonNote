### 生成器

通过列表生成式，我们可以直接创建一个列表，但是，受到内存限制，列表容量肯定是有限的，而且创建一个包含100万个元素的列表，不仅占用很大的存储空间，如果我们仅仅需要访问前面几个元素，那后面绝大多数元素占用的空间都白白浪费了。所以，如果列表元素可以按照某种算法推算出来，那我们是否可以在循环的过程中不断推算出后续的元素呢？这样就不必创建完整的list，从而节省大量的空间。在Python中，这种一边循环调用一边生成计算并返回新的数据的机制，称为生成器：generator。

生成器是一个特殊的程序，可以被用作控制循环的迭代行为，python中生成器是迭代器的一种，使用yield返回值函数，每次调用yield会暂停，而可以使用next()函数和send()函数恢复生成器。

　　生成器类似于返回值为数组的一个函数，这个函数可以接受参数，可以被调用，但是，不同于一般的函数会一次性返回包括了所有数值的数组，生成器一次只能产生一个值，这样消耗的内存数量将大大减小，而且允许调用函数可以很快的处理前几个返回值，因此生成器看起来像是一个函数，但是表现得却像是迭代器

```python
#1、普通生成式创建
# 要创建一个generator，有很多种方法，第一种方法很简单，只要把一个列表生成式的[]中括号改为（）小括号，就创建一个generator

(x**x for x in [1,2,3,4,5,6])
<generator object <genexpr> at 0x000001E15E3CEB48>

# 也可以直接使用iter(),将可迭代对象变成一个生成器

iter([1,2,3,4,5,6])
<list_iterator object at 0x000001E15E3D3CC0>

#2、函数中创建生成器
def IterCreate(count):
    OneIter,TwoIter,Init = 1,1,1
    while Init <= count:
        OneIter,TwoIter = TwoIter,OneIter+TwoIter
        Init += 1
        yield OneIter

IterCreate(10)
<generator object IterCreate at 0x000001E15E3CECA8>

#生成斐波那契前10项
for item in IterCreate(10):
    print(item)

#3、类中创建生成器

class IterCreate():

    def __init__(self,data):
        self.data = data  

    def __repr__(self):
        '''初始化实例时直接返回'''
        return ''

    def Create(self):
        return iter(self.data)

    def __iter__(self):
        return iter(self.data)

# 直接使用IterCreate([1,2,3,4])返回的是'',当使用for循环的时候会返回的是__iter__执行的结果

for item in IterCreate([1,2,3,4]):
    print(item)
```

### 迭代器

我们已经知道，可以直接作用于`for`循环的数据类型有以下几种：

一类是集合数据类型，如`list`、`tuple`、`dict`、`set`、`str`等；一类是`generator`，包括生成器和带`yield`的generator function。这些可以直接作用于`for`循环的对象统称为可迭代对象：`Iterabl``e`。而生成器不但可以作用于`for`循环，还可以被`next()`函数不断调用并返回下一个值，直到最后抛出`StopIteration`错误表示无法继续返回下一个值了。可以被`next()`函数调用并不断返回下一个值的对象称为迭代器：`Iterator`。

　　迭代器是访问集合元素的一种方式。迭代器对象从集合的第一个元素开始访问，直到所有的元素被访问完结束。迭代器的特点：

1. **访问者不需要关心迭代器内部的结构，仅需通过next()方法不断去取下一个内容**
2. **不能随机访问集合中的某个值 ，只能从头到尾依次访问**
3. **访问到一半时不能往回退**
4. **便于循环比较大的数据集合，节省内存**

```python
a='hello'           #字符串是可迭代对象，但不是迭代器
l=[1,2,3,4]          #列表是可迭代对象，但不是迭代器
t=(1,2,3)            #元组是可迭代对象，但不是迭代器
d={'a':1}            #字典是可迭代对象，但不是迭代器
set={1,2,3}          #集合是可迭代对象，但不是迭代器
f=open('test.txt')  #文件是可迭代对象，是迭代器

#判断是否是迭代器
from collections import Iterator  # 迭代器
from collections import Iterable  # 可迭代对象

s = [1,2,3]
print(isinstance(s, Iterator))  # 判断是不是迭代器
print(isinstance(s, Iterable))  # 判断是不是可迭代对象


def IterCreate(count):
    OneIter,TwoIter,Init = 1,1,1
    while Init <= count:
        OneIter,TwoIter = TwoIter,OneIter+TwoIter
        Init += 1
        yield OneIter

IterCreate(10)
#上述生成器是可迭代对象也是生成器
```

### 生成器与迭代器进阶实例

#### 反向迭代

```python
# 使用内置的reversed()函数
a=[1,2,3,4]

for x in reversed(a):
    print(x)

# 反向迭代仅仅当对象的大小可预先确定或者对象实现了__reversed__()的特殊方法时才能生效。如果两者都不符合，那你必须先将对象转换为一个列表才行

f=open('somefile')
for line in reversed(list(f)):
    print(line, end='')

# 将其预先转换为一个列表要消耗大量的内存。

# 在自定义类上实现__reversed__()方法来实现反向迭代。

class CountDown():

    def __init__(self,start):
        self.start = start

    def __iter__(self):
        n = self.start
        while n > 0:
            n -= 1
            yield n

    def __reversed__(self):
        n = 0
        while n < self.start:
            n += 1
            yield n

for item in CountDown(30):
    print(item)

for item in reversed(CountDown(30)):
    print(item)

```

#### 带有外部状态的生成器函数

```python
from collections import deque

'''
    关于生成器，很容易掉进函数无所不能的陷阱。如果生成器函数需要跟你的程序其他部分打交道的话(比如暴露属性值，允许通过方法调用来控制等等)，可能会导致你的代码异常的复杂。如果是这种情况的话，可以考虑使用上面介绍的定义类的方式。在__iter__()方法中定义你的生成器不会改变你任何的算法逻辑。由于它是类的一部分，所以允许你定义各种属性和方法来供用户使用。
    一个需要注意的小地方是，如果你在迭代操作时不使用for循环语句，那么你得先调用iter()函数。
'''
class LineHistory():

    def __init__(self,lines,histlen=3):
        self.lines = lines
        self.history = deque(maxlen=histlen)

    def __iter__(self):
        for lineno,line in enumerate(self.lines,1):
            self.history.append((lineno,line))
            yield line

    def clear(self):
        self.history.clear()

Line = LineHistory(range(100))

for item in Line:
    if item == 50:
        print(Line.history)
        Line.clear()
    print(Line.history)
```

#### 迭代器切片

迭代器和生成器不能使用标准的切片操作，因为它们的长度事先我们并不知道(并且也没有实现索引)。函数islice()返回一个可以生成指定元素的迭代器，它通过遍历并丢弃直到切片开始索引位置的所有元素。然后才开始一个个的返回元素，并直到切片结束索引位置。

```python
import itertools

def count():
    n = 1
    while True:
        yield n
        n += 1

count()[10,20] #直接操作会失败

for item in itertools.islice(count(),10,20):
    print(item)
```

#### 跳过可迭代对象的开始部分

```python
'''
    itertools.dropwhile()函数。使用时，你给它传递一个函数对象和一个可迭代对象。它会返回一个
迭代器对象，丢弃原有序列中直到函数返回Flase之前的所有元素，然后返回后面所有元素。
'''

from itertools import dropwhile

with open('/etc/passwd') as f:
    for line in dropwhile(lambda line: line.startswith('#') ,f):
        print(line, end='')
```

#### 排列组合的迭代

```python
from itertools import permutations,combinations,combinations_with_replacement

a = ['a','b','c','d']

#itertools.permutations()，它接受一个集合并产生一个元组序列，每个元组由集合中所有元素的一个可能排列组成。也就是说通过打乱集合中元素排列顺序生成一个元组
for item in permutations(a):
    print(item)

# 使用itertools.combinations()可得到输入集合中元素的所有的组合
for item in combinations(a,2):
    print(item)
    
# 允许同一个元素被选择多次
for item in combinations_with_replacement(a,3):
    print(item)
```

#### 序列上索引值迭代

内置的enumerate()函数可以很好的解决这个问题

```python
# 这种情况在你遍历文件时想在错误消息中使用行号定位时候非常有用

my_list=['a','b','c']
for idx, val in enumerate(my_list):
    print(idx, val)

# 为了按传统行号输出(行号从1开始)

for idx, val in enumerate(my_list):
    print(idx, val)
```

#### 同时迭代多个列表

为了同时迭代多个序列，使用zip()函数

```python
xpts=[1,5,4,2,10,7]
ypts=[101,78,37,15,62,99]

for x,y in zip(xpts, ypts):
    print(x,y)

a=[1,2,3]
b=['w','x','y','z']

# zip(a, b)会生成一个可返回元组(x, y)的迭代器，其中x来自a，y来自b。一旦其中某个序列到底结尾，迭代宣告结束。因此迭代长度跟参数中最短序列长度一致。

# 如果这个不是你想要的效果，那么还可以使用itertools.zip_longest()函数来代替。短的数据会以None补充

from itertools import zip_longest

for i in zip_longest(a,b):
    print(i)
```

#### 不同集合上元素的迭代

`itertools.chain()` 接受一个或多个可迭代对象最为输入参数。然后创建一个迭代器，依次连续的返回每个可迭代对象中的元素。这种方式要比先将序列合并再迭代要高效的多

```python
# 使用chain()的一个常见场景是当你想对不同的集合中所有元素执行某些操作的时候。

from itertools import chain

a=[1,2,3,4]
b=['x','y','z']
for x in chain(a, b):
    print(x)

# 这种解决方案要比像使用两个单独的循环更加优雅
```

### 反射

在程序开发中，常常会遇到这样的需求：在执行对象中的某个方法，或者在调用对象的某个变量，但是由于一些原因，我们无法确定或者并不知道该方法或者变量是否存在，这时我们需要一个特殊的方法或者机制来访问或操作该未知的方法或变量，这种机制就被称之为反射。

反射机制：反射就是通过字符串的形式，导入模块；**通过字符串的形式，去模块中寻找指定方法和属性，对其进行操作。也就是利用字符串的形式去对象(模块)中操作(查找or获取or删除or添加)成员。**

```python
#方法说明：

hasattr(obj,name_str)         #判断objec是否有name_str这个方法或者属性
getattr(obj,name_str,default) #获取object对象中与name_str同名的方法或者函数,没有默认返回default
setattr(obj,name_str,value)   #为object对象设置一个以name_str为名的value方法或者属性
delattr(obj,name_str)         #删除object对象中的name_str属性


class auth():

    def __init__(self,name):
        self.name = name

    def send(self):
        return '{},Func:send'.format(self.name)

    def get(self):
        return '{},Func:get'.format(self.name)

Auth = auth('jack')

print(hasattr(Auth,'name'))
print(getattr(Auth,'sen1d',object)())
print(setattr(Auth,'count',lambda x:x**x))
print(delattr(Auth,'name'))                     #删除的必须写属性，方法是不可以在实例里面删除，只能在类里面删除
delattr(auth,'send')

Auth1 = auth('jack')
Auth2 = auth('cheng')

#注意想要所有实例化的实例能用新添加的方法，需要在类里面添加，如果在实例里面添加，只能这个实例才能访问，还有需要注意的是在实例里添加不需要传self
setattr(auth,'count',lambda self,x:x**x)

print(Auth1.count(10))
print(Auth2.count(12))
```

#### 动态导入模块

```python
import importlib
 
__import__('import_lib.metaclass') #这是解释器自己内部用的
#importlib.import_module('import_lib.metaclass') #与上面这句效果一样，官方建议用这个
```

