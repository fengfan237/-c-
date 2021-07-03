# 关键字

# ***const***

![image-20210625150638333](C:\Users\ff\AppData\Roaming\Typora\typora-user-images\image-20210625150638333.png)

![image-20210625150834583](C:\Users\ff\AppData\Roaming\Typora\typora-user-images\image-20210625150834583.png)

![image-20210625150919077](C:\Users\ff\AppData\Roaming\Typora\typora-user-images\image-20210625150919077.png)

![image-20210625151026539](C:\Users\ff\AppData\Roaming\Typora\typora-user-images\image-20210625151026539.png)

# *static_cast*

static_cast相当于传统的C语言里的强制转换，该运算符把expression转换为new_type类型，用来强迫隐式转换，例如non-const对象转为const对象，编译时检查，用于非多态的转换，可以转换指针及其他，但*没有运行时类型检查来保证转换的安全性*。它主要有如下几种用法：

①用于类层次结构中基类（父类）和派生类（子类）之间指针或引用的转换。

*进行上行转换（把派生类的指针或引用转换成基类表示）是**安全**的；*

*进行下行转换（把基类指针或引用转换成派生类表示）时，由于没有动态类型检查，所以是**不安全**的。*

②用于基本数据类型之间的转换，如把int转换成char，把int转换成enum。这种转换的安全性也要开发人员来保证。

③把空指针转换成目标类型的空指针。

④把任何类型的表达式转换成void类型。

注意：static_cast不能转换掉expression的const、volatile、或者__unaligned属性

![image-20210625163857661](C:\Users\ff\AppData\Roaming\Typora\typora-user-images\image-20210625163857661.png)



# *dynamic_cast*

```
dynamic_cast<type*>(e)
dynamic_cast<type&>(e)
dynamic_cast<type&&>(e)
```

type必须是一个类类型，在第一种形式中，type必须是一个有效的指针，在第二种形式中，type必须是一个左值，在第三种形式中，type必须是一个右值。在上面所有形式中，e的类型必须符合以下三个条件中的任何一个：e的类型是是目标类型type的公有派生类、e的类型是目标type的共有基类或者e的类型就是目标type的的类型。如果一条dynamic_cast语句的转换目标是指针类型并且失败了，则结果为0。如果转换目标是引用类型并且失败了，则dynamic_cast运算符将抛出一个std::bad_cast异常(该异常定义在typeinfo标准库头文件中)。e也可以是一个空指针，结果是所需类型的空指针。

![image-20210625164131496](C:\Users\ff\AppData\Roaming\Typora\typora-user-images\image-20210625164131496.png)

# *const_cast*



const_cast，用于修改类型的const或volatile属性。 

该运算符用来修改类型的const(唯一有此能力的C++-style转型操作符)或volatile属性。除了const 或volatile修饰之外， new_type和expression的类型是一样的。

①常量指针被转化成非常量的指针，并且仍然指向原来的对象；

②常量引用被转换成非常量的引用，并且仍然指向原来的对象；

③const_cast一般用于修改底指针。如const char *p形式。

![image-20210625164203426](C:\Users\ff\AppData\Roaming\Typora\typora-user-images\image-20210625164203426.png)



# *explicit:*

被explicit关键字修饰的类构造函数，不能进行自动地隐式类型转换，只能显式地进行类型转换。

![image-20210625150252918](C:\Users\ff\AppData\Roaming\Typora\typora-user-images\image-20210625150252918.png)

![image-20210625150324344](C:\Users\ff\AppData\Roaming\Typora\typora-user-images\image-20210625150324344.png)



# *pragma*

#pragma指令的作用是：用于指定计算机或操作系统特定的编译器功能。C 和 C++ 的每个实现均支持某些对其主机或操作系统唯一的功能。 例如，某些程序必须对将数据放入的内存区域进行准确的控制或控制某些函数接收参数的方式。 在保留与 C 和 C++ 语言的总体兼容性的同时，#pragma 指令使每个编译器均能够提供特定于计算机和操作系统的功能。

