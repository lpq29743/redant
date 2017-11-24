---
layout: wiki
title: Java
categories: Java
description: Java
keywords: Java
---

### 第 1 章 概述

### 第 2 章 基本程序设计

#### 2.1 一个简单的 Java 应用程序

#### 2.2 数据类型

#### 2.3 变量和常量

#### 2.4 运算符

##### 2.4.1 赋值运算

赋值运算的作用是为变量或常量指定数值。常用的赋值运算符主要有：`=`、`+=`、`-=`、`*=`、`/=`和`%=`。接下来我们通过几个例子来具体看一下：

**例 1**

```java
int i = 10;
int j = 20;
int k = 0;
k = i + j;
k += i;
k -= i;
k *= i;
k /= i;
k %= i;
```

请问每一次对 k 赋值后，k 的值变成多少？

这个程序中对于 k 的赋值操作，可以等价为：

```java
k = i + j;	// 普通的赋值操作，赋值后 k 的值为 30
k = k + i;	// k += i 等价于 k = k + i，赋值后 k 的值为 40
k = k - i;	// k -= i 等价于 k = k - i，赋值后 k 的值为 30
k = k * i;	// k *= i 等价于 k = k * i，赋值后 k 的值为 300
k = k / i;	// k /= i 等价于 k = k / i，赋值后 k 的值为 30
k = k % i;	// k %= i 等价于 k = k % i，赋值后 k 的值为 0
```

因此，每一次对 k 赋值后，k 的值分别变成 30、40、30、300、30 和 0。

事实上，这里的等价并不是完全等价，具体的内容可以参考 2.4.3 中的例 5 和例 6。

**例 2**

```java
int i = 3;
int k = j = 4;
```

这段代码是否可以编译运行，运行结果是什么？

这段代码的第一句可以编译运行，其相当于`int i; i = 3;`；而第二句语句则无法编译，其相当于`int k; k = j = 4;`，由于变量 j 并没有定义，所以会编译出错。

##### 2.4.2 算术运算

算术运算主要是指加法、减法、乘法、除法和求余这几个基本操作。接下来我们通过几个例子来具体看一下：

**例 1**

```java
double d1 = 3 / 2 + 3 / 2.0;
double d2 = 3 % 2 * 2;
double d3 = 3 % 2.0;
```

这段代码是否可以编译运行，运行结果是什么？

这段代码只有前两句可以成功编译运行，运行后 d1 和 d2 的值分别是 2.5 和 2。

d1 的运算主要考察了除法运算。这里需要注意的是：**当除数和被除数都为整型数据时，除法运算结果为 int 型；当除数和被除数至少有一个为浮点型数据时，除法运算结果为 double 型。**所以，d1 的值为 1 和 1.5 的和，即 2.5。

d2 的运算主要考察了算术运算符的优先级。在算术运算中，优先级最高的是括号，接着是 %、* 和 /，最后才是加法和减法运算。另外，算术运算是从左至右的结合方向。所以这行代码是从左至右进行计算。因此，d2 的值为 2。

d3 的运算主要考察了求余运算。**求余运算只能运用于整型数据。**因此，这行代码并不能成功编译。

##### 2.4.3 数值类型转换

在 2.4.2 赋值运算和 2.4.3 算术运算中，我们所涉及到的运算基本上都是同种数据类型之间的运算，那么当参与运算的数据类型不一致的时候，Java 会怎样处理呢？这实际上涉及到数值之间的类型转换。这里我们先给出八种基本数据类型（boolean / byte / char / short / int / long / float / double）之间的类型转换规则：

1. boolean 类型与其他基本数据类型不能进行类型的转换
2. 数据类型以 byte / char / short / int / long / float / double 的顺序，从左至右的类型转换遵守类型自动提升的规则，而从右至左的类型转换则需要采用强制转换。特别需要注意的是，byte 并不能自动提升为 char，char 也不能自动提升为 short
3. 在 Java 中，对于未声明数据类型的整型，其默认类型为 int；对于未声明数据类型的浮点型，其默认类型为 double

