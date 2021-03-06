# 数据结构

本章详细讨论了你已经学过的一些知识，同样也添加了一些新内容。

## 5.1 关于列表更多的内容

Python的列表数据类型包含更多的方法。这里是所有的列表对象方法：

```python
list.append(x)
```

 把一个元素添加到列表的结尾，相当于 a[len(a):] = [x] 。

```python
list.extend(L)
```

  将一个给定列表中的所有元素都添加到另一个列表中，相当于 a[len(a):] = L。
  
```python
list.insert(i,x)
```

 在指定位置插入一个元素。第一个参数是准备插入到其前面的那个元素的索引，例如 a.insert(0, x) 会插入到整个列表之前，而 a.insert(len(a), x) 相当于 a.append(x)。
  
```python
list.remove(x)
```

 删除列表中值为x的第一个元素。如果没有这样的元素，就会返回一个错误。
 
```python
list.pop([i])
```
 
 从列表的指定位置删除元素，并将其返回。如果没有指定索引，a.pop()返回最后一个元素。元素随即从列表中被删除（方法中i两边的方括号表示这个参数是可选的，而不是要求你输入一对方括号，你会经常在Python库参考手册中遇到这样的标记）。
 
```python
list.clear()
```
 
 从列表中删除所有元素。相当于del a[:]

```python
list.index(x)
```

 返回列表中第一个值为x的元素的索引。如果没有匹配的元素就会返回一个错误。
 
```python
list.count(x)
```

 返回x在列表中出现的次数。

```python
list.sort()
```

 对列表中的元素就地进行排序。

```python
list.reverse()
```

 就地倒排列表中的元素。

```python
list.copy()
```

 返回列表的一个浅拷贝。等同于a[:]。
 
下面这个示例演示了列表的大部分方法：

```python
>>> a = [66.25, 333, 333, 1, 1234.5]
>>> print(a.count(333), a.count(66.25), a.count('x'))
2 1 0
>>> a.insert(2, -1)
>>> a.append(333)
>>> a
[66.25, 333, -1, 333, 1, 1234.5, 333]
>>> a.index(333)
1
>>> a.remove(333)
>>> a
[66.25, -1, 333, 1, 1234.5, 333]
>>> a.reverse()
>>> a
[333, 1234.5, 1, 333, -1, 66.25]
>>> a.sort()
>>> a
[-1, 1, 66.25, 333, 333, 1234.5]
>>> a.pop()
1234.5
>>> a
[-1, 1, 66.25, 333, 333]
```
或者是：
 
```python
>>> fruits = ['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
>>> fruits.count('apple')
2
>>> fruits.count('tangerine')
0
>>> fruits.index('banana')
3
>>> fruits.index('banana', 4)  # Find next banana starting a position 4
6
>>> fruits.reverse()
>>> fruits
['banana', 'apple', 'kiwi', 'banana', 'pear', 'apple', 'orange']
>>> fruits.append('grape')
>>> fruits
['banana', 'apple', 'kiwi', 'banana', 'pear', 'apple', 'orange', 'grape']
>>> fruits.sort()
>>> fruits
['apple', 'apple', 'banana', 'banana', 'grape', 'kiwi', 'orange', 'pear']
>>> fruits.pop()
'pear'
```

也许大家会发现像insert，remove或者sort这些只是修改（modify）了列表，但没有打印返回值-它们返回默认值（default）None。在Python中对所有可变的数据类型这是统一的设计原则。

### 5.1.1 把列表当做堆栈（Stacks）使用

列表的这些方法使得它被用作一个堆栈使用会很方便，堆栈最为特定的数据结构，最先进入的元素最后一个释放（相反，后进先出，last-in，first-out）。

用append()方法可以把一个元素添加到堆栈顶。用不指定索引的pop()方法可以把一个元素从堆栈顶释放出来。例如：

```python
>>> stack = [3, 4, 5]
>>> stack.append(6)
>>> stack.append(7)
>>> stack
[3, 4, 5, 6, 7]
>>> stack.pop()
7
>>> stack
[3, 4, 5, 6]
>>> stack.pop()
6
>>> stack.pop()
5
>>> stack
[3, 4]
```

