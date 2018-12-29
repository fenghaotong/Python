
# pytho你第三章学习

序列类型

- [x] 元组
- [x] 列表    

集合类型     

- [x] 集合

映射类型      

- [ ] 字典

## 序列类型
- 列表、元组和字符串都是序列
- 序列的两个主要特点是索引操作符和切片操作符       
    - 索引操作符让我们从序列中抓取一个特定项目。       
    - 切片操作符让我们能够获取序列的一个切片，即一部分序列。
- 序列的基本操作：              
1.len(): 求序列长度      
2.+：    连接2个序列       
3.\*：   重复序列元素     
4.in:    判断元素是否在序列中     
5.max():  返回最大的值    
6.min():  返回最小的值      
7.cmp(tuple1,tuple2): 比较2个的序列值是否相同     


```python
str1 = 'abcde'
str1[1:4]
```




    'bcd'




```python
len(str1)
```




    5




```python
str2 = '12345'
str1 + str2# 连接2个序列
```




    'abcde12345'




```python
str1*5#重复序列元素
```




    'abcdeabcdeabcdeabcdeabcde'




```python
'c' in str1#判断元素是否在序列中
```




    True




```python
max(str2)#返回最大的值
```




    '5'




```python
str1
str2
```




    '12345'



### 元组
- 元组是个有序的序列，其中包含0个或多个对象引用。原则支持与字符串一样的分片与步距的语法，这使得元组中提取数据比较容易。与字符串类似，元组也会固定的，因此，不能替换或删除其中包含的任意数据项。如果需要修改有序序列，我们应该使用列表而费元祖。如果我们有一个元组，但又需要对其进行修改，那么我们可以使用list()转换函数将其转换为列表，之后在产生的列表上进行适当的修改。


    - 元组通过圆括号中用逗号分隔的项目定义
    - 元组通常用在时语句或用户定义的函数能够安全的采用一组值额时候，即被使用的元组的值不会改变


```python
str2
```




    'abcde'




```python
id(str2)
```




    72430848




```python
str2 = '12345'
str2
```




    '12345'




```python
id(str2)
```




    72431240




```python
userinfo = "milo 30 male"#用字符串这种情况不太方便，单独取时
#如果我们想取出milo
userinfo[:4]
```




    'milo'




```python
t = ("milo",30,"male")#定义一个元组
t[0]
```




    'milo'



####  创建元组
- 一个空的元组由一对空的圆括号组成      
    - 如myempty = ()      
- 含有单个元素的元组      
    - singleton = (2,)      
- 一般的元组       
    - zoo = ('wolf','elephant','penguin')
    - new zoo = ('monkey','dolphin',zoo)


```python
t1 = ()
t2 = (2,)
```


```python
type(t1)
```




    tuple




```python
type(t2)
```




    tuple




```python
#如果不加逗号
t3 = (2)
type(t3)#此时的t就不是元组类型
```




    int



#### 元组操作
- 元组和字符串类型一样属于序列类型，可通过索引和切片操作    
- 元组值亦不可变


