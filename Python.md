# 要点

- 变量名里不能有$，官方推荐用_下划线风格
- len()获取字符串的长度，py的字符串没有length属性
- +号的两边，类型必须一致，字符串不能和数字相加。类型转换：str(),int(),float()。int()只保留整数位会丢失小数位
- input()得到的值始终是字符串(即使输入数字)
- ==不会转换类型，'1'==1 是False
- 字符串*数字,'你好' * 3，得到 '你好你好你好'，str * n，得到n个str
- 0、0.00和''(空字符串)被认为是假值(False)，其他值被认为是真值(True)
- 与或非，不同于其他语言的 && || !，py用 and or not来表示与或非。!不能单独出现，只能和=一起用(!=)，表示不等（not是取反）
- python没有do-while和switch
- 强制退出程序，sys.exit()
- None，用法等同于js的null，但是不表示假值(False)。没有返回值的函数，默认的返回值是None
- 函数的定义和调用，中间要空一行代码，不然会语法错误。
- 在函数内修改全局变量，需要在变量名前加`global`关键字，否则python会把这个变量当局部变量处理。

# 异常处理

```python
try:
    num = int(input())
    print(type(num))
except Exception as e:
    print(e)
```

# 文件读写





# http





# python读文件：
```python
with open(path, 'r', encoding='utf-8') as f:
```
- `open()`读取文件返回文件流
- `with`和其他语言一样，文件流需要关闭，通常为了处理处理异常还要写try catch finaly语句，加上with,python会自动处理文件流关闭
- `path`文件路径，可以是相对路径或绝对路径
- `'r'`读取模式，r=只读，w=可以写入
- `encoding`指定编码，防止出现中文乱码
  
## 读取json
```python
#导入json模块
import json
with open('./score.json', 'r', encoding='utf-8') as file:
    #调用load方法，传入文件流参数
     userData = json.load(file)
```
- python没有对象，所以把json数据对象转成dict字典结构
- 使用从json读取的对象，要用`json['field']`语法格式

# 数据类型
## 数组list
```python
arr = [1, 2, 3]
```

和其他语言一样，数组支持用下标访问。和字符串一样，数组没有length属性，需要用`len()`函数来获取数组的长度。

python的数组有一个其他语言没有的特性：切片。第一个数字表示起始下标，第二个数字表示结束下标(但不包含这个下标)

```python
arr = [1, 2, 3]
nums = arr[0:2] # 取下标0到下标2之间的数字（不包含下标2）
# [1, 2]

arr = [1, 2, 3, 4, 5]
nums = arr[1:-1]
# [2, 3, 4]
```

数组的连接和复制，`+`将两个数组合并为一个新数组，`*`将数组复制n次

```python
[1, 2, 3] + ['a', 'b', 'c'] # 连接
# [1, 2, 3, 'a', 'b', 'c]

['X', 'Y', 'Z'] * 3 # 复制
# ['X', 'Y', 'Z', 'X', 'Y', 'Z', 'X', 'Y', 'Z']
```

删除数组里的元素，使用`del`关键字

```python
arr = [1, 2, 3, 4, 5]
del arr[1]
# [1, 3, 4, 5]
```

del还可以配合切片使用，删除多个元素

```python
arr = [1, 2, 3, 4, 5]
del arr[0:2]
# [3, 4, 5]
```

遍历数组，使用for in来遍历数组，此时的 i 指向数组里的元素

```python
for i in [1, 'AA', 2]:
    print(i)
# 1 AA 2
```

配合len()函数使用

```python
stu = ['tom', 'jack', 'lily']
for i in range(len(stu)):
  print(i, stu[i])
# 0 tom
# 1 jack
# 2 lily
```

数组的查找，`in`和`not in `

```python
stu = ['tom', 'jack', 'lily']
'tom' in stu
# True
'mary' not in stu
True
```










- list和js的数组一样，用下标操作元素
- `len()`list的长度
- `pop()`删除并返回最后一个元素，可以指定删除的下标`pop(i)`
- `append()`追加元素  

|表达式|结果|描述|
|----|----|----|
|len([1, 2, 3])|3|长度|
|[1, 2, 3] + [4, 5, 6]|[1, 2, 3, 4, 5, 6]|组合|
|['Hi!'] * 4|['Hi!', 'Hi!', 'Hi!', 'Hi!']|重复|
|3 in [1, 2, 3]|True|元素是否存在于列表中|
|for x in [1, 2, 3]: print x|1 2 3|迭代|

## 元组tuple
元组和list的唯一区别是元组长度不可变，没有append,insert方法
```python
#定义元组(多个元素)
tup = (1,2,3)
#单个元素（后面必须加逗号）
tup = (1,)
#元组转list
tup_list = list(tup)
```

## 字典dict
字典是键值对，对应JavaScript的对象类型。字典的键只能字符串，没有类似JavaScript map的get set方法，取值用`dict['key']`,添加新值和JavaScript对象动态追加属性一样，`dict['newKey']=''`
```python
# 遍历key (a = {'a': '1', 'b': '2', 'c': '3'})
for key in a:
       print(key+':'+a[key])

#遍历key
>>> for key in a.keys():
       print(key+':'+a[key])
a:1
b:2
c:3

#遍历value
>>> for value in a.values():
       print(value)
1
2
3

#遍历键值
>>> for key,value in a.items():
       print(key+':'+value)
a:1
b:2
c:3

#遍历Item
>>> for kv in a.items():
       print(kv)
('a', '1')
('b', '2')
('c', '3')
```





# 函数参数



# 控制流语句

## for 循环

基础用法，等同于for (let i=0; i<10; i++)

```python
for i in range(10):
	print(i)
# 0 1 2 3 4 5 6 7 8 9 (i < 10)
```

设置初始值，range在接收两个参数时，第一个参数表示初始值，第二个表示上限(不包含上限)

```python
for i in range(10, 15):
	print(i)
# 10 11 12 13 14 (i < 15)
```

设置步长，第三个参数表示递增的值，等同于 for (let i=0; i<10; i+=2)

```python
for i in range(0, 10, 2):
	print(i)
# 0 2 4 6 8 (i < 10)
```

递减循环，等同于for (let i=5; i>0; i--)

```python
for i in range(5, 0, -1):
	print(i)
# 5 4 3 2 1 (i > 0)
```





# 模块

导入模块，`import` 模块名称，可以同时导入多个模块

```python
import math, os, random, sys
```

random.randint(1, 10)，这句代码的意思是，使用random模块下的randint函数。在使用函数时要加模块名称，让python知道去哪个模块下找这个函数

使用import可以导入一整个模块，如果只需要用到模块里的某几个方法，可以用`from 模块名称 import 函数`语句，指定要导入的函数

```py
from os import path, name
```

