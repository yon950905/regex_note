# 正则表达式

## group()与groups()

m.group(N) 返回第N组括号匹配的字符。
而m.group() == m.group(0) == 所有匹配的字符，与括号无关，这个是API规定的。
m.groups() == (m.group(1), m.group(2), ...)。

例：

```python
import re

s = '123-456-789'
r = re.match(r'(\d+)-(\d+)-(\d+)', s)
print(r.group(0))
print(r.group(1))
print(r.group(2))
print(r.group(3))
print(r.groups())
```

输出：

```
123-456-789
123
456
789
('123', '456', '789')
```



## findall()与finditer()

例：

```python
r = re.findall(r'(\d+)', s)
print(r)
r = re.findall(r'(\d+)-(\d+)-(\d+)', s)
print(r)
```

输出：

```
['123', '456', '789']
[('123', '456', '789')]
```

finditer()生成findall()的迭代器版本。

```python
for match in re.finditer(r'(\d+)', s):
    print(match.group())
```

输出：

```
123
456
789
```



## Flags

### re.S (re.DOTALL)

让`.`也匹配`/n`。

例：

```python
s = 'ML\nand AI'
result = re.search(r'.+', s)
print("Without using re.S flag:", result.group())

result = re.search(r".+", s, re.S)
print("With re.S flag:", result.group())

result = re.search(r".+", s, re.DOTALL)
print("With re.DOTALL flag:", result.group())
```

输出：

```
Without using re.S flag: ML
With re.S flag: ML
and AI
With re.DOTALL flag: ML
and AI
```

### re.M (re.MULTILINE)

#### 开启多行模式

`^`可以匹配字符串开头（字符串的开始位置），也可以匹配行的开头（即换行符`\n`之后的位置）。
`$`可以匹配字符串结尾（字符串的结束位置）, 也可以匹配行的结尾（即换行符`\n`之前的位置）。

#### 关闭多行模式

`^`只能匹配字符串开头。
`$`只能匹配字符串结尾。

例：

```python
s = '''As 3G passed by
No doubt 4G still alive
Have been expecting the upcoming 5G no longer a lie'''
r = re.findall(r'^No.+alive$', s)
print(r)
r = re.findall(r'^No.+alive$', s, re.MULTILINE)
print(r)
```

输出：

```
[]
['No doubt 4G still alive']
```

