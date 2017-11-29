# 3 Python非正式介绍

通过提示符（prompt）“>>>”或“...”来区分输入和输出。

注释用井号键（hash character）：“#”。在一行开头或空白或代码之后。

在字符串中的“#”只是一个字符而已。注释不会被Python解释，会被自动忽略。、

```python
# this is the first comment
spam = 1  # and this is the second comment
          # ... and now a third!
text = "# This is not a comment because it's inside quotes."
```

## 3.1 将Python用作计算器（use Python as a calculator）

打开解释器，在提示符之后开始键入。

### 3.1.1 数字（numbers）

```python
>>> 2 + 2
4
>>> 50 - 5*6
20
>>> (50 - 5*6) / 4
5.0
>>> 8 / 5  # division always returns a floating point number
1.6
```

整数：int

浮点数（有小数点）：float

除号（“/”）总会返回一个浮点数。要得到整数就用“//”；要得到余数用“%”。

```python
>>> 17 / 3  # classic division returns a float
5.666666666666667
>>>
>>> 17 // 3  # floor division discards the fractional part
5
>>> 17 % 3  # the % operator returns the remainder of the division
2
>>> 5 * 3 + 2  # result * divisor + remainder
17
```

用“**” 来表示幂（powers）运算

```python
>>> 5 ** 2  # 5 squared
25
>>> 2 ** 7  # 2 to the power of 7
128
```

等号“=”表示赋值给一个变量。在赋值之后不会有结果显示出来

```python
>>> width = 20
>>> height = 5 * 9
>>> width * height
900
```

如果变量没有被“定义”（在python中就是被赋值），会提示错误：

```python
>>> n  # try to access an undefined variable
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'n' is not defined
```

如果有多种操作对象（operands），会统一将整型转换成浮点型：

```python
>>> 4 * 3.75 - 1
14.0
```

交互模式中，上一次打印出来的值会被赋给下划线“_”。也就意味着可以进行连续的计算：

```python
>>> tax = 12.5 / 100
>>> price = 100.50
>>> price * tax
12.5625
>>> price + _
113.0625
>>> round(_, 2)     # round（a，b）是给值a设置一个有效位数b？
113.06
```

除了int（整型）和float（浮点型），Python还支持decimal（小数型，十进制）和fraction（分数）。

同时内置了对复数（complex numbers）的支持，用j或J来表示虚部（如：3+5j）

### 3.1.2 字符串（strings）

用单引号single quotes（'...'）或双引号double quotes（"..."）来表示。反斜线backslashes（\）可以转义引号。

```python
>>> 'spam eggs'  # single quotes
'spam eggs'
>>> 'doesn\'t'  # use \' to escape the single quote...
"doesn't"
>>> "doesn't"  # ...or use double quotes instead
"doesn't"
>>> '"Yes," he said.'
'"Yes," he said.'
>>> "\"Yes,\" he said."
'"Yes," he said.'
>>> '"Isn\'t," she said.'
'"Isn\'t," she said.'
```

如果字符串内有单引号'，则用双引号"括起来。一般来说，单引和双引是一样的。

print()函数提供了更可读的输出，会将外面的引号（enclosing quotes不知道怎么翻译）忽略，打印转移之后的字符和特殊字符：

```python
>>> '"Isn\'t," she said.'
'"Isn\'t," she said.'
>>> print('"Isn\'t," she said.')
"Isn't," she said.
>>> s = 'First line.\nSecond line.'  # \n means newline
>>> s  # without print(), \n is included in the output
'First line.\nSecond line.'
>>> print(s)  # with print(), \n produces a new line
First line.
Second line.
```

如果不希望反斜线\转义，可以用raw string，在第一个引号前加上一个字母r:

```python
>>> print('C:\some\name')  # here \n means newline!
C:\some
ame
>>> print(r'C:\some\name')  # note the r before the quote
C:\some\name
```

多行字符串用三个引号表示：'''...'''或者"""..."""

不过这会自动将第一行包括进去，在第一行末尾加一个反斜线来避免：

```python
print("""\
Usage: thingy [OPTIONS]
     -h                        Display this usage message
     -H hostname               Hostname to connect to
""")
```

