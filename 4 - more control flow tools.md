# 更多的控制流程工具（control flow tools）

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

## 4.4 break和continue声明，循环中的else子句（clause）

## 4.5 pass声明

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
