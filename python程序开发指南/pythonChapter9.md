
# Python第九章学习

- [x] 正则表达式

## 正则表达式
- 正则表达式（Regular expressions 也称为 REs，或 regexes 或 regex patterns）本质上是一个微小的且高度专业化的编程语言。它被嵌入到 Python 中，并通过 re 模块提供使用。使用正则表达式，你需要指定一些规则来描述那些你希望匹配的字符串集合。这些字符串集合可能包含英语句子、 e-mail 地址、TeX 命令，或任何你想要的东西。

>Python 的正则表达式引擎是用 C 语言写的，所以效率是极高的。另，所谓的正则表达式，这里说的 RE，就是上文我们提到的“一些规则”。

- 正则表达式语言相对小型和受限（功能有限）
    - 并非所有的字符串处理都能用正则表达式完成


### 字符匹配
- 普通字符
    - 大多数字母和字符一般都会和自身匹配
    - 如正则表达式test会和字符串“test”完全匹配
- 元字符      
    - .  ^  $  *  +  ?  {}  []  \  | ()

- []符号
    - 常用来指定一个字符集：[abc];[a-z]
    - 元字符在字符集中不起作用：[akm$]
    - 补集匹配不在区间范围内的字符：[^5]


```python
import re#导入模块re

s = r"abc"#定义一个规则

re.findall(s,"abcaaaaaabcaaaaaaaaaa")
```


    ['abc', 'abc']



有时候规则会变化,如果我们想要找到另外规则的字符串


```python
st = "top tip tqp twp tep"#要找到top
res = r"top"
re.findall(res,st)
```


    ['top']




```python
res = r"t[io]p"#可以找到tip、top
re.findall(res,st)
```


    ['top', 'tip']




```python
res = r"t[^io]p"#找到tip、top外的字符串
re.findall(res,st)
```


    ['tqp', 'twp', 'tep']




```python
r = r"[a-zA-Z0-9]"

re.findall(r,"jslkfsj213i9839")
```


    ['j', 's', 'l', 'k', 'f', 's', 'j', '2', '1', '3', 'i', '9', '8', '3', '9']



- **^**符号
    - 匹配行首,除非设置MULTILINE标志，它是匹配字符串的开始，在MULTILINE模式里，它也可以直接匹配字符串的每个换行


```python
s = "hello world,hello Pyhton"

r = r"hello"

re.findall(r,s)
```


    ['hello', 'hello']




```python
r = r"^hello"#返回开始的hello

re.findall(r,s)
```


    ['hello']



- **$**
    - 匹配行尾，行尾被定义为要么是字符串尾，要目是一个换行字符后面的任何位置


```python
r = r"Pyhton$"
re.findall(r,s)
```


    ['Pyhton']




```python
r = "t[abc$]"

re.findall(r,"ta")
re.findall(r,"tax")
re.findall(r,"t$")
```


    ['t$']



