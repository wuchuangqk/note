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
- 在字符串前加一个小写的`r`，表示将字符串看作是原始字符串，原始字符串会将转义字符看作为普通字符。例如 r'你\n好'会输出 你\n好，这里的\n不再有换行效果。

# 异常处理

```python
try:
    num = int(input())
    print(type(num))
except Exception as e:
    print(e)
```

# 文件读写

## open

读取一个文件，参数：文件路径，模式，可选参数：encoding(编码)。模式：r只读，w写入(覆盖)，a写入(追加)。r=read,w=write,a=append。使用后要记得调用close()关闭文件流。以写入模式打开的文件，不存在时会自动创建

```python
open(path, mode='r')
```

- path 绝对路径和相对路径

- mode 读取模式，默认只读。

  | 字符  | 含意                                       |
  | :---- | :----------------------------------------- |
  | `'r'` | 读取（默认）                               |
  | `'w'` | 写入，并先截断文件                         |
  | `'x'` | 排它性创建，如果文件已存在则失败           |
  | `'a'` | 打开文件用于写入，如果文件存在则在末尾追加 |
  | `'b'` | 二进制模式                                 |
  | `'t'` | 文本模式（默认）                           |
  | `'+'` | 打开用于更新（读取与写入）                 |

- encoding 文件编码



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

使用`with`语句自动关闭文件流，在with结构里声明的变量，在外面可以访问到

```py
with open('hello.txt', 'r', encoding='utf-8') as file:
  file.read()
```



# 创建和写入文件

检查文件是否存在

```python
os.path.exists(file_path)
```

默认的读取模式对于不存在的文件会报错

```python
open(not_exists_path, 'r')
# FileNotFoundError
```

改成`w`写入模式就可以访问不存在的文件。以`w`模式打开一个文件的话，如果文件不存在会创建这个文件。可以用`w`模式来创建一个文件

```python
with open(not_exists_path, 'w', encoding='utf8') as file:
  	# 即使不调用write也会创建出这个文件
    # w模式下不能调用readline等读取流方法
    file.write('你好')

with open(not_exists_path, 'r', encoding='utf8') as file:
    print(file.readline())
    # 你好
```



## os模块

```python
import os
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
os.listdir('C:\\Users')
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

删除文件，参数是绝对路径

```py
os.remove(file)
```

删除文件夹

```py
os.rmdir() # 只能删除空文件夹
os.removedirs() # 递归删除所有的文件和文件夹
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

文件路径拼接，Windows和Linux的路径分隔符不一样。

```python
os.path.join('usr','bin','span')
# Windows 'usr\\bin\\span'
# Linux 'use/bin/span'
```



## shutil模块

shutil主要用来复制、移动文件和文件夹

```py
import shutil
```

复制文件，返回复制后的路径。注意：1.文件已存在会报错 2.目录要提前创建好

```py
shutil.copy('C:\\spam.txt', 'C:\\delicious')
# 'C:\\delicious\\spam.txt'
shutil.copy('eggs.txt', 'C:\\delicious\\eggs2.txt')
# 'C:\\delicious\\eggs2.txt'
```

复制文件夹，copytree会复制所有的文件和子文件夹（递归复制）。src必须是目录，dst不存在会自动创建

```py
# copytree(src, dst)
shutil.copytree('C:\\bacon', 'C:\\bacon_backup')
# 'C:\\bacon_backup'
```

移动文件

```py
shutil.move('C:\\bacon.txt', 'C:\\eggs')
# 'C:\\eggs\\bacon.txt'
```

- 覆盖已有文件：如果c:\\eggs下已经有bacon.txt，就会被**覆盖**。要注意这点。
- 移动同时重命名：如果目录路径是c:\\\eggs\\new_bacon.txt，那么文件在移动到c:\\eggs后，会改名为new_bacon.txt
- 目标目录必须存在
- 如果c:\\\下没有eggs文件夹，py会当成移动且重命名操作，最后bacon.txt被重命名为eggs的文件





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

定义一个字典，

字典的key仅支持两种数据类型：

- 字符串
- 数字

```py
dict = {
  'name': '张三', 
  1: 12
}

```

访问字典，仅支持[]语法

```python
name = dict['name']
age = dict[1]
```

查找元素

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



## json

json标准库提供了对json文件读写操作的支持。

导入json库
```python
import json
```

### 读取json

```python
# 指定encoding为utf-8防止出现中文乱码
with open('settings.json', 'r', encoding='utf-8') as file:
    data = json.load(file)
```
1、生成文件流（注意处理文件不存在异常）
2、json.load()加载文件流并解析
3、返回解析结果

