
# Python第十章学习

- [x] 错误与异常
    - [x] 语法错误 
    - [x] 异常
    - [x] 处理异常
    - [x] 引发异常
    - [x] 用户自定义异常
    - [x] 定义清理操作
- [x] 调试
- [x] 测试

## 语法错误
- Python中有两种错误很容易区分：
    - 语法错误
    - 异常
- 语法错误，或称为解析错误


```python
while True print("hello world")
```


      File "<ipython-input-1-69f99b8c51fb>", line 1
        while True print("hello world")
                       ^
    SyntaxError: invalid syntax
    


语法分析器，指出了出错的一行，并且找到了错误的位置，有一个小小的标记，错误就是在标记前引起的，上面的错误是因为print()之前缺少一个冒号。

## 异常
- 即使一条语句或表达式在语法上是正确的，在运行的时候也有可能发生错误。在运行期间检测到的错误被称为异常并且程序不会崩溃

- 大多数的异常都不会被程序处理，导致产生下面类似的信息


```python
"2" + 2
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-2-5dee648c75c4> in <module>()
    ----> 1 "2" + 2
    

    TypeError: Can't convert 'int' object to str implicitly


最后一行给出了异常的详细信息和引起异常的原因

内置的异常列出了内置的异常以及它们的含义

## 处理异常

- 我们可以通过编程来处理部分异常。

下面一个例子是，会一直要求用户输入直到输入一个合法的整数为止


```python
while True:
    try:
        x = int(input("Please enter a number: "))
        break
    except ValueError:
        print("Oops!  That was no valid number.  Try again...")
```

Try语句按以下方式工作。

- 首先，执行try 子句。
- 如果没发生任何异常，忽略except子句且try语句执行完毕。
- 如果在try 子句执行过程中发生异常，跳过该子句的其余部分。如果异常的类型与except关键字后面的异常名匹配, 则执行 except 子句，然后继续执行try语句之后的代码。
- 如果异常的类型与 except 关键字后面的异常名不匹配，它将被传递给上层的try语句；如果没有找到处理这个异常的代码，它就成为一个未处理异常，程序会终止运行并显示一条如上所示的信息。

所以try语句可能有多个子句，以指定不同的异常处理处理程序:
```
try:
    pass
except RuntimeError:
    pass
except TypeError:
    pass
    ...
```

一个except子句可以用带括号的元组列出多个异常的名字：
```
try:
    pass
except(RuntimeError,TypeError,NameError):
    pass
```




```python
import sys

try:
    f = open('myfile.txt')
    s = f.readline()
    i = int(s.strip())
except OSError as err:
    print("OS error: {0}".format(err))
except ValueError:
    print("Could not convert data to an integer.")
except:
    print("Unexpected error:", sys.exc_info()[0])
    raise
```

    Could not convert data to an integer.
    

try...except语句有一个可选的else 子句，其出现时，必须放在所有 except 子句的后面。如果需要在 try 语句没有抛出异常时执行一些代码，可以使用这个子句。例如：


```python
for arg in sys.argv[1:]:
    try:
        f = open(arg, 'r')
    except IOError:
        print('cannot open', arg)
    else:
        print(arg, 'has', len(f.readlines()), 'lines')
        f.close()
```

    cannot open -f
    C:\Users\lovelive\AppData\Roaming\jupyter\runtime\kernel-d009252e-8284-43c0-ae14-42a44325b5bb.json has 12 lines
    

- 当异常发生时，它可能带有相关数据，也称为异常的参数。参数的有无和类型取决于异常的类型。

- except 子句可以在异常名之后指定一个变量。这个变量将绑定于一个异常实例，同时异常的参数将存放在实例的args中。为方便起见，异常实例定义了`__str__()` ，因此异常的参数可以直接打印而不必引用.args。也可以在引发异常之前先实例化一个异常，然后向它添加任何想要的属性。


```python
>>> try:
...    raise Exception('spam', 'eggs')
... except Exception as inst:
...    print(type(inst))    # the exception instance
...    print(inst.args)     # arguments stored in .args
...    print(inst)          # __str__ allows args to be printed directly,
...                         # but may be overridden in exception subclasses
...    x, y = inst.args     # unpack args
...    print('x =', x)
...    print('y =', y)
...
```

    <class 'Exception'>
    ('spam', 'eggs')
    ('spam', 'eggs')
    x = spam
    y = eggs
    

对于未处理的异常，如果它含有参数，那么参数会作为异常信息的最后一部分打印出来

异常处理程序不仅仅直接处理发生在try子句中的异常，而且还处理try子句中调用函数引发的异常。



```python
def this_fails():
    x = 1/0
    
try:
    this_fails()
except ZeroDivisionError as err:
    print("Handing run-time error:",err)
```

    Handing run-time error: division by zero
    

## 引发异常
- raise语句允许程序员强行引发一个指定的异常


```python
raise NameError("HiThere")
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-3-ff90742d1854> in <module>()
    ----> 1 raise NameError("HiThere")
    

    NameError: HiThere


