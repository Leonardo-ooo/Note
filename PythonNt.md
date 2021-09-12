PythonNote

所有变量都是对象，变量存的是引用而非实际值。

#单行注释

print()函数的使用

```python
print(*args, sep = " ", end = "\n")
print("","",...)
```

for的使用

```python
for var_name in <可迭代对象>:
    pass
else:
    pass

#若不需要在循环体中用到迭代变量可用下划线命名迭代变量
#若for或while中遇到break则不执行else，反之则执行
```

range

range是区间类

```python
range(x = 0:y:z = 0)
#一个[x, y)的步长为z的整数区间
```



切片操作

```python
var_name[start = 0: end = len(__object): step]
#将可迭代对象从start到end切片，步长为step
```

val in 可迭代对象查找val是否存在于可迭代对象中，返回一个bool值

list

list的创建：

```python
list_name = [a1, a2 ... , an]

#list生成式
list_name = [i for i in range(start end step)] #生成以i的值构成的列表
```

list为可迭代对象

list添加元素:

```python
lst.append(self, __object)
#list是一种广义表，它的元素可以是任意对象

#在list后面拼接一个可迭代对象，若是dict则添加其key
lst.extend(self, iterable)

#inert()在指定位置添加元素
lst.insert(self， index, __object)

#获取元素index，若有相同则获取第一个的index
lst.index(self, __value, __start = 0, __stop = len(lst))
```

list删除元素:

```python
list_name.remove(self, __value)
#移除值为variable的元素，若存在多个则移除第一个variable

list_name.pop(self, index)
#移除指定索引处的元素

list_name.clear(self)
#清空list
```

列表排序

```python
lst.sort(self, key = None, reverse = False)	#改变原列表， 没有返回值
sorted(__iterable, key = None, reverse = False) #返回一个列表
```



dictionary

字典是一个键值对的集合，底层容器是hash表

字典的创建

```python
dic = {key: val, ke: val, ···}
dic = dict(key=val, key=val, ···)
#使用dict()函数创建，key必须为字符串
```

通过键得到值

```python
dic[key]
dic.get(key)
#若key不存在,第一种方法会报错，第二种方法会得到None
dic.get(key, None_val)
#若不存在key对应的值，得到None_val
```

tuple

元组是一种不可变序列， 不支持增删改操作， 但可以改变元组中可变序列元素的元素

元组的创建

```python
t = (a1, a2, ... an)
#当只有一个元素时，要加上多余的逗号，否则创建的是该元素的对象，例：   t = (a1, )

t = tuple((a1, a2, ... an))
```

set

集合是一种只有key没有value的可变序列，底层容器是hash表

**set是无序的不重复的序列**

set的创建

```python
s = {a1, a2, a3... , an}
s = set({a1, a2, a3... , an})
#空列表只能用set()创建，若用{}会被认为是空字典
```

set的增删改

```python
s.add(self, element) #增加元素
s.update(self, set) #将集合的所有元素添加到当前集合
s.remove(self, element) #移除对应元素，若不存在该元素则抛出异常
s.discard(self, element) #移除对应元素，该元素不存在也不会报错
```



生成式

通过表达式快速生成序列元素

```python
#list生成式
lst = [ i for i in range(6)]
# [0, 1, 2, 3, 4, 5]

#dict生成式
lsta = [1, 2, 3]
lstb = ['一', '二', '三', '四']
dic = {i:j for i, j in zip(lsta, lstb)}
#{1: '一', 2: '二', 3: '三'}

#元组为不可变序列，故没有生成式

#set生成式
s = {i for i in range(6)}
# [0, 1, 2, 3, 4, 5]
```

字符串常用类函数

```python
#以下方法均不改变原字符串而是返回一个新的(不同id的)字符串对象
s.upper(self) #小写转大写
s.lower(self) #大写转小写
s.swapcase(self) #小写转大写，大写转小写
s.capitalize(self) #第一个字符大写
s.title(self) #每个单词的第一个字母大写

s.center(self, __with, __fillchar == ' ') #生成一个居中的字符串
s.ljust(self, __with, __fillchar == ' ') #左对齐
s.rjust(self, __with, __fillchar == ' ') #右对齐
s.zfill(self, __with) #0填充右对齐

#===========================================
s.split(self, sep = None, maxsplit) #以sep为分隔符切割字符串， 若maxsplit有参数则最多切割为maxsplit + 1个子字符串
s.strip()	#去掉空格
#===========================================

s.index(self, sub, __start, __end) #从左至右找子串sub第一次出现的位置，没有则抛出异常
s.rindex(self, sub, __start, __end) #从右至左
s.find(self, sub, __start, __end)	#从左至右，找不到返回-1
s.rfind(self, sub, __start, __end)	#从右至左，找不到返回-1

#============= ======================
s.join(self, __iterable) #将可迭代对象__iterable的元素（必须为字符串）以s为分隔连接起来，返回生成的字符串
#===================================

#格式化字符串的两种方法
"xxx%dxxx%s” % (a1, a2)
"xxx{0}xxx{1}".format(a0, a1)


```

文件读写

```python
#创建文件对象/释放系统资源
file = open('__filename', 'r/w/a')
file.close()

#whith open写法
    with open("文件路径","读写方式") as 赋值变量:
        pass

#文件对象的常用方法

file.read([size]) #读取size个字节或字符返回，若省略size则读取全部内容
file.readline() #读取一行返回字符串
file.readlines() #读取全部，按行返回字符串列表
file.write(str) #将字符串写入文件
file.writelines(s_list) #将字符串列表写入文件
```

![image-20210410125610163](C:\Users\78447\AppData\Roaming\Typora\typora-user-images\image-20210410125610163.png)



异常处理

```python
try:
    pass
except Exception_name [as e]:
    pass
except Exception2:
    pass
else:
    pass
finally:
    pass
    
```

模块

```python
import 模块名 as 别名
from 模块名 import 函数/变量/类
from 包名 import 模块名
#以主程序形式运行
#在每个模块的定义中都包括一个记录模块名称的变量 __name__。如果一个模块不是被导入到其他程序中执行，那么它可能在解释器的顶级模块中执行。顶级模块的 __name__ 变量值为 __main__
if __name__ == '__main__' :
    pass
```