### 5.1.2 把列表仿作队列（Queues）使用

列表也可以作为队列使用，队列作为特定的数据结构，最先进入的元素最先释放（先进先出）。但是，这样使用列表效率不高。

相对来说，从列表末尾添加(appends)和弹出(pops)很快；在头部插入(inserts)和弹出(pops)很慢。（因为，所有的元素都必须移动一位）

要实现一个队列，可以使用collections.deque，这个collection.deque被设计成添加和从两端弹出。 例如：

```python
>>> from collections import deque
>>> queue = deque(["Eric", "John", "Michael"])
>>> queue.append("Terry")           # Terry arrives
>>> queue.append("Graham")          # Graham arrives
>>> queue.popleft()                 # The first to arrive now leaves
'Eric'
>>> queue.popleft()                 # The second to arrive now leaves
'John'
>>> queue                           # Remaining queue in order of arrival
deque(['Michael', 'Terry', 'Graham'])
```

### 5.1.3 函数式编程工具

在使用列表时有三个函数非常有用：filter()、map()和reduce()。

filter(function, sequence)返回的序列由function(item)结果为真的元素组成。如果sequence是一个字符串或元组，结果将是相同的类型；否则，结果将始终是一个列表。例如，若要计算一个不能被2和3整除的序列：

```python
>>> def f(x): return x % 2 != 0 and x % 3 != 0
...
>>> filter(f, range(2, 25))
[5, 7, 11, 13, 17, 19, 23]
```

map(function, sequence) 为序列中的每一个元素调用 function(item) 函数并返回结果的列表。例如，计算列表中所有元素的立方值：

```python
>>> def cube(x): return x*x*x
...
>>> map(cube, range(1, 11))
[1, 8, 27, 64, 125, 216, 343, 512, 729, 1000]
```

可以传入多个序列；此时，传入的函数也必须要有和序列数目相同的参数，执行时会依次用各序列上对应的元素来调用函数（如果某个序列比另外一个短，就用 None 代替）。例如：

```python
>>> seq = range(8)
>>> def add(x, y): return x+y
...
>>> map(add, seq, seq)
[0, 2, 4, 6, 8, 10, 12, 14]
```

reduce(function, sequence) 只返回一个值，它首先以序列的前两个元素调用函数 function，然后再以返回的结果和下一个元素继续调用，依此执行下去。例如，若要计算数字 1 到 10 的总和：

```python
>>> def add(x,y): return x+y
...
>>> reduce(add, range(1, 11))
55
```

如果序列中只有一个元素，将返回这个元素的值；如果序列为空，则引发异常。

可以传入第三个参数作为初始值。在这种情况下，如果序列为空则返回起始值，否则会首先以初始值和序列的第一个元素调用function，然后是返回值和下一个元素，依此执行下去。例如，

```python
>>> def sum(seq):
...     def add(x,y): return x+y
...     return reduce(add, seq, 0)
...
>>> sum(range(1, 11))
55
>>> sum([])
0
```

不要使用示例中定义的sum()：由于计算数字的总和是一个如此常见的需求，Python提供了内置的函数sum(sequence)，其工作原理和示例几乎一样。

### 5.1.4 列表推导式（List Comprehensions）

列表推导式

### 5.1.5 嵌套列表推导式（Nested List Comprehensions）

列表推导式的最初始表达式可以是任意的表达式，包括另一个列表推导式。

思考一下下面这个例子，一个3x4的矩阵，也就是3个长度为4的列表：

```python
>>> matrix = [
...     [1, 2, 3, 4],
...     [5, 6, 7, 8],
...     [9, 10, 11, 12],
... ]
```

下面的列表表达式会将行（rows）和列（columns）转置（transpose），如果想交换行和列，就用嵌套列表推导式：

```python
>>> [[row[i] for row in matrix] for i in range(4)]
[[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]
```

像前面看到的，嵌套的列表推导式是对for后面的内容进行求值，所以上列就等价于：

```python
>>> transposed = []
>>> for i in range(4):
...     transposed.append([row[i] for row in matrix])
...
>>> transposed
[[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]
```

