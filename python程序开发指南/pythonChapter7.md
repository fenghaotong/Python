
# python第七章学习

- [x] 面向对象方法
- [x] Python中的类与对象
- [x] 异常也是类
- [x] 迭代器
- [x] 生成器

## 面向对象方法
- 提到面向对象，我们应该能想到这样几个词语：多态（Polymorphism），继承（Inheritance）和封装（Encapsulation）。Python也是一种支持OOP的动态语言。

- 面向对象的优势之一是如果我们有一个类，就可以对其进行专用化，这意味着创建一个新类，新类继承原始类的所有属性（数据和方法），通常可以添加或替换原始类的某些方法，或添加更多的实例变量

- 在Python中每个内置的类、库类以及我们创建的每个类都直接或间接的从最顶层的基类——object衍生而来

- 如果有一个MyDict（继承自dict的类）类的对象，并调用同时又dict与MyDict定义的方法，Python将正确地调用MyDict版本的方法——这也就是所谓的动态方法绑定，也称为多态性。如果我们在重新实现后的方法内部调用该方法的基类版本，就可以使用内置的super()函数实现

- 有些面向对象语言提供了Python没有提供的两个功能，第一个是重载，也就是说在同一个类内，使得方法有同样的名称，但又不同的参数列表。由于Python具有非常丰富的参数处理功能，因此这并不会成为限制因素。第二个访问控制——实际上并不存在强制数据隐私的“防禅”机制，不过，我们创建属性是在属性名前以两个下划线引导，Python就会阻止无心的访问，因此也可以认为是私有的。

#### 在讨论Python的OOP之前，先看几个OOP术语的定义：
- 类：对具有相同数据和方法的一组对象的描述或定义。
- 对象：对象是一个类的实例。
- 实例(instance)：一个对象的实例化实现。
- 标识(identity)：每个对象的实例都需要一个可以唯一标识这个实例的标记。
- 实例属性（instance attribute）：一个对象就是一组属性的集合。
- 实例方法(instance method)：所有存取或者更新对象某个实例一条或者多条属性的函数的集合。
- 类属性（classattribute）：属于一个类中所有对象的属性，不会只在某个实例上发生变化
- 类方法（classmethod）：那些无须特定的对性实例就能够工作的从属于类的函数。

## Python中的类与对象

- Python中定义类的方式比较简单：    

      class 类名：    
        类变量
         def __init__(self,name):
         def 函数(self,...)
      
>其中直接定义在类体中的变量叫类变量，而在类的方法中定义的变量叫实例变量。类的属性包括成员变量和方法，其中方法的定义和普通函数的定义非常类似，但方法必须以self作为第一个参数。下面是一个例子：


```python
class person(object):
    percount = 0
    def __init__(self,name,age):
        self.name = name
        self.age = age
    def tar(self):
        return ('快乐')  
tom=person('Tom',17)
print('我是',tom.name)
print('我',tom.age)
print('我很',tom.tar())
```

    我是 Tom
    我 17
    我很 快乐
    

>- percount变量是一个类变量，它的值将在这个类的所有实例之间共享，我们可以在内部类或外部类使用person.percount访问。
>- 第一种方法__init__()方法是一种特殊的方法，被称为类的构造函数或初始化方法，当创建了这个类的实例时就会调用该方法

### 创建实例对象

- 要创建一个对象，需要两个必须的步骤，首先要创建一个原始的或未初始化的对象，之后必须对该对象进行初始化以备使用，有些面向对象语言将这两个步骤结合在一起，Python则将其作为两个单独的步骤。在创建对象时，首先调用特殊方法`__new__()`来创建该对象，之后调用特殊方法`__init__()`对其初始化

在上例中语句    
- tom=person（'tom'，17）#就创建了一个实例对象

在实际编程中，我们创建的几乎所有Python类都只需要重新实现`__init__()`方法，因为如果我们不提供自己的`__new__()`方法，Python就会自动调用`object.__new__()`方法，并且这一方法也已足够

### 访问对象属性       
- tom.name
- tom.age
- tom.tar()

#### 删除、添加、修改类的属性
- tom.height = 60 #添加类的属性
- tom.height = 70 #修改类的属性
- del tom.height #删除类的属性

