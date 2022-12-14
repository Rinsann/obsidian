## Python 之 集合

### 什么是集合

1. 集合（set）是一个无序的不重复元素序列
2. 常用来对两个列表进行交并差的处理性
3. 集合与列表一样，支持所有的数据类型   `{'name',1,'xiaomu'}`


### 集合与列表的区别

 - 列表是有序的，集合是无序的
 - 列表可以重复，集合不能重复
 - 列表用于数据的使用，集合用于数据的交集并集差集的获取
 - 列表有索引，集合没有索引
 - 列表符号` [] [1,2,3]`，集合符号`{} {1,2,3}`


### 集合的创建方法

- 通过 `set` 函数来创建集合，不能使用 `{}` 来创建空集合
```python
a_set = set()  -> 空集合
a_set = set([1,2,3]) -> 传入列表或元组
b_set = {1,2,3} -> 传入元素
c_set = {} -> 错误，会被认为是字典类型
```

### 集合中的函数

- 常用的有 `add`函数、`update` 函数、`remove` 函数、`clear` 函数、`del` 删除集合

**`add` 的功能**

用于在集合中添加一个元素，如果集合中已存在该元素则该函数不执行
用法：
			`set.add(item)`
参数：
			`item`：要添加到集合中的元素
返回值：无返回值

```python
a_list = ['python', 'django', 'django', 'flask']  
a_set = set()  

a_set.add(a_list[0])  
a_set.add(a_list[1])  
a_set.add(a_list[2])  
a_set.add(a_list[-1])  
print(a_set)  
  
a_set.add(True)  
a_set.add(None)  
print(a_set)
```

**`update` 的功能**

- 加入一个新的集合（或列表、元组、字符串），如新集合内的元素在原集合中存在则无视。

用法：`set.update(iterable)`
参数：`iterable` 集合，列表、元组、字符串
返回值：无返回值，直接作用于原集合

```python
a_tuple = ('a', 'b', 'c')  
a_set.update(a_tuple)  
print(a_set)  
a_set.update('python')  
print(a_set)
```


**`remove` 的功能**

- 将集合中的某个元素删除，如果元素不存在则会报错

用法：`set.remove(item)`  # 注意元素不是索引
参数：`item` 当前集合中的一个元素
返回值：无返回值，直接作用于原集合

```python
a_set = {1,2,3}
a_set.remove(3)

print(a_set) # {1, 2}
```

**`clear` 函数的功能**

- 清空当前集合中的所有元素

用法：`set.clear()`  
参数：无
返回值：无返回值，直接作用于原集合

```python
a_set = {1,2,3}
a_set.clear()

print(a_set) # set()
```

**`del` 删除集合**

- `del` 可以直接将变量完全删除
- 集合没有索引，所以`del`无法进行索引删除，`del`只能删除集合对象自身

```python
a_set = {1,2,3}
del a_set
print(a_set) # 报错
```

**关于集合的说明**

- 集合无法通过索引获取元素
- 集合无直接获取元素的任何方法
- 集合只是用来处理列表和元组的一种临时类型，它不适合存储与传输


### 集合的差集 --- `difference`函数

#### 什么是差集
- `a,b` 两个集合，由所有属于`a`且不属于`b`的元素组成的集合叫做`a`于`b`的差集
![[Pasted image 20221002105939.png]]

#### `difference` 的功能

- 返回集合的差集，即返回的集合元素包含在第一个集合中，但不包含在第二个集合（方法的参数）中

#### `difference` 的用法

用法：
			`a_set.difference(b_set)`
参数：
			`b_set`：当前集合需要对比的集合
返回值：
			返回原始集合与对比集合的差集

```python
  
drivers = ['xiaomu', 'xiaoming', 'xiaomeng','xiaohong']  
testers = ['xiaomu', 'xiaoming', 'xiaogang', 'xiaotao']  
  
drivers_set = set(drivers)  
testers_set = set(testers)  
  
sample_drivers = drivers_set.difference(testers_set)  
  
print(sample_drivers)
```

### 集合的交集---`intersection`函数

#### 什么是交集

- `a,b` 两个集合分别拥有的并且相同的元素集，称之为`a`与`b`的交集

![[Pasted image 20221002110708.png]]
#### `intersection` 的功能

`intersection` 可以返回两个或者更多集合中都包含的元素，即交集

#### `intersection` 的用法

用法：
			`a_set.intersection(b_set...)`
参数：
			`b_set...`：当前集合需要对比的1个或者多个集合
返回值：
			返回原始集合与对比集合的交集


```python
a = ['xiaowang', 'xiaohong', 'xiaoli', 'zhangsan']  
b = ['xiaohong', 'xiaohong', 'wanggang', 'zhangsan']  
c = ['lihua', 'wangwu', 'wanggang', 'zhangsan']  
  
a_set = set(a)  
b_set = set(b)  
c_set = set(c)  
  
print(a_set, b_set, c_set)  
xiaotou = list(a_set.intersection(b_set, c_set))  
print('{} 是小偷 '.format(xiaotou[0]))
```


### 集合的并集--- `union` 函数

#### 什么是并集

- `a,b` 两个集合中所有的元素（去掉重复）即为 `a`与 `b` 的并集

![[Pasted image 20221002111858.png]]

#### `union` 函数的功能

`union` 函数返回多个集合的并集，即包含了所有集合的元素，重复的元素只会出现一次

#### `union` 函数的用法

用法：
			`a_set.union(b_set...)`
参数：
			`b_set...`：与当前集合需要对比的1个或者多个集合
返回值：
			返回原始集合与对比集合的并集

```python
a_school = ['周五半天', '周末培训', '周五休息']  
b_school = ['增加社团活动', '体育课', '周五半天']  
c_school = ['作业少留点', '周末培训', '改善伙食']  
  
a_set = set(a_school)  
b_set = set(b_school)  
c_set = set(c_school)  
  
print(a_set, b_set, c_set)  
  
# help_data = a_set.union(b_set, c_set)  
help_data = a_set.union(b_school, c_school)  # 除了可以使用集合，union同样对列表起作业  
print(help_data, len(help_data))
```


### 集合的 `isdisjoint` 函数

####  `isdisjoint` 函数的功能

用于判断两个集合是否包含相同的元素，如果没有返回 `True`，否则返回 `False`

####  `isdisjoint` 函数的用法


用法：
			`a_set.isdisjoint(b_set)`
参数：
			`b_set`：与当前集合用来作判断的集合
返回值：
			返回一个布尔值 `True` 或者 `False`

```python
# coding:utf-8  
  
company_not_allow = {'Men', '喝酒', '抽烟', '打牌'}  
  
one_player = {'female', '跑步', '早起', '喝酒'}  
  
tow_player = {'Men', '生活规律', '跆拳道'}  
three_player = {'female', '太极拳'}  
four_player = {'female', '空手道', '年轻'}  
  
print(company_not_allow.isdisjoint(one_player))  
print(company_not_allow.isdisjoint(tow_player))  
print(company_not_allow.isdisjoint(three_player))  
print(company_not_allow.isdisjoint(four_player))
```


