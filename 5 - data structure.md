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

下面的列表表达式会将行（rows）和列（columns）转置（transpose）：

```python
>>> [[row[i] for row in matrix] for i in range(4)]
[[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]
```

## 5.2 del语句

## 5.3 元组和序列

## 5.4 集合

## 5.5 字典

## 5.6 循环技巧

## 5.7 深入条件控制

## 5.8 比较序列和其他类型