接下来我们通过几个例子来具体看一下：

**例 1**

```java
boolean boolean_b = 0;
byte byte_b = 0;
boolean_b = (boolean) byte_b;
```

这段代码是否可以编译运行？

这段代码的第一行和第三行都会提示编译错误信息。其中第一行代码中 0 在 Java 中默认类型为 int（根据规则 3），而根据规则 1，boolean 不能与其他数据类型进行数据类型转换，所以会出现编译错误；同样的，第三行代码也会提示编译错误。

但是第二行代码按照我们刚才的分析，应该是会出现编译错误的。因为 int 类型转 byte 数据类型，理应进行强制类型转换的。那么为什么它可以编译成功呢？

原因在于：**当默认类型为 int 的数值赋给一个比 int 数值范围小的数据类型变量（byte / char / short）时，会进行判断。如果数值不在该数据类型的取值范围内，则会提示编译出错，需要进行强制类型转换，反之则会编译成功，无需强制类型转换。**这里需要特别注意的是，这条规则只适用于默认类型为 int 的数值，并不适用于直接以 int 定义的变量。像`int i = 0; byte j = i;`这样的语句是会提示编译错误的。

**例 2**

```java
long l1 = 10000000000;
long l2 = 10000000000L;
float f1 = 1.0;
float f2 = 1.0F;
```

这段代码是否可以编译运行？

这段代码的第一行和第三行都会提示编译错误信息。

在第一行代码中，10000000000 默认为 int 类型，但是由于 10000000000 已经超过 int 型取值范围的最大值，所以会提示编译错误；而第二行代码中，在数值后加上 L 可以使数值定义为 long 类型，此时赋值语句则会编译成功。

在第三行代码中，1.0 默认为 double 类型，但是 double 类型转 float 类型需要进行强制类型转换，所以会提示编译错误；而第四行代码中，在数值后加上 F 可以使数值定义为 float 类型，此时赋值语句则会编译成功。

**例 3**

```java
byte byte_b = 0;
char char_c = 0;
short short_s = 0;
char_c = byte_b;
short_s = char_c;
```

这段代码是否可以编译运行？

这段代码的第四行和第五行都会提示编译错误信息。根据上面规则 2 提及的特殊情况，我们可以知道这样的赋值是错误的。要想成功赋值，必须进行强制类型转换方可以赋值成功。

这里是因为 char 本身是 unsigned 类型，所以考虑到负数的问题，代码中所涉及到的自动类型转换才没有被允许。

**例 4**

```java
int int_i = 233;
byte byte_b = (byte) int_i;
```

运行这段代码后，变量 byte_b 的值是多少？

byte_b 的值分别是 -23。int 型总共有 32 位，所以 233 表示为二进制数为 24 位 0 + 11101001，而 byte 型只有 8 位，所以从高位开始舍弃得 byte_b 的二进制表示为：11101001，转换为十进制便是 -23。注意，在计算机中，二进制表示形式通常为补码形式。

**例 5**

```java
int int_i = 1;
float float_f = 2;
int_i = int_i + float_f;
int_i = (int) (int_i + float_f);
int_i += float_f;
```

这段代码是否可以编译运行？

这段代码的第三行会提示编译错误信息。**当两个不同数据类型进行算术运算的时候，较小的数据类型会自动转换为较大的数据类型。**所以，int_i 会提升为 float 型，最后运算的结果也是 float 型，而 float 型转换为 int 型需要进行强制类型转换。因此，第三行代码编译错误，第四行代码编译成功。

那么，第五行代码不是应该与第三行代码等价吗？为什么它不会提示编译错误呢？实际上，`+=`符号带有**自动类型转换**的作用（同理，`-=`、`*=`、`/=`和`%=`亦然），所以不会提示编译错误。

**例 6**

```java
byte b1 = 1;
byte b2 = 2;
b2 = b1 + b2;
```

