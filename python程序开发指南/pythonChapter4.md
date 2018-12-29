
# Python第四章

## 控制结构

- [x] if语句

- [x] while语句

- [x] for语句

- [x] 逻辑

- [x] 遍历序列及字典

- [x] 循环控制

- [x] 异常处理

### if语句
- if语句
    - python的if语句类似其他语言，if语句包含一个逻辑表达式，使用表达式比较，在比较的结果的基础上做出决定。
    - ifexpression：     
        statement（s）
>注：python使用缩进作为其语句分组的方法，建议使用4个空格代替缩进


```python
if 1 < 2:
    print("OK")#必须缩进，没有缩进就会出现IndentationError错误
print("OK!OK!")
```

    OK
    OK!OK!
    

- 逻辑值（bool）用来表示诸如：对于错，真与假，空与非空等概念
- 逻辑值包含了两个值：
    - True：表示非空的量（比如：string，tuple，list，set，dictonary等）所有非零数    
    - False：表示0，None，空的量等    
- 作用：主要用于判断语句中，用来判断
    - 一个字符串是否是空的    
    - 一个运算结果是否为零     
    - 一个表达式是否可用
    


```python
if 1 + 2:#非空的量
    print("OK")
print("OK!OK!")
```

    OK
    OK!OK!
    


```python
if 1 - 1:#0，None，空的量
    print("OK")
print("OK!OK!")
```

    OK!OK!
    


```python
#我们可以定义一个函数
def fun():
    return 1;
if fun():
    print("OK")
```

    OK
    

- else语句
```
    - if expression：     
       statement（s）    
     else：          
       statement(s)     
````
    - 如果在条件表达式if语句解析为0或false值。else语句是一个可选的语句，并最多只能有一个else语句


```python
def fun():
    return 1

if fun():
    print("OK")    
#print("#############")
else:
    print("bad")
```

    OK
    

- elif语句
```
    - if expression：     
        statement(s)     
     elif expression2:      
        statement(s)     
     elif expression2:     
        statement(s)     
     else:     
        statement(s)    
```
    - elif语句可以让你检查多个表达式为真值，并提供一个代码块，elif语句是可选的，可以有任意数量的elif。


```python
def fun():
    return 1

x = int(input("please input :"))
y = int(input("please input :"))

if x >= 90:
    if y >= 90:#if的嵌套
        print("A") 
    print("x >= 90")
#print("#############")
elif x >= 80:
    print("B")  
elif x >= 70:
    print("C")      
else:
    print("bad")
```

    please input :90
    please input :80
    x >= 90
    

- 使用and、or、not


```python
def fun():
    return 1

x = int(input("please input :"))
y = int(input("please input :"))

if x >= 90 and y >= 90:
    print("A") 
elif x >= 80:
    print("B")  
elif x >= 70:
    print("C")      
else:
    print("bad")
```

    please input :90
    please input :80
    B
    

### 逻辑运算符

- and 
- or
- not


```python
1 and 1
```




    1




```python
1 and 0
```




    0




```python
1 or 1
```




    1




```python
1 or 0
```




    1




```python
not 1
```




    False



### for循环
- 循环是一个结构，导致一个程序要重复一定次数
- 条件循环也是如此，当条件变为假时，循环结束

- for循环：
    - 在Python for循环遍历序列，如一个列表或一个字符
- for循环语法
```
for iterating_var in sequernce:
    statemnet(s)
```
>注：如果一个序列包含一个表达列表，它是第一个执行。然后该序列中的第一项赋值给迭代变量iterating_var。接下来，执行语句块，列表中的每个项目分配到iterating_var，代码块被执行，直到整个序列被耗尽。       
>格式遵循代码块缩进原则


```python
for x in "abcd":
    print(x,"hello world")
```

    a hello world
    b hello world
    c hello world
    d hello world
    


```python
for x in [1,2,3,4,5,6,7,]:
    print(x,"hello world")