raise的唯一参数指示要引发的异常，他必须是一个异常实例或异常类（从Exception派生的类）

如果确定要引发异常，但不打算处理它，一个简单形式的raise语句允许重新引发异常


```python
try:
    raise NameError("HiThere")
except NameError:
    print("A exception flew by!")
    raise
```

    A exception flew by!
    


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-4-794729ea0079> in <module>()
          1 try:
    ----> 2     raise NameError("HiThere")
          3 except NameError:
          4     print("A exception flew by!")
          5     raise
    

    NameError: HiThere


## 用户自定义的异常
- 程序可以通过创建新的异常类来命名自己的异常。异常通常是应该继承Exception类，直接继承或间接继承都可以


```python
class MyError(Exception):
    def __init__(self,value):
        self.value = value
    def __str__(self):
        return repr(self.value)
    
try:
    raise MyError(2*2)
except MyError as e:
    print("My exception occurred,value:",e.value)
```

    My exception occurred,value: 4
    


```python
raise MyError("oops!")
```


    ---------------------------------------------------------------------------

    MyError                                   Traceback (most recent call last)

    <ipython-input-7-722549cbd961> in <module>()
    ----> 1 raise MyError("oops!")
    

    MyError: 'oops!'



```python
#help(Exception) 
```

在这个示例中，Exception默认的`__init__()`被覆盖了，新的行为，简单的创建了value属性。这将替换默认的创建args属性的行为

## 定义清理操作
- try语句有另外一个可选的子句，目的在于定义必须在所有情况下执行的清理操作：


```python
try:
    raise NameError("HiThere")
finally:
    print("Goodbye,world!")
```

    Goodbye,world!
    


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-15-b60db5c5f7ea> in <module>()
          1 try:
    ----> 2     raise NameError("HiThere")
          3 finally:
          4     print("Goodbye,world!")
    

    NameError: HiThere


不管有没有发生异常，在离开try语句之前总是会执行finally子句，当try子句中发生一个异常，并且没有except处理，在执行finally子句后将重新引发这个异常，如果有except处理，则先执行except子句


```python
#定义一个函数
def divide(x,y):
    try:
        result = x/y
    except ZeroDivisionError:
        print("division by zero!")
    else:
        print("result is ",result)
    finally:
        print("executing finally clause")
```


```python
divide(2,1)
```

    result is  2.0
    executing finally clause
    


```python
divide(2,0)
```

    division by zero!
    executing finally clause
    


```python
divide("2","1")
```

    executing finally clause
    


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-20-da42c9ab7899> in <module>()
    ----> 1 divide("2","1")
    

    <ipython-input-16-67da972937b0> in divide(x, y)
          2 def divide(x,y):
          3     try:
    ----> 4         result = x/y
          5     except ZeroDivisionError:
          6         print("division by zero!")
    

    TypeError: unsupported operand type(s) for /: 'str' and 'str'


## 调试
- 程序能一次写完并正常运行的概率很小，基本不超过1%。总会有各种各样的bug需要修正。有的bug很简单，看看错误信息就知道，有的bug很复杂，我们需要知道出错时，哪些变量的值是正确的，哪些变量的值是错误的，因此，需要一整套调试程序的手段来修复bug。


**第一种方法简单直接粗暴有效，就是用print()把可能有问题的变量打印出来看看：**


```python
def foo(s):
    n = int(s)
    print('>>> n = %d' % n)
    return 10 / n

def main():
    foo('0')

main()
```

**第二种方法是断言（assert），print()的部分用assert代替**


```python
def foo(s):
    n = int(s)
    assert n != 0, 'n is zero!'
    return 10 / n

def main():
    foo('0')
    
main()
```

**第三种方法就是启动Python的调试器pdb，让程序以单步方式运行，可以随时查看运行状态**

- 这个方式要在交互模式下进行
- 使用命令`python -m pdb ****.py`打开文件,进入pdb
- 然后输入命令n，单行执行程序，有错误的会提示错误
- 输入命令q退出

**pdb.set_trace()**

- 这个方法也是用pdb，但是不需要单步执行，我们只需要import pdb，然后，在可能出错的地方放一个pdb.set_trace()，就可以设置一个断点：
- 运行代码，程序会自动在pdb.set_trace()暂停并进入pdb调试环境，可以用命令p查看变量，或者用命令c继续运行：


```python
import pdb

s = '0'
n = int(s)
pdb.set_trace()
print(10 / n)
```

## 测试
### 单元测试
- 单元测试是用来对一个模块、一个函数或者一个类来进行正确性检验的测试工作。

比如对函数abs()，我们可以编写出以下几个测试用例：

- 输入正数，比如1、1.2、0.99，期待返回值与输入相同；

