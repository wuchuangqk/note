# 要点

- 变量名里不能有$，官方推荐用_下划线风格
- 数组和字段串都用len()函数获取长度，python的数组和字符串没有length属性
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
- 字符串是不可变的
- type()方法可以查看变量是什么类型
- python除法运算得到的结果都是float类型，不能用于数组下标。4 / 2 = 2.0
- 字符串查找也用in 和 not in，字符串切片只有get没有set，给切片赋值会报错，切片不能访问不存在的索引

# 异常处理

```python
try:
    num = int(input())
    print(type(num))
except Exception as e:
    print(e)
```

# 文件读写

## os模块

```python
import os
```



文件路径拼接，Windows和Linux的路径分隔符不一样。

```python
os.path.join('usr','bin','span')
# Windows 'usr\\bin\\span'
# Linux 'use/bin/span'
```



获取当前所在目录路径，cwd "current work directory"（当前工作目录）

```python
os.getcwd()
# 'D:\\Program Files\\Python311'
```



创建文件夹，os.makedirs()

```python
os.makedirs('fold1/fold2/fold3')
# 将依次创建 fold1 fold2 fold3 目录
```



列出目录下所有文件， os.listdir()

```python
os.listdir(':\\Users')
```



文件或目录重命名, os.rename(src, dst)。src要修改的文件或目录名，dst修改后的目录名

```py
import os

def re_name(path):
    for file in os.listdir(path):
        file_path = os.path.join(path, file)
        # 判断这个文件是否是文件夹，是文件夹的话就调用自己，把路径拼接好传过去
        if os.path.isdir(file_path):
            re_name(file_path)
        else:  # 如果不是文件夹，就开始改名字
            if "i.cnblogs .com" in file:
                file_new = file.replace("i.cnblogs.com", "")
                file_new_path = os.path.join(path, file_new)
                os.rename(file_path, file_new_path)

if __name__ == "__main__":
    path = r'F:\\BaiduNetdiskDownload\\'
    re_name(path)

```





## os.path模块

```python
from os import path
```

判断是否是文件，path.isfile()

```py
path.isfile('猜数字.py')
# 参数必须是相对路径或绝对路径
```



## open

读取一个文件，参数：文件路径，模式，可选参数：encoding(编码)。模式：r只读，w写入(覆盖)，a写入(追加)。r=read,w=write,a=append。使用后要记得调用close()关闭文件流。以写入模式打开的文件，不存在时会自动创建

```python
# hello.txt
hello world

# 只读
text_file = open('hello.txt', 'r', encoding='utf-8')
text_file.read()
# hello world

# 覆盖写入
text_file = open('hello.txt', 'w', encoding='utf-8')
text_file.write('new content')
# hello.txt new content

# 追加写入
text_file = open('hello.txt', 'a', encoding='utf-8')
text_file.write(' new content')
# hello.txt hello world new content

```







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

数组排序，`sort()`，只能对**纯数字数组**或**纯字符串数组**使用sort，不能混杂数字和字符串。sort会改变原数组。默认升序，可以传入**reverse=True**来降序排序。

```python
arr = [2, 5, 3.14, 1, -7]
arr.sort()
# [-7, 1, 2, 3.14, 5]
```



| 方法                                      | 示例                                               | 备注                         |
| ----------------------------------------- | -------------------------------------------------- | ---------------------------- |
| list.index(el) 查找元素在数组中的下标     | ['a','b','c'].index('a')，输出 0                   | 不存在会抛出异常而不是返回-1 |
| list.append(el) 追加元素到数组末尾        | ['a','b','c'].append('d')，输出['a','b','c','d']   |                              |
| list.insert(index, el) 在指定位置插入元素 | ['a','b','c'].insert(1,'d')，输出['a','d','b','c'] |                              |
| list.remove(el) 删除数组里的元素          | ['a','b','c'].remove('a')，输出['b','c']           | 删除不存在的元素会抛出异常   |


## 元组tuple
元组和list的区别是元组长度不可变，所以元组没有append、insert、remove等方法
```python
#定义元组(多个元素)
tup = (1,2,3)
#单个元素（后面必须加逗号）
tup = (1,)
```

元组转换成list

```python
tup = (1, 2, 3)
arr = list(tup)
# [1, 2, 3]
```





## 字典dict

定义一个字典，字典的key可以用字符串或数字类型

```py
dict = {'name': '张三', 1: 12}
name = dict['name']
age = dict[1]
```

用`in`和`not in`判断键名或值在不在字典中，访问不存在的键名时会抛出错误

```py
dict = {'name': '张三', 'age': 14}
'birthday' in dict.keys() # False
'age' not in dict.keys() # False
'张三' in dict.values() # True
```

keys()、values()和 items()。注意：这三个方法返回的不是真正的数组，需要用list()转换，但for循环可以直接使用

```py
dict = {'a': 1, 'b': 2}
dict.keys()
# dict_keys(['a', 'b'])
dict.values()
# dict_values([1, 2])
dict.items()
# dict_items([('a', 1), ('b', 2)])
```

遍历字典，items()列表里的是一个元组

```py
dict = {'name': '张三', 'age': 14}
for key in dict.keys():
  print(key)
# name age
for value in dict.values():
  print(value)
# 张三 14
for item in dict.items():
  print(item, len(item), item[0],item[1])
# ('name', '张三') 2 name 张三	 ('age', 14) 2 age 14
```

用`get()`设置备用值，当访问不存在的键时，get的第二个参数会被返回

```py
dict = {'name': '张三', 'age': 14}
birthday = dict.get('birthday', '2020-10-11')
# 2020-10-11
```

`setdefault()`，为了防止添加键时，覆盖之前的键，可以用setdefault()来简化操作，不用加in keys判断

```py
dict = {'name': '张三', 'age': 14}
print(dict.setdefault('name', 'aaaa')) # 当键名存在时，返回对应的值
# 张三
print(dict.setdefault('name1', 'aaaa')) # 当键名不存在时，返回设置的值
# aaaa

```





## 列表、元组、字典之间的转换

列表转元组 `tuple()`

```python
arr = [1, 2, 3]
tul = tuple(arr)
# (1, 2, 3)
```

元组转列表 `list()`

```python
tul = (1, 2, 3)
arr = list(tul)
# [1, 2, 3]
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



# 标准库

## copy

```py
from copy import copy, deepcopy
```

浅拷贝copy()，深拷贝deepcopy()，deepcopy用来列表中嵌套列表的qing'k

```python
arr = [1, 2, 3]
arr2 = copy(arr)
arr2.append(4)
# arr: [1, 2, 3]
# arr2: [1, 2, 3, 4]
```

