```python
#如果我们去改一个值是就会出错
t[1] = 31
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-40-3470b0533219> in <module>()
          1 #如果我们去改一个值是就会出错
    ----> 2 t[1] = 31
    

    TypeError: 'tuple' object does not support item assignment



```python
t = ("milo",30,"male")
t[1]
```




    30




```python
name,age,gender = t
print(name)
print(age)
print(gender)
```

    milo
    30
    male
    

- tuple数据类型可以作为一个函数进行调用，tuple()——不指定参数时将返回一个空元组，使用tuple作为参数时将返回该参数的浅拷贝，对其他任意参数，将尝试把给定的对象转换为tuple类型，该函数最多只能接受一个参数


- 元组只提供了两种方法:  

    1.t.count(x),返回对象x在元组中出现的次数        
    2.t.index(x)，返回对象在元组t中出现的最左边位置——在元组中不包含x时，则产生ValueError异常
    
下面给出几个分片实例：   


```python
hair = "black","brown","blonde","red"
hair[2]
```




    'blonde'




```python
hair[-3:]
```




    ('brown', 'blonde', 'red')




```python
hair[:2],"gray",hair[2:]
```




    (('black', 'brown'), 'gray', ('blonde', 'red'))



这里我们本来想创建一个新的5元组，但结果是一个三元组，其中包含两个二元组，之所以会这样，是因为我们在3个项（一个元组，一个字符串，一个元组）之间使用了逗号操作符。要得到一个单独的元组，并包含所需项，我们必须对其进行连接：


```python
hair[:2] + ("gray",) + hair[2:]
```




    ('black', 'brown', 'gray', 'blonde', 'red')



一个元组内可以有两个嵌套的元组，任何嵌套层次的组合类型都可以类似以下方式进行创建，而不需要格式化处理


```python
eyes = ("brown","hazel","amber","green","blue","gray")
colors = (hair,eyes)
colors[1][3:-1]
```




    ('green', 'blue')




```python
things = (1,-7.5,("pea",(5,"Xyz"),"queue"))
things[2][1][1][2]
```




    'z'



#### 命名的元组
- 命名的元组与普通元组一样，有相同的表现特征，其添加的功能就是可以根据名称引用元组中的项，就像根据索引位置一样，这一功能使我们可以创建数据项的聚集

- collection模块提供了namedtuple()函数，该函数创建自定义的元组数据类型，例如：
```
Sale = collections.namedtuple("Sale",
        "productid custonerid data quantity price")
```
collections.namedtuple()的第一个参数时想要创建的自定义元组数据类型的名称，第二个参数是一个字符串，其中包含使用空格分隔的名称，每个名称代表该元组数据类型的一项。



```python
import collections
Aircraft = collections.namedtuple("Aircraft",
                                "manufacturer model seating")
Seating = collections.namedtuple("Seating",
                               "minimum maximum")
aircraft = Aircraft("Airbus","A320-220",Seating(100,220))
aircraft.seating.maximum
```




    220



### 列表

- 列表是包含0ge或多个对象引用的有序序列，支持与字符串以及元组一样的分片与步距语法，这使得从列表中提取数据项很容易实现，与字符串以及元组不同的是，列表是可变的，因此，我们可以对列表的项进行删除或替换，插入、替换或者删除列表中的分片也是可能的。
- list数据类型可以作为函数进行调用，list()——不带参数进行调用时，将返回一个空列表；带一个list参数时，返回该参数的浅拷贝；对任意其他参数，则尝试将给定的对象转换为列表可以使用空的方括号来创建，包含一个或多个项的列表则可以使用逗号分隔的数据项（包含在[]）序列来创建。

- list是处理一组有序项目的数据结构，即你可以在一个列表中存储一个序列的项目
- 列表是可变类型的数据
- 列表的组成：用[]表示列表，包含了多个以逗号分隔开的数字，或者字串。
    - List = ["Simon","David","Clotho","张三"]
    - List2 = [1,2,3,4,5]
    - List3 = ["str1","str2","str3","str4"]


```python
listmilo = []
```


```python
type(listmilo)
```




    list




```python
listmilo = ['milo',30,'male']
listmilo[0]
```




    'milo'



列表和元组的区别：元组在定义一个值的时候需要加逗号


```python
t3 = ('abc')#不加逗号的时候就是字符串
```


```python
type(t3)
```




    str




```python
l3 = ['abc']
type(l3)
```




    list



#### 列表操作
- 取值
    - 切片和索引
    - list[]
- 添加
    - list.append()
- 删除
    - del(list[])
    - list.remove(list[])
- 修改
    - list[] = x
- 查找
    - var in list


```python
listmilo
```




    ['milo', 30, 'male']




```python
listmilo[0]#取值
```




    'milo'




```python
listmilo[0] = 'zou'#修改
listmilo
```




    ['zou', 30, 'male']




```python
type(listmilo)
```




    list




```python
id(listmilo)#存储空间
```




    60921608




```python
listmilo[0] = 'milo'
id(listmilo)#存储空间一样
```




    60921608




```python
listmilo.append("12345")#增加一个值
listmilo
```




    ['milo', 30, 'male', '12345', '12345']




```python
listmilo.remove("12345")#删除操作
```


```python
listmilo
```




    ['milo', 30, 'male', '12345']




```python
listmilo.remove(listmilo[3])#删除操作
```


```python
listmilo
```




    ['milo', 30, 'male']



- 有些情况下，我们需要一次提取两个或者更多个数据项，可以使用序列拆分实现。任意可迭代的（列表、元组等）数据类型都可以使用序列拆分操作符进行拆分，即\*,用于赋值操作符左边的两个或者对个变量是，其中的一个使用\*进行引导，数据项将赋值给该变量，而剩下的所有的数据项将赋值给带星号的变量

- 操作符\*号是用多复制操作符还是序列拆分操作符并不会产生语义上的二义性，当\*出现在赋值操作的左边是，用作拆分操作符，出现在其他位置是，若用作单值操作符，则代表拆分操作符；若用作二进制操作符，则代表多复制操作符。


```python
first,*rest = [9,2,-4,8,7]
first,rest
```




    (9, [2, -4, 8, 7])




```python
first,*mid,last = "Charles Philip Arthur George Windsor".split()
first,mid,last
```




    ('Charles', ['Philip', 'Arthur', 'George'], 'Windsor')




```python
#定义一个有三个参数的函数
def product(a,b,c):
    return a * b * c 
