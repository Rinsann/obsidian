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


#### 字符串转列表之`split`函数









































