## Jump to Section

* [Python文件类型](#python%E6%96%87%E4%BB%B6%E7%B1%BB%E5%9E%8B)
* [Python变量](#python%E5%8F%98%E9%87%8F)
* [Python运算符](#python%E8%BF%90%E7%AE%97%E7%AC%A6)
* [Python数据类型](#python%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B)
* [Python序列](#python%E5%BA%8F%E5%88%97)
* []()
* []()
* []()

## Python文件类型

[[Back To Top]](#jump-to-section)

- 源代码
  - Python源代码的文件以`*.py`为扩展名，由`python`命令解释执行，不需要编译
   <pre>
    $ cat hello.py
    print 'hello world'
    $ python hello.py
    hello world
   </pre>
  - 在`linux`中文件头部分添加如下代码，并附加可执行权限，就能够直接执行
   <pre>
    $ cat hello.py
    #!/c/Python27/python
    print 'hello world'
    $ chmod +x hello.py
    $ hello.py
    hello world
   </pre>
- 字节代码
  - Python源文件经编译后生成的扩展名为`*.pyc`的文件，需要用`python`命令执行
  - 编译方法
   <pre>
    $ ls
    hello.py  world.py
    $ cat world.py
    import py_compile
    py_compile.compile("hello.py")
    $ python world.py
    $ ls
    hello.py  hello.pyc  world.py
    $ python hello.pyc
    hello world
   </pre>
- 优化代码
  - 经过优化后的源文件，扩展名为`*.pyo`，需要用`python`命令执行
  - 执行方法，注意参数是大写的`O`
   <pre>
    $ python -O -m py_compile hello.py
    $ ls
    hello.py  hello.pyo
    $ python hello.pyo
    hello world
   </pre>

## Python变量

[[Back To Top]](#jump-to-section)

**变量是计算机内存中的一块区域，变量可以存储规定范围内的值，而且值可以改变。**

- 变量的命名
  - 变量名由字母、数字、下划线组成
  - 不能以数字开头
  - 不可以使用关键字
- 变量的赋值
  - 变量声明和使用
  ```python
  >>> a=1
  >>> a
  1
  >>> print a
  1
  >>> b=10
  >>> a*b+3
  13
  ```
  - 查看变量内存空间地址`id(VarName)`，同一内存空间地址可以被多个变量所使用
  ```python
  >>> id(a)
  5090592
  >>> id(b)
  5090484
  >>> c=10
  >>> id(c)
  5090484
  ```

## Python运算符

[[Back To Top]](#jump-to-section)

- 算术运算符
  - 加法：`+`
  ```python
  >>> 2+3
  5
  ```
  - 减法：`-`
  ```python
  >>> 5-4
  1
  ```
  - 乘法：`*`
  ```python
  >>> 3*2
  6
  ```
  - 实数除法：`/`
  ```python
  >>> 3/2
  1
  >>> 3.0/2
  1.5
  ```
  - 整数除法：`//`
  ```python
  >>> 3//2
  1
  >>> 3.0//2
  1.0
  >>> 3.2//2
  1.0
  ```
  - 求余数：`%`
  ```python
  >>> 10%3
  1
  ```
  - 幂运算：`**`
  ```python
  >>> 2**3
  8
  ```
- 关系运算符，返回`True/False`
  - 小于：`1<2`
  - 大于：`3>2`
  - 小于等于：`1<=1`
  - 大于等于：`2>=2`
  - 不等于：`1!=2`
  - 等于：`2==2`
- 逻辑运算符，返回`True/False`
  - 逻辑与：`3>2 and 2<3`
  - 逻辑或：`1>2 or 3>2`
  - 逻辑非：`not 1>2`
- 赋值运算符，先用左边的变量和右边的表达式计算，再赋值给左边的变量
  - 等于：`=`
  ```python
  >>> a=22
  >>> b='xyz'
  >>> a
  22
  >>> b
  'xyz'
  ```
  - 加等于：`+=`
  ```python
  >>> a=22
  >>> a+=5
  >>> a
  27
  ```
  - 减等于：`-=`
  ```python
  >>> a=27
  >>> a-=4
  >>> a
  23
  ```
  - 乘等于：`*=`
  ```python
  >>> a=5
  >>> a*=4
  >>> a
  20
  ```
  - 除等于：`/=`
  ```python
  >>> a=20
  >>> a/=4
  >>> a
    5
  ```
  - 求余等于：`%=`
  ```python
  >>> a=5
  >>> a%=3
  >>> a
  2
  ```
  - 算术运算符优先级由低到高顺序
   <pre>
    Lambda
    逻辑或：or
    逻辑与：and
    逻辑非：not
    范围：in, not in
    同一性测试：is, is not
    比较：<, <=, >, >=, !=, ==
    按位或：|
    按位异或：^
    移位：<<, >>
    加法与减法：+, -
    乘法、除法与取余：`*, /, %`
    正负号：+X, -X
    按位翻转：~X
    幂运算：**
   </pre>

## Python数据类型

[[Back To Top]](#jump-to-section)

- 数字类型
  - 整型：`int`，范围`-2,147,483,648~2,147,483,647`
  ```python
  >>> num=21435435
  >>> type(num)
  <type 'int'>
  ```
  - 长整型：`long`，范围可以是任意大的整数均可以储存，也可以在普通整数后加`L`或`l`强制声明。
  ```python
  >>> num=9999999999999999999
  >>> type(num)
  <type 'long'>
  >>> num=123L
  >>> type(num)
  <type 'long'>
  ```
  - 浮点型：`float`，加上`.`声明即可
  ```python
  >>> num=1.0
  >>> type(num)
  <type 'float'>
  ```
  - 复数型：`complex`，加上`j`声明即可
  ```python
  >>> num=3.14j
  >>> type(num)
  <type 'complex'>
  >>> num
  3.14j
  ```
- 字符串：`String`
  - 一旦生成，不可变
  - 使用引号定义的一组集合，可以包含数字、字母、符号（非特殊系统符号）
  - 必要时字符串中可以添加转义符号：`\`, `\n`
  ```python
  >>> str='string'
  >>> str="string"
  >>> str="""string"""
  >>> type(str)
  <type 'str'>
  >>> print str
  string
  >>> str='let\'s go'
  >>> print str
  let's go
  ```
  - 三重引号（docstring）通常用来制作字符串
  ```python
  >>> str="""jay:
  ...   How are you?
  ...        Gooodbye!
  ... """
  >>> str
  'jay:\n  How are you?\n       Gooodbye!\n'
  >>> print str
  jay:
    How are you?
         Gooodbye!

  ```
  - 操作字符串：索引、连接、截取
  ```python
  >>> str="12345"
  >>> str[0] #索引位置从0开始
  '1'
  >>> str[2]+str[0] #使用`+`连接字符串
  '31'
  >>> str[1:4] #从索引1截取到索引4-1的字符，默认从左向右截取
  '234'
  >>> str[:4] #从索引0开始截取到索引4-1的字符
  '1234'
  >>> str[4:] #从索引4开始截取到末尾
  '5'
  >>> str[::1] #从索引0开始每隔1个字符进行截取
  '12345'
  >>> str[::2] #从索引0开始每隔2个字符进行截取
  '135'
  >>> str[::3] #从索引0开始每隔3个字符进行截取
  '14'
  >>> str[-1] #从右向左索引位置即-1, -2, -3, ...
  '5'
  >>> str[-4:-1]
  '234'
  >>> str[4::-1] #使用-1从右向左截取，即字符串反转
  '54321'
  >>> str[3::-1]
  '4321'
  ```
- 元组（类似于java中的数组）：`tuple`
  - 一旦生成，不可以改变
  - 固定长度，支持嵌套
  - 通过偏移读取
  ```python
  >>> empty=() #空元组
  >>>
  >>> singleton=(2,) #单个元素的元组
  >>> singleton2=(2) #这是整数
  >>> type(singleton)
  <type 'tuple'>
  >>> type(singleton2)
  <type 'int'>
  >>>
  >>> a=('x','y','z') #一般的元组
  >>> b=('w',a,1) #嵌套元组
  >>> print b
  ('w', ('x', 'y', 'z'), 1)
  >>> b[2] #取元组中的元素
  1
  >>> b[1]
  ('x', 'y', 'z')
  >>> b[1][1] #取元组中的元素
  'y'
  >>>
  >>> c1,c2,c3=b #同时定义三个变量，并赋值
  >>> print c1
  w
  >>> c2
  ('x', 'y', 'z')
  >>> c3
  1
  ```

## Python序列

[[Back To Top]](#jump-to-section)

**列表、元组和字符串都是序列**

- 序列的两个主要特点是索引操作符和切片符
  - 索引操作符可以从序列中抓取一个特定范围的值
  - 切片操作符可以截取序列的一部分元素

- 序列的基本操作
  - 求序列长度：`len()`
  ```python
  >>> len('abc')
  3
  ```
  - 连接2个序列：`+`
  ```python
  >>> 'abc'+'123'
  'abc123'
  ```
  - 重复序列元素：`*`
  ```python
  >>> '#'*3
  '###'
  ```
  - 判断元素是否在序列中：`in`
  ```python
  >>> 'c' in 'abc'
  'True'
  >>> 'd' in 'abc'
  'False'
  ```
  - 取最大/小值：`max()`, `min()`，不能单独操作数字
  ```python
  >>> max('abc')
  'c'
  >>> max(12345679,1234)
  12345679
  >>> max('189')
  '9'
  >>> min(11,22,33)
  11
  >>> min('abc')
  'a'
  ```