最终输出结果是：

```
Usage: thingy [OPTIONS]
     -h                        Display this usage message
     -H hostname               Hostname to connect to
```

加号+表示连接字符串，星号*表示重复字符串。

```python
>>> # 3 times 'un', followed by 'ium'
>>> 3 * 'un' + 'ium'
'unununium'
```

两个以上紧挨着的字符串会自动串级（concatenate）：

```python
>>> 'Py' 'thon'
'Python'
```

上面这个特性在你希望将长字符串分开的时候特别有用：

```python
>>> text = ('Put several strings within parentheses '
...         'to have them joined together.')
>>> text
'Put several strings within parentheses to have them joined together.'
```

这只在文字（literals）之间可以实现，在变量（variables）和表述（expressions）不行：

```python
>>> prefix = 'Py'
>>> prefix 'thon'  # can't concatenate a variable and a string literal
  ...
SyntaxError: invalid syntax
>>> ('un' * 3) 'ium'
  ...
SyntaxError: invalid syntax
```

如果想连接变量和文字，用加号+

```python
>>> prefix + 'thon'
'Python'
```

字符可以被索引，第一个字符的索引是0。没有不同的字符类型，一个字符就是大小为1的字符串：

```python
>>> word = 'Python'
>>> word[0]  # character in position 0
'P'
>>> word[5]  # character in position 5
'n'
```

索引（indices）也可为负数，从右侧开始数。（由于-0与0一样，所以负数索引从-1开始）

```python
>>> word[-1]  # last character
'n'
>>> word[-2]  # second-last character
'o'
>>> word[-6]
'P'
```

也可以用切片（slicing）截取一个子串（substring）。

用[a:b]来表示，a是开头，b是结尾，包括开头，但不包括结尾。所以s[:i]+s[i:]总是等于s：

```python
>>> word[0:2]  # characters from position 0 (included) to 2 (excluded)
'Py'
>>> word[2:5]  # characters from position 2 (included) to 5 (excluded)
'tho'
>>> word[:2] + word[2:]
'Python'
>>> word[:4] + word[4:]
'Python'
```

省略的第一个索引默认为0，省略的第二个索引默认为切割的字符串大小。

为方便记住切割的工作原理，将索引视为字符之间的索引。第一个字符左边缘编号为0，最后一个字符右边缘是n

```
 +---+---+---+---+---+---+
 | P | y | t | h | o | n |
 +---+---+---+---+---+---+
 0   1   2   3   4   5   6
-6  -5  -4  -3  -2  -1
```

索引为非负数时，切片的长度和索引是不一样的。例如，word[1:3]的长度是2。

太大的索引会报错，但是超出范围的切片索引会被自动处理：

```python
>>> word[42]  # the word only has 6 characters
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: string index out of range
>>> word[4:42]
'on'
>>> word[42:]
''
```

字符串是不能够被改变的（immutable）。分配给字符串中的索引位置会导致错误（Therefore, assigning to an indexed position in the string results in an error. 这句话不知道怎么翻译）。

```python
>>> word[0] = 'J'
  ...
TypeError: 'str' object does not support item assignment
>>> word[2:] = 'py'
  ...
TypeError: 'str' object does not support item assignment
```

如果想要一个不同的字符串，那就用加号+创造一个新的。

```python
>>> 'J' + word[1:]
'Jython'
>>> word[:2] + 'py'
'Pypy'
```

内建函数len()可以返回字符串的长度：

```python
>>> s = 'supercalifragilisticexpialidocious'
>>> len(s)  # 表示获取s这个字符串的长度
34
```

### 3.1.3 列表（lists）

方括号（square brackets），逗号分开（comma-separated）的值，通常这个元素（items）是相同的类型。

```python
>>> squares = [1, 4, 9, 16, 25]
>>> squares
[1, 4, 9, 16, 25]
```

与字符串一样，列表也能被索引（indexed）和切片（sliced）：

```python
>>> squares[0]  # indexing returns the item
1
>>> squares[-1]
25
>>> squares[-3:]  # slicing returns a new list
[9, 16, 25]
```

