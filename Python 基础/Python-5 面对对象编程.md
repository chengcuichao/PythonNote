### 面向对象编程

#### 概念

面向过程编程最易被初学者接受，其往往用一长段代码来实现指定功能，开发过程中最常见的操作就是粘贴复制，即：将之前实现的代码块复制到现需功能处。

1. 面向过程：根据业务逻辑从上到下写垒代码
2. 函数式：将某功能代码封装到函数中，日后便无需重复编写，仅调用函数即可
3. 面向对象：对函数进行分类和封装，让开发“更快更好更强...”

#### 封装

封装最好理解了。封装是面向对象的特征之一，是对象和类概念的主要特性。

封装，也就是把客观事物封装成抽象的类，并且类可以把自己的数据和方法只让可信的类或者对象操作，对不可信的进行信息隐藏。

#### 继承

面向对象编程 (OOP) 语言的一个主要功能就是“继承”。继承是指这样一种能力：它可以使用现有类的所有功能，并在无需重新编写原来的类的情况下对这些功能进行扩展。

通过继承创建的新类称为“子类”或“派生类”。

被继承的类称为“基类”、“父类”或“超类”。

继承的过程，就是从一般到特殊的过程。

要实现继承，可以通过“继承”（Inheritance）和“组合”（Composition）来实现。

在某些 OOP 语言中，一个子类可以继承多个基类。但是一般情况下，一个子类只能有一个基类，要实现多重继承，可以通过多级继承来实现。

继承概念的实现方式主要有2类：实现继承、接口继承。

Ø     实现继承是指使用基类的属性和方法而无需额外编码的能力；

Ø     接口继承是指仅使用属性和方法的名称、但是子类必须提供实现的能力(子类重构爹类方法)；

在考虑使用继承时，有一点需要注意，那就是两个类之间的关系应该是“属于”关系。例如，Employee 是一个人，Manager 也是一个人，因此这两个类都可以继承 Person 类。但是 Leg 类却不能继承 Person 类，因为腿并不是一个人。

抽象类仅定义将由子类创建的一般属性和方法。

OO开发范式大致为：划分对象→抽象类→将类组织成为层次化结构(继承和合成) →用类与实例进行设计和实现几个阶段。

#### 多态

多态性（polymorphisn）是允许你将父对象设置成为和一个或更多的他的子对象相等的技术，赋值之后，父对象就可以根据当前赋值给它的子对象的特性以不同的方式运作。简单的说，就是一句话：允许将子类类型的指针赋值给父类类型的指针。

那么，多态的作用是什么呢？我们知道，封装可以隐藏实现细节，使得代码模块化；继承可以扩展已存在的代码模块（类）；它们的目的都是为了——代码重用。而多态则是为了实现另一个目的——接口重用！多态的作用，就是为了类在继承和派生的时候，保证使用“家谱”中任一类的实例的某一属性时的正确调用。

Pyhon 很多语法都是支持多态的，比如 len(),sorted(), 你给len传字符串就返回字符串的长度，传列表就返回列表长度。

### 示例

#### 封装

```python
#实例变量，类变量：
class  a(object):
    name = 123321     #类变量（存在类的里面）
    def __init__(self,name,age):
        self.name= name         #实例变量，作用域为实例本身。（存在实例化的实例里面）
        self.age =age
b = a('cheng',22)
print(b.name)
注：b.name先找实例变量里有没有，再看类变量有没有。　　

#私有方法，私有属性：
class  a(object):
    name = 123321
    __age = 24    #私有属性
    def __init__(self,name,age):
        self.name= name
        self.__age =age
    def __ab(self):      #私有方法
        print(self.__age)

b = a('cheng',22)
print(b.__age)
#注：私有方法，属性只能在类里面调用，不能在外面调用。使用的时候用self.__属性或方法名。
```

#### 继承

在多继承里，只继承一个构造函数，继承顺序为：

在Python2里：经典类：深度优先，新式类：广度优先

在python3里：经典类和新式类都是广度优先。

