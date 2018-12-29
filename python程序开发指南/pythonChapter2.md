
# Python第二章学习

- [x] 标识符与关键字

- [x] Intergral类型

- [x] 浮点类型

- [x] 字符串

## 标识符与关键字
- 创建一个数据项时，我们或许将其赋值给一个变量，或者将其插入到一个组合中，为对象引用赋予的名称称为标识符，python标识符符合两个原则：         
1.只要是Unicode编码的字母，都可以充当引导字符，包括字母、下划线以及大多数非英文语言的字母。       
2.Python标识符不能与关键字同名。         


两条约定：       
- 第一条是不要使用python预定义的标识符对自定义的标识符进行命名，因此，要避免使用NotImplemented与Ellipsis，以及python内置数据类型（比如int、float、list、str与tuple）的名，也不要使用内置函数名与异常名作为标识符。

- 第二条约定：是关于下划线的使用，名的开头和结尾都使用下划线的情况应该避免使用，因为python定义了各种特殊方法与变量，使用的就是这样的名称。

## integral类型

- python提供了两种内置的Intergral类型，即int与bool。整数和布尔型值都是固定的，但是由于pyhton提供了增强的赋值操作符，使得这一约束极少导致实际问题。

### 整数
- 整数的大小只受限于机器的内存大小，默认情况下，整数采用的是十进制，但在方便的时候也可以使用其他进制：


```python
10#decimal
```




    10




```python
0b1010#binary
```




    10




```python
0o12#octal
```




    10




```python
0xa#hexadecimal
```




    10



所有常见的数学函数与操作符都可用于整数

使用数据类型创建对象时，有3种用例。      
- 第一种是不使用参数调用数据类型函数，在这种情况下，对象会被赋值为一个默认值，你如，x=int（）会创建一个值为0的整数，所有内置的数据类型都可以作为函数并不带任何参数进行调用

- 第二种情况是，使用一个参数调用数据类型函数，如果给定的参数是同样的数据类型，就会创建一个新对象，新对象是原始对象的一个浅拷贝，如果给定的参数不是同样的数据类型，就会尝试进行转换。如果给定的参数支持到给定数据类型的转换，但是转换失败，就会产生一个ValueError异常，否则返回给定类型对象。如果给定参数不知道给定数据类型的转换，就会产生一种TypeError异常

- 第三种情况是，给定两个或多个参数--但不是所有数据类型都支持，而对支持这一情况的数据类型，参数类型以及内涵都是变化的。对于int类型，允许给定两个参数，其中一个参数是一个表示整数的字符串，第二个参数则是字符串表示的base，如下例：


```python
int("A4",16)
```




    164



### 布尔值
- 有两个内置的布尔型对象：True与False，与所有其他的python数据类型相似，布尔数据类型也可以当做函数进行调用--不指定参数时将返回False，给定的是布尔型参数时，会返回该参数的一个拷贝，给定的是其他类型的参数时，则会尝试将其转换为布尔型值。下面给出了两个布尔型赋值操作以及两个布尔表达式：


```python
t = True
f = False
t and f
```




    False




```python
t and True
```




    True



## 浮点类型
- python提供了3种浮点值：内置的float与complex类型，以及来自标准库的decimal.Decimal类型，这3种数据类型都是固定的。

### 浮点数
- float数据类型可以作为函数调用--不指定参数时返回0.0，指定的是float型参数时返回该参数的一个拷贝，指定其他任意类型的参数时都尝试将其转换为float

下面给出一个简单函数，该函数用于比较floatS是否相等


```python
import sys
def equal_float(a,b):
    return abs(a - b)<= sys.float_info.epsilon
```

sys.float_info是一个对象，有很多属性，epsilon是机器可以区分出的两个浮点数的最小区别


```python
type(sys.float_info)
```




    sys.float_info