反过来说，如下也是一样的：

```python
>>> transposed = []
>>> for i in range(4):
...     # the following 3 lines implement the nested listcomp
...     transposed_row = []
...     for row in matrix:
...         transposed_row.append(row[i])
...     transposed.append(transposed_row)
...
>>> transposed
[[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]
```

在实际中，你应该更喜欢使用内置函数组成复杂流程语句。对此种情况zip()函数将会做得更好：

```python
>>> list(zip(*matrix))
[(1, 5, 9), (2, 6, 10), (3, 7, 11), (4, 8, 12)]
```

更多关于上面星号的用法说明，参考 参数列表的分拆。

## 5.2 del语句

有个方法可以从列表中按给定的索引而不是值来删除一个子项： del 语句。它不同于有返回值的 pop() 方法。语句 del 还可以从列表中删除切片或清空整个列表（我们以前介绍过一个方法是将空列表赋值给列表的切片）。例如:

```python
>>> a = [-1, 1, 66.25, 333, 333, 1234.5]
>>> del a[0]
>>> a
[1, 66.25, 333, 333, 1234.5]
>>> del a[2:4]
>>> a
[1, 66.25, 1234.5]
>>> del a[:]
>>> a
[]
```

del也可以删除整个变量：

```python
>>> del a
```

此后再引用a会引发错误（直到另一个值赋给它为止）。我们在后面的内容中可以看到del的其他用法。

## 5.3 元组和序列

我们看到列表和字符串有许多常见的属性，如索引和切片操作。有两种序列数据类型（参见序列类型——列表、元组、range）。由于Python是一种演进的语言，可以添加其他序列数据类型。还有另一种标准序列数据类型：元组。

元组由一组用逗号分隔的值组成，例如：

```python
>>> t = 12345, 54321, 'hello!'
>>> t[0]
12345
>>> t
(12345, 54321, 'hello!')
>>> # Tuples may be nested:
... u = t, (1, 2, 3, 4, 5)
>>> u
((12345, 54321, 'hello!'), (1, 2, 3, 4, 5))
>>> # Tuples are immutable:
... t[0] = 88888
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment
>>> # but they can contain mutable objects:
... v = ([1, 2, 3], [3, 2, 1])
>>> v
([1, 2, 3], [3, 2, 1])
```

正如你所见，在输出中，元组总是位于圆括号中，所以嵌套的元组可以正确解析；输入的时候它们的周围可以放置圆括号也可以不放，然而圆括号经常是必要的（如果元组是一个更大的表达式的一部分）。不可能分配到元组的单个项目，但是可以创建包含可变对象（例如列表）的元组。

尽管元组可能看起来类似于列表，但它们通常用于不同的情况和不同的目的。元组是不可变的，通常包含各种各样的元素，这些元素通过分拆（参见本节的后面部分）或索引（或甚至是属性namedtuples）访问。序列是可变的，它们的元素通常是相同类型，并通过迭代列表来访问。

一个特殊的问题是构造包含0个或1个元素的元组：为了实现这种情况，语法上有一些奇怪。空的元组通过一对空的圆括号构造；只有一个元素的元组通过一个元素跟随一个逗号构造（仅用圆括号把一个值括起来是不够的）。丑陋，但有效。例如：

```python
>>> empty = ()
>>> singleton = 'hello',    # <-- note trailing comma
>>> len(empty)
0
>>> len(singleton)
1
>>> singleton
('hello',)
```

语句t = 12345, 54321, 'hello!'是元组封装的一个例子：值12345、54321和'hello!'被一起分封装在一个元组中。反向操作也是可能的：

```python
>>> x, y, z = t
```

这被称为序列分拆再恰当不过了，且可以用于右边的任何序列。序列分拆要求在等号的左侧有与序列中的元素一样多的变量。注意，多个赋值实际上只是元组封装和序列分拆的组合。

## 5.4 集合

Python还包括集的数据类型。集合是没有重复元素的无序容器。基本用法包括成员资格测试和消除重复条目。集合对象也支持数学运算，如并，交，差和对称差。