```


```python
#可以使用3个参数来调用该函数
product(2,3,5)
```




    30




```python
#也可以使用带星号的参数
L = [2,3,5]
product(*L)
#在这里列表的3个参数被*拆分，调用函数时，函数将得到这三个参数
```




    30



#### 列表内涵
- 小列表通常可以使用列表字面值来创建，但是长一点的列表，通常需要使用程序进行创建。对于一系列整数，我们可以使用list(range(n))创建，或者如果需要一个整数迭代子，使用range()就足以完成任务，但对更复杂一些的列表，使用for...in循环创建是一种更常见的做法。


```python
#生成给定时间范围内的闰年列表
leaps = []
for year in range(1900,1940):
    if(year % 4 == 0 and year % 100 != 0)or(year % 400 == 0):
        leaps.append(year)
leaps
```




    [1904, 1908, 1912, 1916, 1920, 1924, 1928, 1932, 1936]



- 列表内涵是一个表达式，也是一个循环该循环有一个可选的、包含在方括号中的条件，作用是为列表生成的数据项，并且可以使用条件过滤掉不需要的数据项。列表内涵最简单的形式如下：
```
[item for item in iterable]
```
上面的语句将返回一个列表，其中包含iterable中的每个数据项，在语义上与list(iterable)是一致的。有两个特点使得列表内涵具有强大的功能，也更能引起使用者的兴趣，一个是可以使用表达式，另一个是可以附加条件——由此带来如下两种列表内涵的常见语法格式：
```
[expression for item in iterable]       
[expression for item in iterable if condition]     
```

第二种语法格式实际上等价于：
```
temp = []     
for item in iterable:     
    if condition:
        temp.append(expression)
```


```python
#上面例子如果使用列表内涵,减少了代码量

leaps = [y for y in range(1900,1940)
        if(y % 4 == 0 and y % 100 != 0)or(y % 400 == 0)]
leaps
```




    [1904, 1908, 1912, 1916, 1920, 1924, 1928, 1932, 1936]




```python
#举一个复杂一点的例子

codes = []
for sex in "MF":
    for size in "SMLX":
        if sex  == "F" and size == "X":
            continue
        for color in "BGM":
            codes.append(sex + size +color)
codes
```




    ['MSB',
     'MSG',
     'MSM',
     'MMB',
     'MMG',
     'MMM',
     'MLB',
     'MLG',
     'MLM',
     'MXB',
     'MXG',
     'MXM',
     'FSB',
     'FSG',
     'FSM',
     'FMB',
     'FMG',
     'FMM',
     'FLB',
     'FLG',
     'FLM']




```python
#使用列表内涵
codes = [s + z + c for s in "MF" for z in "SMLX" for c in "BGM"
        if not(s == "F" and z == "X")]
