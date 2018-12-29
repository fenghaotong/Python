
# Python第五章学习

函数：

- [x] 函数定义和调用

- [x] 函数名称与Docstrings

- [x] 函数参数

- [x] 函数变量作用域

- [x] 函数及return返回值

- [x] 函数冗余参数

- [x] 函数lambda匿名函数

- [x] switch实现

内建函数：      

- [x] 字符串处理

- [x] 序列处理

## 函数

- 函数就是为了完成特定功能的一个语句组，这组语句可以作为一个单位使用，并且给他取一个名字

- 可以通过函数名在程序的不同地方多次执行（这通常叫做函数的调用），却不需要在所有地方都重复编写这些语句

- 自定义函数
    - 用户自己编写的     

- 预定义的Python函数
    - 系自带的一些函数，还有一些第三方编写的函数，如其他程序员编写的一些函数，对于这些现成的函数用户可以直接拿来使用

**为什么使用函数：**     

- 降低编程难度
    - 通常将一个复杂的大问题，分解成一系列更简单的小问题，然后将小问题继续划分成更小的问题，当问题细化的足够简单的时候，我们就可以分而治之，这是，我们可以使用函数来处理待定的问题，各个小问题解决了，大问题也就迎刃而解。      
    
- 代码重用      
    - 我们定义的函数可以在一个程序的多个位置使用，也可以用于多个程序，此外，我们还可以把函数放到一个模块中供其他程序员使用，同时，我们也可以使用其他程序员定义的函数，这就避免了重复劳动，提高了工作效率。

### 函数的定义和调用
- 但我们自己定义一个函数时，通常用def语句，其语法形式如下：
```
def function(parameter):
    suite
```

- 调用函数时：
```
function(parameter)
```


```python
#实现a+b
a = 100
b = 200
c = a + b
print(c)
```

    300
    


```python
#如果我们重复使用的时候就要不停的去写这几句代码，下面我们可以使用函数定义
def add():
    c = a + b
    print(c)
    
#下面我们用函数名调用这个函数
add()
```

    300
    


```python
#定义一个函数，不去调用时不会有任何操作
a = 100

def fun():
    if True:
        print("good")
        
#调用函数
print(a)

fun()
fun()
```

    100
    good
    good
    

### 函数名称和Docstrings
- 对函数及其参数进行合理的命名可以使得其他的程序员更容易理解函数的用途和用法：
    - 使用命名框架，并保持一致性
    - 对所有名称，要避免使用缩略，除非是标准化并广泛使用的。
    - 合理的使用变量和参数名：x非常适合用作x坐标参数，i适合于用作循环计数器等。通常情况下，名称应该足够长以具备很好的描述性，名称应该描述数据的含义，而不是其类型。
    - 函数名与方法名应该可以表明其行为或返回值，但不应该是为了表示如何实现的——因为事先方法因人而异。
- Docstrings
    - 通过使用Docstrings，我们可以添加任何函数文档信息，他可以简单的添加在def行之后，函数代码开始之前的字符串，下面例子：


```python
def printMax(x,y):
    """ Print the maximum of two number.
    
    The two value must be integers."""
    x = int(x)
    y = int(y)
    
    if x > y:
        print(x,"is maximum")
    else:
        print(y,"is maximum")
    
printMax(3,5)
print(printMax.__doc__)
```

    5 is maximum
     Print the maximum of two number.
        
        The two value must be integers.
    

- 文档字符串的惯例是一个多行字符串，它的首行是以大写字母开始，句号结尾。第二行是空行，从第三行开始是详细的描述

### 函数参数

- 形式参数和实际参数
    - 在定义函数时函数名后面圆括号中的变量名称叫做“形式参数”，简称“形参”。     
    - 在调用函数时，函数名后面圆括号里面的参数名称叫做实际参数，简称“实参”


```python
def fun(x):#x位形参
    print("I get a:",x)

s = input("input somethin:")

fun(s)#s为实参
```

    input somethin:hello
    I get a: hello
    


