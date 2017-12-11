# 4 更多的控制流程工具（control flow tools）

除了while声明意外，还有很多常见的控制流声明

## 4.1 if声明（statement）

if声明也许是最知名的声明类型

```python
>>> x = int(input("Please enter an integer: "))
Please enter an integer: 42
>>> if x < 0:
...     x = 0
...     print('Negative changed to zero')
... elif x == 0:
...     print('Zero')
... elif x == 1:
...     print('Single')
... else:
...     print('More')
...
More
```

可以有0个或多个elif部分。为了避免过度的缩进，将'else if'简写成'elif'。

if...elif...elif...序列（sequence）在其他语言中用switch或case声明来替代（substitute）。

## 4.2 for声明

Python中的for声明与Pascal和C语言中不太一样。

|语言|用法|
|------|-------|
|Pascal|迭代算数数列（arithmetic progression of numbers）|
|C|用户可以自定义迭代步骤（iteration step）和停止条件（halting condition）|
|Python|可以迭代任何项目（item）的任何序列（sequence）|

Python也可以迭代列表和字符串

```python
>>> # Measure some strings:
... words = ['cat', 'window', 'defenestrate']
>>> for w in words:
...     print(w, len(w))
...
cat 3
window 6
defenestrate 12
```

在循环中修改序列（比如复制（duplicate）选中的项目（item））,它会建议你先做一个复制。迭代某个序列不会暗中创造一个副本（make a copy）

切片符号（slice notation）会更方便：

```python
>>> for w in words[:]:  # Loop over a slice copy of the entire list.
...     if len(w) > 6:
...         words.insert(0, w)
...
>>> words
['defenestrate', 'cat', 'window', 'defenestrate']
```

这个例子中会试图创造一个无限的列表，不停地插入“defenestrate”

## 4.3 range()函数

要迭代数列，range()会很方便，它生成（generate）算数级数（arithmetic progression）：

```python
>>> for i in range(5):
...     print(i)
...
0
1
2
3
4
```

需要注意的是，给定的终点不是生成的序列的一部分：range(10)生成10个值，长度为10的序列的序列的项目的合法声明（the legal indices for items of a seaquence of length 10）。

可让其从另一个数字开始，或者指定不同的增量（可为负数，称之为步长（step））：

```python
range(5, 10)
   5 through 9

range(0, 10, 3)
   0, 3, 6, 9

range(-10, -100, -30)
  -10, -40, -70
```

要通过索引来迭代序列的话，可以将range()和len()结合在一起：

```python
>>> a = ['Mary', 'had', 'a', 'little', 'lamb']
>>> for i in range(len(a)):
...     print(i, a[i])
...
0 Mary
1 had
2 a
3 little
4 lamb
```

在上述的例子中，用enumerate()函数更方便。（在Looping Techniques中有介绍）

如果直接打印range()的话，会很奇怪：

```python
>>> print(range(10))
range(0, 10)
```

在许多方面，由range()返回的对象表现得像是一个列表，但实际上并非如此。 它是一个对象，当你迭代它时，它会返回所需序列的连续项目，但它并不真正生成列表，从而节省空间。

我们说这样的对象是可迭代的，也就是说，适合作为函数和构造的目标，期望从中可以获得连续的东西，直到耗尽为止。 我们已经看到for语句就是这样一个迭代器。 函数list()是另一个; 它从迭代中创建列表：

```python
>>> list(range(5))
[0, 1, 2, 3, 4]
```

之后会看到更多返回迭代器（iterable）的函数，并将这些迭代器当做变量或者变量？（argument）

## 4.4 break和continue声明，循环中的else子句（clause）

break语句，和C语言中一样，打破了最内层（innermost）的for或while循环。

循环语句可能会有一个else语句；当循环用尽列表（用for语句）或者条件变为false时执行，而不是在循环由break语句终止时执行。

以下面为例，搜索素数（prime numbers）： 

