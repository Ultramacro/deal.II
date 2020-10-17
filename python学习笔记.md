<center><font size=6 color='blue'>Python学习笔记</font></center>

<center><font size=2 color='blue'>based on boyu learning platform</font></center>

[TOC]

# 一、基本语法

## 1.1 输出语句

print(输出内容1, 输出内容2, …, 输出内容n)

```python
print("Hello VScode!")
print('Hello VScode!')	// 单双引号均可
print("Hello", "VScode!")
a = "Hello"
b = "VScode!"
print(a, b)
print("Hello", "VScode", sep=' ')
print("Hello", end=' ')
print("VScode!", end=' ')
```

screen out:

>Hello VScode!
>Hello VScode!
>Hello VScode!
>Hello VScode!
>Hello VScode!
>Hello VScode!

```
1. 修改输出的间隔符
print(输出内容1, 输出内容2, …, 输出内容n, sep='') # sep：用来表示用什么符号间隔多个对象，默认为空格。
```

```
2. 修改输出的换行符
print(输出内容1, 输出内容2, …, 输出内容n, end='\n') # end：用来设定输出以什么结尾，默认为换行\n。
```

## 1.2 注释

==注释==：介绍代码的功能，注释还可用于临时禁用一段代码。

```
1. 单行注释语法
# 这是第一个注释 
```

```
2. 多行注释语法
"""
这是多行注释，用三个双引号 
这是多行注释，用三个单引号 
"""
```

==python之禅==

```python
# 优美胜于丑陋（Python 以编写优美的代码为目标）
print("Beautiful is better than ugly.")

# 明了胜于晦涩（优美的代码应当是明了的，命名规范，风格相似
print("Explicit is better than implicit.")

# 简洁胜于复杂（优美的代码应当是简洁的，不要有复杂的内部实现）
print("Simple is better than complex.")

# 复杂胜于凌乱（如果复杂不可避免，那代码间也不能有难懂的关系，要保持接口简洁）
print("Complex is better than complicated.")

# 扁平胜于嵌套（优美的代码应当是扁平的，不能有太多的嵌套）
print("Flat is better than nested.")

# 间隔胜于紧凑（优美的代码有适当的间隔，不要奢望一行代码解决问题）
print("Sparse is better than dense.")

# 可读性很重要（优美的代码是可读的）
print("Readability counts.")

# 即便假借特例的实用性之名，也不可违背这些规则（这些规则至高无上）
print("Special cases aren't special enough to break the rules.")
print("Although practicality beats purity.")

# 不要包容所有错误，除非你确定需要这样做（精准地捕获异常，不写 except:pass 风格的代码）
print("Errors should never pass silently.")
print("Unless explicitly silenced.")

"""
当存在多种可能，不要尝试去猜测
而是尽量找一种，最好是唯一一种明显的解决方案（如果不确定，就用穷举法）
虽然这并不容易，因为你不是 Python 之父（这里的 Dutch 是指 Guido ）
"""
print("In the face of ambiguity, refuse the temptation to guess.")
print("There should be one-- and preferably only one --obvious way to do it.")
print("Although that way may not be obvious at first unless you're Dutch.")

# 做也许好过不做，但不假思索就动手还不如不做（动手之前要细思量）
print("Now is better than never.")
print("Although never is often better than *right* now.")

# 如果你无法向人描述你的方案，那肯定不是一个好方案；反之亦然（方案测评标准）
print("If the implementation is hard to explain, it's a bad idea.")
print("If the implementation is easy to explain, it may be a good idea.")

# 命名空间是一种绝妙的理念，我们应当多加利用（倡导与号召）
print("Namespaces are one honking great idea -- let's do more of those!")
```

## 1.3 常量与变量

==常量==是程序运行过程中值不改变的量。与常量相反，==变量==是在程序运行过程中值可以被改变的量。

```python
print("Hello VScode")	# 常量
print(666)
a = "Hello"		# 变量
b = "VScode!"
print(a, b)
```

```
1. 变量命名规则
	可以包括字母（区分大小写），数字和下划线
    不能以数字开头，不能包含空格
    python的关键字不能用（False, True, if）
    变量名尽量有实际意义
```

## 1.4 简单表达式

1. 算术运算符

   ```
   num1 = 10
   num2 = 20
   num1 + num2 # 加，运算结果为 30
   num1 - num2 # 减，运算结果为 -10
   num1 * num2 # 乘，运算结果为 200
   num2 / num1 # 除，运算结果为 2
   num2 % num1 # 取余，运算结果为 0
   num1 ** 2  # 幂，运算结果为 100
   num1 // 3  # 取整除(向下取整)，运算结果为 3
   ```