codes
```




    ['MSB',
     'MSG',
     'MSM',
     'MMB',
     'MMG',
     'MMM',
     'MLB',
     'MLG',
     'MLM',
     'MXB',
     'MXG',
     'MXM',
     'FSB',
     'FSG',
     'FSM',
     'FMB',
     'FMG',
     'FMM',
     'FLB',
     'FLG',
     'FLM']



## 集合类型
- set也是一种组合数据类型，支持成员关系操作符（in）、对象大小计算操作符（len（）），并且也是iterable.
- Python提供了两种内置的集合类型：可变的set类型，固定的frozenset类型。
- 只有可哈希运算的对象可以添加到集合中，所有的内置的固定类型（比如：float、frozenset、int、str、tuple）都是可哈希运算的，都可以添加到集合中。内置的可变数据类型（比如：dict、list、set）都不是可哈希运算的，因为其哈希值会随着包含项数的变化而变化，因此，这些数据类型不能添加到集合中。


### 集合
- 集合是0个或者对个对象引用的无序组合，这些对象引用所引用的对象都是可哈希运算的。集合是可变的，因此可以很容易的添加或者移除数据项，但由于其中项是无序的，因此没有索引位置的概念，也不能分片或按步距分片。
- set数据类型可以作为函数进行调用，set()——不带参数进行调用时将返回一个空集合；带一个set参数返回该参数的浅拷贝；对任意其他参数，则尝试将给定的对象转换为集合。该参数只接受一个参数的情况。非空集合也可以不使用set()函数创建，空集合必须使用set()函数创建，而不能使用空的圆括号来创建。包含一个或多个项的集合，可以使用逗号分隔的数据项（包括在圆括号中）序列来创建，另一种创建方法就是使用集合内涵。

使用集合内涵创建集合的语法格式：
```
{expression for item in iterable}      
{expression for item in iterable if condition}

```


```python
#下面产生的三个集合是一样的
s1 = set("apple")  
print(s1)
s2 = set("aple") 
print(s2)
{'e','p','a','l'}
```

    {'p', 'a', 'e', 'l'}
    {'p', 'a', 'e', 'l'}
    




    {'a', 'e', 'l', 'p'}



## 映射类型
- 映射类型是一种支持成员关系操作符（in）与尺寸函数（len（））的数据类型，并且也是可以迭代的。映射是键-值数据项的组合，并提供了存取数据项及其键、值得方法。
- python 3.0支持两种无序的映射类型——内置的dict类型，以及标准库中的collections.defaultdict类型。
- 只有哈希运算的对象可用作字典的键，因此，固定的数据类型比如：float、frozenset、int、str、tuple）都可以做字典的键，可变的数据类型（比如dict、list与set）则不能

### 字典

- 字典是python中唯一的映射类型（哈希表）
- 字典对象是可变的，但是字典的键必须使用不可变对象，并且一个字典中可以使用不同类型的键值
- key()或者value（)返回键列表或者数值列表
- items()返回包含键值的元组


```python
#定义一个列表
#t = [name "milo",age = 30]
t1 = ['name','age','gender']
t2 = ['milo',30,'male']
```

#### 创建字典
- {}
- 使用工厂方法dict（0
    - 例：fdict = dict(['x',1],['y',2])
- 内建方法：fromkey()，字典中的元素具有相同的值，默认为None
    - 例：ddict = {}.fromkeys(('x','y'),-1)


```python
dic = {"name":"milo",'age':30,"gender":"amle"}
dic['name']
```




    'milo'




```python
dic1 = {1:'123',"name":"milo",'x':456}
dic1
```




    {1: '123', 'name': 'milo', 'x': 456}




```python
a = 123
b = 456
dic2 = {a:"aaa","b":"bbbb"}
dic2[123]
```




    'aaa'




```python
ddict = {}.fromkeys(('x','y'),-1)
ddict
```




    {'x': -1, 'y': -1}



#### 访问字典的值
- 直接使用key访问，key不存在报错，可以使用had_key()或者in和not in判断，但是had_key()方法即将放弃。
- 循环遍历：
    - 例：for key in dict1.keys():
- 使用迭代器：for key in dict1:


```python
dic
```




    {'age': 30, 'gender': 'amle', 'name': 'milo'}




```python
for k in dic:
    print(k)
