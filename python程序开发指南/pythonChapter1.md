
# python第一章学习（补充）

## python的关键要素
Python的8个关键要素

- [x] 要素1：数据类型

- [x] 要素2：对象引用

- [x] 要素3：组合数据类型

- [x] 要素4：逻辑操作符

- [x] 要素5：控制流语句

- [x] 要素6：算术操作符

- [ ] 要素7：输入、输出

- [ ] 要素8：函数的创建与调用

### 数据类型
任何程序语言呢都必须能完成的基本任务是表示数据项，python提供了几种内置的数据类型，现在我们关注两种：int和str。

python所能表示的整数大小只受限于机器内存，而非固定数量的字数。

字符串可以使用双引号或者单引号封装--只要字符串头尾使用的而符号对称。

str类型与基本的数值类型（比如int）都是固定的。

如果需要将一个数据项从某种类型转换为另一种类型，可以使用语法datatype（item）。例如


```python
int("45")
```




    45




```python
str(912)
```




    '912'



### 对象引用
先看一个例子：      
x = "blue"     
y =  "green"    
z = x      
- 在上面的几条语句中，语法都会很简单的objectReference = value。这里不需要预先的声明语句，也没有必要指定值的类型。执行上面第一条语句是，python就会创建一个str对象，其文本是“blue”，同时创建了一个名为x的对象引用，x引用的就是这个str对象；第二条一样；第三条语句创建了一个名为z的新对象引用并将其设置为对象引用x所指向的相同对象。


- 用于对象引用的名称（标识符）有一些限制，尤其是不能与任何Python关键字相同，并且必须以字母或下划线引导，其后跟随0个或多个非空格字符、下划线或者数字。表示符没有长度限制

- python使用“动态类型”机制，也就是说，某个对象可以重新引用一个不同的对象（可以使不同的数据类型），但只允许与某种特定的数据类型绑定的操作。


```python
route = 866
print(route,type(route))
route = "North"
print(route,type(route))
```

    866 <class 'int'>
    North <class 'str'>


刚开始创建了一个route的对象引用，将其设置为引用一个新的int型数据866，这时候对于route，我们可以使用“/”,因为除法对整数而言是一个有效的操作符。之后我们重用了route这一对象引用，用它引用了一个str变量，int进入垃圾收集流程。如果此时在使用“/”,就会导致产生一个TypeError，因为对字符串而言，“/”不是一个有效的操作符。

### 组合数据类型
python提供了几种组合数据类型，我们讨论一下：元组和列表

python元组与列表可用于存储任意数量、任意类型的数据项。

元组是固定的，创建之后不能改变；列表是可变的，在需要的时候，可以插入或移除数据。


```python
# 元组用逗号创建
"denmark","finland","norway","sweden"
```




    ('denmark', 'finland', 'norway', 'sweden')




```python
"one",
```




    ('one',)




```python
#列表可以使用[]创建
x = ["zebra",49,-879,"aardvark",200]
#append()方法可以添加对象
x.append("more")
x
```




    ['zebra', 49, -879, 'aardvark', 200, 'more']



- 对象x知道自身是一个list（所有的python对象都知道自身的数据类型），因此不需要明确的指定数据类型。所以使用列表的append（）方法也可以完成同样的功能：


```python
list.append(x,"extra")
x
```




    ['zebra', 49, -879, 'aardvark', 200, 'more', 'extra']



- list类型还有很多其他的方法，包括insert（）方法，该方法用于在某给定的索引位置插入数据项；remove（）方法，该方法用于移除某给定索引位置上的数据项，python的索引总是以0开始的，列表本身也是一种序列，我们可以使用方括号操作符从字符串中获得某个字符，并且该操作符可用于任何序列，因此，可以对其进行如下操作：


```python
x[0]
```




    'zebra'




```python
x[4]
```




    200




```python
x[1] = "forty nine"
x
```




    ['zebra', 'forty nine', -879, 'aardvark', 200, 'more', 'extra']



### 逻辑操作符
任何一种程序设计语言的一个基本功能都是其逻辑运算，下面是python中的4组逻辑运算
#### 身份操作符
身份操作符，is操作符是一个二元操作符，如果左右两端同指一个对象，则返回true，is not是对身份测试的反向测试



```python
a = ["retention",3,None]
b = ["retention",3,None]
a is b
```




    False




```python
b = a
a is b
```




    True




```python
a = "something"
b = None
a is not None,b is None
```




    (True, True)



#### 比较操作符
比较操作符有<，<=，==，>=，>
这些操作符对对象值进行比较


```python
a = 2
b = 6
a == b

```




    False




```python
a < b
```




    True




```python
a <= b,a != b,a >= b,a > b
```




    (True, True, False, False)




```python
a = ["retention",3,None]
b = ["retention",3,None]
a is b
```




    False




```python
a == b#a和b虽为不同的对象，但具有相同的值，因此比较结果相同
```




    True



#### 成员操作符
我们可以用操作符in来测试成员关系，用not in来测试非成员关系


```python
p = (4,"frog",9,-33,9,2)
2 in p
```




    True