>我们也可以使用以下函数的方式来访问属性：
>- getattr(obj, name[, default]) : 访问对象的属性。
>- hasattr(obj,name) : 检查是否存在一个属性。
>- setattr(obj,name,value) : 设置一个属性。如果属性不存在，会创建一个新属性。
>- delattr(obj, name) : 删除属性。


```python
class person(object):
    percount = 0
    def __init__(self,name,age):
       self.name = name
       self.age = age
    def tar(self):
        return ('快乐')  
tom=person('Tom',17)
print('我是',tom.name)
print('我',tom.age)
print('我很',tom.tar())
hasattr(tom, 'age')    # 如果存在 'age' 属性返回 True。
getattr(tom, 'age')    # 返回 'age' 属性的值
setattr(tom, 'age', 8) # 添加属性 'age' 值为 8
print("添加之后的属性age=",tom.age)
delattr(tom, 'age')    # 删除属性 'age'
# print（tom.age）当加上这句话的时候就会出错，因为此的属性age已经被删除“SyntaxError: invalid character in identifier”
```

    我是 Tom
    我 17
    我很 快乐
    添加之后的属性age= 8
    

### python内置类属性
- \____dict\____:类的属性（包含一个字典，由类的数据属性组成）
- \____doc\____ :类的文档字符串
- \____name\____: 类名
- \____module\____: 类定义所在的模块（类的全名是'__main__.className'，如果类位于一个导入模块mymod中，那么className.__module__ 等于 mymod）
- \____bases\____ : 类的所有父类构成元素（包含了以个由所有父类组成的元组）


```python
class person(object):
    '所有人的基类'
    percount = 0
    def __init__(self,name,age):
       self.name = name
       self.age = age
    def tar(self):
        return ('快乐') 
    
tom=person('Tom',17)

print('我是',tom.name)
print('我',tom.age)
print('我很',tom.tar())


print("Person.__doc__:", person.__doc__)
print ("Person.__name__:",person.__name__)
print ("Person.__module__:",person.__module__)
print ("Person.__bases__:",person.__bases__)
print ('Person.__dict__:',person.__dict__)
```

    我是 Tom
    我 17
    我很 快乐
    Person.__doc__: 所有人的基类
    Person.__name__: person
    Person.__module__: __main__
    Person.__bases__: (<class 'object'>,)
    Person.__dict__: {'tar': <function person.tar at 0x0000000004566158>, '__dict__': <attribute '__dict__' of 'person' objects>, 'percount': 0, '__weakref__': <attribute '__weakref__' of 'person' objects>, '__module__': '__main__', '__init__': <function person.__init__ at 0x00000000045660D0>, '__doc__': '所有人的基类'}
    

### python对象销毁(垃圾回收)
- 和java一样，python也使用了引用计数这一技术来追踪内存中的对象      
- 在Python内部记录着所有使用中的对象各有多少引用。
- 一个内部跟踪变量，称为一个引用计数器。
- 当对象被创建时， 就创建了一个引用计数， 当这个对象不再需要时， 也就是说， 这个对象的引用计数变为0 时， 它被垃圾回收。但是回收不是"立即"的， 由解释器在适当的时机，将垃圾对象占用的内存空间回收。       
> 垃圾回收机制不仅仅针对引用计数为0的时候，也可以处理循环引用的情况，所谓循环引用意思就是，两个对象相互引用，而不被其他的变量引用。这种情况下，使用引用计数是不够的。python的垃圾收集器其实是一个引用计数器和循环垃圾收集器。作为引用计数的补充， 如果那些对象分配的内存过高，垃圾收集器也会进行处理（及未通过引用计数销毁的那些）。 在这种情况下， 解释器会暂停下来， 试图清理所有未引用的循环。    

下面有个例子：


```python
class person(object):
    '所有人的基类'
    percount = 0
    def __init__(self,name,age):
       self.name = name
       self.age = age
    def tar(self):
        return ('快乐') 
    def __del__(self):
        class_name = self.__class__.__name__
        print (class_name,'销毁')
    
tom=person('Tom',17)

print('我是',tom.name)
print('我',tom.age)
print('我很',tom.tar())

del tom

#print('我很',tom.tar()) #加上这个就会出错因为tom这个对象已经被删除
```

    我是 Tom
    我 17
    我很 快乐
    person 销毁
    

## 封装
- 面向对象的程序设计中，某个类把所需要的数据（也可以说是类的属性）和对数据的操作（也可以说是类的行为）全部都封装在类中，分别称为类的成员变量和方法（或成员函数）。这种把成员变量和成员函数封装在一起的编程特性称为封装。

