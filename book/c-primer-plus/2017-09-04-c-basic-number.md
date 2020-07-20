
C 语言中的一些基本数据类型整理。

# 基本数据类型


* 最小的存储单元是位（bit），可以存储0或1，位是计算机内存的基本构件块。
* 字节（byte）是常用的计算机存储单位。对于几乎所有的机器，1字节均为8位。
* 字（word）是设计计算机时给定的自然存储单位。对于8位的微型计算机，1个字长只有8位，之后逐步增长到16位，32位，直到目前的64位。

* 计算机把浮点数分成小数部分和整数部分来表示，而且分开存储这两部分。

## int 类型

* `int` 类型是有符号整型。其取值范围依计算机系统而已。一般而言，储存一个 int 占用一个字长，ISO C 规定 int 的取值范围最小为 -32768-32767（16位下）。
* 十六进制以 0x 或者 0X 开头，八进制以 0 开头。

其他整数类型：

* `short int` 类型（简写 `short` ）占用的存储空间可能比 int 类型少，常用于较小数值以节省空间,至少占 16 位。
* `long int` 类型（简写 `long` ）占用的空间可能比 int 类型多，适用于较大数值的场合，至少占 32 位。
* `long long int` 或 `long long` 占用的空间可能比 long 多，至少占 64 位。
* `unsigned int` 或 `unsigned` 只用于非负值的场合。用于表示正负号的位现在用于表示另一个二进制位，所以无符号整数可以表达更大的数。
* C90 标准中，添加了 `unsigned long int/unsigned long` 和 `unsigned short int/unsigned short`。C99 标准又添加了 `unsigned long long int/unsigned long long` 。
* 单独的 unsigned 相当于 unsignedint 。

C 规定了 short 占用的存储空间不能多于 int ，long 占用的存储空间不能少于 int。这是为了使用不用的机器。

##　char 类型

`char` 类型用于存储字符，但是从技术层面看，char 是整数类型。因为 char 类型实际上存储的是整数而不是字符。计算机使用数字编码来处理字符，即用特定的整数表示特定的字符，例如 ASCII 编码。

标准 ASCII 编码的范围是0-127，只需7位二进制数。通常，char 类型被定义位8位的存储单元，容纳标准 ASCII 编码绰绰有余。

## 可移植类型：stdint.h 和  inttypes.h

C99 新增，以确保 C语言的类型在各系统中的功能相同。

例如：int32_t 表示 32 位有符号整数。在使用 32 位 int 的系统中，头文件会把 int32_t 作为 int 的别名。而在 16 位 int，32 位 long 的系统中，会作为 long 的别名。

## float，double 和 long double

* `float` 类型必须至少能表示 6 位有效数字，且取值范围至少是 10^-37~10^37。通常，系统储存一个浮点数要占用 32 位，其中 8 位用于表示指数的值和符号，剩下 24 位用于表示非指数部分及其符号。

* `double` 和 float 的最小取值范围相同，但至少必须能表示 10 位数字。一般情况下， double 占用 64 位。

* `long double` 以满足比 double 类型更高的精度要求。不过，C 只保证 long double 类型至少与 double 类型的精度相同。

常见写法： `-1.56e+12` `2.87e-3` `3.14159` `.2` `4e16` `.8e-6` `100.`

正号可以省略，可以没有小数点或者指数部分，但是不能同时省略两者。
可以省略小数部分或者整数部分，但是不能同时省略两者。
默认情况下，编译器默认浮点型常亮是 double 类型的精度。

后缀：f/F -> float   l/L long -> double  无后缀 -> double

## 复数和虚数类型

3 种复数类型：`float_Complex` `double_Complex` `long double_Complex`
3 种虚数类型: `float_Imaginary` `double_Imaginary` `long double_Imaginary`

## _Bool 类型

C99 标准添加了 `_Bool` 类型，用于表示布尔值，用值1表示 true ，值0表示 false，所以 _Bool 类型实际上也是一种整数类型，但是原则上仅占用1位存储空间。

sizeof 是 C 语言的内置运算符，以字节为单位给出指定类型的大小
