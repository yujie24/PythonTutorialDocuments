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

## 4.7 更多关于定义函数

### 4.7.1 默认参数值（Default Argument Values）

### 4.7.2 关键字参数（Keyword Arguments）

### 4.7.3 任意参数列表（Arbitrary Argument Lists）

### 4.7.4 解压参数列表（Unpacking Argument Lists）

### 4.7.5 Lambda表达式（Lambda Expressions）

### 4.7.6 文档字符串（Documentation Strings）

### 4.7.7 函数注释（Annotations）

## 4.8 Intermezzo: Coding Style