```

    1 hello world
    2 hello world
    3 hello world
    4 hello world
    5 hello world
    6 hello world
    7 hello world
    

- 迭代序列指数（索引）
    - 遍历每个项目的另一种方法是由序列本身的便宜指数（索引）： 
- range函数
    - 循环结构是用于迭代多个项的for语句，迭代形式可以循环序列的所有成员。    
- range(i,j,[,步进值])     
    - 如果所创建的对象为整数，可以用range     
    - i为初始数值，      
    - j为终止数值，但不包括在范围内，步进值为可选参数，不选的话默认为1，     
    - i不选的话默认为0     


```python
range(10)
```




    range(0, 10)




```python
print(range(100))
```

    range(0, 100)
    


```python
for x in range(10):
    print(x,"hello world")
```

    0 hello world
    1 hello world
    2 hello world
    3 hello world
    4 hello world
    5 hello world
    6 hello world
    7 hello world
    8 hello world
    9 hello world
    


```python
for x in range(1,10):
    print(x,"hello world")
```

    1 hello world
    2 hello world
    3 hello world
    4 hello world
    5 hello world
    6 hello world
    7 hello world
    8 hello world
    9 hello world
    


```python
for x in range(1,10,2):
    print(x,"hello world")
```

    1 hello world
    3 hello world
    5 hello world
    7 hello world
    9 hello world
    


```python
L = ['Bart', 'Lisa', 'Adam']
for x in range(len(L)):
    print("hello",L[x])
```

    hello Bart
    hello Lisa
    hello Adam
    

### 遍历



```python
for x in "hello":#正常的遍历方法,直接从序列取值
    print(x)
```

    h
    e
    l
    l
    o
    


```python
s = "hello"#从序列本身偏移指数取值
l = [1,2,3,'a','b']
t = (7,8,9,'x','y')

for x in range(len(l)):
    print(l[x])
```

    1
    2
    3
    a
    b
    

- 遍历字典


```python
d = {1:11,2:22,5:555,3:333}

for x in d:#遍历的是字典中的key
    print(x)

print(d.items())

for k,v in d.items():
    print(k)
    print(v)
```

    1
    2
    3
    5
    dict_items([(1, 11), (2, 22), (3, 333), (5, 555)])
    1
    11
    2
    22
    3
    333
    5
    555
    

### 循环控制


```python
d = {1:11,2:22,5:555,3:333}

for x in d:#遍历的是字典中的key
    print(x)
else:
    print("ending")

for k,v in d.items():
    print(k)
    print(v)
else:
    print("ending")
```

    1
    2
    3
    5
    ending
    1
    11
    2
    22
    3
    333
    5
    555
    ending
    

当非正常结束时else不会执行，正常运行时循环结束时else执行


```python
import time
for x in range(3):#遍历的是字典中的key
    print(x)
    time.sleep(1)
else:
    print("ending")
```

    0
    1
    2
    ending
    


```python
import time
for x in range(1,10):
    print(x)
    if x == 1:
        pass
    if x == 2:
        continue #当执行到x = 2时跳出本次循环
        print("hello")
    if x == 6:
        break #终止循环
else:
    print("ending")#程序非正常结束，不执行这一句
    
print("------------") 

for x in range(1,10):
    print(x)
```

    1
    2
    3
    4
    5
    6
    ------------
    1
    2
    3
    4
    5
    6
    7
    8
    9
    

### while循环
- while循环，直到表达式变为假，表达的是一个逻辑表达式，必须返回一个true或false值
- 语法：
```
while expression:
    statement(s)
```
>注：遵循代码块缩进原则


```python
while True:
    print("hello")
    x = input("please input:")
    if x == "q":
        break
```

    hello
    please input:we
    hello
    please input:we
    hello
    please input:e
    hello
    please input:q
    


```python
x = ""
while x != 'q':#如果x=“q”终止循环
    print("hello")
    x = input("please input:")
    if not x :
        break
```

    hello
    please input:
    

while和for循环一样，也可以使用else语句，当正常结束时，执行else语句，如果非正常结束，则不执行else语句。

### 异常处理
- Python通过产生异常来指明发生错误或异常条件

- 异常的捕获是使用try...except块实现的，其通常语法格式如下：
```
try:
    try_suite
