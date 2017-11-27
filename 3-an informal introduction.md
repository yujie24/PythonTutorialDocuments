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

## 3.1 将Python用作计算器

打开解释器，在提示符之后开始键入。

### 3.1.1 数字

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