```python
>>> for n in range(2, 10):
...     for x in range(2, n):
...         if n % x == 0:
...             print(n, 'equals', x, '*', n//x)
...             break
...     else:
...         # loop fell through without finding a factor
...         print(n, 'is a prime number')
...
2 is a prime number
3 is a prime number
4 equals 2 * 2
5 is a prime number
6 equals 2 * 3
7 is a prime number
8 equals 2 * 4
9 equals 3 * 3
```

（注意：上述代码是正确的。else语句属于第二个for循环，而不是if声明）

当与循环一起使用，相比于if中的else语句，else子句与try语句中的else子句更相似一些：

try语句中的else子句在没有异常发生（no exception occurs）时执行；循环中的else子句在没有break发生的情况下执行。更多有关try语句和异常，参阅Handling Exceptions。

从C语言中借用一个continue语句，继续下一个迭代循环：

```python
>>> for num in range(2, 10):
...     if num % 2 == 0:
...         print("Found an even number", num)
...         continue
...     print("Found a number", num)
Found an even number 2
Found a number 3
Found an even number 4
Found a number 5
Found an even number 6
Found a number 7
Found an even number 8
Found a number 9
```

## 4.5 pass声明

pass语句什么都不执行（The pass statement does nothing）。

语句需要语法时使用它，但程序不需要任何操作。例如：

```python
>>> while True:
...     pass  # Busy-wait for keyboard interrupt (Ctrl+C)
...
```

这个通常用来创建最小类（minimal classes）：

```python
>>> class MyEmptyClass:
...     pass
...
```

当写一段新的代码时，pass语句也可以用作占位符（place-holder），在函数（function）或者条件体（conditional body）中。使你可以继续思考一个更抽象的层次（at a more abstract level）。pass语句被无声地忽略了：

```python
>>> def initlog(*args):
...     pass   # Remember to implement this!
...
```

## 4.6 定义函数（defining functions）

我们可以穿件一个用来生成指定边界的斐波那契数列的函数：

```python
>>> def fib(n):    # write Fibonacci series up to n
...     """Print a Fibonacci series up to n."""
...     a, b = 0, 1
...     while a < n:
...         print(a, end=' ')
...         a, b = b, a+b
...     print()
...
>>> # Now call the function we just defined:
... fib(2000)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987 1597
```

关键字 def 引入了一个函数 定义。在其后必须跟有函数名和包括形式参数的圆括号。函数体语句从下一行开始，必须是缩进的。

函数体的第一行语句可以是可选的字符串文本，这个字符串是函数的文档字符串，或者称为 docstring。（更多关于 docstrings 的信息请参考 文档字符串） 有些工具通过 docstrings 自动生成在线的或可打印的文档，或者让用户通过代码交互浏览；在你的代码中包含 docstrings 是一个好的实践，让它成为习惯吧。

函数 调用 会为函数局部变量生成一个新的符号表。确切的说，所有函数中的变量赋值都是将值存储在局部符号表。变量引用首先在局部符号表中查找，然后是包含函数的局部符号表，然后是全局符号表，最后是内置名字表。因此，全局变量不能在函数中直接赋值（除非用 global 语句命名），尽管他们可以被引用。

函数引用的实际参数在函数调用时引入局部符号表，因此，实参总是 传值调用 （这里的 值 总是一个对象 引用 ，而不是该对象的值）。一个函数被另一个函数调用时，一个新的局部符号表在调用过程中被创建。

一个函数定义会在当前符号表内引入函数名。函数名指代的值（即函数体）有一个被 Python 解释器认定为 用户自定义函数 的类型。 这个值可以赋予其他的名字（即变量名），然后它也可以被当做函数使用。这可以作为通用的重命名机制:

```python
>>> fib
<function fib at 10042ed0>
>>> f = fib
>>> f(100)
0 1 1 2 3 5 8 13 21 34 55 89
```