```python
help(sys.float_info)#显示sys.float_info对象的某些属性和方法功能
```

    Help on float_info object:
    
    class float_info(builtins.tuple)
     |  sys.float_info
     |  
     |  A structseq holding information about the float type. It contains low level
     |  information about the precision and internal representation. Please study
     |  your system's :file:`float.h` for more information.
     |  
     |  Method resolution order:
     |      float_info
     |      builtins.tuple
     |      builtins.object
     |  
     |  Methods defined here:
     |  
     |  __new__(*args, **kwargs) from builtins.type
     |      Create and return a new object.  See help(type) for accurate signature.
     |  
     |  __reduce__(...)
     |      helper for pickle
     |  
     |  __repr__(self, /)
     |      Return repr(self).
     |  
     |  ----------------------------------------------------------------------
     |  Data descriptors defined here:
     |  
     |  dig
     |      DBL_DIG -- digits
     |  
     |  epsilon
     |      DBL_EPSILON -- Difference between 1 and the next representable float
     |  
     |  mant_dig
     |      DBL_MANT_DIG -- mantissa digits
     |  
     |  max
     |      DBL_MAX -- maximum representable finite float
     |  
     |  max_10_exp
     |      DBL_MAX_10_EXP -- maximum int e such that 10**e is representable
     |  
     |  max_exp
     |      DBL_MAX_EXP -- maximum int e such that radix**(e-1) is representable
     |  
     |  min
     |      DBL_MIN -- Minimum positive normalizer float
     |  
     |  min_10_exp
     |      DBL_MIN_10_EXP -- minimum int e such that 10**e is a normalized
     |  
     |  min_exp
     |      DBL_MIN_EXP -- minimum int e such that radix**(e-1) is a normalized float
     |  
     |  radix
     |      FLT_RADIX -- radix of exponent
     |  
     |  rounds
     |      FLT_ROUNDS -- addition rounds
     |  
     |  ----------------------------------------------------------------------
     |  Data and other attributes defined here:
     |  
     |  n_fields = 11
     |  
     |  n_sequence_fields = 11
     |  
     |  n_unnamed_fields = 0
     |  
     |  ----------------------------------------------------------------------
     |  Methods inherited from builtins.tuple:
     |  
     |  __add__(self, value, /)
     |      Return self+value.
     |  
     |  __contains__(self, key, /)
     |      Return key in self.
     |  
     |  __eq__(self, value, /)
     |      Return self==value.
     |  
     |  __ge__(self, value, /)
     |      Return self>=value.
     |  
     |  __getattribute__(self, name, /)
     |      Return getattr(self, name).
     |  
     |  __getitem__(self, key, /)
     |      Return self[key].
     |  
     |  __getnewargs__(...)
     |  
     |  __gt__(self, value, /)
     |      Return self>value.
     |  
     |  __hash__(self, /)
     |      Return hash(self).
     |  
     |  __iter__(self, /)
     |      Implement iter(self).
     |  
     |  __le__(self, value, /)
     |      Return self<=value.
     |  
     |  __len__(self, /)
     |      Return len(self).
     |  
     |  __lt__(self, value, /)
     |      Return self<value.
     |  
     |  __mul__(self, value, /)
     |      Return self*value.n
     |  
     |  __ne__(self, value, /)
     |      Return self!=value.
     |  
     |  __rmul__(self, value, /)
     |      Return self*value.
     |  
     |  count(...)
     |      T.count(value) -> integer -- return number of occurrences of value
     |  
     |  index(...)
     |      T.index(value, [start, [stop]]) -> integer -- return first index of value.
     |      Raises ValueError if the value is not present.
    
    


```python
print(dir(sys.float_info))
```

    ['__add__', '__class__', '__contains__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__getnewargs__', '__gt__', '__hash__', '__init__', '__iter__', '__le__', '__len__', '__lt__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__rmul__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', 'count', 'dig', 'epsilon', 'index', 'mant_dig', 'max', 'max_10_exp', 'max_exp', 'min', 'min_10_exp', 'min_exp', 'n_fields', 'n_sequence_fields', 'n_unnamed_fields', 'radix', 'rounds']
    

使用int（）函数，可以将浮点数转换为整数--返回其整数部分，舍弃小数部分；使用round函数，该函数将对小说部分四舍五入；math.floor（）函数，或者math.ceil（）函数--该函数可以将浮点数转化为最近邻的整数。

如果浮点数的小数部分为0，float.is_interger()方法将返回True，浮点数的小数可以使用float.as_integer_ratio方法获取。