2. 算术优先级
    从最高到最低优先级
    `**` ：返回x的y次幂

  `* /  % // `：乘，除，取模和取整除

  `+ -`：加法减法
  `()`：注意加括号的情况
3. 赋值语句
   变量名 = 存储在变量中的值

4. 赋值语句语法结构
   语法1：变量名 = 表达式
   语法2：变量名1 = 变量名2 = 表达式
   语法3：变量名1 ，变量名2 = 表达式1，表达式2

5. 字符串运算符

   `+`：加 - 字符串拼接 `*`：乘 - 字符串重复若干次

6. 强制类型转换 

   在变量或表达式外加上`str()`,将括号中的内容类型转为字符串。 

   在变量或表达式外加上`int()`,将括号中的内容类型转为整型。必须保证括号中的内容是整数。 

   在变量或表达式外加上`float()`,将括号中的内容类型转为浮点型。必须保证括号中的内容是浮点数。

7. ```
   1. 常用转义字符
   \\ # 反斜杠符号
   \' # 单引号
   \" # 双引号
   \n # 换行
   ```

## 1.5 字符串

1. `type()` 语句：用于返回对象的类型 

2. Python 中常见数据类型： 

   Numbers -- 数字 

   String  -- 字符串 

   List    -- 列表 

   Tuple   -- 元组 

   Dictionary -- 字典

   ```
   1. 单行字符串书写方式
   "这是单行字符串" # 也可以用单引号，注意前后一致
   2. 多行字符串书写方式：
   """
   这是多行字符串
   这是多行字符串 
   """
   ```

   ```
   1. 字符串的索引: 使用 [头下标:尾下标] 来截取相应的字符串，注意左闭右开！
   word = "BoyuAI" # 注意索引从0开始
   print(word[0]) # 输出结果：B
   print(word[0:1]) # 输出结果：B
   print(word[1:7]) # 输出结果：oyuAI
   print(word[-3:-1]) # 输出结果：uA
   2. 字符串运算符
   + ：加 - 字符串拼接
   * ：乘 - 字符串重复若干次
   3. 字符串格式化：
   print(f" 这是第一个变量：{变量1}，这是第二个变量：{变量2}")
   ```

## 1.6 输入语句

```
1. 读入语句语法
输入变量 = input("提示内容")
```

`input()` 获得的输入内容是**字符串**类型。

## 1.7 文件读写与操作

```python
file = open("filename.txt")      # 以只读形式打开文件，并赋给文件变量 file
file.read()                      # 读取的是文件中的所有信息。
file.readline()                  # 读取文件的当前行
file = open("filename.txt",'w')  # 以写入形式打开文件，并赋给文件变量 file
file.write("content")            # 写入内容，可以写入常量或变量
# 每个write语句的括号内每次只能传入一个写入的内容，多个内容需多次调用 file.write()
file.close()             # 关闭文件
```

## 1.8 函数

```
1. 函数的定义：
def 函数名(参数1, 参数2, ……, 参数n)：
    函数内部的执行语句
    return 返回值
2. 函数的调用
函数名(参数1, 参数2, ……, 参数n)
```

## 1.9 逻辑表达式

* Python中的布尔类型只有两种值：`True` 和 `False`。
* 使用 `bool()` 内置函数可以给出 `True` 或 `False` 的结果。

```
1. Python中常用的关系表达式
# 先定义两个变量
num1 = 10
num2 = 20

num1 == num2  # 等于，运算结果为 False
num1 != num2  # 不等于，运算结果为 True
num1 < num2   # 小于，运算结果为 True
num1 > num2   # 大于，运算结果为 False
num1 <= num2  # 小于等于，运算结果为 True
num1 >= 2     # 大于等于，运算结果为 True
2. Python中常用的逻辑表达式
# 先定义两个布尔型变量
state1 = True
state2 = False

state1 and state2  # 与，运算结果为 False
state1 or state2   # 或，运算结果为 True
not state2         # 非，运算结果为 True
3. 逻辑表达式中的运算优先级
not > and > or		注意：有括号要先算括号。
```

<img src="https://staticcdn.boyuai.com/materials/2020/06/14/ZeZc8D3eL9MUEiL5MhjcV.png!png" alt="img" style="zoom:67%;" />

## 1.10 条件语句