### 类的属性
- 类由属性和方法组成，类的属性是对数据的封装，而类的方法是对类的行为的封装。
- 类的属性按使用范围分为共有属性和私有属性。
>- 具体地，在python实现面向对象的编程思想的时候，封装在类中的属性可以分为两种数据类的属性和数据对象的属性（也可以成为数据类的成员变量和属于对象的成员变量），其中，这两种成员变量又各自分为共有成员变量和私有成员变量。

####  类的成员变量和对象的成员变量
- 类的成员变量定义在类中，和类的成员函数在同一缩进等级。而对象的成员变量定义在\____init\____(self)成员函数中，和\____init\____(self)函数下的变量和语句在同一等级。通俗地讲，类的成员变量属于类，共类的所有对象和类本身所共有，也就是说所有的类的对象和类只有一份这样的变量。而对象的成员变量属于类的对象本身，每个对象都有一份，而且各个对象之间互不影响。
```
class person(object):
    percount = 0
    def __init__(self,name,age):
       self.name = name
       self.age = age
    def tar(self):
        return ('快乐')  
tom=person('Tom',17)
print('我是',tom.name)
print('我',tom.age)
print('我很',tom.tar())
```     
>这个例子里我们知道percount就是类的成员变量，而name，age是对象的成员变量

#### 公有成员变量和私有成员变量
- python中用成员变量的名字来区分是共有成员变量或者是私有成员变量。python中，以两个下划线‘\__’开头的变量都是私有成员变量，而其余的变量都属于公有成员变量。其中，私有的成员变量只能在类的内部访问，而共有的公有的成员变量可以在类的外部进行访问。

>- 四种成员变量其使用方法如下表： 

| 类型   | 在类外部通过类名 | 在类外部通过对象名 | 在类内部通过类名 | 在类内部通过对象名 |     
|:-----------|:-----------|:------------|:-------------|:---------------:|
|类的公有变量  |可以访问   |可以访问      |可以访问     |可以访问      |   
|类的私有变量  |不可以访问  |不可以访问     |可以访问    | 可以访问      |   
|对象的公有变量|不可以访问  |可以访问      |不能访问     |可以访问      |    
|对象的私有变量|不可以访问  |不可以访问     |不能访问    |可以访问      |     

>要注意的是，这里有一个例外但是紧紧用来体调试程序。可以通过“objName.\____ClsName\____attriName”的方式来访问类的私有变量，但是注意这种方式也仅仅用于调试程序（比如可以用tom.\____person\____ gold来访问Person类的私有成员变量\___gold）。

>除了上面提到的属性之外，类还有一种属性叫内置属性，它们是在系统定义类的时候默认添加的，由前后两个下划线命名。
>- \____dict\____ : 类的属性（包含一个字典，由类的数据属性组成）
>- \____doc\____ :类的文档字符串
>- \____name\____: 类名
>- \____module\____: 类定义所在的模块（类的全名是'\____main\____.className'，如果类位于一个导入模块mymod中，那么className.\____module\____ 等于 mymod）
>- \____bases\____ : 类的所有父类构成元素（包含了以个由所有父类组成的元组）

### 类的方法
- 如上面所说，类的方法是对类行为的封装。类的方法也分为公有方法和私有方法。类的私有方法只能通过对象名（在类内部也就是self）在类的内部进行访问，而公有方法可以在类的外部通过对象名进行访问。和属性不同的是，一般意义上的类方法属于对象，也就是说只有通过对象才可以进行调用，不能直接通过类名进行调用。一般类方法的第一个参数必须是代指类对象本身的（一般我们常用self，实际上可以是任何自定义的名字，只不过self是大家约定俗成的用法，在下面介绍的类方法中，大家一般用cls，因为那里更多地标识的是一个类），可以通过self访问类对象的成员函数和数据。
>同样，公有的成员函数和私有的成员函数也是通过名字来区分的，双下划线‘__’开头的函数是私有成员函数。

#### 类方法和静态方法（这个还不太理解）