```python
def printMax(a,b):
    if a > b:
        print(a,"is maximum")
    else:
        print(b,"is maximum")
        
printMax(3,4)

x = 5
y = 7

printMax(x,y)

def mashine(x,y):
    print("正在生成一个",x,"元",y,"口味的冰激凌")

s1 = input("input price:")
s2 = input("input taste:")

mashine(s1,s2)
```

    4 is maximum
    7 is maximum
    input price:10
    input taste:巧克力
    正在生成一个 10 元 巧克力 口味的冰激凌
    

- 缺省参数（默认参数）在没有输入参数的情况下，默认输出
```
def function(a,b="1")
```
>注意：只有在形参末尾的那些参数可以有默认参数值，即不能声明函数形参的时候先声明有默认值得形参而后声明没有默认值的形参，如：def func(a = 5,b)是无效的


```python
def mashine(x = 10,y = "巧克力"):
    print("正在生成一个",x,"元",y,"口味的冰激凌")

s1 = input("input price:")
s2 = input("input taste:")

mashine()
```

    input price:
    input taste:
    正在生成一个 10 元 巧克力 口味的冰激凌
    

### 函数变量作用域
- 局部变量和全局变量
    - Python的任何变量都有其特定的作用域     
    - 在函数中定义的变量一般只能在函数内部使用，这些只能在程序的特定部分使用的变量我们称之为局部变量；      
    - 在一个文件顶部定义的变量可以供该文件中的任何函数调用，这些可以为整个程序所使用的变量我们成为全局变量。


```python
x = "i am global var"

def fun():
    
    c = 100  #局部变量    
    print(c)
    print(x)
    
fun()
#print(c)
print(x)
```

    100
    i am global var
    i am global var
    


```python
x = "i am global var"

def fun():
    x = 100#局部变量只能在函数内部使用
    global y#强制声明为一个全局变量
    y = 200
    print(x)
    
fun()#当函数没有调用时，y仍然不是全局变量    
#print(c)
print(x)
print(y)
```

    100
    i am global var
    200
    

>这里需要注意的是global语句的使用，该语句的作用是告知Python，某个变量的作用范围是全局范围，对变量的赋值应该应用于全局变量，而不是创建一个同名的本地变量

### 函数及return返回值
- 函数返回值
    - 函数被调用后会返回一个指定的值
    - 函数调用后默认返回None
    - return 返回值
    - 返回值可以是任意类型
    - return执行后，函数终止
    - 区分返回值和打印


```python
def f(x,y):
    print("welcome!")#向屏幕输出
    return(x + y)#返回一个值

f(2,3)
```

    welcome!
    




    5




```python
def f():
    return "one"#return执行后，函数终止
    return "two"
f()
```




    'one'




```python
def f(x,y):
    if x > y:
        return 1
    print("hello world")
    if x < y:
        return 0
    return -1
f(1,2)
```

    hello world
    




    0



### 函数冗余参数
- 多类型传值
    - 向函数传元组和字典
    ```
    fun(*args)
    fun(**kwords)
    ```
    - 处理多余实参
    ```
    def fun(*arg,**kw)
    ```
- 传值冗余




```python
def f(x):
    print(x)

l = list(range(10))

f(l)
```

    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
    


```python
def f(x,y):
    print("{0}:{1}".format(x,y))

f("a","b")

t = ("name","milo")

f(*t)#*号对列表进行了拆分
```

    a:b
    name:milo
    


```python
x = "10"
y = "10"
print("{0},{1}".format(x,y))#字符串的格式化
```

    10,10
    

option字典的键值进行拆分是，每个键的值被赋予适当的参数，参数的名称与键相同，我们可以在参数中使用映射拆分操作符，通过这种方式创建的函数可以接受给定的任意数量的关键字参数


```python
def f(name = "name",age = 0):
    print("name:{0}".format(name))
    print("age:{0}".format(age))

d = {"age" : 30, "name" :"milo"}
f(**d)#双星号拆分字典
```

    name:milo
    age:30
    

- 处理多余参数


```python
def f(x,*args):
    print(x)
    print(args)

f(1,2,3)
```

    1
    (2, 3)
    

- 这一函数有一个名为args的参数，在args前面有一个“\*”，这意味着，在函数内部，参数args可以是一个元组，其项数随给定的位置参数个数的变化而变化