```python
#_*_coding:utf-8_*_
class A:
    def __init__(self):
        self.n = 'A'
class B(A):
    # def __init__(self):
    #     self.n = 'B'
    pass
class C(A):
    def __init__(self):
        self.n = 'C'
class D(B,C):
    # def __init__(self):
    #     self.n = 'D'
    pass 
obj = D()
print(obj.n)
```

方法继承

```python
class People(object):
    def __init__(self,name,age):
        self.name = name
        self.age = age
    def talk(self):
        print('%s is talking'%self.name)

class Man(People):
    def __init__(self,name,age,eye):
        super(Man,self).__init__(name,age)      #上面和下面是一样的
#        People.__init__(self,name,age)
        self.eye = eye

man1=Man('cheng',22,'blue')
print(man1.name)

#重构父类的方法后，再想调用父类的方法，用父类名.重构的方法名（self）
```

#### 静态方法

通过@staticmethod装饰器即可把其装饰的方法变为一个静态方法，什么是静态方法呢？其实不难理解，普通的方法，可以在实例化后直接调用，并且在方法里可以通过self.调用实例变量或类变量，但静态方法是不可以访问实例变量或类变量的，一个不能访问实例变量和类变量的方法，其实相当于跟类本身已经没什么关系了，它与类唯一的关联就是需要通过类名来调用这个方法

```python
class people(object):
    def __init__(self,name):
        self.name = name
    @staticmethod
    def eat(self):
        print("%s is eating ...."%self.name)
a = people("xiao")
a.eat()
```

上面的调用会出以下错误，说是eat需要一个self参数，但调用时却没有传递，没错，当eat变成静态方法后，再通过实例调用时就不会自动把实例本身当作一个参数传给self了。

想让上面的代码可以正常工作有两种办法

1. 调用时主动传递实例本身给eat方法，即d.eat(a)

2. 在eat方法中去掉self参数，但这也意味着，在eat中不能通过self.调用实例中的其它变量了

```python
class people(object):
    def __init__(self,name):
        self.name = name
    @staticmethod
    def eat():
        print(" is eating ....")
a = people("xiao")
a.eat()
```

#### 类方法

类方法通过@classmethod装饰器实现，类方法和普通方法的区别是， 类方法只能访问类变量，不能访问实例变量

```python
class people(object):
    def __init__(self,name):
        self.name = name
    @classmethod
    def eat(self):
        print("%s is eating ...."%self.name)
a = people("xiao")
a.eat()
```

执行报错，说Dog没有name属性，因为name是个实例变量，类方法是不能访问实例变量的

此时可以定义一个类变量，也叫name,看下执行效果

```python
class people(object):
    name = "类变量"
    def __init__(self,name):
        self.name = name
    @classmethod
    def eat(self):
        print("%s is eating ...."%self.name)
a = people("xiao")
a.eat()
```

#### 属性方法　

属性方法的作用就是通过@property把一个方法变成一个静态属性

```python
class people(object):
    name = "类变量"
    def __init__(self,name):
        self.name = name
    @property
    def eat(self):
        print("%s is eating ...."%self.name)
a = people("xiao")
a.eat()
```

调用会出错误， 说NoneType is not callable, 因为eat此时已经变成一个静态属性了， 不是方法了， 想调用已经不需要加()号了，直接d.eat就可以了，正常调用如下

```python
a = people("xiao")
a.eat
```

#### 私有属性和方法

单下划线或双下划线，来命名私有属性和方法。

### 类的特殊成员方法

#### `__doc__`

`__doc__`表示类的描述信息

```python
class Foo(object):
    """描述信息"""
    def __init__(self):
        self.name = 'alex'

    def func(self):
        print("is ok")
        #return 'func'
obj = Foo()
print(obj.__doc__)
```

#### `__str__ ` `__repr__`

如果一个类中定义了`__str__`方法，那么在打印对象时，默认输出该方法的返回值。

如果一个类中定义了`__repr__`方法，那么当初始化实例时就把`__repr__`的值返回给实例