- python中对象有两种：经典对象和新型对象。经典对象就是不继承object父类定义出来的对象，新型对象就是要继承object类定义出的对象。新型对象和经典对象最大的区别就是，新型对象中提供了对类方法和静态方法的支持。
- 类方法就是被classmethod()函数处理过的函数，能够直接通过类名进行调用，也能够被对象直接调用。静态方法相当于类层面的全局函数，可以被类直接调用，可以被所有实例化对象共享，通过staticmethod()定义静态方法，静态方法没有self参数。当然，也可以用更加方便的装饰器@classmethod和@staticmethod来定义类方法和静态方法。

>区别： 
>- 类方法和静态方法都可以被类和类实例调用，类实例方法仅可以被类实例调用
>- 类方法的隐含调用参数是类，而类实例方法的隐含调用参数是类的实例，静态方法没有隐含调用参数

下面有一个例子


```python
class A(object):  
    def foo(self,x):  
    #类实例方法  
        print ("executing foo(%s,%s)"%(self,x))
 
    @classmethod  
    def class_foo(cls,x):  
    #类方法  
        print ("executing class_foo(%s,%s)"%(cls,x)) 
 
    @staticmethod  
    def static_foo(x):  
    #静态方法  
        print ("executing static_foo(%s)"%x)  
        
#调用方法
a = A()# 创建一个对象

a.foo(1)    #隐含调用参数是类
  
a.class_foo(1)   #隐含调用参数是类的实例 
A.class_foo(1)  
  
a.static_foo(1)  #没有隐含调用参数  
A.static_foo(1)   
```

    executing foo(<__main__.A object at 0x0000000004559668>,1)
    executing class_foo(<class '__main__.A'>,1)
    executing class_foo(<class '__main__.A'>,1)
    executing static_foo(1)
    executing static_foo(1)
    

#### 2.2.2 构造函数和析构函数

构造函数\____init\____和析构函数\____del\____(如果学过C++应该都知道)

- python中的构造函数是\____init\____，用于初始化类对象的初始化，\____init\____方法是可选的，如果不提供，python会给出一个默认的\____init\____方法。python中的析构函数是\____del\____，用于释放对象占用的资源。python中析构函数也是可选的，如果不提供，则python会提供默认的析构函数。如果要显示调用析构函数，可以使用del关键字。
>关于\____init\____构造函数要注意点，上面说到对象的变量定义在\____init\____函数中。其实，除了\____init\____函数，其他函数通过传入的self参数，也可以给对象增加一个变量，在其它对象中可以访问到。这里，上面之所以这样说，是因为\____init\____函数的好处是不用自己显示调用，在对象创建的时候，自动被调用。这样 ，在\____init\____中定义的变量就会有一个效果就是在对象存在的时候，它们就已经存在了，这实际上更符合我们对于对象的变量的期望，因此，我们就说对象的变量一般定义在\____init\____函数中。(如下面例子)


```python
class Person:
    def __init__(self,name,age):
        self.name = name
        self.age = age
tom = Person('tom',23)#在__init__中定义的变量就会有一个效果就是在对象存在的时候，它们就已经存在了
print(tom.name)
print(tom.age)
```

    tom
    23
    

## 继承
对我们来说继承的通俗意思就是，下一代把上一代的东西继承下来，变成自己的，计算机中的继承也很类似这个意思    

- 面向对象的编程带来的主要好处之一是代码的重用，实现这种重用的方法之一是通过继承机制。继承完全可以理解成类之间的类型和子类型关系。
>- 需要注意的地方：继承语法 class 派生类名（基类名）：//... 基类名写作括号里，基本类是在类定义的时候，在元组之中指明的。

在Python中继承拥有以下几个特征：

1.父类中的构造函数\____init\____()在子类中不会被调用，需要在子类中单独调用    
2.在调用基类的方法时，需要加上基类的类名前缀，且需要带上self参数变量。区别于在类中调用普通函数时并不需要带上self参数 
3.Python总是首先查找对应类型的方法，如果它不能在派生类中找到对应的方法，它才开始到基类中逐个查找。（先在本类中查找调用的方法，找不到才去基类中找）。
>如果继承元组中继承了一个以上的类，称为“多重继承”。

语法如下：    
class sun（Father1,[Father2,....]）:


```python
#举个例子
class Father:
    FatherNum = 50
    def __init__(self):
        print('父类构造函数')
    def FatherMethon(self):
        print('调用父类方法')
class Sun(Father):
    def __init__(self):
        print("子类构造函数")
    def SunMethon(self):
        print('调用子类方法')
sun = Sun()
sun.__init__()
sun.FatherMethon()
sun.SunMethon()
```

    子类构造函数
    子类构造函数
    调用父类方法
    调用子类方法
    