解析结果有两种数据类型，字典或列表。根据json定义的格式：
- 数组对应列表
- 对象对应字典

示例
```python
data = json.load(file)
print(data, type(data))

# {'name': '张三'} <class 'dict'>
# [{'name': '张三'}] <class 'list'>
```

### 写入(修改)json

使用json.dump()将字典或列表里的数据写入json文件。每次写入都是全局覆盖写入，无法做到只修改某一部分。
```python
dict = {'age': 12}
with open('settings.json', 'w', encoding='utf-8') as file:
	 json.dump(dict, f)
```

默认情况下，写入后的json文件会挤在一行，设置indent参数可以设置缩进，美化json样式
```python
json.dump(dict, f, indent=2)
```
- index=2 缩进两个空格


## zipfile

查看、压缩、解压zip文件

```py
import zipfile
```

创建压缩文件，注意要添加第二个参数 w，用write()写入要压缩的文件，最后调用close()

```py
new_zip = zipfile.ZipFile('新建压缩文件.zip', 'w')
new_zip.write('a.json', compress_type=zipfile.ZIP_DEFLATED)
new_zip.close()
```

- 如果要向现有压缩文件里追加文件，可以使用`a`作为第二个参数
- compress_type指定压缩算法，推荐用ZIP_DEFLATED
- 多次调用write()可以写入多个文件
- 如果向write()传入文件夹目录，会递归压缩文件夹内的所有文件

查看压缩文件，namelist()获取压缩文件里有哪些文件，getinfo()查看文件的详细信息

```py
zip = zipfile.ZipFile('新建压缩文件1.zip')
names = zip.namelist()
print(names)
# ['a.json', 'b.txt']
info = zip.getinfo(names[0])
print(info)
# <ZipInfo filename='a.json' compress_type=deflate filemode='-rw-rw-rw-' file_size=14 compress_size=16>
# info.filename
# info.file_size
# ……
zip.close()
```

解压zip

```py
zip = zipfile.ZipFile('新建压缩文件.zip')
zip.extractall('result')
zip.extract('spam.txt', 'C:\\some\\new\\folders')
zip.close()
```

- extractall() 解压全部文件，默认解压到当前目录。可以指定解压的目录，不存在时自动创建
- extract() 解压单个文件，默认解压到当前目录。可以指定解压的目录，不存在时自动创建

## time

```python
import time
```

### 代码执行用时
```python
start_time = time.time()
end_time = time.time()
print('程序用时%s秒' % (round(end_time - start_time, 2)))
```

### 当前时间戳
返回自1970年1月1日午夜以来的秒数。
```python
time.time()
# 1684825513.1463313
```

### 年月日时分秒
```python
time_info = time.localtime()
# time.struct_time(tm_year=2023, tm_mon=5, tm_mday=23, tm_hour=15, tm_min=6, tm_sec=55, tm_wday=1, tm_yday=143, tm_isdst=0)
```
- tm_year 年
- tm_mon 月
- tm_mday 日
- tm_hour 时
- tm_min 分
- tm_sec 秒
- tm_wday 星期几（取值范围为0-6，星期一到星期日）
- tm_yday 表示一年中的第几天，取值范围为1-366。
- tm_isdst 表示是否为夏令时，其取值有三种情况：
	-   如果为正数，则表示当前时间处于夏令时。
	-   如果为0，则表示当前时间不处于夏令时。
	-   如果为负数，则表示当前时间夏令时状态未知。

### 日期格式化
```python
localtime = time.localtime()
formatted_time = time.strftime("%Y-%m-%d %H:%M:%S", localtime)
# 2023-05-23 15:13:54
```


# pip

安装一个模块，模板会被安装到全局，下个项目就不用再次安装了

```shell
pip install 模块名称
```

linux下pip要单独安装，且名称是`pip3`

```sh
sudo pip3 install 模块名称
```

更新模块

```shell
pip install -U 模块名称
```

查看已安装的库

```powershell
pip list
```

> Package            Version
> ------------------ ---------
> certifi            2022.12.7
> charset-normalizer 2.1.1
> click              8.1.3
> colorama           0.4.6
> Flask              2.2.2
> Flask-Cors         3.0.10
> idna               3.4
> itsdangerous       2.1.2
> Jinja2             3.1.2
> MarkupSafe         2.1.1
> pip                22.3
> pyperclip          1.8.2
> requests           2.28.1
> setuptools         65.5.0
> six                1.16.0
> urllib3            1.26.13
> Werkzeug           2.2.2
> yapf               0.32.0