```python
class Pair():

    def __str__(self):
        return '__str__'

    def __repr__(self):
        return '__repr__'

P = Pair()

P
>>>__repr__

# print(P) 输出等于str(P)
print(P,str(P)
```

#### `__module__ ` `__class__`

`__module__` 表示当前操作的对象在那个模块

`__class__` 表示当前操作的对象的类是什么

```python
class C(object):
    def __init__(self):
        self.name = "name"
```

```python
from lib.abc import C
obj = C()
print(obj.__module__)
print(obj.__class__)
输出：
lib.abc
<class 'lib.abc.C'>
```

#### `__init__`

构造方法，通过类创建对象时，自动触发执行。

#### `__del__`

当对象在内存中被释放时，自动触发执行。此方法一般无须定义，因为Python是一门高级语言，程序员在使用时无需关心内存的分配和释放，因为此工作都是交给Python解释器来执行，所以，析构函数的调用是由解释器在进行垃圾回收时自动触发执行的

#### `__call__`

对象后面加括号，触发执行。

注：构造方法的执行是由创建对象触发的，即：对象 = 类名() ；而对于 `__call__` 方法的执行是由对象后加括号触发的，即：对象() 或者 类()()

```python
class a(object):
    def __init__(self):
        pass
    def __call__(self, *args, **kwargs):
        print(args[0])
obj = a()
obj(1)
```

#### `__dict__`

查看类或对象中的所有成员

```python
class people(object):
    def __init__(self):
        self.name = "alex"
        self.age = 45
obj = people()
print(obj.__dict__)
输出：
{'name': 'alex', 'age': 45}
```

#### `__format__`

自定义字符串的格式化

```python
_formats = {'ymd':'{d.year}-{d.month}-{d.day}',
            'mdy':'{d.month}/{d.day}/{d.year}',
            'dmy':'{d.day}/{d.month}/{d.year}'}


class Date:
    def __init__(self, year, month, day):
        self.year = year
        self.month = month
        self.day = day
    def __format__(self, code):
        if code == '':
            code = 'ymd'
        fmt = _formats[code]return fmt.format(d=self)

d=Date(2012,12,21)

print(format(d))

#__format__()方法给Python的字符串格式化功能提供了一个钩子。这里需要着重强调的是格式化代码的解析工作完全由类自己决定。因此，格式化代码可以是任何值。
```

#### `__enter__` `__exit__`

使对象支持上下文管理协议(with语句)

```python
from socket import socket, AF_INET, SOCK_STREAM
from functools import partial

class LazyConnection:
    def __init__(self, address, family=AF_INET, type=SOCK_STREAM):
        self.address = address
        self.family = family
        self.type = type
        self.sock = None

    def __enter__(self):
        if self.sock is not None:
            raise RuntimeError('Already connected')
        self.sock = socket(self.family, self.type)
        self.sock.connect(self.address)
        return self.sock

    def __exit__(self, exc_type, exc_val, exc_tb):
        self.sock.close()
        self.sock = None

#这个类的关键特点在于它表示了一个网络连接，但是初始化的时候并不会做任何事情(比如它并没有建立一个连接)。连接的建立和关闭是使用with语句自动完成的

with LazyConnection(('www.python.org', 80)) as s:
    s.send(b'GET /index.html HTTP/1.0\r\n')
    s.send(b'Host: www.python.org\r\n')
    s.send(b'\r\n')
    resp = b''.join(iter(partial(s.recv, 8192), b''))
    print(resp)
'''
	编写上下文管理器的主要原理是你的代码会放到with语句块中执行。当出现with语句的时候，对象的__enter__()方法被触发，它返回的值(如果有的话)会被赋值给as声明的变量。
然后，with语句块里面的代码开始执行。最后，__exit__()方法被触发进行清理工作。
'''

```

#### `__getitem__` `__setitem__` `__delitem__`

用于索引操作，如字典。以上分别表示获取、设置、删除数据。

