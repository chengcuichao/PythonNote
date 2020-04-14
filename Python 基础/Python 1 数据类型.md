### 标准数据类型

Python3 中有六个标准的数据类型：Number（数字）、String（字符串）、List（列表）、Tuple（元组）、Sets（集合）、Dictionary（字典）。

### Number

- 整型(Int)，通常被称为是整型或整数，是正或负整数，不带小数点。Python3 整型是没有限制大小的，可以当作 Long 类型使用，所以 Python3 没有 Python2 的 Long 类型。
- 浮点型(float)，浮点型由整数部分与小数部分组成，浮点型也可以使用科学计数法表示（2.5e2 = 2.5 x 102 = 250）
- 复数( complex)，复数由实数部分和虚数部分构成，可以用a + bj,或者complex(a,b)表示， 复数的实部a和虚部b都是浮点型。

#### 数字类型转换

- int(x)，将x转换为一个整数。
- float(x)，将x转换到一个浮点数。
- complex(x)，将x转换到一个复数，实数部分为 x，虚数部分为 0。
- complex(x, y)，将 x 和 y 转换到一个复数，实数部分为 x，虚数部分为 y。x 和 y 是数字表达式。、

```python
number = 235
print(type(number))         #查看number的类型。
if isinstance(number,dict): #判断是否是(int、float、bool、complex)类型的数字,也可以判断是否是（str,list,tuple,set,dict）类型。
    print("is ok")
else:
    print("is no")
money = input("输入数字：")
if money.isdigit() :        #判断是否是数字，money必须是input输入的。
    print("is ok")
else:
    print("is no")
'''
isinstance(变量，要判断的类型)  #判断是否是要判断的类型
变量.isdigit()               #判断是否为正整数
'''
```

#### 数学函数

|      函数       |                       返回值 ( 描述 )                        |
| :-------------: | :----------------------------------------------------------: |
|     abs(x)      |             返回数字的绝对值，如abs(-10) 返回 10             |
|     ceil(x)     |         返回数字的上入整数，如math.ceil(4.1) 返回 5          |
|    floor(x)     |         返回数字的下舍整数，如math.floor(4.9)返回 4          |
|     exp(x)      |     返回e的x次幂(ex),如math.exp(1) 返回2.718281828459045     |
|     fabs(x)     |         返回数字的绝对值，如math.fabs(-10) 返回10.0          |
|     log(x)      |      如math.log(math.e)返回1.0,math.log(100,10)返回2.0       |
|    log10(x)     |      返回以10为基数的x的对数，如math.log10(100)返回 2.0      |
| max(x1, x2,...) |            返回给定参数的最大值，参数可以为序列。            |
| min(x1, x2,...) |            返回给定参数的最小值，参数可以为序列。            |
|     modf(x)     | 返回x的整数部分与小数部分，两部分的数值符号与x相同，整数部分以浮点型表示。 |
|    pow(x, y)    |                      x**y 运算后的值。                       |
|  round(x [,n])  | 返回浮点数x的四舍五入值，如给出n值，则代表舍入到小数点后的位数。 |
|     sqrt(x)     | 返回数字x的平方根，数字可以为负数，返回类型为实数，如math.sqrt(4)返回 2+0j |

#### 三角函数

|    函数     |                       描述                        |
| :---------: | :-----------------------------------------------: |
|   acos(x)   |               返回x的反余弦弧度值。               |
|   asin(x)   |               返回x的反正弦弧度值。               |
|   atan(x)   |               返回x的反正切弧度值。               |
| atan2(y, x) |       返回给定的 X 及 Y 坐标值的反正切值。        |
|   cos(x)    |               返回x的弧度的余弦值。               |
| hypot(x, y) |        返回欧几里德范数 sqrt(x*x + y*y)。         |
|   sin(x)    |               返回的x弧度的正弦值。               |
|   tan(x)    |                返回x弧度的正切值。                |
| degrees(x)  | 将弧度转换为角度,如degrees(math.pi/2) ， 返回90.0 |
| radians(x)  |                 将角度转换为弧度                  |

#### 数学常量