花括号或者set()函数可以用来创建集合。注意，你必须使用set()创建一个空的集合，而不能用{}；后面这种写法创建一个空的字典，我们将在下一节讨论这个数据结构。

这里是一个简要的演示：

```python
>>> basket = {'apple', 'orange', 'apple', 'pear', 'orange', 'banana'}
>>> print(basket)                      # show that duplicates have been removed
{'orange', 'banana', 'pear', 'apple'}
>>> 'orange' in basket                 # fast membership testing
True
>>> 'crabgrass' in basket
False

>>> # Demonstrate set operations on unique letters from two words
...
>>> a = set('abracadabra')
>>> b = set('alacazam')
>>> a                                  # unique letters in a
{'a', 'r', 'b', 'c', 'd'}
>>> a - b                              # letters in a but not in b
{'r', 'd', 'b'}
>>> a | b                              # letters in either a or b
{'a', 'c', 'r', 'd', 'b', 'm', 'z', 'l'}
>>> a & b                              # letters in both a and b
{'a', 'c'}
>>> a ^ b                              # letters in a or b but not both
{'r', 'd', 'b', 'm', 'z', 'l'}
```

类似于列表推导式，这里有一种集合推导式语法：

```python 
>>> a = {x for x in 'abracadabra' if x not in 'abc'}
>>> a
{'r', 'd'}
```

## 5.5 字典

另一个非常有用的 Python 内建数据类型是 字典 （参见 Mapping Types — dict ）。字典在某些语言中可能称为 联合内存 （ associative memories ）或 联合数组 （ associative arrays ）。序列是以连续的整数为索引，与此不同的是，字典以 关键字 为索引，关键字可以是任意不可变类型，通常用字符串或数值。如果元组中只包含字符串和数字，它可以做为关键字，如果它直接或间接的包含了可变对象，就不能当做关键字。不能用列表做关键字，因为列表可以用索引、切割或者 append() 和 extend() 等方法改变。

理解字典的最佳方式是把它看做无序的键： 值对 （key:value 对）集合，键必须是互不相同的（在同一个字典之内）。一对大括号创建一个空的字典： {} 。初始化列表时，在大括号内放置一组逗号分隔的键：值对，这也是字典输出的方式。

字典的主要操作是依据键来存储和析取值。也可以用 del 来删除键：值对（key:value）。如果你用一个已经存在的关键字存储值，以前为该关键字分配的值就会被遗忘。试图从一个不存在的键中取值会导致错误。

对一个字典执行 list(d.keys()) 将返回一个字典中所有关键字组成的无序列表（如果你想要排序，只需使用 sorted(d.keys()) ）。使用 in 关键字（指Python语法）可以检查字典中是否存在某个关键字（指字典）。

这里是使用字典的一个小示例:

```python
>>> tel = {'jack': 4098, 'sape': 4139}
>>> tel['guido'] = 4127
>>> tel
{'sape': 4139, 'guido': 4127, 'jack': 4098}
>>> tel['jack']
4098
>>> del tel['sape']
>>> tel['irv'] = 4127
>>> tel
{'guido': 4127, 'irv': 4127, 'jack': 4098}
>>> list(tel.keys())
['irv', 'guido', 'jack']
>>> sorted(tel.keys())
['guido', 'irv', 'jack']
>>> 'guido' in tel
True
>>> 'jack' not in tel
False
```

dict()构造函数可以直接从key-value对中创建字典：

```python
>>> dict([('sape', 4139), ('guido', 4127), ('jack', 4098)])
{'sape': 4139, 'jack': 4098, 'guido': 4127}
```

此外，字典推导式可以从任意的键值表达式中创建字典:

```python
>>> {x: x**2 for x in (2, 4, 6)}
{2: 4, 4: 16, 6: 36}
```

如果关键字都是简单的字符串，有时通过关键字参数指定 key-value 对更为方便:


```python
>>> dict(sape=4139, guido=4127, jack=4098)
{'sape': 4139, 'jack': 4098, 'guido': 4127}
```

## 5.6 循环技巧

## 5.7 深入条件控制

## 5.8 比较序列和其他类型