float.hex()方法，可以将浮点数以十六进制形式表示为字符串，相反的转换可以使用float.fromhex()实现


```python
x = 2.75
x.as_integer_ratio()
```




    (11, 4)




```python
s = 14.25.hex()
f = float.fromhex(s)
t = f.hex()
```

### 复数
- 复数这种数据类型是固定的，其中存放的是一对浮点数，一个是实数部分，另一个是虚数部分，两个部分都以属性名的形式存在，分别为real与imag

下面是如何创建一个复数对象：


```python
z = 23.0 + 23.2j#创建一个复数对象
z.real,z.imag
```




    (23.0, 23.2)




```python
z.conjugate()#共轭复数
```




    (23-23.2j)



### 十进制数字
- 在很多应用程序中使用浮点数时导致的数值不精确并没有很大的影响，在很多时候都要被浮点计算的速度优势所掩盖，但有些情况下，我们更需要完全的准确性，即使要付出速度降低的代价。decimal模块可以提供固定的十进制数，其精度可以自己指定。

要创建Decimal，必须先导入decimal模块，例如：


```python
import decimal
a = decimal.Decimal(9876)
b = decimal.Decimal("54321.012345678987654321")
a + b
```




    Decimal('64197.012345678987654321')



十进制数是使用decimal.Decimal()函数创建的，该函数可以接受一个整数或字符串作为参数--但不能以浮点数作为参数，因为浮点数不够准确，decimal泽很准确。

下面看一下浮点数与decimal.Decimal在精度上的差别：


```python
23/1.05
```




    21.904761904761905




```python
print(23/1.05)
```

    21.904761904761905
    


```python
print(decimal.Decimal(23)/decimal.Decimal("1.05"))
```

    21.90476190476190476190476190
    


```python
decimal.Decimal(23)/decimal.Decimal("1.05")
```




    Decimal('21.90476190476190476190476190')



## 字符串

- [x] 比较字符串

- [x] 字符串分片与步距

- [x] 字符串操作符与方法

- [x] 使用str.format()方法进行字符串格式化

- [ ] 字符编码            


- 字符串是使用固定不变的str数据类型表示的，其中存放Unicode字符序列。str数据类型可以作为函数进行调用，用于创建字符串对象--参数为空时返回一个空字符串，参数为非字符串类型时返回该参数的字符串形式，参数为字符串是返回该字符串的拷贝。       

- 前面我们注意到，字符串是使用引号创建的，可以使单引号，也可以是双引号，单字符串两顿必须相同，此外，我们还可以使用三引号包含的字符串。如：
   
```      
text="""A triple quoted string like this can include 'quotes' and "quotes""""     
      
```       
- python使用换行作为其语句终结符，但是如果在圆括号内、方括号内、花括号内或者三引号包含的字符串内侧则是例外，在三引号包含的字符串中，可以直接使用换行，而不需要进行格式化处理操作，通过使用\n转义序列，也可以在任何字符串中包含换行。          

- 如果我们需要写一个长字符串，跨越了2行或更多行，但是不使用三引号包含的字符串，那么有两种解决帮法      

```       
t = "this is not the best way to join two long strings"+\       
   "together since it relies on ugly newline escaping"       
s = ("this is not the best way to join two long strings"       
   "together since it relies on ugly newline escaping")  
   
```

上面第二种情况，我们必须使用圆括号将其包含在一起，构成一个单独的表达式，如果不使用圆括号，就只有第一个字符串s进行赋值，第二个字符串则会导致IndentantionError异常。

|    转义字符     |      含义      |
|:-------------------:|:-------------------:|
|    \newline    |      忽略换行     |
|    \\        |  反斜杠（\）        |
|    \'       |  单引号（‘）  |
|    \"        | 双引号（“）   |
|   \a         | ASCLL蜂鸣（BEL）   |
|   \b         | ASCLL退格（BS）   |
|    \f        |  ASCLL走纸（FF）  |
|    \n        |  ASCLL换行（LF）  |
|    \N{name}   |  给定名称的Unicode字符  |
|    \ooo     |  给定八进制的字符  |
|    \r       | ASCLL回车符（CR）   |
|    \t        | ASCLL制表符（TAB）   |
|    \uhhhh     | 给定16位十六进制的Unicode字符   |
|    \Uhhhhhhhhh  |  给定32位十六进制的Unicode字符  |
|    \v        |  ASCLL垂直指标（VT）  |
|    \xhh       |  给定8位十六进制的Unicode字符  |