| 常量 |                 描述                 |
| :--: | :----------------------------------: |
|  pi  | 数学常量 pi（圆周率，一般以π来表示） |
|  e   | 数学常量 e，e即自然常数（自然常数）  |

### String

Python中的字符串用单引号(')或双引号(")括起来，同时使用反斜杠(\)转义特殊字符。字符串的截取的语法格式如下：

```python
变量[头下标:尾下标]
```

#### 字符串切片操作：

```python
str = 'Runoob'
print (str)          # 输出字符串
print (str[0:-1])    # 输出第一个到倒数第二个的所有字符
print (str[0])       # 输出字符串第一个字符
print (str[2:5])     # 输出从第三个开始到第五个的字符
print (str[2:])      # 输出从第三个开始的后的所有字符
print (str * 2)      # 输出字符串两次
print (str + "TEST") # 连接字符串
```

#### 字符串内建函数

##### 判断方法

|                   方法                   |                             描述                             |
| :--------------------------------------: | :----------------------------------------------------------: |
|                isalnum()                 | 如果字符串至少有一个字符并且所有字符都是字母或数字则返回 True,否则返回 False |
|                isalpha()                 | 如果字符串至少有一个字符并且所有字符都是字母则返回 True, 否则返回 False |
|                isdigit()                 |        如果字符串只包含数字则返回 True 否则返回 False        |
|                isupper()                 | 如果字符串中包含至少一个区分大小写的字符，并且所有这些(区分大小写的)字符都是大写，则返回 True，否则返回 False |
|                islower()                 | 如果字符串中包含至少一个区分大小写的字符，并且所有这些(区分大小写的)字符都是小写，则返回 True，否则返回 False |
|               isnumeric()                |   如果字符串中只包含数字字符，则返回 True，否则返回 False    |
|                isspace()                 |     如果字符串中只包含空格，则返回 True，否则返回 False      |
|                istitle()                 | 如果字符串是标题化的(见 title())则返回 True，否则返回 False  |
|               isdecimal()                | 检查字符串是否只包含十进制字符，如果是返回 true，否则返回 false |
|  startswith(str, beg=0,end=len(string))  | 检查字符串是否是以 obj 开头，是则返回 True，否则返回 False。如果beg 和 end 指定值，则在指定范围内检查。 |
| endswith(suffix, beg=0, end=len(string)) | 检查字符串是否以 obj 结束，如果beg 或者 end 指定则检查指定的范围内是否以 obj 结束，如果是，返回 True,否则返回 False |

##### 修改方法

|                 方法                 |                             描述                             |
| :----------------------------------: | :----------------------------------------------------------: |
|             capitalize()             |                将字符串的第一个字符转换为大写                |
|       center(width, fillchar)        | 返回一个指定的宽度 width 居中的字符串，fillchar 为填充的字符，默认为空格 |
|        expandtabs(tabsize=8)         | 把字符串 string 中的 tab 符号转为空格，tab 符号默认的空格数是 8 。 |
|              join(seq)               | 以指定字符串作为分隔符，将 seq 中所有的元素(的字符串表示)合并为一个新的字符串 |
|       ljust(width[, fillchar])       | 返回一个原字符串左对齐,并使用 fillchar 填充至长度 width 的新字符串，fillchar 默认为空格。 |
|      rjust(width,[, fillchar])       | 返回一个原字符串右对齐,并使用fillchar(默认空格）填充至长度 width 的新字符串 |
|            zfill (width)             |     返回长度为 width 的字符串，原字符串右对齐，前面填充0     |
|               lower()                |                转换字符串中所有大写字符为小写                |
|               upper()                |                 转换字符串中的小写字母为大写                 |
|              swapcase()              |           将字符串中大写转换为小写，小写转换为大写           |
|               lstrip()               |                     截掉字符串左边的空格                     |
|               rstrip()               |                  删除字符串字符串末尾的空格                  |
|            strip([chars])            |              在字符串上执行 lstrip()和 rstrip()              |
|      replace(old, new [, max])       | 把 将字符串中的 str1 替换成 str2,如果 max 指定，则替换不超过 max 次。 |
| split(str="", num=string.count(str)) | 以 str 为分隔符截取字符串，如果 num 有指定值，则仅截取 num 个子字符串 |
|        splitlines([keepends])        | 按照行('\r', '\r\n', \n')分隔，返回一个包含各行作为元素的列表，如果参数 keepends 为 False，不包含换行符，如果为 True，则保留换行符。 |
|             maketrans()              | 创建字符映射的转换表，对于接受两个参数的最简单的调用方式，第一个参数是字符串，表示需要转换的字符，第二个参数也是字符串表示转换的目标。 |
|               title()                | 返回"标题化"的字符串,就是说所有单词都是以大写开始，其余字母均为小写(见 istitle()) |

##### 查找方法

|                 方法                 |                             描述                             |
| :----------------------------------: | :----------------------------------------------------------: |
|  index(str, beg=0, end=len(string))  |   跟find()方法一样，只不过如果str不在字符串中会报一个异常    |
| rindex( str, beg=0, end=len(string)) |               类似于 index()，不过是从右边开始               |
|  count(str, beg= 0,end=len(string))  | 返回 str 在 string 里面出现的次数，如果 beg 或者 end 指定则返回指定范围内 str 出现的次数 |
|   find(str, beg=0 end=len(string))   | 检测 str 是否包含在字符串中 中，如果 beg 和 end 指定范围，则检查是否包含在指定范围内，如果是返回开始的索引值，否则返回-1 |
|  rfind(str, beg=0,end=len(string))   |           类似于 find()函数，不过是从右边开始查找            |

#### List

列表可以完成大多数集合类的数据结构实现。列表中元素的类型可以不相同，它支持数字，字符串甚至可以包含列表（所谓嵌套）。列表是写在方括号([])之间、用逗号分隔开的元素列表。和字符串一样，列表同样可以被索引和截取，列表被截取后返回一个包含所需元素的新列表。

```python
list_ = [ 'abcd', 786 , 2.23, 'runoob', 70.2 ]
tinylist = [123, 'runoob']
 
print (list_)            # 输出完整列表
print (list_[0])         # 输出列表第一个元素
print (list_[1:3])       # 从第二个开始输出到第三个元素
print (list_[2:])        # 输出从第三个元素开始的所有元素
print (tinylist * 2)    # 输出两次列表
print (list_ + tinylist) # 连接列表
```

##### 列表方法

|          方法           |                             描述                             |
| :---------------------: | :----------------------------------------------------------: |
|    list.append(obj)     |                    在列表末尾添加新的对象                    |
|     list.count(obj)     |                统计某个元素在列表中出现的次数                |
|    list.extend(seq)     | 在列表末尾一次性追加另一个序列中的多个值（用新列表扩展原来的列表） |
|     list.index(obj)     |           从列表中找出某个值第一个匹配项的索引位置           |
| list.insert(index, obj) |                        将对象插入列表                        |
| list.pop(obj=list[-1])  | 移除列表中的一个元素（默认最后一个元素），并且返回该元素的值 |
|    list.remove(obj)     |                移除列表中某个值的第一个匹配项                |
|     list.reverse()      |                        反向列表中元素                        |
|    list.sort([func])    |                       对原列表进行排序                       |
|      list.clear()       |                           清空列表                           |
|       list.copy()       |                           复制列表                           |

#### Tuple

元组（tuple）与列表类似，不同之处在于元组的元素不能修改。元组写在小括号里，元素之间用逗号隔开。

```python
print (tuple_)             # 输出完整元组
print (tuple_[0])          # 输出元组的第一个元素
print (tuple_[1:3])        # 输出从第二个元素开始到第三个元素
print (tuple_[2:])         # 输出从第三个元素开始的所有元素
print (tinytuple * 2)     # 输出两次元组
print (tuple_ + tinytuple) # 连接元组
```

#### Sets

集合（set）是一个无序不重复元素的序列，基本功能是进行成员关系测试和删除重复元素。可以使用大括号 { } 或者 set() 函数创建集合，注意：创建一个空集合必须用 set() 而不是 { }，因为 { } 是用来创建一个空字典。

```python
student = {'Tom', 'Jim', 'Mary', 'Tom', 'Jack', 'Rose'}
print(student) # 输出集合，重复的元素被自动去掉

# 成员测试
if('Rose' in student) :
print('Rose 在集合中')
else :
print('Rose 不在集合中')

# set可以进行集合运算
a = set('abracadabra')
b = set('alacazam')

print(a)
print(a - b) # a和b的差集
print(a | b) # a和b的并集
print(a & b) # a和b的交集
print(a ^ b) # a和b中不同时存在的元素 

基本操作：
t.add('x')                  #添加一项  
s.update([10,37,42])        #在s中添加多项  
t.remove('H')               #删除一项：   
len(s)                      #set 的长度   
x in s                      #测试 x 是否是 s 的成员  
x not in s                  #测试 x 是否不是 s 的成员  
s.issubset(t)               #测试是否 s 中的每一个元素都在 t 中  
s.issuperset(t)             #测试是否 t 中的每一个元素都在 s 中  
s.union(t)                  #s | t 返回一个新的 set 包含 s 和 t 中的每一个元素  
s.intersection(t)           #s & t 返回一个新的 set 包含 s 和 t 中的公共元素  
s.difference(t)             #s - t 返回一个新的 set 包含 s 中有但是 t 中没有的元素  
s.symmetric_difference(t)   #s ^ t 返回一个新的 set 包含 s 和 t 中不重复的元素  
s.copy()                    #返回 set “s”的一个浅复制
```

##### 集合方法

|       方法       |                             描述                             |
| :--------------: | :----------------------------------------------------------: |
|   s.update(t)    |                  将t集合中的成员添加到集合s                  |
|    s.add(obj)    |                    增加操作，将obj添加到s                    |
|  s.remove(obj)   |                           删除操作                           |
|  s.discard(obj)  |  丢弃操作，remove()的友好版本，如果s中存在ojb，从s中删除它   |
|     s.pop()      |                  移除任意一个值并返回这个值                  |
|    s.clear()     |                      移除s中的所有元素                       |
| frozenset([obj]) | 不可变集合工厂函数，执行方式好set()方法相同，但它返回的是不可变集合 |

#### Dictionary

字典（dictionary）是Python中另一个非常有用的内置数据类型。列表是有序的对象结合，字典是无序的对象集合。两者之间的区别在于：字典当中的元素是通过键来存取的，而不是通过偏移存取。字典是一种映射类型，字典用"{ }"标识，它是一个无序的键(key) : 值(value)对集合。键(key)必须使用不可变类型。在同一个字典中，键(key)必须是唯一的。

```python
dict_ = {}
dict_['one'] = "www.w23.com"
dict_[2]     = "www.4dd.com"
 
tinydict = {'name': 'runoob','code':1, 'site': 'www.runoob.com'}

print (dict_['one'])       # 输出键为 'one' 的值
print (dict_[2])           # 输出键为 2 的值
print (tinydict)          # 输出完整的字典
print (tinydict.keys())   # 输出所有键
print (tinydict.values()) # 输出所有值
```

##### 字典方法

|                方法                |                       描述                        |
| :--------------------------------: | :-----------------------------------------------: |
|    dict.get(key, default=None)     |   返回指定键的值，如果值不在字典中返回default值   |
|            dict.items()            |        以列表返回可遍历的(键, 值) 元组数组        |
|            dict.keys()             |            以列表返回一个字典所有的键             |
|        radiansdict.values()        |             以列表返回字典中的所有值              |
| dict.setdefault(key, default=None) | 如果键不存在于字典中，将会添加键并将值设为default |
|         dict.update(dict2)         |         把字典dict2的键/值对更新到dict里          |
|      dict.pop(key[,default])       | 删除字典给定键 key 所对应的值，返回值为被删除的值 |
|           dict.popitem()           |         随机返回并删除字典中的一对键和值          |
|            dict.clear()            |                删除字典内所有元素                 |
|            dict.copy()             |               返回一个字典的浅复制                |

