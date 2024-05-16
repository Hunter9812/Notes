# 基本的输入输出

C++ 标准库提供了一组丰富的输入/输出功能，我们将在后续的章节进行介绍。本章将讨论 C++ 编程中最基本和最常见的 I/O 操作。

C++ 的 I/O 发生在流中，流是字节序列。如果字节流是从设备（如键盘、磁盘驱动器、网络连接等）流向内存，这叫做**输入操作**。如果字节流是从内存流向设备（如显示屏、打印机、磁盘驱动器、网络连接等），这叫做**输出操作**。

## I/O 库头文件

下列的头文件在 C++ 编程中很重要。

| 头文件     | 函数和描述                                                   |
| ---------- | ------------------------------------------------------------ |
| <iostream> | 该文件定义了 **cin、cout、cerr** 和 **clog** 对象，分别对应于标准输入流、标准输出流、非缓冲标准错误流和缓冲标准错误流。 |
| <iomanip>  | 该文件通过所谓的参数化的流操纵器（比如 **setw** 和 **setprecision**），来声明对执行标准化 I/O 有用的服务。 |
| <fstream>  | 该文件为用户控制的文件处理声明服务。我们将在文件和流的相关章节讨论它的细节。 |

## 标准输出流（cout）

预定义的对象 **cout** 是 **iostream** 类的一个实例。cout 对象"连接"到标准输出设备，通常是显示屏。**cout** 是与流插入运算符 << 结合使用的，如下所示：

```cpp
#include <bits/stdc++.h>
using namespace std;
int main()
{
    char str[] = "Fuck you very much";
    cout << str << endl;
    return 0;
}
```

