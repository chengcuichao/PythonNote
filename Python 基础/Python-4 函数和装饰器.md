### 函数

#### 函数的参数

1. 位置参数，调用函数时根据函数定义的参数位置来传递参数。
2. 关键字参数，用于函数调用，通过“键-值”形式加以指定。可以让函数更加清晰、容易使用，同时也清除了参数的顺序需求。
3. 默认参数，用于定义函数，为参数提供默认值，调用函数时可传可不传该默认参数的值（注意：所有位置参数必须出现在默认参数前，包括函数定义和调用）
4. 参数组，有时候我们不确定调用的时候会传递多少个参数(不传参也可以)。此时，可用包裹(packing)位置参数，或者包裹关键字参数，来进行参数传递。

```python
#基本原则是：先位置参数，默认参数，包裹位置，包裹关键字(定义和调用都应遵循)

def name(a,b,c,d=1,*args,**kwargs):
    print(a,b,c,d,args,kwargs)
name(2,2,3,33,'asda',asd=1212,bbs=1213)

>>2 2 3 33 ('asda',) {'asd': 1212, 'bbs': 1213}
```

 注：`*args` 表示任何多个无名参数，它是一个tuple；`**kwargs` 表示关键字参数，它是一个dict。并且同时使用`*args`和`**kwargs`时，必须`*args`参数列要在`**kwargs`前。

#### 匿名函数

　　尽管lambda表达式允许你定义简单函数，但是它的使用是有限制的。你只能指定单个表达式，它的值就是最后的返回值。也就是说不能包含其他的语言特性了，包括多个语句、条件表达式、迭代以及异常处理等等。你可以不使用lambda表达式就能编写大部分python代码。但是，当有人编写大量计算表达式值的短小函数或者需要用户提供回调函数的程序的时候，你就会看到lambda表达式的身影了。

```python
lambda a,b:a**b
```

#### 进阶操作

##### 减少可调用对象的参数个数

```python
from functools import partial

def sum(x,y,z):
    return x+y+z

#partial可以固定一个和多个参数
sum_1 = partial(sum,y=1,x=1)

print(sum_1(z=3))

#可以看出partial()固定某些参数并返回一个新的callable对象。这个新的callable接受未赋值的参数，然后跟之前已经赋值过的参数合并起来，最后将所有参数传递给原始函数。
```

##### 将单方法的类转换为函数

```python
# 大多数情况下，可以使用闭包来将单个方法的类转换成函数
import requests

def urltemplate(template):
    def opener(**kwargs):
        return requests.get(template.format_map(kwargs))

    return opener

BaiDu = urltemplate('https://baidu.com/')

print(BaiDu(fields='sl1c1v').text)

# 简单来讲，一个闭包就是一个函数，只不过在函数内部带上了一个额外的变量环境。闭包关键特点就是它会记住自己被定义时的环境。

```

##### 带额外状态信息的回调函数

```python
def apply_async(func,args,*,callback):
    result = func(*args)

    callback(result)

def print_result(result):
    print('Got:', result)

def add(x, y):
    return x+y

apply_async(add, (2,3), callback=print_result)

# print_result()函数仅仅只接受一个参数result。不能再传入其他信息。而当你想让回调函数访问其他变量或者特定环境的变量值的时候就会遇到麻烦

#可以使用类来保存状态

class ResultHandler:
    def __init__(self):
        self.sequence=0

    def handler(self, result):
        self.sequence+=1
        print('[{}] Got: {}'.format(self.sequence, result))

r=ResultHandler()
apply_async(add, (2,3), callback=r.handler)
apply_async(add, ('hello ','world'), callback=r.handler)

# 第二种方式，作为类的替代，可以使用一个闭包捕获状态值

def make_handler():
    sequence=0
    def handler(result):
        nonlocal sequence  #nonlocal 它的作用是把变量标记为自由变量
        sequence+=1
        print('[{}] Got: {}'.format(sequence, result))
    return handler

handler=make_handler()
apply_async(add, (2,3), callback=handler)
apply_async(add, ('hello','world'), callback=handler)

#apply_async(add, ('hello','world'), callback=handler)

def make_handler():
    sequence=0
    while True:
        result = yield
        sequence+=1
        print('[{}] Got: {}'.format(sequence, result))

handler=make_handler()
next(handler)
apply_async(add, (2,3), callback=handler.send)
apply_async(add, ('hello','world'), callback=handler.send)
```

### 内置函数

Python内置(built-in)函数随着python解释器的运行而创建。在Python的程序中，你可以随时调用这些函数，不需要定义。

