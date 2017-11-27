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

3.1.1 数字

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