```python
"dog" not in p
```




    True



#### 逻辑操作符
python提供了3个逻辑运算符：and、or和not

### 控制流语句
- if语句
- while语句
- for...in语句     
在python中，一块代码，也就是说一条或多条语句组成的序列，称为suite，由于python中的某些语法要求存在suite，python就提供了关键字pass，pass实际上是一条空语句，不进行任何操作，可以用在需要suite但又不需要进行处理的地方。

#### if语句
python的常规if语句语法如下 
```
if boolean_expression1:     
    suite1     
elif boolean_expression2:       
    suite2           
...               
elif boolean_expressionN:              
    suiteN           
else:            
    else_suite  
```
与if语句对应可以有0个或者对个elif分支，最后的else分支是可选的，如果需要考虑某个特定的情况，但又不需要在这种情况发生时进行处理，那么可以使用pass作为该分支的suite

#### while语句
while语句用于0次或多次执行某个suite，循环执行的次数取决于while循环中布尔表达式的状态，下面是其语法格式：    
```
while boolean_expression:
    suite
```
while循环完整语法比上面的要复杂的多，因为其中还支持break与continue，还包括可选的else分支，break的作用是将控制流导向到break所在的内循环--也就是说跳出循环；continue语句的作用是将控制流导向到循环起始处，通常这两个都用在if语句内部。
```
while True:
    item = get_next_item()
    if not item:
        break
    process_item(item)
```

#### for...in语句
python的for循环语句重用了关键字in（在其上下文中，in是一个成员操作符），并使用如下的语法格式：    
```
for variable in iterable:
    suite
```
for也支持break与continue语句，也包含可选的else分支，variable将逐一引用iterable中的每个对象，iterable是可以迭代的任意数据类型，包括字符串、列表、元组以及python的其他组合数据类型


```python
for country in ["Denmark","Finland","Norway","Sweden"]:
    print(country)
```

    Denmark
    Finland
    Norway
    Sweden

```python
for letter in "ABCDEFGHIJKLMNOPQRSTUVWXYZ":
    if letter in "AEIOU":
        print(letter,"is a voowel")
    else:
        print(letter,"is a consonant")
```

    A is a voowel
    B is a consonant
    C is a consonant
    D is a consonant
    E is a voowel
    F is a consonant
    G is a consonant
    H is a consonant
    I is a voowel
    J is a consonant
    K is a consonant
    L is a consonant
    M is a consonant
    N is a consonant
    O is a voowel
    P is a consonant
    Q is a consonant
    R is a consonant
    S is a consonant
    T is a consonant
    U is a voowel
    V is a consonant
    W is a consonant
    X is a consonant
    Y is a consonant
    Z is a consonant


### 算术运算符
Python提供了完整的算术运算符集，包括用于基本四则运算的操作符+，-，\*，/。此外也可以使用一些增强的赋值操作符，如+=与\*=。在操作数都为整数时，以上操作符分别按正常的加，减，乘，除运算：


```python
5 + 6
```


    11


```python
3 * 8
```


    24


```python
12 / 4
```


    3.0


```python
a = 5
a += 8
a
```


    13



看到这里会看到python与一般程序语言不同的地方，除法操作符会产生一个浮点值，而不是一个整数值。

我们需要记住的一点是,int数据类型是固定的，一旦赋值就不能改变，上例中在执行a += 8时，python计算a + 8，将结果存储在新的int对象，之后将a重新绑定为引用这个新的int对象。

python重载了操作符+和+=，将其分别用于字符串与列表，前者表示连接，后者表示追加字符串并扩展列表


```python
name = "John"
name + "Doe"
```


    'JohnDoe'


```python
name += "Doe"
name
```


    'JohnDoeDoeDoe'


```python
seeds = ["sesame","sunflower"]
seeds += ["punpkin"]
seeds
```


    ['sesame', 'sunflower', 'punpkin']


```python
seeds += "durian"#添加一个普通的字符串
seeds
```


    ['sesame', 'sunflower', 'punpkin', 'd', 'u', 'r', 'i', 'a', 'n']

### 输入、输出
python 提供了内置的input（）函数，用于接收来自用户的输入，这一函数需要一个可选的字符串参数，之后等待用户输入响应信息或按enter来终止，如果用户不输入任何文本，而只是按Enter键，那么input（）函数会返回一个空字符串；否则会返回一个包含用户输入内容的字符串，而没有任何行终止符。


```python
print("Type intergers,each followed by Enter;or just Enter to finish")

total = 0
count = 0

while True:
    line = input("interger:")
    if line:
        try:
            number = int (line)
        except ValueError as err:
            print(err)
            continue
        total += number
        count +=1
    else:
        break

if count:
    print("count = ",count,"total = ",total,"mean = ",total/count)
```

```python
Type intergers,each followed by Enter;or just Enter to finish
interger:112
interger:7
interger:1x
invalid literal for int() with base 10: '1x'
interger:15
interger:5
interger:
count =  4 total =  139 mean =  34.75
```


#### 函数的创建与调用
创建函数的通常语法格式：
```python
def functionName(arguments):
    suite
```