```python
def f1(self, x, y):
    return min(x, x+y)

f = f1
f(f,2,1)
```




    2



## 异常也是类



用户定义的异常类也由类标识。利用这个机制可以创建可扩展的异常层次。

raise语句有两种新的有效的（语义上的）形式：

```
raise Class

raise Instance
```

第一种形式中，Class 必须是type或者它的子类的一个实例。第一种形式是一种简写：

raise Class()

except子句中的类如果与异常是同一个类或者是其基类，那么它们就是相容的（但是反过来是不行的——except子句列出的子类与基类是不相容的）。例如，下面的代码将按该顺序打印 B、 C、 D：


```python
class B(Exception):
    pass
class C(B):
    pass
class D(C):
    pass

for cls in [B, C, D]:
    try:
        raise cls()
    except D:
        print("D")
    except C:
        print("C")
    except B:
        print("B")
```

    B
    C
    D
    

请注意，如果except 子句的顺序倒过来 (excpet B在最前面），它就会打印B，B，B —— 第一个匹配的异常被触发。

打印一个异常类的错误信息时，先打印类名，然后是一个空格、一个冒号，然后是用内置函数str()将类转换得到的完整字符串。

## 迭代器


```python
#现在你可能注意到大多数容器对象都可以用for遍历：
#coding:utf-8
for element in [1, 2, 3]:
    print(element)
for element in (1, 2, 3):
    print(element)
for key in {'one':1, 'two':2}:
    print(key)
for char in "123":
    print(char)
for line in open("myfile.txt"):
    print(line, end='')
```

    1
    2
    3
    1
    2
    3
    one
    two
    1
    2
    3
    first
     
    end

这种访问风格清晰、 简洁又方便。迭代器的用法在 Python 中普遍而且统一。在后台， for语句调用传入了容器对象的iter() 。该函数返回一个定义了`__next__()`方法的迭代器对象，它在容器中逐一访问元素。没有后续的元素时，`__next__()`会引发StopIteration异常，告诉for循环终止。你可以是用内建的next()函数调用`__next__()`方法；此示例显示它是如何工作：


```python
s = 'abc'
it = iter(s)
next(it)
```




    'a'




```python
next(it)
```




    'b'




```python
next(it)
```




    'c'




```python
next(it)
```


    ---------------------------------------------------------------------------

    StopIteration                             Traceback (most recent call last)

    <ipython-input-18-2cdb14c0d4d6> in <module>()
    ----> 1 next(it)
    

    StopIteration: 


看过迭代器协议背后的机制后，将很容易将迭代器的行为添加到你的类中。定义一个`__iter__()`方法，它使用`__next__()`方法返回一个对象。如果类定义了`__next__()`，`__iter__()`可以只返回self：


```python
class Reverse:
    """Iterator for looping over a sequence backwards."""
    def __init__(self, data):
        self.data = data
        self.index = len(data)
    def __iter__(self):
        return self
    def __next__(self):
        if self.index == 0:
            raise StopIteration
        self.index = self.index - 1
        return self.data[self.index]
```


```python
re = Reverse("hello")
iter(re)
```




    <__main__.Reverse at 0x455b048>




```python
for char in re:
    print(char)
```

    o
    l
    l
    e
    h
    

## 生成器

- 生成器是简单且功能强大的工具，用于创建迭代器。它们写起来就像是正规的函数，需要返回数据的时候使用yield语句。每次在它上面调用next()时，生成器恢复它脱离的位置（它记忆语句最后一次执行的位置和所有的数据值）。以下示例演示了生成器可以非常简单地创建出来：


```python
def reverse(data):
    for index in range(len(data)-1, -1, -1):
        yield data[index]
```


```python
for char in reverse("hello"):
    print(char)
```

    o
    l
    l
    e
    h
    

- 生成器能做到的什么事，前一节所述的基于类的迭代器也能做到。生成器这么简洁是因为`__iter__()`和`__next__()`方法是自动创建的。

- 另一个关键特征是在调用中本地变量和执行状态会自动保存，这使得该函数更容易写，也比使用实例变量的方法，如self.index和self.data更清晰。

- 除了自动创建方法和保存程序的状态，当生成器终止时，它们会自动引发StopIteration。结合这些特点，创建迭代器就和写一个普通函数一样简单


```python

```