```

    gender
    name
    age
    


```python
for k in dic:
    print(dic[k])
```

    amle
    milo
    30
    

#### 更新和删除
- 直接用键值访问更新：内建的update()方法可以将整个字典内容拷贝到另一个字典中。
- del dict1['a']删除字典中键值为a的元素
    - dict1.pop('a')删除并且返回键为'a'的元素
    - dict1.clear()删除字典所有元素
    - del dict1删除整个字典


```python
dic
```




    {'age': 30, 'gender': 'amle', 'name': 'milo'}




```python
dic['tel'] = '12345678'#在字典中增加一个值
dic
```




    {'age': 30, 'gender': 'amle', 'name': 'milo', 'tel': '12345678'}




```python
del(dic['tel'])
dic
```




    {'age': 30, 'gender': 'amle', 'name': 'milo'}




```python
dic.pop('age')#弹出age的值
```




    30




```python
dic
```




    {'gender': 'amle', 'name': 'milo'}




```python
dic.clear()#清空整个字典，此时字典dic仍然存在，只是一个空字典
```


```python
dic
```




    {}




```python
del(dic)#删除字典
dic
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-84-9841ee1c8079> in <module>()
          1 del(dic)#删除字典
    ----> 2 dic
    

    NameError: name 'dic' is not defined


- 字典相关的内建函数：
    - type(),str(),cmp()(cmp很少用于字典的比较，比较依次是字典的大小、键、值)
- 工厂函数dict():
    - 例如：dict(zip('x','y'),(1,2))或者dict(x = 1,y = 2)
    -     {'y':2,'x':1}
- 使用字典生成字典比用copy慢，因此这种情况下推荐使用copy()

字典方法

| 语法  |  描述 |
|:------:|:---------:|
| d.clear()   | 从dict d中移除所有项   |
| d.copy()   |  返回dict d的浅拷贝  |
| d.fromkeys(s,v)   | 返回一个dict，改字典的键为序列s中的项，值为None或v   |
| d.get(k)    | 返回键k相关联的值，如果k不存在dict d中就返回None   |
| d.get(k,v)   | 返回键k相关联的值，如果k不存在dict d中就返回v   |
| d.items()   | 返回dict d中所有（key，value）对的视图   |
| d.keys()   |  返回dict d中所有键的视图  |
| d.pop(k)   | 返回键k相关联的值，并移除键为k的项，如果k不包含在d中就产生KeyError异常   |
| d.pop(k,v)   | 返回键k相关联的值，并移除键为k的项，如果k不包含在d中就返回v   |
| d.popitem()   |  返回并移除dict d中的任意的（key，value）对，如果d为空就产生KeyError异常  |
| d.setdefault(k,v)   | 与dict.get()方法一样，不同之处在于，如果k没有包含在dict d中就插入一个键为k的新项，其值为None或v（如果给定了参数v）   |
| d.update(a)   | 将a额每个尚未包含在dict d中的（key，value）对添加到d，对同时包含在d与a中的每个键，使用a中对应的值替换d中对应的值——a可以是字典，也可以是（key，value）对的iterable，或关键字参数|
| d.value()   | 返回dict d所有值得视图   |


和list比较，dict有以下几个特点：


- 查找和插入的速度极快，不会随着key的增加而变慢；
- 需要占用大量的内存，内存浪费多。

而list相反：

- 查找和插入的时间随着元素的增加而增加；
- 占用空间小，浪费内存很少。


```python

```