这段代码是否可以编译运行？

这段代码的第三行会提示编译错误信息。**byte 类型之间的算术运算结果都为 int 类型。**因此，int 类型不能直接转换为 byte 类型，所以会提示编译错误。实际上，这道题如果使用`b2 += b1;`的语句，则可以编译成功，因为`+=`符号具有自动类型转换功能。

##### 2.4.4 自增自减运算

自增自减运算的作用是让变量的值在运算前（前缀式）或运算后（后缀式）加一（自增运算符）或减一（自减运算符）。接下来我们通过几个例子来具体看一下：

**例 1 **

```java
int i = 0;
int j = i++;
int k = --i;
```

运行这段代码后，变量 i、j 和 k 的值分别是多少？

i、j 和 k 的值分别是 0、0 和 0。

在第二行代码中，使用到的运算符号是后缀自增运算符。它的作用是让 i 的值在运算后加一，其等价代码如下：

```java
int j = i;	// 将 i 的值 0 赋给 j，所以 j 的值为 0
i = i + 1;	// i 的值加一，所以 i 的值为 1
```

在第三行代码中，使用到的运算符号是前缀自减运算符。它的作用是让 i 的值在运算前减一，其等价代码如下：

```java
i = i - 1;	// i 的值减一，所以 i 的值为 0
int k = i;	// 将 i 的值 0 赋给 k，所以 k 的值为 0
```

因此，我们可以得到 i、j 和 k 的值分别是 0、0 和 0。

**注：这里我们的等价代码实际上不够严谨，我们将在例 3 中进行补充说明**

**例 2 **

```java
int i = 0;
int j = 2 * ++i;
int k = 2 * i--;
```

运行这段代码后，变量 i、j 和 k 的值分别是多少？

i、j 和 k 的值分别是 0、2 和 2。

在这个程序中，我们需要掌握的是**自增自减运算符的优先级高于四则运算符**，关于运算发优先级的内容可以参见 2.4.8 。

在第二行代码中，使用到的运算符号是前缀自增运算符。它的作用是让 i 的值在运算前加一，所以 i 的值先自增为 1，然后 j 的值通过乘法运算初始化为 2。

在第三行代码中，使用到的运算符号是后缀自减运算符。它的作用是让 i 的值在运算后减一，所以 k 的值先通过乘法运算初始化为 2，然后 i 的值自减为 0。

因此，我们可以得到 i、j 和 k 的值分别是 0、2 和 2。

**例 3 **

```java
int i = 0, j = 0;
i = i++;
j = --j;
```

运行这段代码后，变量 i 和 j 的值分别是多少？

i 和 j 的值分别是 0 和 -1。

看完例 1 和例 2 后，你可能对这个结果存在疑问。我们先用前面的思维对代码进行分析。

在第二行代码中，i 的值先被 i 赋值为 0，然后 i 自增为1；同理可得，j 的值为 -1。那么为什么最后得到的答案与我们分析的有偏差呢？

**实际上，Java 编译器在遇到自增自减运算符的时候都会为变量重新开辟一块内存空间，用来存储运算时的值。等到运算结束后，在将这块内存释放掉。**根据这一点，我们可以得到例子中第二行和第三行的等价代码：

```java
// 第二行代码
int temp1 = i;	// 开辟一块内存空间存储运算时的值，即 0
i = i + 1;	// i 进行自增操作后，值变成 1
i = temp1;	// 将运算时的值赋给 i，则 i 的值为 0

// 第三行代码
int temp2 = j - 1;	// 开辟一块内存空间存储运算时的值，即 -1
j = j - 1;	// j 进行自减操作后，值变成 -1
j = temp2;	// 将运算时的值赋给 j，则 i 的值为 -1
```

从上面的分析我们可以看到`i = i++;`和`j = --j;`这样的语句使我们的代码显得不够清晰，容易让我们的程序出现错误。所以，在实际工作中，我们应该尽可能避免写出这样的语句。如果我们要单纯实现自增自减的话，直接使用`i++;`或`j--;`之类的语句就可以了。