根据定义，#pragma指令是计算机或操作系统特定的，并且通常对于每个编译器而言都有所不同。 #pragma指令可用于条件语句以提供新的预处理器功能，或为编译器提供实现所定义的信息。

语法是：

```
1 #pragma  token-string
2 __pragma( token-string )	//__pragma 关键字是特定于 Microsoft 编译器的
```

token-string 是一系列字符，这些字符提供了特定的编译器指令和参数（如果有）。 数字符号"#" 必须是位于包含#pragma指令行上的第一个非空白字符；空白字符可以分隔数字符号和词“pragma”。 在 #pragma 之后，编译转换器可分析为预处理标记的所有文本。 #pragma 的参数受宏展开的约束，如果编译器发现它无法识别的杂注，则它会发出警告并继续编译。

#### #pragma once:

大家应该都知道：指定该文件在编译源代码文件时仅由编译器包含（打开）一次。
使用 #pragma once 可减少生成次数，和使用预处理宏定义来避免多次包含文件的内容的效果是一样的，但是需要键入的代码少，可减少错误率，例如：

```
使用#progma once
#pragma once  
// Code placed here is included only once per translation unit 

使用宏定义方式
#ifndef HEADER_H_ 
#define HEADER_H_  
// Code placed here is included only once per translation unit  
#endif // HEADER_H_  
```

#### #pragma message（messageString）

不中断编译的情况下，发送一个字符串文字量到标准输出。message编译指示的典型运用是在编译时显示信息，例如：

```
#if _M_IX86 >= 500  		//查看定义的宏有没有大于500，或者有时用作检查有没有定义宏
#pragma message("_M_IX86 >= 500")  
#endif 
```


messagestring 参数可以是扩展到字符串的宏，您可以通过任意组合将此类宏与字符串串联起来，例如：

```
#pragma message( "Compiling " __FILE__ )   		//显示被编译的文件
#pragma message( "Last modified on " __TIMESTAMP__ ) 	//文件最后一次修改的日期和时间
```

如果在 message 杂注中使用预定义的宏，则该宏应返回字符串，否则必须将该宏的输出转换为字符串，例如：

```
#define STRING2(x) #x  
#define STRING(x) STRING2(x)  

#pragma message (__FILE__ "[" STRING(__LINE__) "]: test")   //注意把行号转成了字符串
```

# &&...

万能引用
传左值表现为左值
传右值表现为右值，右值就是无地址的值，左值有地址 



# 左值右值

首先，让我们避开那些正式的定义。在C++中，一个左值是指向一个指定内存的东西。另一方面，右值就是不指向任何地方的东西。通常来说，右值是暂时和短命的，而左值则活的很久，因为他们以变量的形式（variable）存在。我们可以将左值看作为容器（container）而将右值看做容器中的事物。如果容器消失了，容器中的事物也就自然就无法存在了

让我们现在来看一些例子：

```cpp
int x = 666; //ok
```

在这里，`666`是一个右值。一个数字（从技术角度来说他是一个字面常量（literal constant））没有指定的内存地址，当然在程序运行时一些临时的寄存器除外。在该例中，`666`被赋值（assign）给`x`，`x`是一个变量。一个变量有着具体（specific）的内存位置，所以他是一个左值。C++中声明一个赋值（assignment）需要一个左值作为它的左操作数（left operand）：这完全合法。
 对于左值`x`，你可以做像这样的操作：

```cpp
int* y = &x;  //ok
```

在这里我通过取地址操作符`&`获取了`x`的内存地址并且把它放进了`y`。`&`操作符需要一个左值并且产生了一个右值，这也是另一个完全合法的操作：在赋值操作符的左边我们有一个左值（一个变量），在右边我们使用取地址操作符产生的右值。
 然而，我们不能这样写：

```cpp
int y;
666 = y; //error!
```

可能上面的结论是显而易见的，但是从技术上来说是因为`666`是一个字面常量也就是一个右值，它没有一个具体的内存位置（memory location），所以我们会把`y`分配到一个不存在的地方。
 下面是GCC给出的变异错误提示：

