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

也许大家会发现像insert，remove或者sort这些修改列表的方法没有打印返回值-它们返回None。在Python中对所有可变的数据类型这是同意的设计原则。

### 5.1.1 把列表当做堆栈（Stacks）使用



## 5.2 del语句

## 5.3 元组和序列

## 5.4 集合

## 5.5 字典

## 5.6 循环技巧

## 5.7 深入条件控制

## 5.8 比较序列和其他类型