对列表的所有切片操作，都会返回一个新的所请求的列表。

```python
>>> squares[:]
[1, 4, 9, 16, 25]
```

列表也支持连接（concatenation）操作

```python
>>> squares + [36, 49, 64, 81, 100]
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

列表可变（mutable），字符串不可变（immutable）。可以更改列表的内容：

```python
>>> cubes = [1, 8, 27, 65, 125]  # something's wrong here
>>> 4 ** 3  # the cube of 4 is 64, not 65!
64
>>> cubes[3] = 64  # replace the wrong value
>>> cubes
[1, 8, 27, 64, 125]
```

用append()方法在列表最后添加元素：

```python
>>> cubes.append(216)  # add the cube of 6
>>> cubes.append(7 ** 3)  # and the cube of 7
>>> cubes
[1, 8, 27, 64, 125, 216, 343]
```

 分配到切片也是可以的，这可能会改变列表的大小或者将其完全清空。（Assignment to slices is also possible, and this can even change the size of the list or clear it entirely）：
 
 ```python
 >>> letters = ['a', 'b', 'c', 'd', 'e', 'f', 'g']
>>> letters
['a', 'b', 'c', 'd', 'e', 'f', 'g']
>>> # replace some values
>>> letters[2:5] = ['C', 'D', 'E']
>>> letters
['a', 'b', 'C', 'D', 'E', 'f', 'g']
>>> # now remove them
>>> letters[2:5] = []
>>> letters
['a', 'b', 'f', 'g']
>>> # clear the list by replacing all the elements with an empty list
>>> letters[:] = []
>>> letters
[]
```

内建函数len()同样适用于列表：

```python
>>> letters = ['a', 'b', 'c', 'd']
>>> len(letters)
4
```

也可以嵌套（nest）列表，也就是在列表中创建新的列表（create lists containing other lists）：

```python
>>> a = ['a', 'b', 'c']
>>> n = [1, 2, 3]
>>> x = [a, n]
>>> x
[['a', 'b', 'c'], [1, 2, 3]]
>>> x[0]
['a', 'b', 'c']
>>> x[0][1]
'b'
```

## 3.2 向编程踏出第一步

例：完成复杂的任务，编写菲波那切数列的初始子序列：

```python
>>> # Fibonacci series:
... # the sum of two elements defines the next
... a, b = 0, 1
>>> while b < 10:
...     print(b)
...     a, b = b, a+b
...
1
1
2
3
5
8
```

这个例子介绍了几个新功能：

- 多重赋值（multiple assignment）：

第一行中，a和b被分别赋值为0和1。最后一行也用到了。在赋值之前，右侧的表达式最先被评估，右侧的表示从左到右进行评估。

- while循环（loop）：

当条件为真时，循环一直继续。Python和C一样，非零整数为真（true），零为假（false）。

比较操作符，与C语言一样：

|小于|less than|<|
|大于|greater than|>|
|等于|equal to|=|
|小于等于|less than or equal to|<=|
|大于等于|greater than or equal to|>=|
|不等于|not equal to|!=|

- 循环的主体全部缩进（indented）:

缩进是Python的一种群组声明的方式（Indentation is Python’s way of grouping statements.）

用tab或者space键来设定缩进。补充：一般python的缩进规定是4个字符。

当输入复合声明的时候，最后一行用空白行来表示完成（indicate completion）因为解析器（parser）猜不出你什么时候输入最后一行。

注意：每一基本块（basic block）需要相同的缩进单位。

- print()函数：

打印出给出的参数的值。其处理多个参数、浮点数和字符串的方式不同。

字符串打印的时候没有引号，元素之间会插入（inserted）空格，所以可以很好地格式化：

```python
>>> i = 256*256
>>> print('The value of i is', i)
The value of i is 65536
```

关键字参数（keyword argument）end用来避免输出后的换行符（avoid the newline），或者用不同的字符串结束输出：

```python
>>> a, b = 0, 1
>>> while b < 1000:
...     print(b, end=',')
...     a, b = b, a+b
...
1,1,2,3,5,8,13,21,34,55,89,144,233,377,610,987,
```