如果你使用过其他语言，你可能会反对说：fib 不是一个函数，而是一个方法，因为它并不返回任何值。事实上，没有 return 语句的函数确实会返回一个值，虽然是一个相当令人厌烦的值（指 None ）。这个值被称为 None （这是一个内建名称）。如果 None 值是唯一被书写的值，那么在写的时候通常会被解释器忽略（即不输出任何内容）。如果你确实想看到这个值的输出内容，请使用 print() 函数:

```python
>>> fib(0)
>>> print(fib(0))
None
```

定义一个返回斐波那契数列数字列表的函数，而不是打印它，是很简单的：

```python
>>> def fib2(n): # return Fibonacci series up to n
...     """Return a list containing the Fibonacci series up to n."""
...     result = []
...     a, b = 0, 1
...     while a < n:
...         result.append(a)    # see below
...         a, b = b, a+b
...     return result
...
>>> f100 = fib2(100)    # call it
>>> f100                # write the result
[0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89]
```

和以前一样，这个例子演示了一些新的Python的功能：

- return语句从函数中返回一个值，不带表达式的return返回None。过程结束后也会返回None。

- 语句 return.append(b)称为链表对象result的一个方法。方法是一“属于”个某个对象的函数，它被命名为obj.methodename，这里的obj是某个对象（可能是一个表达式），methodename是某个在该对象类型定义中的方法的命名。

不同的类型定义不同的方法。不同类型可能有同样名字的方法，但不会混淆。（当你定义自己的对象类型和方法时，可能会出现这种情况，class的定义方法详见“类”）。示例中演示的append()方法由链表对象定义，它向链表中加入一个新元素。在示例中

## 4.7 更多关于定义函数

在Python中，你也可以定义包含若干参数的函数。这里有三种可用的形式，也可以混合使用。

### 4.7.1 默认参数值（Default Argument Values）

最常用的一种形式是为一个或多个参数指定默认值。这会创建一个可以使用比定义时允许的参数更少的参数调用的函数。

```python
def ask_ok(prompt, retries=4, complaint='Yes or no, please!'):
    while True:
        ok = input(prompt)
        if ok in ('y', 'ye', 'yes'):
            return True
        if ok in ('n', 'no', 'nop', 'nope'):
            return False
        retries = retries - 1
        if retries < 0:
            raise OSError('uncooperative user')
        print(complaint)
```

这个函数可以通过集中不同的方式调用：

- 只给出必要的参数：

   ```python
   ask_ok('Do you really want to quit?')
   ```

- 给出一个可选的参数：

   ```python
   ask_ok('OK to overwrite the file?', 2)
   ```

- 或者给出所有的参数：

   ```python
   ask_ok('OK to overwrite the file?', 2, 'Come on, only yes or no!')
   ```

这个例子还介绍了in关键字。它测定序列中是否包含某个确定的值。

默认值在函数定义作用阈被解析，如下所示：

```python
i = 5

def f(arg=i):
    print(arg)

i = 6
f()
```

将会输出 5

重要警告：默认值只被赋值一次。这使得当默认值是可变对象时会有所不同，比如列表、字典或者大多数类的实例。例如，下面的函数在后续调用过程中会累积（前面）传给它的参数:

```python
def f(a, L=[]):
    L.append(a)
    return L

print(f(1))
print(f(2))
print(f(3))
```

这将输出：

```python
[1]
[1, 2]
[1, 2, 3]
```

如果你不想让默认值在后续调用中积累，可以这样定义函数：

```python
def f(a, L=None):
    if L is None:
        L = []
    L.append(a)
    return L
```

### 4.7.2 关键字参数（Keyword Arguments）

### 4.7.3 任意参数列表（Arbitrary Argument Lists）

### 4.7.4 分拆参数列表（Unpacking Argument Lists）

### 4.7.5 Lambda表达式（Lambda Expressions）

### 4.7.6 文档字符串（Documentation Strings）

### 4.7.7 函数注释（Annotations）

## 4.8 Intermezzo: 编码风格（Coding Style）