```
1. 条件语句
if 判断条件:
    执行语句…… 
2. 多个条件的if语句
if 判断条件1:
	执行语句1……
elif 判断条件2:
	执行语句2……
else:
	执行语句3……
```

## 1.11 列表

```
1. 列表的定义
# 定义一个列表
list0 = [1, "2", 3, [4, 5]] # 列表中可以包含不同的数据类型
2. 切片选取列表中的元素
# 注意左闭右开
list0[开始索引值:结束索引值:选取间隔]
3. 列表尾部元素添加
list0.append(新元素)
4. 列表元素删除
list0.remove(元素) # 删除第一个匹配的“元素”
del list0[元素索引]
5. 列表元素修改
list0[元素索引] = 新元素 
```

## 1.12 for循环

```
1. 程序执行结构
    a. 顺序结构
    b. 分支结构(if语句)
    c. 循环结构(for循环)
2. for循环的定义
for 循环变量 in 序列: # 英文冒号要注意
	执行语句… # 缩进不能忘！
	
使用 range() 功能可以输入起始值和结束值，获得一个对应的整数序列，注意左闭右开。
len() 方法返回对象（字符、列表等）的长度，或者说元素个数。
```

## 1.13 while循环

```
1. while循环的定义
while 循环条件: # 英文冒号要注意
	执行语句…   # 缩进不能忘！
2. 当 while 中的条件始终为 True 时，Python 就会一直执行循环体内的执行语句。
3. break 语句用来终止循环语句。break语句将停止执行最内层的循环，并执行循环之后的下一行代码。
4. continue 语句用来告诉Python跳过当前这一轮循环的剩余语句，然后继续进行下一轮循环。continue 语句跳出本次循环，而break跳出整个循环。
```

## 1.14 字典

```
1. 字典的定义
# 定义一个字典
dic = {key1: value1, key2: value2} # 键必须唯一，值可以不唯一
# 键只能是数字，字符串和布尔值
2. 字典元素的选取
字典名[键]
3. 字典元素添加
字典名[键] = 值
4. 字典元素删除
del 字典名[键]
5. 字典元素修改
字典名[键] = 新的值
```

## 1.15 类与库

```
1. 类的样例
class Name_of_class:          # name_of_class 是类名
	attribute1 = 0            # 基本属性1
	attribute2 = ''           # 基本属性2

	def __init__(self, x, y): # 构造方法，注意一定是 __init__() # 双下划线
		self.attribute1 = x
		self.attribute2 = y

	def function1(self):      # 自己定义的方法1
		print('hello world')

	def function2(self):      # 自己定义的方法2
		print(self.attribute1, self.attribute2)
2. 类的继承
class 基类: # 已定义好的基类
    共有属性
    共有方法
    
class 子类(基类): # 继承了基类的子类
    独有属性
    独有方法
3. math库常用函数
math.hypot(x,y)  # 得到x和y的平方和的平方根
math.pow(x,y)    # 得到x的y次方
math.sqrt(x)     # 得到x的平方根
```





# 二、Turtle

2.1 turtle

```
1. 初始化Turtle画布和画笔
Boyu_pen = Turtle(width=300, height=300) # 给画笔起名为 Boyu_pen
Boyu_pen # 使画布和画笔出现在屏幕上，这句语句可不能少
```

```
2. 修改画笔颜色
# 使用pencolor()语句会修改Boyu_pen的画笔颜色为蓝色，需要其他颜色只需要在括号中填写对应的英文即可
Boyu_pen.pencolor("blue")
```

```
3. 使画笔按当前方向前进一段距离
# 使用forward()语句会使Boyu_pen在画布上按当前方向前进k个像素的距离，初始状态下画笔默认朝上
# 括号里可以填整数常量，也可以填整数变量
Boyu_pen.forward(k)
```

```
4. 使画笔左转/右转
# 使用left()语句会使Boyu_pen在画布上左转30度，括号里可以填整数常量，也可以填整数变量
Boyu_pen.left(30)
# 使用right()语句会使Boyu_pen在画布上右转x度，括号里可以填整数常量，也可以填整数变量
Boyu_pen.right(x)
```

```python
from ipyturtle2 import TurtleWidget
# 下述语句定义了画笔 Boyu_pen
Boyu_pen = TurtleWidget()
Boyu_pen
Boyu_pen.reset()
color = "red"
length = 75
Boyu_pen.forward(100)
Boyu_pen.left(90)
Boyu_pen.forward(100)
Boyu_pen.left(90)
Boyu_pen.forward(100)
Boyu_pen.left(90)
Boyu_pen.forward(100)
```