```python
def f(x,*args,**kwargs):
    print(x)
    print(args)
    print(kwargs)
    
f(1,2,3,4,5,6)
```

    1
    (2, 3, 4, 5, 6)
    {}
    

- 这里有一个kwargs的参数，在其之前有两个星号，在函数内部，参数kwargs可以是一个字典


```python
def f(x,*args,**kwargs):
    print(x)
    print(args)
    print(kwargs)
    
f(1,2,3,4,5,6,y = 20,z = 30)
```

    1
    (2, 3, 4, 5, 6)
    {'z': 30, 'y': 20}
    

### lambda
- 匿名函数
    - lambda函数是一种快速定义单行的最小函数，是从Lisp借来用的，可以用在任何需要函数的地方
- 语法格式：
lambda paraments:expressiom
>paraments是可选的，如果提供，通常是逗号分隔的变量名形式，也就是位置参数，当然，def语句支持的完整参数语法格式也可以使用
- lambda语句中，冒号前是参数，可以有多个，用逗号隔开，冒号右边是返回值。lambda语句构建的其实是一个函数对象


```python
#定义一个平常的函数
def f(x,y):
    return(x*y)
f(2,3)
```




    6




```python
#用lamabda定义
g = lambda x,y:x*y
g(2,3)
```




    6



- 1.使用python写一些执行脚本时，使用lambda可以省去定义函数的过程，让代码更加精简
- 2.对于一些抽象的，不会别的地方再复用的函数，有时候给函数起个名字也是也难题，使用lambda不需要考虑命名的问题
- 3.使用lambda在某些时候让代码更容易理解

### switch实现
- switch语句用于编写多分支结构的程序，类似于if...elif...else语句
- switch语句表达的分支结构比if..elif..else语句表达的更清晰，代码的可读性更高
- **但python并没有提供switch语句**
- python可以通过字典实现switch语句的功能
- 实现方法分为两步：
    - 首先，定义一个字典。
    - 其次，调用字典的get()获取相应的表达式
 
- 通过字典调用函数：
    - {1：case1,2:case2}.get(x,lambda \*arg,\*\*key:)()


```python
from __future__ import division
def add(x,y):
    return x + y

def jian(x,y):
    return x - y

def cheng(x,y):
    return x * y

def chu(x,y):
    return x / y

def operator(x,y,o):
    if o == "+":
        print(add(x,y))
    elif o == "-":
        print(jian(x,y))
    elif o == "*":
        print(cheng(x,y))
    elif o == "/":
        print(chu(x,y))
    else:
        pass
    
operator(2,3,'+')
operator(2,4,'/')
```

    5
    0.5
    


```python
from __future__ import division

def jia(x,y):
    return x + y

def jian(x,y):
    return x - y

def cheng(x,y):
    return x * y

def chu(x,y):
    return x / y

operator = {"+":jia,"-":jian,"*":cheng,"/":chu}#通过字典取得字典对象

print(operator["+"](2,3))

def f(x,o,y):
    print(operator.get(o)(x,y))

f(3,"+",2)
```

    5
    5
    

## 内置函数

常用函数   

- abs():绝对值
- max():最大值
- min():最小值
- len():长度
- divmod():两数相除的商和余数
- pow():幂运算
- round:返回浮点数
- callable():测试函数是否能被调用
- isinstance():判断某个对象的类型
- cmp():比较两个字符串
- range():快速生成一个序列

类型转化的函数：
- type()
- int()
- long()
- float()
- complex()
- tuple()
- str()
- list()
- hex()
- oct()
- chr()
- ord()

>以上函数都可以通过help了解其功能用法


```python
def a(x):
    if x < 0:
        return -x
    return x

n = a(10)
print(n)
```

    10
    


```python
abs(-10)
```




    10




```python
l = [2,3,4,5,6,67,68,79,23]
len(l)
min(l)
```




    2




```python
#当我们想知道一个函数怎么用时，可以使用help（object）
divmod(5,2)
```




    (2, 1)