#### 基本函數

```python
type()  #查看数据类型
dir()   #获得当前模块的属性列表
help()  #用于查看函数或模块用途的详细说明。
len()   #查看数据长度
iter()  #函数用来生成迭代器
next()  #返回下一个值
hash()  #用于获取取一个对象（字符串或者数值等）的哈希值。
id()    #函数返回对象的唯一标识符，标识符是一个整数。CPython中id() 函数用于获取对象的内存地址。
super() #函数是用于调用父类(超类)的一个方法。
repr() 	#函数将对象转化为供解释器读取的形式。
```

#### 数学运算

```python
abs(-5)                          # 取绝对值，也就是5
round(2.6)                       # 四舍五入取整，也就是3.0
pow(2, 3)                        # 相当于2**3，如果是pow(2, 3, 5)，相当于2**3 % 5
cmp(2.3, 3.2)                    # 比较两个数的大小
divmod(9,2)                      # 返回除法结果和余数
max([1,5,2,9])                   # 求最大值
min([9,2,-4,2])                  # 求最小值
sum([2,-1,9,12])                 # 求和
vars() 							 # 函数返回对象object的属性和属性值的字典对象
```

#### 类型转换

```python
int("5")                         # 转换为整数 integer
float(2)                         # 转换为浮点数 float
long("23")                       # 转换为长整数 long integer
str(2.3)                         # 转换为字符串 string
complex(3, 9)                    # 返回复数 3 + 9i
ord("A")                         # "A"字符对应的数值
chr(65)                          # 数值65对应的字符
unichr(65)                       # 数值65对应的unicode字符
bool(0)                          # 转换为相应的真假值，在Python中，0相当于False
#在Python中，下列对象都相当于False： [], (), {}, 0, None, 0.0, ''
bin(56)                          # 返回一个字符串，表示56的二进制数
hex(56)                          # 返回一个字符串，表示56的十六进制数
oct(56)                          # 返回一个字符串，表示56的八进制数
list((1,2,3))                    # 转换为表 list
tuple([2,3,4])                   # 转换为定值表 tuple
slice(5,2,-1)                    # 构建下标对象 slice
dict(a=1,b="hello",c=[1,2,3])    # 构建词典 dictionary
frozenset() 					 # 返回一个冻结的集合，冻结后集合不能再添加或删除任何元素
```

#### 序列操作

```python
all([True, 1, "hello!"])         # 是否所有的元素都相当于True值
any(["", 0, False, [], None])    # 是否有任意一个元素相当于True值
sorted([1,5,3])                  # 返回正序的序列，也就是[1,3,5]
reversed([1,5,3])                # 返回反序的序列，也就是[3,5,1]
```

#### 类的属性方法操作

```python
hasattr(me, "test")               # 检查me对象是否有test属性
getattr(me, "test")               # 返回test属性
setattr(me, "test", new_test)     # 将test属性设置为new_test
delattr(me, "test")               # 删除test属性
isinstance(me, Me)                # me对象是否为Me类生成的对象 (一个instance)
issubclass(Me, object)            # Me类是否为object类的子类
```

#### 编译执行

```python
repr(me)                          # 返回对象的字符串表达
compile("print('Hello')",'','exec')       #将一个字符串编译为字节代码
eval("1 + 1")                     # 解释字符串表达式。参数也可以是compile()返回的code对象
execfile() 						  # 函数可以用来执行一个文件。
exec("print('Hello')")            # 解释并执行字符串，print('Hello')。参数也可以是compile()返回的code对象
```

#### 其他

```python
input("Please input:")            # 等待输入
globals()                         # 返回全局命名空间，比如全局变量名，全局函数名
locals()                          # 返回局部命名空间
__import__() 					  # 函数用于动态加载类和函数 。
```

##### enumerate

`enumerate()` 用于将一个可遍历的数据对象(如列表、元组或字符串)组合为一个索引序列，同时列出数据和数据下标。

```python
seq = ['one', 'two', 'three']
for i, element in enumerate(seq):
    print(i, element)
```

##### filter

`filter()` 函数用于过滤序列，过滤掉不符合条件的元素，返回一个迭代器对象，如果要转换为列表，可以使用 `list()`来转换。

该接收两个参数，第一个为函数，第二个为序列，序列的每个元素作为参数传递给函数进行判，然后返回 True 或 False，最后将返回 True 的元素放到新列表中。

```python
filter(lambda x:math.sqrt(x) % 1 == 0, range(1, 101))
```

##### range