### 定义字符串
 
定义字符串的三种方法

- str1 = 'hello world'
- str2 = "hello world"
- str3 = """hello world"""

看下面实例


```python
str1 = 'hello world'
type(str1)
```




    str




```python
str2 = "hello world"
type(str2)
```




    str



上面两种定义字符串的方法一样，没有区别，有区别的情况看下面的例子：


```python
say = 'let's go' 
```


      File "<ipython-input-30-b7831a02770c>", line 1
        say = 'let's go'
                   ^
    SyntaxError: invalid syntax
    



```python
say = "let's go"#这才是正确的定义方法
print(say)
```

    let's go
    

如果双引号里面还有双引号时，该怎么定义呢？这时候就需要加转义字符


```python
say = "let's \"go\""
print(say)
```

    let's "go"
    


```python
mail = 'tom: hello i am jack'
print (mail)
```

    tom: hello i am jack
    


```python
mail = 'tom:\n hello\n i am jack'
print(mail)
```

    tom:
     hello
     i am jack
    

上面例子中我们需要换行的时候，需要加转义字符\n，但是如果需要的转义字符多的时候就会容易弄混，所以我们可以用第三种定义字符串的方法。


```python
mail = """tom:
    i am jack
    goobye
"""
print(mail)
```

    tom:
        i am jack
        goobye
    
    


```python
mail#当我们使用三引号的时候就会把我们所做的操作给记录下来
```




    'tom:\n    i am jack\n    goobye\n'



### 比较字符串
- 字符串支持通常的比较操作符<、<=、==、！=、>、>=，这些操作符在内存中逐个字节对字符串进行比较

### 字符串分片与步距
- 序列中的单个数据项或者字符串中的单个字符，可以使用数据项存取操作符[]来提取


```python
a = 'abcde'
a[0]
```




    'a'




```python
a[0]+a[1]
```




    'ab'



我们首先从提取单个字符开始，字符串的索引位置从0开始，直至字符串长度减去1.但是使用负索引位置也是可能的----此时的计数方式是从最后一个字符到第一个字符。

分片操作符有三种语法格式：

- seq[start]
- seq[start:end]
- seq[start:end:step]

例子如下：


```python
a
```




    'abcde'




```python
a[1:3]#从零开始计数，从第一个开始去到第三个
```




    'bc'




```python
a[:4]#也可以省略start，这是从零个开始取
```




    'abcd'




```python
a[4:]#如果省略end，就是从start开始取，到结尾
```




    'e'




```python
a[::1]#从开头到结尾，一步一取step=1
```




    'abcde'



### 使用str.format()方法进行字符串格式化
- str.format()方法提供了非常灵活而强大的创建字符串的途径，此方法会返回一个新的字符串，在新字符串中，源字符串的替换字段被适当的格式化后的参数所替代。举个简单的例子


```python
x = "three"
s = "{0} {1} {2}"
s = s.format("the",x,"tops")
s
```




    'the three tops'



#### 字段名
- 字段名或者是一个与某个str.format()方法参数对应整数，或者是方法的某个关键字参数的名称。


```python
"{who} turned {age} this year".format(who = "She",age = "88")
```




    'She turned 88 this year'




```python
stock = ["paper","envelopes","notepads","pens"]
"we have {0[1]} and {0[2]} in stock".format(stock)#0引用的是位置参数

```




    'we have envelopes and notepads in stock'




```python
"{} {} {}".format("python","can","count")#从python3.1开始，忽略字段名成为可能，这种情况下，python会自动处理（使用从0开始的数值）

```




    'python can count'



- 当前还在作用范围内的局部变量可以通过内置的locals（）函数访问，该函数会返回一个字典，字典的键是局部变量名。字典的值则是对变量值的引用，现在，我们可以使用映射拆分将该字典提供给str.format()方法，映射拆分操作符为\*\*.


```python
element = "sliver"
number = 47
"Element {number} is {element}".format(**locals())
```




    'Element 47 is sliver'




```python

```