- **`\`**
    - 反斜杠后面可以加不同的字符以表示不同特殊意义
    - 也可以用于取消所有的元字符：`\[`或`\\`


```python
%%html
<tbody>
<tr><td>特殊字符</td><td>含义</td></tr>
<tr><td>\d</td> <td> 匹配任何十进制数字；相当于类</td></tr>
<tr><td>\D</td><td> 与 \d相反，匹配任何非十进制数字的字符；相当于类 [^0-9]</tr>
<tr><td>\s</td><td> 匹配任何空白字符（包含空格、换行符、制表符等）；相当于类[ \t\n\r\f\v]</td></tr>
<tr><td>\S</td><td> 与 \s相反，匹配任何非空白字符；相当于类[^ \t\n\r\f\v]</td></tr>
<tr><td>\w</td><td> 匹配任何单词字符，见上方解释</td></tr>
<tr><td>\W</td><td> 于 \w相反</td></tr>
<tr><td>\b</td><td>匹配单词的开始或结束 </td></tr>
<tr><td>\B</td><td> 与 \b相反</td></tr>
</tbody>
```

<tbody>
<tr><td>特殊字符</td><td>含义</td></tr>
<tr><td>\d</td> <td> 匹配任何十进制数字；相当于类</td></tr>
<tr><td>\D</td><td> 与 \d相反，匹配任何非十进制数字的字符；相当于类 [^0-9]</tr>
<tr><td>\s</td><td> 匹配任何空白字符（包含空格、换行符、制表符等）；相当于类[ \t\n\r\f\v]</td></tr>
<tr><td>\S</td><td> 与 \s相反，匹配任何非空白字符；相当于类[^ \t\n\r\f\v]</td></tr>
<tr><td>\w</td><td> 匹配任何单词字符，见上方解释</td></tr>
<tr><td>\W</td><td> 于 \w相反</td></tr>
<tr><td>\b</td><td>匹配单词的开始或结束 </td></tr>
<tr><td>\B</td><td> 与 \b相反</td></tr>
</tbody>



```python
r = r"\^abc"

re.findall(r,"^abc ^abc ^abc")
```


    ['^abc', '^abc', '^abc']




```python
r = r"\d"

re.findall(r,"1234568")
```


    ['1', '2', '3', '4', '5', '6', '8']



- 重复
    - 我们在指定规则时避免不了的会重复，这时候就用到了**{}**符号
    - 还有一个**`*`**号，指定一个字符可以被匹配零次或更多次，儿不是只有一次。匹配引擎会试着重复尽可能多的次数
    - **+**号表示匹配一次或更多次，注意和`*`的区别
    - **？**号匹配一次或者零次；我们可以用它来标识某事物是可选的


```python
r = r"^010-\d\d\d\d\d\d\d\d"

re.findall(r,"010-87654321")
```


    ['010-87654321']




```python
r = r"^010-\d{8}"
re.findall(r,"010-87654321")
```


    ['010-87654321']




```python
r = r"ab*"

re.findall(r,"a")#匹配零次
```


    ['a']




```python
re.findall(r,"abbbbbbbbbbbbbbbbbbb")#匹配多次
```


    ['abbbbbbbbbbbbbbbbbbb']




```python
r = r"ab+"

re.findall(r,"a")#匹配零次是不行
```


    []




```python
re.findall(r,"abbbbbb")
```


    ['abbbbbb']




```python
r = r"^010-?\d{8}"#中间的-可有可无

re.findall(r,"010-87654321")
```


    ['010-87654321']




```python
re.findall(r,"01087654321")
```


    ['01087654321']



正则表达式有两种模式：贪婪模式和非贪婪模式，贪婪模式就是最大匹配，非贪婪模式就是最小匹配，下面是例子


```python
r = r"ab+"#贪婪模式，最大匹配
re.findall(r,"abbbbbbbbbbbbbbbbbbb")
```


    ['abbbbbbbbbbbbbbbbbbb']




```python
r = r"ab+?"#非贪婪模式，最小匹配
re.findall(r,"abbbbbbbbbbbbbbbbbbb")
```


    ['ab']



- **{m,n}**
    - 其中m和n是十进制整数，该限定符的意思是至少有m个重复，至多有n个重复
    - 忽略m会认为下边界是0，而忽略n的结果是上边界无穷大（20亿）
    - {0，}等同于**`*`**，{1，}等同于**+**，而{0,1}泽宇**？**相同。


```python
r = r"a{1,3}"

re.findall(r,"aa")
```


    ['aa']



### 使用正则表达式
- re模块提供了一个正则表达式引擎的接口，可以使我们将REstring编译成对象并用他们来进行匹配
>如果我们经常使用某个正则表达式，可以对他进行编译,使用re.compile函数


```python
#编译正则表达式
import re

r1 = r"\d{3,4}-?\d{8}"

p_tel = re.compile(r1)
p_tel
```


    re.compile(r'\d{3,4}-?\d{8}', re.UNICODE)


```python
p_tel.findall("010-12345678")
```


    ['010-12345678']


```python
#编译一个不区分大小写的正则表达式,使用到一个参数re.I
csvt_re = re.compile(r"csvt",re.I)

csvt_re.findall("cSvT")
```


    ['cSvT']

- 执行匹配
    - ·RegexObject·实例有一些方法和属性，完整的列表可查阅Python Library reference
    
|方法/属性|作用|
|:-------:|:----|
|match()|    决定RE是否在字符串岗开始的位置匹配|
|search()|    扫描字符串，找到RE匹配的位置|
|findall()|  找到RE匹配的所有字符串，并把他们组为一个列表返回|
|finditer()|找到RE匹配的所有字符串，并把他们组为一个迭代器返回|

>如果没有匹配到的话，macth()和search()将返回None


```python
csvt_re.match("csvt hello")#返回一个对象
```


    <_sre.SRE_Match object; span=(0, 4), match='csvt'>


```python
csvt_re.search("csvt hello")#返回一个对象
```


    <_sre.SRE_Match object; span=(0, 4), match='csvt'>


```python
csvt_re.finditer("csvt hello")#返回一个对象
```


    <callable_iterator at 0x447c908>

- 模块顶级函数
    - re模块也提供了顶级函数如match()、search()、sub()、subn()、spilt()、findall()函数等


```python
help(re.sub)
```

    Help on function sub in module re:
    
    sub(pattern, repl, string, count=0, flags=0)
        Return the string obtained by replacing the leftmost
        non-overlapping occurrences of the pattern in string by the
        replacement repl.  repl can be either a string or a callable;
        if a string, backslash escapes in it are processed.  If it is
        a callable, it's passed the match object and must return
        a replacement string to be used.


```python
rs = r"c..t"

re.sub(rs,"python","csvt caat cvvt cccc")
```


    'python python python cccc'


```python
re.subn(rs,"python","csvt caat cvvt cccc")
```


    ('python python python cccc', 3)


```python
ip = "192.168.1.1"

ip.split('.')#切分字符串
```


    ['192', '168', '1', '1']


```python
s = "123+456-789*000"

re.split(r"[\+\-\*]",s)
```


    ['123', '456', '789', '000']

- 编译标志-flags

|标志|含义|
|:---:|:---|
|DOTALL,S|使**.**匹配包括换行在内的所有字符|
|IGNORECASE,I|是匹配对大小写不敏感|
|LOCALE,L|使本地化识别（local-aware）匹配|
|MULTILINE,M|多行匹配，影响**`^`**和**`$`**|
|VERBOSE,X|能使用REs的verbose状态，使之被组织的更清晰易懂|


```python
import re

r1 = r"csvt.net"

re.findall(r1,"csvt\nnet")
```


    []



```python
re.findall(r1,"csvt\nnet",re.S)
```


    ['csvt\nnet']



```python
s = """hello csvt
csvt hello
hello python
"""
r = r"^csvt"

re.findall(r,s,re.M)#多行匹配
```


    ['csvt']



```python
tel = r"""
\d{3,4}
-?
\d{8}
"""
re.findall(tel,"010-12345678",re.VERBOSE)
```


    ['010-12345678']

- 分组“（”和“）”


```python
email = r"\w{3}@\w+(.com|.cn)"

re.match(email,"zzz@csvt.com")
```


    <_sre.SRE_Match object; span=(0, 12), match='zzz@csvt.com'>



```python
re.findall(email,"zzz@csvt.com")#findall优先输出分组中的匹配
```


    ['.com']


