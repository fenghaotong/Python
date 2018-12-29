
#  Python第八章学习

- [x] open函数
- [x] 文件对象方法
    - [x] 读取文本文件
    - [x] 写入文本文件
- [x] 二进制文件
- [x] 非文件来源的流对象
- [x] 标准输入、输出和错误

## open()函数
- 我们使用open()函数来返回文件对象和打开文件


```python
help(open)
```

    Help on built-in function open in module io:
    
    open(file, mode='r', buffering=-1, encoding=None, errors=None, newline=None, closefd=True, opener=None)
        Open file and return a stream.  Raise IOError upon failure.
        
        file is either a text or byte string giving the name (and the path
        if the file isn't in the current working directory) of the file to
        be opened or an integer file descriptor of the file to be
        wrapped. (If a file descriptor is given, it is closed when the
        returned I/O object is closed, unless closefd is set to False.)
        
        mode is an optional string that specifies the mode in which the file
        is opened. It defaults to 'r' which means open for reading in text
        mode.  Other common values are 'w' for writing (truncating the file if
        it already exists), 'x' for creating and writing to a new file, and
        'a' for appending (which on some Unix systems, means that all writes
        append to the end of the file regardless of the current seek position).
        In text mode, if encoding is not specified the encoding used is platform
        dependent: locale.getpreferredencoding(False) is called to get the
        current locale encoding. (For reading and writing raw bytes use binary
        mode and leave encoding unspecified.) The available modes are:
        
        ========= ===============================================================
        Character Meaning
        --------- ---------------------------------------------------------------
        'r'       open for reading (default)
        'w'       open for writing, truncating the file first
        'x'       create a new file and open it for writing
        'a'       open for writing, appending to the end of the file if it exists
        'b'       binary mode
        't'       text mode (default)
        '+'       open a disk file for updating (reading and writing)
        'U'       universal newline mode (deprecated)
        ========= ===============================================================
        
        The default mode is 'rt' (open for reading text). For binary random
        access, the mode 'w+b' opens and truncates the file to 0 bytes, while
        'r+b' opens the file without truncation. The 'x' mode implies 'w' and
        raises an `FileExistsError` if the file already exists.
        
        Python distinguishes between files opened in binary and text modes,
        even when the underlying operating system doesn't. Files opened in
        binary mode (appending 'b' to the mode argument) return contents as
        bytes objects without any decoding. In text mode (the default, or when
        't' is appended to the mode argument), the contents of the file are
        returned as strings, the bytes having been first decoded using a
        platform-dependent encoding or using the specified encoding if given.
        
        'U' mode is deprecated and will raise an exception in future versions
        of Python.  It has no effect in Python 3.  Use newline to control
        universal newlines mode.
        
        buffering is an optional integer used to set the buffering policy.
        Pass 0 to switch buffering off (only allowed in binary mode), 1 to select
        line buffering (only usable in text mode), and an integer > 1 to indicate
        the size of a fixed-size chunk buffer.  When no buffering argument is
        given, the default buffering policy works as follows:
        
        * Binary files are buffered in fixed-size chunks; the size of the buffer
          is chosen using a heuristic trying to determine the underlying device's
          "block size" and falling back on `io.DEFAULT_BUFFER_SIZE`.
          On many systems, the buffer will typically be 4096 or 8192 bytes long.
        
        * "Interactive" text files (files for which isatty() returns True)
          use line buffering.  Other text files use the policy described above
          for binary files.
        
        encoding is the name of the encoding used to decode or encode the
        file. This should only be used in text mode. The default encoding is
        platform dependent, but any encoding supported by Python can be
        passed.  See the codecs module for the list of supported encodings.
        
        errors is an optional string that specifies how encoding errors are to
        be handled---this argument should not be used in binary mode. Pass
        'strict' to raise a ValueError exception if there is an encoding error
        (the default of None has the same effect), or pass 'ignore' to ignore
        errors. (Note that ignoring encoding errors can lead to data loss.)
        See the documentation for codecs.register or run 'help(codecs.Codec)'
        for a list of the permitted encoding error strings.
        
        newline controls how universal newlines works (it only applies to text
        mode). It can be None, '', '\n', '\r', and '\r\n'.  It works as
        follows:
        
        * On input, if newline is None, universal newlines mode is
          enabled. Lines in the input can end in '\n', '\r', or '\r\n', and
          these are translated into '\n' before being returned to the
          caller. If it is '', universal newline mode is enabled, but line
          endings are returned to the caller untranslated. If it has any of
          the other legal values, input lines are only terminated by the given
          string, and the line ending is returned to the caller untranslated.
        
        * On output, if newline is None, any '\n' characters written are
          translated to the system default line separator, os.linesep. If
          newline is '' or '\n', no translation takes place. If newline is any
          of the other legal values, any '\n' characters written are translated
          to the given string.
        
        If closefd is False, the underlying file descriptor will be kept open
        when the file is closed. This does not work when a file name is given
        and must be True in that case.
        
        A custom opener can be used by passing a callable as *opener*. The
        underlying file descriptor for the file object is then obtained by
        calling *opener* with (*file*, *flags*). *opener* must return an open
        file descriptor (passing os.open as *opener* results in functionality
        similar to passing None).
        
        open() returns a file object whose type depends on the mode, and
        through which the standard file operations such as reading and writing
        are performed. When open() is used to open a file in a text mode ('w',
        'r', 'wt', 'rt', etc.), it returns a TextIOWrapper. When used to open
        a file in a binary mode, the returned class varies: in read binary
        mode, it returns a BufferedReader; in write binary and append binary
        modes, it returns a BufferedWriter, and in read/write mode, it returns
        a BufferedRandom.
        
        It is also possible to use a string or bytearray as a file for both
        reading and writing. For strings StringIO can be used like a file
        opened in a text mode, and for bytes a BytesIO can be used like a file
        opened in a binary mode.
    
    

我们可以看到，open()函数的参数列表，第一个参数是文件名称，当问价不存在时就用到了第二个参数，第二个参数是文件的打开模式，后面的参数不予讨论，下面是文件的打开模式列表

|打开模式|执行操作|
|:-----:|:-------|
|r|以只读方式打开文件（默认）|
|w|以写入的方式打开文件，会覆盖已存在的文件|
|x|如果文件已经存在，使用此模式打开将引发异常|
|a|以写入模式打开，如果文件存在，则在末尾追加写入|
|b|以二进制模式打开文件|
|t|以文本模式打开文件（默认）|
|+|可读写模式（可添加到其他模式中使用）|
|U|通用换行符支持|


```python
open("myfile.txt",encoding = "utf-8")
```




    <_io.TextIOWrapper name='myfile.txt' mode='r' encoding='utf-8'>



- 关于这个文件名，有五件值得一讲的事情：
    - 它不仅是一个文件的名字；实际上，它是文件路径和文件名的组合；一般来说，文件打开函数应该有两个参数 — 路径和文件名 — 但是函数open()只使用一个参数。在Python里，当你使用“filename,”作为参数的时候，你可以将部分或者全部的路径也包括进去。
    - 在这个例子中，目录路径中使用的是斜杠(forward slash)，Windows使用反斜杠来表示子目录，但是Mac OS X和Linux使用斜杠。但是，在Python中，斜杠永远都是正确的，即使是在Windows环境下。
    - 不使用斜杠或者反斜杠的路径被称作相对路径(relative path)。
    - “filename,”参数是一个字符串。所有现代的操作系统（甚至Windows！）使用Unicode编码方式来存储文件名和目录名。Python 3全面支持非ascii编码的路径。
    - 文件不一定需要在本地磁盘上。也许你挂载了一个网络驱动器。它也可以是一个完全虚拟的文件系统(an entirely virtual filesystem)上的文件。只要你的操作系统认为它是一个文件，并且能够以文件的方式访问，那么，Python就能打开它。
    >但是对open()函数的调用不局限于filename。还有另外一个叫做encoding参数。

## 文件对象方法

我们应该怎么样去打开文件呢？下面是对应的文件对象方法：


```python
%%html
<tbody>
<tr>
    <td><strong> 文件对象方法</strong></td>
    <td><strong> 执行操作</strong></td>
</tr>
<tr>
    <td> f.close()</td>
    <td> 关闭文件</td>
</tr>
<tr>
    <td> f.read([size=-1])</td>
    <td> 从文件读取size个字符，当未给定size或给定负值的时候，读取剩余的所有字符，然后作为字符串返回</td>
</tr>
<tr>
    <td> f.readline([size=-1])</td>
    <td>从文件中读取并返回一行（包括行结束符），如果有size有定义则返回size个字符</td>
</tr>
<tr>
    <td> f.write(str)</td>
    <td> 将字符串str写入文件</td>
</tr>
<tr>
    <td> f.writelines(seq)</td>
    <td> 向文件写入字符串序列seq，seq应该是一个返回字符串的可迭代对象<br></td>
</tr>
<tr>
    <td> f.seek(offset, from)</td>
    <td> 在文件中移动文件指针，从from（0代表文件起始位置，1代表当前位置，2代表文件末尾）偏移offset个字节</td>
</tr>
<tr>
    <td> f.tell()</td>
    <td> 返回当前在文件中的位置</td>
</tr>
<tr>
    <td> f.truncate([size=file.tell()])</td>
    <td> 截取文件到size个字节，默认是截取到文件指针当前位置</td>
</tr>
</tbody>
```


<tbody><tr><td><strong> 文件对象方法</strong></td><td><strong> 执行操作</strong></td></tr><tr><td> f.close()</td><td> 关闭文件</td></tr><tr><td> f.read([size=-1])</td><td> 从文件读取size个字符，当未给定size或给定负值的时候，读取剩余的所有字符，然后作为字符串返回</td></tr><tr><td> f.readline([size=-1])</td><td>从文件中读取并返回一行（包括行结束符），如果有size有定义则返回size个字符</td></tr><tr><td> f.write(str)</td><td> 将字符串str写入文件</td></tr><tr><td> f.writelines(seq)</td><td> 向文件写入字符串序列seq，seq应该是一个返回字符串的可迭代对象<br>
</td></tr><tr><td> f.seek(offset, from)</td><td> 在文件中移动文件指针，从from（0代表文件起始位置，1代表当前位置，2代表文件末尾）偏移offset个字节</td></tr><tr><td> f.tell()</td><td> 返回当前在文件中的位置</td></tr><tr><td> f.truncate([size=file.tell()])</td><td> 截取文件到size个字节，默认是截取到文件指针当前位置</td></tr></tbody>


### 读取文本文件

#### 字符编码

- 在我们读取文件直接，我们要注意一个字符编码。字节及字节，字符是一种抽象，字符串由使用Unicode编码的字符系列构成，但是磁盘上的文件不是Unicode编码的字符序列，文件是字节序列，我们读取一个文件，Python怎样把这个字节转为为字符序列。

下面我们先看一个例子


```python
f = open("myfile.txt")
f.read()
```


    ---------------------------------------------------------------------------

    UnicodeDecodeError                        Traceback (most recent call last)

    <ipython-input-27-6ebc6dc80385> in <module>()
          1 f = open("myfile.txt")
    ----> 2 f.read()
    

    UnicodeDecodeError: 'gbk' codec can't decode byte 0xab in position 8: illegal multibyte sequence


我们看到上例中出现了一个UnicodeDecodeError的错误，这是因为，没有指定字符编码方式，Python使用默认的编码，所以要给它指定一个编码方式，就是加上这句代码encoding='utf-8'

#### 流对象
- 到目前为止，我们都知道Python有一个内置的函数open(),open()函数返回一个流对象，它拥有一些用来获取信息和操作字符流的方法和属性


```python
f = open('myfile.txt',encoding='utf-8')
f.name
```




    'myfile.txt'




```python
f.encoding
```




    'utf-8'




```python
f.mode
```




    'r'



- name属性反映的是当你打开文件时传递给open()函数的文件名。它没有被标准化(normalize)成绝对路径。
- 同样的，encoding属性反映的是在你调用open()函数时指定的编码方式。如果你在打开文件的时候没有指定编码方式（不好的开发人员！），那么encoding属性反映的是locale.getpreferredencoding()的返回值。
- mode属性会告诉你被打开文件的访问模式。你可以传递一个可选的mode参数给open()函数。如果在打开文件的时候没有指定访问模式，Python默认设置模式为'r'，意思是“在文本模式下以只读的方式打开。”在这章的后面你会看到，文件的访问模式有各种用途；不同模式能够使你写入一个文件，追加到一个文件，或者以二进制模式打开一个文件（在这种情况下，你处理的是字节，不再是字符）。

#### 读取数据


```python
f = open('myfile.txt',encoding='utf-8')
f.read()
```




    '测试一下\n换行测试'




```python
f.read()
```




    ''



看到这里会有疑问，问什么什么都没有打印出来？

- 只要成功打开了一个文件（并且指定了正确的编码方式），你只需要调用流对象的read()方法即可以读取它。返回的结果是文件的一个字符串表示。
- Python不认为到达了文件末尾(end-of-file)还继续执行读取操作是一个错误；这种情况下，它只是简单地返回一个空字符串。（因为在上面的实例中已经读取过了）

那么如何重新读取文件呢？


```python
f.seek(0)
```




    0




```python
f.read(4)
```




    '测试一下'




```python
f.tell()
```




    12



>- 这里为什么会是12呢？seek()和tell()方法总是以字节的方式计数，但是，由于你是以文本文件的方式打开的，read()方法以字符的个数计数。中文字符的UTF-8编码需要多个字节。而文件里的英文字符每一个只需要一个字节来存储，所以你可能会产生这样的误解：seek()和read()方法对相同的目标计数。而实际上，只有对部分字符的情况是这样的。

>- 另外不能试图从中间位置读取否则会出现UnicodeDecodeError错误，如下例


```python
f.seek(10)
f.read(1)
```


    ---------------------------------------------------------------------------

    UnicodeDecodeError                        Traceback (most recent call last)

    <ipython-input-57-01d839b97cab> in <module>()
          1 f.seek(10)
    ----> 2 f.read(1)
    

    C:\Users\lovelive\Anaconda3\lib\codecs.py in decode(self, input, final)
        319         # decode input (taking the buffer into account)
        320         data = self.buffer + input
    --> 321         (result, consumed) = self._buffer_decode(data, self.errors, final)
        322         # keep undecoded input until the next call
        323         self.buffer = data[consumed:]
    

    UnicodeDecodeError: 'utf-8' codec can't decode byte 0xb8 in position 0: invalid start byte


#### 关闭文件
- 打开文件会占用系统资源，根据文件的打开模式不同，其他的程序也许不能访问他们。所以当我们完成对文件的操作后就要立即关闭他们，It is importment！！！


```python
f.close()
```

但是这还不够，流对象f任然存在，调用close()方法并没有把对象本身销毁。所以这并不是非常有效的

#### 自动关闭文件

- 这里用到了with语句


```python
with open("myfile.txt",encoding = 'utf-8') as f:
    f.seek(9)
    character = f.read(10)
    print(character)
    
```

    下
    换行测试
    


```python
f.tell()
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-61-322ae27c0b94> in <module>()
    ----> 1 f.tell()
    

    ValueError: I/O operation on closed file.


- 上例中并没有对其使用close方法，但是文件却关闭了，因为这里Pyhton自动调用了f.close()
- 无论你以何种方式跳出with块，Python会自动关闭那个文件…即使是因为未处理的异常而“exit”。是的，即使代码中引发了一个异常，整个程序突然中止了，Python也能够保证那个文件能被关闭掉。

#### 按行读取


```python
line_number = 0
with open('myfile.txt', encoding='utf-8') as a_file: 
    for a_line in a_file:                                               
        line_number += 1
        print('{:>4} {}'.format(line_number, a_line.rstrip()))          
```

       1 测试一下
       2 换行测试
    

- 使用with语句，安全地打开这个文件，然后让Python为你关闭它。
- 为了一次读取文件的一行，使用for循环。是的，除了像read()这样显式的方法，流对象也是一个迭代器(iterator)，它能在你每次请求一个值时分离出单独的一行。
- 使用字符串的format()方法，你可以打印出行号和行自身。格式说明符{:>4}的意思是“使用最多四个空格使之右对齐，然后打印此参数。”变量a_line是包括回车符等在内的完整的一行。字符串方法rstrip()可以去掉尾随的空白符，包括回车符。


### 写入文本文件
- 写入文件和读取文件相似，首先打开一个文件，获取流对象，然后调用一些方法作用在流对象上来写入数据到文件，最后关闭文件

- 为了写入儿打开一个文件，我们可以使用open（）函数，并且指定写入模式。有两种文件模式用于写入：
    - “写”模式会重写文件。传递mode = ‘w’参数给open()函数。
    - “追加”模式会在文件末尾添加数据。传递mode = ‘a'参数给open()函数。
    
- 如果文件不存在，两种模式下都会自动创建新文件，所以就不需要“如果文件还不存在，创建一个新的空白文件以能够打开它”这种琐碎的过程了。所以，只需要打开一个文件，然后开始写入即可。

- 在完成写入后你应该马上关闭文件，释放文件句柄(file handle)，并且保证数据被完整地写入到了磁盘。跟读取文件一样，可以调用流对象的close()方法，或者你也可以使用with语句让Python为你关闭文件。


```python
with open('test.log',mode = 'w',encoding = 'utf-8') as a_file:#创建新文件test.log,然后以写入模式打开
    a_file.write("test succeeded")
```


```python
with open("test.log",encoding = "utf-8") as a_file:
    print(a_file.read())
```

    test succeeded
    


```python
with open("test.log",mode = "a",encoding = "utf-8") as a_file:#追加模式，不会破坏现有文件的内容
    a_file.write("add again")
```


```python
with open("test.log",encoding = "utf-8") as a_file:
    print(a_file.read())
```

    test succeededadd again
    

当我们在打开文件用于写入数据的时候，也要传递给open()函数encoding参数，正如开始说的，文件中不存在字符串，他们由字节组成，只有当告诉Python使用何种编码方式把字节转换为字符串，从文件读取字符串才可能。相反的，写入文本到文件一样，实际上你不能直接把字符直接写入到文件中，为了写入字符到文件，Python需要知道如何将字符串转换为字节序列唯一保证正确地执行转换的方法就是当我们为了写入而打开一个文件的时候，指定encoding参数。

## 二进制文件
- 并不是所有的文件都只包含文本内容，有些还包含了图片


```python
an_image = open("../task/image/question.png",mode = "rb")
an_image.mode
```




    'rb'




```python
an_image.name
```




    '../task/image/question.png'




```python
an_image.encoding
```


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    <ipython-input-79-206e331c9e5c> in <module>()
    ----> 1 an_image.encoding
    

    AttributeError: '_io.BufferedReader' object has no attribute 'encoding'


- 用二进制打开文件很简单，很是很精细，与文本模式唯一不同的是mode参数包含一个字符“b”。
- 以二进制模式打开文件得到的流对象与之前的有很多相同的属性，包括mode属性，它记录了你调用open()函数时指定的mode参数的值。
- 二进制文件的流对象也有name属性，和文本文件的流对象一样。
- 二进制的流对象没有encoding属性，因为现在我们读写的是字节，不是字符串，不需要转换


```python
an_image.tell()
```




    0




```python
data = an_image.read(3)
data
```




    b'\x89PN'




```python
type(data)
```




    bytes




```python
an_image.tell()
```




    3




```python
an_image.seek(0)
```




    0




```python
data = an_image.read()
len(data)
```




    19472



**跟读取文本文件一样，唯一的不同就是，这时候我们读的是字节，不是字符。**

## 非文件来源的流对象

- 我们要求的并不只是针对真是的文件，而是能够“读取”的输入源可以是任何东西：网页，内存中的字符串，甚至是另外一个程序的输出。只要你的函数使用的是流对象，调用对象的read()方法，你可以处理任何行为与文件类似的输入源，而不需要为每种类型的输入指定特别的代码。


```python
import io

a_string = "This is a test string"

a_file = io.StringIO(a_string)
a_file.read()
```




    'This is a test string'



- io模块定义了StringIO类，可以用它来把内存中的字符串当作文件来处理
- 为了从字符串创建一个流对象，可以把想要作为“文件”的字符串传递给io.StringIO()来创建一个StringIO的实例。
- 调用read()方法“读取”整个“文件”，以StringIO对象为例及返回原字符串


```python
a_file.read()
```




    ''



- 就像一个真是的文件一样，再次调用read()方法返回一个空串


```python
a_file.seek(0)
```




    0



通过使用StringIO对象的seek()方法，你可以显式地定位到字符串的开头，就像在一个真实的文件中定位一样。


```python
a_file.read(10)
```




    'This is a '




```python
a_file.tell()
```




    10




```python
a_file.seek(14)
a_file.read()
```




    ' string'



通过传递size参数给read()方法，你也可以以数据块的形式读取字符串。
>io.StringIO能够将一个字符串作为文本文件来看待。另外还有一个io.ByteIO类，它允许将字节数组当做二进制文件来处理。

## 标准输入、输出和错误
- 标准输出和标准错误（缩写为stdout和stderr）是被集成到每一个类UNIX操作系统的两个管道，包括Mac OS X和Linux
- 当调用print()函数的时候，需要打印的内容被发送到stdout管道，当当程序出错，并且需要打印跟踪信息是，会被发送到stderr管道
- 默认的，这两个管道都被连接到正在工作的终端窗口上，当程序打印某些东西，可以在终端看到这些输出，当程序出错是，也可以从终端看到错误信息


```python
for i in range(3):
    print("PapayWhip")
```

    PapayWhip
    PapayWhip
    PapayWhip
    


```python
import sys

for i in range(3):
    sys.stdout.write("is the")
```

    is theis theis the

stdout被定义在sys模块里，它是一个流对象(stream object)。使用任意字符串调用其write()函数会按原样输出。事实上，这就是print()函数实际在做的事情；它在串的结尾添加一个回车符，然后调用sys.stdout.write。


```python
for i in range(3):
    sys.stderr.write("new black")
```

    new blacknew blacknew black

最简单的情况下，sys.stdout和sys.stderr把他们的输出发送到同一个位置：Python ide（如果你在那里执行操作），或者终端（如果你从命令行执行Python指令）。跟标准输出一样，标准错误也不会自动为你添加回车符。如果你需要回车符，你需要手工写入回车符到标准错误。

- sys.stdout和sys.stderr都是流对象，但是他们都只支持写入。试图调用他们的read()方法会引发IOError异常。


```python
import sys
sys.stdout.read()
```


    ---------------------------------------------------------------------------

    OSError                                   Traceback (most recent call last)

    <ipython-input-99-b249ed7d8dd2> in <module>()
          1 import sys
    ----> 2 sys.stdout.read()
    

    C:\Users\lovelive\Anaconda3\lib\site-packages\ipykernel\iostream.py in read(self, size)
        298 
        299     def read(self, size=-1):
    --> 300         raise IOError('Read not supported on a write only stream.')
        301 
        302     def readline(self, size=-1):
    

    OSError: Read not supported on a write only stream.


#### 标准输出重定向
- sys.stdout和sys.stderr都是流对象，尽管他们只支持写入。但是他们是变量而不是常量。这就意味着你可以给它们赋上新值 — 任意其他流对象 — 来重定向他们的输出。


```python
import sys

class RedirectStdoutTo:
    def __init__(self, out_new):
        self.out_new = out_new

    def __enter__(self):
        self.out_old = sys.stdout
        sys.stdout = self.out_new

    def __exit__(self, *args):
        sys.stdout = self.out_old

print('A')
with open('out.log', mode='w', encoding='utf-8') as a_file, RedirectStdoutTo(a_file):
    print('B')
print('C')
```

    A
    C
    


```python
import sys

class RedirectStdoutTo:
    def __init__(self, out_new):
        self.out_new = out_new

    def __enter__(self):
        self.out_old = sys.stdout
        sys.stdout = self.out_new

    def __exit__(self, *args):
        sys.stdout = self.out_old

print('A')
with open('out.log', mode='w', encoding='utf-8') as a_file:
    with RedirectStdoutTo(a_file):
        print('B')
print('C')
```

    A
    C
    

正如改动后的代码所展示的，实际上你使用了两个with语句，其中一个嵌套在另外一个的作用域(scope)里。“外层的”with语句你应该已经熟悉了：它打开一个使用utf-8编码的叫做out.log的文本文件用来写入，然后把返回的流对象赋给一个叫做a_file的变量。

```
with RedirectStdoutTo(a_file):
```
这句代码中，会发现as子句没有了，其实with语句并不一定需要as子句。就像调用一个函数然后忽略其返回值一样，可以不把with语句的上下文环境赋给一个变量。在这种情况下，我们只关心RedirectStdoutTo上下文环境的边际效应(side effect)。

那么，这些边际效应都是些什么呢？我们来看一看RedirectStdoutTo类的内部结构。这是一个用户自定义的上下文管理器(context manager)。任何类只要定义了两个特殊方法：`__enter__()`和`__exit__()`就可以变成上下文管理器。


```python
class RedirectStdoutTo:
    def __init__(self, out_new):   
        self.out_new = out_new

    def __enter__(self):            
        self.out_old = sys.stdout
        sys.stdout = self.out_new

    def __exit__(self, *args):      
        sys.stdout = self.out_old
```

- 在实例被创建后__init__()方法马上被调用。它使用一个参数，即在上下文环境的生命周期内你想用做标准输出的流对象。这个方法只是把该流对象保存在一个实例变量里(instance variable)以使其他方法在后边能够使用到它。
- `__enter__()`方法是一个特殊的类方法(special class method)；在进入一个上下文环境时Python会调用它（即，在with语句的开始处）。该方法把当前sys.stdout的值保存在self.out_old内，然后通过把self.out_new赋给sys.stdout来重定向标准输出。
- `__exit__()`是另外一个特殊类方法；当离开一个上下文环境时（即，在with语句的末尾）Python会调用它。这个方法通过把保存的self.out_old的值赋给sys.stdout来恢复标准输出到原来的状态。

所以由于print("b")在with语句创建的山下完呢环境执行，所以不会输入到屏幕上，它会写入到out.log文件中


```python
with open('out.log',encoding='utf-8') as a_file:
    print(a_file.read())
```

    B
    
    