从这个分析中，我们也隐约可以感觉到，自增自减符的运算过程中，运算和自增自减貌似是独立的。实际上，自增自减运算符并不是线程安全的操作。关于线程安全这一块的内容，我们将在第 11 章中进行讲解。

**例 4**

```java
float f = 0.1f;
f++;
double d = 0.1;
d++;
char c = 'a';
c++;
```

这段代码是否可以编译运行，运行结果是什么？

这段代码是可以编译运行的，运行之后 f、d 和 c 的值分别是 0.2，0.2 和 ‘b’。

自增自减运算符实际上不仅可以用于整数类型，也可以用于浮点类型以及字符串类型char。另外，它们也可以用于 2.8 中的大数值。

自增自减运算符运算结果的类型与被运算的变量类型一致。

##### 2.4.5 关系运算

##### 2.4.6 逻辑运算

##### 2.4.7 位运算

##### 2.4.8 其他运算

##### 2.4.9 运算符优先级和结合方向

#### 2.5 字符串

#### 2.6 输入输出

#### 2.7 控制流程

#### 2.8 大数值

#### 2.9 方法

#### 2.10 数组

##### 2.10.1 数组的基本操作

数组可以看成是多个数据类型相同的数据的组合。其声明语法如下：

```java
// 可选声明语法 1
dataType[] var;
// 可选声明语法 2
dataType var[];
```

尽管这两种声明语法在 Java 中都是可行的，但我们一般优先选择第一种。第一种声明语法更加规范。接下来我们使用第一种声明语法来定义一个数据类型为 int 的数组：

```java
int[] arr;
```

声明数组之后我们就可以创建数组了，创建数组的方法也有两种：

```java
// 声明一个 int 型数组，然后创建一个容量为 10 的数组
int int_array = new int[10];
// 声明一个 double 型数组，通过初始化的方式创建一个容量为 2 的数组
double double_array = { 1.1, 2.2 };
```

数组的元素是通过索引访问的。数组索引的取值范围从 0 到数组长度 - 1。在 Java 中，数组长度可以通过`.length`获得。接下来我们通过一个例子来简单看一下数组的基本操作：

```java
int[] int_array = { 1, 3, 2, 5 };
for (int i = 0; i < int_array.length; i++) {
	System.out.print(int_array[i] + " ");
}
```

这个程序编译运行后的输出为：

```java
1 3 2 5
```

实际上，对数组的遍历除了普通的 for 循环之外，还可以采用 foreach 语句。将上面的代码改成 foreach 语句，结果如下：

```java
int[] int_array = { 1, 3, 2, 5 };
for (int i : int_array) {
	System.out.print(i + " ");
}
```

foreach 语句的主要优势在于其简单方便，但实际上效率效率并不如 for 循环，所以 for 循环的使用更为普遍。另外需要特别注意的是：**foreach 语句只能读取元素，而不能修改元素。**这主要是因为 foreach 遍历元素的时候实际上是把每个元素的值赋给其定义的临时变量，其真正操作的是这个临时变量。我们看下面这个例子：

```java
int[] int_array = { 1, 3, 2, 5 };
for (int i : int_array) {
	i = 0;
}
for (int i : int_array) {
	System.out.print(i + " ");
}
```

这个程序的编译运行后的输出为：

```java
1 3 2 5
```

而不是：

```java
0 0 0 0
```

##### 2.10.2 数组作为方法的参数和返回值

##### 2.10.3 多维数组 

##### 2.10.4 Arrays 类

### 第 3 章 对象和类

### 第 4 章 继承和多态

### 第 5 章 接口、抽象类和内部类

### 第 6 章 异常处理

### 第 7 章 泛型

### 第 8 章 容器

### 第 9 章 Java I/O 系统

### 第 10 章 注解

### 第 11 章 并发