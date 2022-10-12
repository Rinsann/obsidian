### 字符串与数字直接的转换

- 什么是类型转换，为什么要做类型转换
- 字符串与数字直接的转换要求
- 字符串与数字之间的转换函数

#### 什么是类型转换，为什么要做类型转换

- 将自身数据类型变成新的数据类型，并拥有新的数据类型的所有功能的过程即为类型转换

`a = '1'`  # 无法做数字操作

为了方便更好的处理业务，将类型变更为更适合业务场景的类型

#### 字符串与数字直接的转换要求

- `str` => `number` ：数字组成的字符串，不能有字母或其它符号出现  `int_str = '103245365' or float_str = '3.14159'`
- `number` => `str`：无要求

#### 字符串与数字之间的转换函数

![[Pasted image 20221004214113.png]]


```python
# coding:utf-8  
  
int_data = 12  
float_data = 3.14  
  
str_int_data = str(int_data)  
str_float_data = str(float_data)  
  
print(str_int_data, type(str_int_data), str_float_data, type(str_float_data))  # 12 <class 'str'> 3.14 <class 'str'>  
  
zero_number = 0  
_number = -1  
str_zero_number = str(zero_number)  
str_numer = str(_number)  
print(str_zero_number, type(str_zero_number), str_numer, type(str_numer))  # 0 <class 'str'> -1 <class 'str'>  
  
str_float = '3.14'  
str_int = '123456'  
  
real_float = float(str_float)  
real_int = int(str_int)  
print(real_float, type(real_float), real_int, type(real_int))  # 3.14 <class 'float'> 123456 <class 'int'>  
  
mix_str = '123a'  
# print(float(mix_str))  # ValueError: could not convert string to float: '123a'  
  
float_data_str = '3.14'  
# test_data = int(float_data_str)  
# print(test_data, type(test_data)) # ValueError: invalid literal for int() with base 10: '3.14'  
test_data = float(float_data_str)  
print(test_data, type(test_data))  # 3.14 <class 'float'>  
  
int_data_str = '123'  
test_data_int = float(int_data_str)  
print(test_data_int, type(test_data_int))  # 123.0 <class 'float'>
```



### 字符串与列表之间的转换

- 字符串转列表的函数---`split`
- 列表转字符串的函数---`join`


#### 字符串转列表之`split`函数功能

- 将字符串以一定规则切割转成列表


#### 字符串转列表之split函数用法

用法：
			`string.split(seq=None,maxsplit=-1)`
参数：
			`seq`：切割的规则符号，不填写，默认空格，如字符串无空格则不分割生成列表
			`maxsplit`：根据切割符号切割的次数，默认-1不限制
返回值：
			返回一个列表


```python
# coding:utf-8  
  
a = 'abc'  
print(a.split())  
  
b = 'a,b,c'  
print(b.split(','))  
  
c = 'a|b|c|d'  
print(c.split('|', 1))  
  
d = 'a|b|c|d'  
print(d.split('|', 2))  
  
f = 'a~b~c'  
print(f.split(''))  # ValueError: empty separator split('')的参数不能传空字符串
```

#### 列表转字符串之`join`函数

- 将列表以一定规则转换成字符串


#### 列表转字符串之`join`用法

用法：
			`sep.join(iterable)`
参数：
			`sep`：生成字符串用来分割列表每个元素的符号
			`iterable`：非数字类型的列表或元祖或集合
返回值：
			返回一个字符串

```python
  
test = ['a', 'b', 'c']  
test_str = '|'.join(test)  
print(test_str)  
  
test2 = [1, 2, 3]  
# print('|'.join(test2)) # TypeError: sequence item 0: expected str instance, int found  
  
test3 = [{'name': 'rick'}, {'name': 'xiaoming'}]  
# print('.'.join(test3)) # TypeError: sequence item 0: expected str instance, dict found  
  
sort_str = 'a b d f i p q c'  
sort_list = sort_str.split()  
print(sort_list)  
sort_list.sort()  
print(sort_list)  
sort_str = ''.join(sort_list)  
print(sort_list)  
  
sort_str_new = 'abdfipqc'  
print(sort_str_new)  
res = sorted(sort_str_new)  
print(res)  
print(''.join(res))
```