- 输入负数，比如-1、-1.2、-0.99，期待返回值与输入相反；

- 输入0，期待返回0；

- 输入非数值类型，比如None、[]、{}，期待抛出TypeError。

把上面的测试用例放到一个测试模块里，就是一个完整的单元测试。

如果单元测试通过，说明我们测试的这个函数能够正常工作。如果单元测试不通过，要么函数有bug，要么测试条件输入不正确，总之，需要修复使单元测试能够通过。

单元测试通过后有什么意义呢？如果我们对abs()函数代码做了修改，只需要再跑一遍单元测试，如果通过，说明我们的修改不会对abs()函数原有的行为造成影响，如果测试不通过，说明我们的修改与原有行为不一致，要么修改代码，要么修改测试。



*我们先编写一个类Dict*     mydict.py
```mydict.py
class Dict(dict):

    def __init__(self, **kw):
        super().__init__(**kw)

    def __getattr__(self, key):
        try:
            return self[key]
        except KeyError:
            raise AttributeError(r"'Dict' object has no attribute '%s'" % key)

    def __setattr__(self, key, value):
        self[key] = value
        
```

为了编写单元测试，我们需要引入Python自带的unittest模块，编写mydict_test.py如下：

```mydict_test.py
import unittest

class TestDict(unittest.TestCase):

    def test_init(self):
        d = Dict(a=1, b='test')
        self.assertEqual(d.a, 1)
        self.assertEqual(d.b, 'test')
        self.assertTrue(isinstance(d, dict))

    def test_key(self):
        d = Dict()
        d['key'] = 'value'
        self.assertEqual(d.key, 'value')

    def test_attr(self):
        d = Dict()
        d.key = 'value'
        self.assertTrue('key' in d)
        self.assertEqual(d['key'], 'value')

    def test_keyerror(self):
        d = Dict()
        with self.assertRaises(KeyError):
            value = d['empty']

    def test_attrerror(self):
        d = Dict()
        with self.assertRaises(AttributeError):
            value = d.empty

if __name__ == '__main__':
    unittest.main()
    
```

编写单元程序时，我们需要编写一个测试类，从unittest.Testcase继承

以test开头的方法就是测试方法，不以test开头的方法不被认为是测试方法，测试的时候不会被执行。

对每一类测试都需要编写一个test_xxx()方法。由于unittest.TestCase提供了很多内置的条件判断，我们只需要调用这些方法就可以断言输出是否是我们所期望的。最常用的断言就是assertEqual()：
```python
self.assertEqual(abs(-1), 1) # 断言函数返回的结果与1相等
```

另一种重要的断言就是期待抛出指定类型的Error，比如通过d['empty']访问不存在的key时，断言会抛出KeyError：
```python
with self.assertRaises(KeyError):
    value = d['empty']
```   
而通过d.empty访问不存在的key时，我们期待抛出AttributeError：
```python
with self.assertRaises(AttributeError):
    value = d.empty
    
```

一旦编写好单元测试，我们就可以运行单元测试。最简单的运行方式是在mydict_test.py的最后加上两行代码：
```python
if __name__ == '__main__':
    unittest.main()
```

然后在脚本里运行
```python
python mydict_test.py
```

### 文档测试
- 我们在读python文档的时候，可以看到很多的文档都有示例代码。可以把这些示例代码在python的交互式环境下输入并执行，结果与文档中的实例代码显示的一致。

- 这些代码与其说明可以写在注释中，然后，有一些工具来自动生成文档，既然这些代码本身就可以粘贴出来直接运行，那么可不可以直接执行写在注释里面的代码呢？

如下例，当我们编写注释的时候，如果写上这样的注释：


```python
def abs(n):
    '''
    Function to get absolute value of number.

    Example:

    >>> abs(1)
    1
    >>> abs(-1)
    1
    >>> abs(0)
    0
    '''
    if n >= 0:
        return n 
    else: 
        return -n
if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

Python内置的“文档测试”（doctest）模块可以直接提取注释中的代码并执行测试。

doctest严格按照Python交互式命令行的输入和输出来判断测试结果是否正确。只有测试异常的时候，可以用...表示中间一大段烦人的输出。

注意到最后3行代码。当模块正常导入时，doctest不会被执行。只有在命令行直接运行时，才执行doctest。所以，不必担心doctest会在非测试环境下执行。


```python
def abs(n):
    '''
    Function to get absolute value of number.

    Example:

    >>> abs(1)
    1
    >>> abs(-1)
    1
    >>> abs(0)
    0
    '''
    if n >= 0:
        return n 
if __name__=='__main__':
    import doctest
    doctest.testmod()
```

    **********************************************************************
    File "__main__", line 9, in __main__.abs
    Failed example:
        abs(-1)
    Expected:
        1
    Got nothing
    **********************************************************************
    1 items had failures:
       1 of   3 in __main__.abs
    ***Test Failed*** 1 failures.
    


```python

```