except exception_group1 as variable1:
    except_suite1
...
except exception_groupN as variableN:
    except_suiteN
else:
    else_suite
finally:
    finally_suite
```
- 其中至少要包含一个except块，但是else和finally块都是可选的，在try块的suite正常执行完毕时，会执行else块的suite——如果发生异常，就不会执行。如果存在一个finally块，则最后总会执行。
- 每个except分支的异常组可以是一个单独的异常，也可以是包含在括号中的异常元组，对每个异常组，as variable部分是可选的，如果使用，该变量就会包含发生的异常，并且可以在异常块的suite中进行存取。
- 如果某个异常发生在try块的suite中，那么每个except分支会顺序尝试执行。如果该异常与某个异常组匹配，则相应的suite得以执行。


```python
#下面给出一个不正确使用的实例
d = {1:111,2:222,3:333,4:444}
try:
    x = d[5]
except LookupError:
    print("Lookup error occurred")
except KeyError:
    print("Invalid key used")
```

    Lookup error occurred
    

- 如果字典d不包含key为5的数据项，那么我们希望产生最具针对性的异常KeyError，而不是通常的LookupError，但是这里KeyError块代码总是无法执行到，如果产生KeyError异常，就会与LookupError except块匹配，因为LookupError是keyError的一个基类，也就是说，在异常体系中LookupError要高于KeyError，因此，在使用多个except块时，我们必须坚持对其排序，从最具针对性的异常到最通常的异常。

- 如果没有异常产生，那么任意可选的else块都将执行，在所有情况下——也就是说，如果没有发生异常，或者发生异常被处理，或发生异常并回溯到调用栈——任意finally块的suite总是会得以执行。如果没有异常产生，或产生的异常被某个except块处理，那么finally块的suite将在最后执行，如果异常产生，但是没有匹配的except块，就首先执行finally块的suite，之后将该异常在调用栈中回溯，在需要确保资源被正确释放是，这种执行机制是很有用的。

#### 产生异常
- 异常提供了一种改变控制流的有用方法，我们可以使用内置的异常，或创建自己的异常，以便我们所需要的异常并对其进行处理。有两种产生异常的语法：
```
raise exception(args)
raise exception(args) from original_exception
raise
```

- 使用第一种语法是，指定的异常应该或者是内置的异常，或者继承exception的自定义异常，如果给定一些文本作为该异常的参数，那么在捕捉到该异常并打印时，这些文本应该为输出信息。
- 使用第二种语法，也就是没有指定异常时，raise将重新产生当前活跃的异常——如果当前没有，就会产生一个TypeError

#### 自定义异常
- 自定义异常是自定义的数据类型（类），基本的语法：
```
class exceptionName(baseException):pass
```
基类应该为Exception类或继承自Exception的类。

- 自定义异常的一个用途是跳出深层嵌套的循环，比如，如果某个表格对象存放记录（行），每个记录有很多字段（列），每个字段有很多值（项），我们可以使用类似于下面的代码搜索某个特定的值：


```python
found = False
for row,record in enumerate(table):
    for column,field in enumerate(record):
        for index,item in enumerate(field):
            if item == target:
                found == True
                break
        if found:
            break
    if found:
        break
if found:
    print("found at ({0},{1},{2})".format(row,column,index))
else:
    print("not found")
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-7-85576999eea0> in <module>()
          1 found = False
    ----> 2 for row,record in enumerate(table):
          3     for column,field in enumerate(record):
          4         for index,item in enumerate(field):
          5             if item == target:
    

    NameError: name 'table' is not defined



```python
#上面的代码看起来很复杂，下面我们用一个自定义异常来解决
class exceptionName(Exception):
    pass

found = False
for row,record in enumerate(table):
    for column,field in enumerate(record):
        for index,item in enumerate(field):
            if item == target:
                rasie exceptionName()
except FoundException:   
    print("found at ({0},{1},{2})".format(row,column,index))
else:
    print("not found")
```


      File "<ipython-input-3-6be8bbdc18e1>", line 8
        rasie exceptionName()
                          ^
    SyntaxError: invalid syntax
    



```python

```