# 运行程序

py文件的第一行应该是`#!`，例如\#! /usr/bin/python3，这句话的意思是让操作系统知道用什么程序来运行这个脚本

```py
windows
#! python3
linux
#! /usr/bin/python3
```



# 从网络流中抓取图片

导入库
```python
import requests, sys, os
```
- 网络请求库`request`
- 操作系统`os`

图片地址
```http
img_web_url = 'https://pic.leetcode-cn.com/1599880866-aLaPYz-Picture1.png'
```

## 发起请求
```python
res = requests.get(img_web_url)
print(res.content)
print(res.status_code)
print(res.headers)
print(res.url)
```
- content 二进制文件内容数据
```html
e7i\xc0\xe1SO=5\xe8\x1e\x96\x18\xb4\x94\xa9fx\xd2\xe7\x96\xb2\xa5\x94\xa9\xa7q`\xf4\x1e\xd2\x0c@\xf5\x05\xd5\x9a\xf2Z\x9b\xe23T\xbf\x1fa\xd1\xf1\x14,T\x17\x9b\x
```
- status_code 状态码
```html
200
```
- headers 返回的头部信息
```html
{'Last-Modified': 'Sat, 12 Sep 2020 03:21:07 GMT', 'Etag': '"39DFF6DAEF81694DA66E26432133428E"', 'Server': 'AliyunOSS', 'Date': 'Sat, 20 May 2023 13:15:12 GMT', 'Content-Type': 'image/png', 'x-oss-request-id': '6468C7E02D1F293432D90D15', 'x-oss-object-type': 'Normal', 'x-oss-hash-crc64ecma': '7161063256739480774', 'x-oss-storage-class': 'Standard', 'Content-MD5': 'Od/22u+BaU2mbiZDITNCjg==', 'x-oss-server-time': '72', 'Content-Length': '77907', 'Accept-Ranges': 'bytes', 'X-NWS-LOG-UUID': '7436313969761764876', 'Connection': 'keep-alive', 'X-Cache-Lookup': 'Cache Hit', 'Cache-Control': 'max-age=3600'}
```
- url 请求地址
```html
https://pic.leetcode-cn.com/1599880866-aLaPYz-Picture1.png
```

## 写入到本地
设置保存地址，相对路径或绝对路径。目录如果不存在会自动创建，同名文件自动覆盖。
```python
# 绝对路径(D:\Programming\WorkSpace\python project\img\test.png)
save_path = os.path.join(sys.path[0], 'img/test.png')
# 相对路径
save_path = 'img/test.png'
```
使用文件流写入
```python
with open(save_path, 'wb') as file:
  file.write(res.content)
  print('ok')
```
- wb `w(write)写入` + `b(byte)二进制`指定文件流模式是写入二进制数据
- res.content 图片的二进制数据流

在文件管理器打开图片所在目录
```python
# 图片目录
file_path = os.path.join(sys.path[0], 'img')
# 图片
file_path = os.path.join(sys.path[0], 'img/test.png')
os.startfile(file_path)
```
- 对于目录：在文件管理器打开目录
- 对于文件：用默认程序打开文件

# 脚本所在目录

python获取脚本所在目录有两种常用方式：
- os.getcwd() 获取当前工作目录
- sys.path[0] 

以这个脚本为例，比较两种方法的区别
`D:\Programming\WorkSpace\python project\test.py`
```python
import sys, os

print('os.getcwd()——%s' % (os.getcwd()))
print('sys.path[0]——%s' % (sys.path[0]))
```

- 当在`D:\Programming\WorkSpace\python project`目录执行脚本时，两种方法获取到了一样的结果
```html
os.getcwd()——D:\Programming\WorkSpace\python project
sys.path[0]——d:\Programming\WorkSpace\python project
```
- 当在`C:\Users\wuchu`目录执行脚本时
	- os.getcwd() 返回的是执行脚本所在的目录，而非脚本真实目录
	- sys.path[0] 返回了脚本的真实目录
```html
os.getcwd()——C:\Users\wuchu
sys.path[0]——D:\Programming\WorkSpace\python project
```

# 网络请求
request

```python
import requests
```



```python
res = requests.get(url)
# <Response [200]>
```

Response:

- text 纯文本
- content 二进制，类型是字节<class 'bytes'>
- status_code 状态码，200、404、500
- headers 返回头
- json() 尝试将文本转换成字典dict
- url 请求地址

# 面向对象