```python
#pow函数的用法
help(pow)
```

    Help on built-in function pow in module builtins:
    
    pow(x, y, z=None, /)
        Equivalent to x**y (with two arguments) or x**y % z (with three arguments)
        
        Some types, such as ints, are able to use a more efficient algorithm when
        invoked using the three argument form.
    
    


```python
pow(2,3,4)
```




    0




```python
#round函数用法
round(12)
```




    12




```python
callable(max)
```




    True




```python
isinstance(l,list)#判断某个对象的类型
```




    True




```python
range(10)
```




    range(0, 10)




```python
tuple(l)
```




    (2, 3, 4, 5, 6, 67, 68, 79, 23)



当我们使用函数时，应该现象一下Python是否提供了这种内置函数，如果提供就省了自己编写的时间

### string函数
- str.capitalize()
- str.replace()
- str.split()


```python
s = "hello world"
#让字符串首字母大写
s.capitalize()
```




    'Hello world'




```python
#字符串替换
s.replace("hello","good")
```




    'good world'




```python
ip = "192.168.1.123"
ip.split(".",1)
```




    ['192', '168.1.123']



### 序列处理函数
- len()
- max()
- min()
- filter()
- zip()
- map()
- reduce()


```python
help(filter)
```

    Help on class filter in module builtins:
    
    class filter(object)
     |  filter(function or None, iterable) --> filter object
     |  
     |  Return an iterator yielding those items of iterable for which function(item)
     |  is true. If function is None, return the items that are true.
     |  
     |  Methods defined here:
     |  
     |  __getattribute__(self, name, /)
     |      Return getattr(self, name).
     |  
     |  __iter__(self, /)
     |      Implement iter(self).
     |  
     |  __new__(*args, **kwargs) from builtins.type
     |      Create and return a new object.  See help(type) for accurate signature.
     |  
     |  __next__(self, /)
     |      Implement next(self).
     |  
     |  __reduce__(...)
     |      Return state information for pickling.
    
    


```python
def f(x):
    if x > 5:
        return True

f(10)

l = [1,23,4,4,5,6,7]

a = list(filter(f,l))#过滤掉小于等于5的数
a
```




    [23, 6, 7]




```python
name = ["milo","zou","tom"]
age = [20,30,40]
tel = ["133","156","189"]
list(zip(name,age,tel))
```




    [('milo', 20, '133'), ('zou', 30, '156'), ('tom', 40, '189')]




```python
def f1( x,y,z ):  
    return (x,y,z)

list(map(f1,name,age,tel))
```




    [('milo', 20, '133'), ('zou', 30, '156'), ('tom', 40, '189')]




```python
l = list(range(1,101))
print(l)

n = 0

for i in l:
    n += i
    
print(n)
```

    [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99, 100]
    5050
    

在Python 3里,reduce()函数已经被从全局名字空间里移除了,它现在被放置在fucntools模块里用的话要先引入：


```python
from functools import reduce 

def f2(x,y):
    return(x + y)

reduce(f2,l)
```




    5050




```python
reduce(lambda x,y:x + y,l)
```




    5050




```python
print(list(filter(lambda x:x % 2 == 0,l)))
```

    [2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30, 32, 34, 36, 38, 40, 42, 44, 46, 48, 50, 52, 54, 56, 58, 60, 62, 64, 66, 68, 70, 72, 74, 76, 78, 80, 82, 84, 86, 88, 90, 92, 94, 96, 98, 100]
    


```python
print(list(map(lambda x:x * 2 +10,l)))
```

    [12, 14, 16, 18, 20, 22, 24, 26, 28, 30, 32, 34, 36, 38, 40, 42, 44, 46, 48, 50, 52, 54, 56, 58, 60, 62, 64, 66, 68, 70, 72, 74, 76, 78, 80, 82, 84, 86, 88, 90, 92, 94, 96, 98, 100, 102, 104, 106, 108, 110, 112, 114, 116, 118, 120, 122, 124, 126, 128, 130, 132, 134, 136, 138, 140, 142, 144, 146, 148, 150, 152, 154, 156, 158, 160, 162, 164, 166, 168, 170, 172, 174, 176, 178, 180, 182, 184, 186, 188, 190, 192, 194, 196, 198, 200, 202, 204, 206, 208, 210]
    


```python

```