`range()` 函数返回的是一个可迭代对象（类型是对象），而不是列表类型

```python
range(start, stop[, step])
'''
start	计数从 start 开始。默认是从 0 开始。例如range（5）等价于range（0， 5）;
stop	计数到 stop 结束，但不包括 stop。例如：range（0， 5） 是[0, 1, 2, 3, 4]没有5
step	步长，默认为1。例如：range（0， 5） 等价于 range(0, 5, 1)
'''
```

##### callable

`callable()` 函数用于检查一个对象是否是可调用的。如果返回 True，object 仍然可能调用失败；但如果返回 False，调用对象 object 绝对不会成功。

对于函数、方法、lambda 函式、 类以及实现了 **__call__** 方法的类实例, 它都返回 True。

```python
>>>callable(0)
False
>>> callable("runoob")
False
 
>>> def add(a, b):
...     return a + b
... 
>>> callable(add)             # 函数返回 True
True
>>> class A:                  # 类
...     def method(self):
...             return 0
... 
>>> callable(A)               # 类返回 True
True
```

##### map

map()会根据提供的函数对指定序列做映射。第一个参数 function 以参数序列中的每一个元素调用 function 函数，返回包含每次 function 函数返回值的新列表。

```python
map(lambda x: x ** 2, [1, 2, 3, 4, 5])  #计算列表各个元素的平方
```

##### zip

zip() 函数用于将可迭代的对象作为参数，将对象中对应的元素打包成一个个元组，然后返回由这些元组组成的对象，这样做的好处是节约了不少的内存。我们可以使用 list() 转换来输出列表。如果各个迭代器的元素个数不一致，则返回列表长度与最短的对象相同，利用 ***** 号操作符，可以将元组解压为列表。

```python
a = [1,2,3]
b = [4,5,6]

zipped = zip(a,b)     # 返回一个对象
for x,y in zipped:
	print(x,y)
```

### 装饰器

#### 定义

在不改变原函数代码和调用的基础上，为原函数附加新功能的机制为装饰器。

#### 装饰器示例

```python
import time
from functools import wraps

#1、普通创建装饰器
def count_time(func):
    def inner():
        start_time = time.time()
        func()
        end_time = time.time()
        print(func.__name__,end_time - start_time)
    return inner

@count_time         #method1=count_time(method1)=inner
def method1():
    '''method1'''
    time.sleep(0.7)

@count_time
def method2():
    '''method2'''
    time.sleep(0.8)

method1()
method2()


# 2、使用@wraps(func)注解是可以保留原始函数的元数据。
def CountTimes(func):

    @wraps(func)
    def Wraps_(*args,**kwargs):
        StartTime = time.time()
        func(*args,**kwargs)
        print(func.__name__,time.time()-StartTime)

    return Wraps_

@CountTimes
def CountDown(number):
    '''当number小于0是结束'''

    while number > 0:
        number -= 1

CountDown(1000)
CountDown(1000000)

#保留了原函数的元数据
print(CountDown.__name__,CountDown.__doc__)

#丢失了函数的元数据
print(method1.__name__,method2.__doc__)
```

#### 如果被修饰函数增加参数并且有返回值

```python
from functools import wraps
import time

def CountTimes(func):

    @wraps(func)
    def Wraps_(*args,**kwargs):
        StartTime = time.time()
        ReturnData = func(*args,**kwargs)
        print(func.__name__,time.time()-StartTime)
        return ReturnData

    return Wraps_

@CountTimes
def CountDown(number):
    '''当number小于0是结束'''

    while number > 0:
        number -= 13
    return number

print(CountDown(10))
```

#### 装饰器带参数

```python
from functools import wraps
import time


def CountTimes(RunType):
    if RunType == 'CountTime':
        def Inner(func):
            @wraps(func)
            def Wraps_(*args,**kwargs):
                StartTime = time.time()
                ReturnData = func(*args,**kwargs)
                print(func.__name__,time.time()-StartTime)
                return ReturnData
            return Wraps_
        return Inner
    else:
        def WiteLog(func):
            @wraps(func)
            def Wraps_(*args,**kwargs):
                StartTime = time.time()
                ReturnData = func(*args,**kwargs)
                with open('Run.log','a+') as f:
                    print(func.__name__,time.time()-StartTime,file=f)
                return ReturnData
            return Wraps_
        return WiteLog

@CountTimes(RunType='WriteLog')
def CountDown(number):
    '''当number小于0是结束'''

    while number > 0:
        number -= 13
    return number

print(CountDown(10))
```