### 字符串与`bytes`的转换

#### 什么是比特类型

- 二进制的数据流---`bytes`
- 在`python`可以理解为一种特殊的字符串
- 字符串的前面添加一个 `b` 的标记就是`bytes`类型

> `dir(x)`  `dir`可以将传入参数的对应类型其相关函数全部打印出来

```python
# coding:utf-8  
  
a = 'hello xiaoming'  
print(a, type(a))  # hello xiaoming <class 'str'>  
  
b = b'hello xiaoming'  
print(b, type(b))  # b'hello xiaoming' <class 'bytes'>  
  
print(b.capitalize())  
# print(b.replace('xiaoming','xiaohong')) # TypeError: a bytes-like object is required, not 'str'  
print(b.replace(b'xiaoming', b'xiaohong'))  # TypeError: a bytes-like object is required, not 'str'  
print(b[:3])  
print(b.find(b'x'))  
  
print(dir(b))  # dir 将对应类型的相关函数全部打印出来  
'''  
带下划线的是属性  
['__add__', '__class__', '__contains__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__getnewargs__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__mod__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__rmod__', '__rmul__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__',   
 'capitalize', 'center', 'count', 'decode', 'endswith', 'expandtabs', 'find', 'fromhex', 'hex', 'index', 'isalnum', 'isalpha', 'isascii', 'isdigit', 'islower', 'isspace', 'istitle', 'isupper', 'join', 'ljust', 'lower', 'lstrip', 'maketrans', 'partition', 'removeprefix', 'removesuffix', 'replace', 'rfind', 'rindex', 'rjust', 'rpartition', 'rsplit', 'rstrip', 'split', 'splitlines', 'startswith', 'strip', 'swapcase', 'title', 'translate', 'upper', 'zfill']  
'''  
  
c = b'hello 小明'  
print(c) # SyntaxError: bytes can only contain ASCII literal characters
```

#### 字符串转 `bytes` 的函数 --- `encode` 函数

- `encode` 可以将字符串转换成比特(`bytes`)类型

用法：
			`string.encode(encodeing='utf-8',errors='strict')`
参数：
			`encode`：转换成的编码格式，如 `ascii`，`gbk`，默认 `utf-8`
			`errors`：出错时的处理方法。默认 `strict`，直接抛出错误，也可以选择 ignore 忽略错误
返回值：
			返回一个比特(`bytes`)类型

#### `bytes` 转字符串的函数 --- `decode`

- 将比特（`bytes`）类型转换成字符串

用法：
			`bytes.decode(encodeing='utf-8',errors='strict')`
参数：
			`encode`：转换成的编码格式，如 `ascii`，`gbk`，默认 `utf-8`
			`errors`：出错时的处理方法。默认 `strict`，直接抛出错误，也可以选择 ignore 忽略错误
返回值：
			返回一个字符串类型

```python
  
c = 'hello 小明'  
d = c.encode('utf-8')  
print(d, type(d))  # b'hello \xe5\xb0\x8f\xe6\x98\x8e' <class 'bytes'>
print(d.decode('utf-8')) # hello 小明
```

### 元祖、列表、集合之间的转换

#### 列表元祖集合间的转换函数

![[Pasted image 20221005111747.png]]

```python
# coding:utf-8  
  
a = [1, 2, 3]  
b = (1, 2, 3)  
c = {1, 2, 3}  
  
print(type(tuple(a)), type(set(a)))  # <class 'tuple'> <class 'set'>  
print(tuple(a) == b)  # True  
print(set(a) == c)  # True  
print(tuple(a) is b)  # False 不是相同的内存地址  
print(set(a) is c)  # False  
  
print(list(b), set(b))  
print(list(c), tuple(c))  
  
print(list(a))  
  
print(str(a), type(str(a)))  # print(str(a), type(str(a))) #  
print(str(b), type(str(b)))  # (1, 2, 3) <class 'str'>  
print(str(c), type(str(c)))  # {1, 2, 3} <class 'str'>  
  
print(list(str(a)))  # ['[', '1', ',', ' ', '2', ',', ' ', '3', ']']
```