- [C++中setiosflags(ios::fixed)与setprecision( 1 )的用法](https://www.cnblogs.com/nzpdbk/p/16684373.html)

## 标准输入流（cin）

预定义的对象 **cin** 是 **iostream** 类的一个实例。cin 对象附属到标准输入设备，通常是键盘。**cin** 是与流提取运算符 >> 结合使用的，如下所示：

```cpp
#include<bits/stdc++.h>
using namespace std;
int main()
{
    char name[50];
    cout << "请输入你的名字：" << endl;
    cin >> name;
    cout << name << endl;
    return 0;
}
```

C++ 编译器根据要输入值的数据类型，选择合适的流提取运算符来提取值，并把它存储在给定的变量中。

流提取运算符 >> 在一个语句中可以多次使用，如果要求输入多个数据，可以使用如下语句：

```cpp
cin >> name >> age;
```

这相当于下面两个语句：

```cpp
cin >> name;
cin >> age;
```

1. std::ios::sync_with_stdio(false);

    C++为了兼容C，默认使iostream与stdio关联，使cin与scanf、cout和printf保持同步，保证混用过程中文件指针不混乱。
     此方式会造成性能损失，导致使用cin/cout效率远远低于使用scanf/printf。若保证程序只是用一套指令，可取消同步：

    ```cpp
    std::ios::sync_with_stdio(false);
    ```

    取消后使用cin/cout速度有明显提升，但注意不要混用iostream与stdio

    ```cpp
    std::cin.tie(0);
    ```

    当传入参数为0时，实现cin与cout独立运行，不会等待，提高cin速度

    全局域的通过静态常量初始化一个lambda的方式实现对此代码的优先调用

    ```cpp
    static const int _ = []() {
        ios::sync_with_stdio(false);
        cin.tie(nullptr);
        cout.tie(nullptr);
        return 0;
    }();
    ```

2. `sort(_RandomAccessIterator __first, _RandomAccessIterator __last,_Compare __comp)`

    `greater<int>()`表示内置类型从大到小排序，`less<int>()`表示内置类型从小到大排序

3. 将字符变成数

    - ch-48：48是'0'的ASCII码值。

    - ch^48：异或，转换成数的时候和ch-48效果相同。

        > 异或，英文为exclusive OR，缩写成xor
        >
        > 异或也叫半加运算，其运算法则相当于不带进位的二进制加法：二进制下用1表示真，0表示假，则异或的运算法则为：0⊕0=0，1⊕0=1，0⊕1=1，1⊕1=0（同为0，异为1），这些法则与加法是相同的，只是不带进位，所以异或常被认作**不进位加法**。

4. 

    

### **ps:**

- **C++ 输入多个字符，中间用一个字符隔开。**

    好像 C++ 没有像 scanf 控制的那么精确，有个 cin.get() 是可以忽略掉一个字符的，但那个字符可以是任何字符，不限定是逗号。

    比如:

    ```
    cin>>a;cin.get();
    cin>>b;cin.get();
    cin>>c;
    ```

    你输入 **1, 2, 3** 或者 **1a2b3** 都可以。

- 注意 **cin** 输入的时候是按照空白字符（不管是换行还是回车）分割的。

    如果要按空格分割直到回车:

    ```
    while( cin >> a ){
        ...
        if(cin.get()=='\n'){
            break;
        }
    }
    ```

    **cin.get()** 则是直接读取，不忽略空白字符缓冲。

## 标准错误流（cerr）

预定义的对象 **cerr** 是 **iostream** 类的一个实例。cerr 对象附属到标准输出设备，通常也是显示屏，但是 **cerr** 对象是非缓冲的，且每个流插入到 cerr 都会立即输出。

**cerr** 也是与流插入运算符 << 结合使用的，如下所示：

```cpp
#include<bits/stdc++.h>
using namespace std;
int main()
{
    char str[] = "Unable to read……";
    cerr << "Error message : " << str << endl;
    return 0;
}
```

## 标准日志流（clog）

预定义的对象 **clog** 是 **iostream** 类的一个实例。clog 对象附属到标准输出设备，通常也是显示屏，但是 **clog** 对象是缓冲的。这意味着每个流插入到 clog 都会先存储在缓冲区，直到缓冲填满或者缓冲区刷新时才会输出。

**clog** 也是与流插入运算符 << 结合使用的，如下所示：

```cpp
#include<bits/stdc++.h>
using namespace std;
int main()
{
    char str[] = "Unable to read……";
    clog << "Error message : " << str << endl;
    return 0;
}
```

通过这些小实例，我们无法区分 cout、cerr 和 clog 的差异，但在编写和执行大型程序时，它们之间的差异就变得非常明显。所以良好的编程实践告诉我们，使用 cerr 流来显示错误消息，而其他的日志消息则使用 clog 流来输出。

# 注释

C++ 支持单行注释和多行注释。注释中的所有字符会被 C++ 编译器忽略。

C++ 注释一般有两种：

- // - 一般用于单行注释。
- /* ... */ - 一般用于多行注释。

**ps:**

- 块注释符（`/*...*/`）是不可以嵌套使用的。

- \#if 0 ... #endif 属于条件编译，0 即为参数。

    此外，我们还可以使用 #if 0 ... #endif  来实现注释，且可以实现嵌套，格式为：

    ```
    #if 0
       code
    #endif 
    ```

    你可以把 #if 0 改成 #if 1 来执行 **code** 的代码。

    这种形式对程序调试也可以帮助，测试时使用 **#if 1** 来执行测试代码，发布后使用 **#if 0** 来屏蔽测试代码。

    **#if** 后可以是任意的条件语句。

    下面的代码如果 condition 条件为 true 执行 code1 ，否则执行 code2。

    ```
    #if condition
      code1
    #else
      code2
    #endif
    ```

# 数据类型

使用编程语言进行编程时，需要用到各种变量来存储各种信息。变量保留的是它所存储的值的内存位置。这意味着，当您创建一个变量时，就会在内存中保留一些空间。

您可能需要存储各种数据类型（比如字符型、宽字符型、整型、浮点型、双浮点型、布尔型等）的信息，操作系统会根据变量的数据类型，来分配内存和决定在保留内存中存储什么。

## 基本的内置类型

C++ 为程序员提供了种类丰富的内置数据类型和用户自定义的数据类型。下表列出了七种基本的 C++ 数据类型：

| 类型     | 关键字  |
| -------- | ------- |
| 布尔型   | bool    |
| 字符型   | char    |
| 整型     | int     |
| 浮点型   | float   |
| 双浮点型 | double  |
| 无类型   | void    |
| 宽字符型 | wchar_t |

其实 wchar_t 是这样来的：

```cpp
typedef short int wchar_t;
```

所以 wchar_t 实际上的空间是和 short int 一样。

# 修饰符类型

C++ 允许在 **char、int 和 double** 数据类型前放置修饰符。修饰符用于改变基本类型的含义，所以它更能满足各种情境的需求。

下面列出了数据类型修饰符：

- signed
- unsigned
- long
- short

修饰符 **signed、unsigned、long 和 short** 可应用于整型，**signed** 和 **unsigned** 可应用于字符型，**long** 可应用于双精度型。

修饰符 **signed** 和 **unsigned** 也可以作为 **long** 或 **short** 修饰符的前缀。例如：**unsigned long int**。

C++ 允许使用速记符号来声明**无符号短整数**或**无符号长整数**。您可以不写 int，只写单词 **unsigned、short** 或 **long**，**int** 是隐含的。例如，下面的两个语句都声明了无符号整型变量。

```cpp
unsigned x;
unsigned int y;
```

# 关键字

## auto

> 自 C++ 11 以来，**auto** 关键字用于两种情况：声明变量时根据初始化表达式自动推断该变量的类型、声明函数时函数返回值的占位符。
>
> C++98标准中auto关键字用于自动变量的声明，但由于使用极少且多余，在 C++17 中已删除这一用法。

C++中auto的用法：

auto是C++11标准中引入的关键字，是根据后面的值来推测前面的变量类型是什么，对于简化代码具有重要意义。
 1.auto的原理是通过后面的值来推断变量类型，因此后面的值必须存在且类型明确，即auto变量必须被正确地初始化；
 2.auto并非单独的类型，其不能用于类型转换等操作；
 3.auto序列的多个变量必须为同一类型。

【注意点】
 适用场景：

- auto是在C++11中被引入的关键字，需要支持C++11标准的编译器，像一些老版本的gcc编译器需要在命令行输入`-std=c++11`来激活C++11用法；
- 如前文所述，auto可替换一些书写很长的类型长度；
- 函数返回值不确定时，可以使用auto来替代，由编译器自动推导。
     （注：这是C++14中引入的用法，因此在低于C++14版本中可能会报错，因此推荐使用void）
- 函数参数类型中不能用auto，否则会报错，如：`int func(auto,auto);`这样的代码会报错；
- 类的成员变量不能用auto；静态成员变量可以使用auto，但需要使用const修饰，且需要在类内初始化；
- 在需要C与C++兼容的代码中不要使用auto，因为auto在C语言和C++语言中的意思是完全不同的。在C语言中，auto是类型说明符，省去auto表示都是自动变量。非自动变量须显式声明类型（static、register和extern）。

auto常用于使用STL的C++代码中，这类代码类型声明处通常比较长，需要用auto代替来简化代码；auto由编译器自动推导。

## const

您可以使用 **const** 前缀声明指定类型的常量，如下所示：

```cpp
const type variable = value;
```

- 1.const  定义常量之后，是不能够改变的

    2.宏定义是可以取消的

    ```cpp
    定义：
    #define N 21
    取消： 
    #undef N 12
    ```

- 请注意，把常量定义为大写字母形式，是一个很好的编程实践。

    1、const 关键字出现在 * 的左边：指针指向的内容不能被修改。

    2、const 关键字出现在 * 的右边：指针本身不能被修改。

    3、const 关键字出现在 * 的两边：指针指向的内容和指针本身都不能被修改。

- 

# 搜索

1. ```cpp
    #include<bits/stdc++.h>
    using namespace std;
    #define ll long long
    #define inf 0x3f3f3f3f
    #define mem(a,b) memset(a,b,sizeof(a))
    #define closeio std::ios::sync_with_stdio(false)
    ```