> error: lvalue required as left operand of assignment

赋值的左操作数需要一个左值，这里我们使用了一个右值`666`。
 我们也不能这样做：

```cpp
int* y = &666;//   error~
```

GCC给出了以下错误提示：

> error: lvalue required as unary '&' operand`

`&`操作符需要一个左值作为操作数，因为只有一个左值才拥有地址。

### 返回左值和右值的函数

我们知道一个赋值的左操作数必须是一个左值，因此下面的这个函数肯定会抛出错误：`lvalue required as left operand of assignment`

```cpp
int setValue()
{
    return 6;
}

// ... somewhere in main() ...

setValue() = 3; // error!
```

错误原因很清楚：`setValue()`返回了一个右值（一个临时值`6`），他不能作为一个赋值的左操作数。现在，我们看看如果函数返回一个左值，这样的赋值会发生什么变化。看下面的代码片段（snippet）：

```csharp
int global = 100;

int& setGlobal()
{
    return global;    
}

// ... somewhere in main() ...

setGlobal() = 400; // OK
```

该程序可以运行，因为在这里`setGlobal()`返回一个引用（reference），跟之前的`setValue()`不同。一个引用是指向一个已经存在的内存位置（`global`变量）的东西，因此它是一个左值，所以它能被赋值。注意这里的`&`：它不是取地址操作符，他定义了返回的类型（一个引用）。



### 左值到右值的转换

一个左值可以被转换（convert）为右值，这完全合法且经常发生。让我们先用`+`操作符作为一个例子，根据C++的规范（specification），它使用两个右值作为参数并返回一个右值（译者按：可以将操作符理解为一个函数）。
 让我们看下面的代码片段：



```cpp
int x = 1;
int y = 3;
int z = x + y;   // ok
```

等一下，`x`和`y`是左值，但是加法操作符需要右值作为参数：发生了什么？答案很简单：`x`和`y`经历了一个隐式（implicit）的左值到右值（lvalue-to-rvalue）的转换。许多其他的操作符也有同样的转换——减法、加法、除法等等



### 左值引用

相反呢？一个右值可以被转化为左值吗？不可以，它不是技术所限，而是C++编程语言就是那样设计的。
 在C++中，当你做这样的事：



```cpp
int y = 10;
int& yref = y;
yref++;        // y is now 11
```

这里将`yref`声明为类型`int&`：一个对`y`的引用，它被称作左值引用（lvalue reference）。现在你可以开心地通过该引用改变`y`的值了。
 我们知道，一个引用必须只想一个具体的内存位置中的一个已经存在的对象，即一个左值。这里`y`确实存在，所以代码运行完美。
 现在，如果我缩短整个过程，尝试将`10`直接赋值给我的引用，并且没有任何对象持有该引用，将会发生什么？

```cpp
int& yref = 10;  // will it work?
```

在右边我们有一个临时值，一个需要被存储在一个左值中的右值。在左边我们有一个引用（一个左值），他应该指向一个已经存在的对象。但是`10` 是一个数字常量（numeric constant），也就是一个左值，将它赋给引用与引用所表述的精神冲突。
 如果你仔细想想，那就是被禁止的从右值到左值的转换。一个`volitile`的数字常量（右值）如果想要被引用，需要先变成一个左值。如果那被允许，你就可以通过它的引用来改变数字常量的值。相当没有意义，不是吗？更重要的是，一旦这些值不再存在这些引用该指向哪里呢？
 下面的代码片段同样会发生错误，原因跟刚才的一样：

```cpp
void fnc(int& x)
{
}

int main()
{
    fnc(10);  // Nope!
    // This works instead:
    // int x = 10;
    // fnc(x);
}
```

我将一个临时值`10`传入了一个需要引用作为参数的函数中，产生了将右值转换为左值的错误。这里有一个解决方法（workaround），创造一个临时的变量来存储右值，然后将变量传入函数中（就像注释中写的那样）。将一个数字传入一个函数确实不太方便
