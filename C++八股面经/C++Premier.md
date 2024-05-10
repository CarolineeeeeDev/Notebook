# C++ Premier

[TOC]

## 预编译、编译、链接

==预编译==：

#include <> 和include ""

搜索路径不同：

​	<>在系统规定的目录下搜索

​	""在自己的工程目录下搜索

编译：编译器将cpp文件转化为二进制文件obj

链接：链接器将obj文件与库(lib) 链接为可执行文件exe



## 输入输出

cin - 标准输入

cout - 标准输出   	 //先输出到缓冲区里面，结束后将**缓冲区**中的内容刷新到屏幕上

cerr - 输出错误

clog - 输出信息

std - 标准库的命名空间

:: - 作用域运算符

/      >> : 输入运算符

<< : 输出运算符

cin>>v1>>v2 : 顺序赋值给这两个变量

==cin可以跳过空格、制表符、换行符等空白字符==

```c++
while (std::cin>>value) //处于无效状态的istream对象会使条件变为假
{
    sum+=value;
}
```

命令行Ctrl+C是强制终止进程，Ctrl+Z是中断进程



## 注释

//  单行注释

/* */  界定符对注释，不能嵌套



## 类（class）

抽象（类）->具体（对象）

一个类定义了一个类型，以及与其相关联的一组操作



## 基本内置类型

C++是一种**静态**数据类型语言，在**编译**时进行类型检查；

C++定义了：算术类型、空类型(void)

C++对算术类型只规定了最小尺寸，没有规定具体是多大。x位 = 可以表示2^x^种状态

计算机以比特存储数据，每个比特非0即1。**可寻址的最小内存块称为字节（byte），内存的基本单元称为字（word）**

**大多数机器1字节 = 8bit ， 1字 = 32或64bit**

无符号类型unsigned可以节省空间

```c++
unsigned char c = -1;//假设char占8比特，c的值为255//0~255
signed char c2 = 256;//假设char占8比特，c2的值未定义//-128~127
```

不能将unsigned和signed一起用

进制转换：

20/*十进制*/  024/*八进制*/  0x14/*十六进制*/



## 变量

变量：具有类型、名称、可操作的存储空间。对c++程序员来说，变量(variable)和对象(object)一般是可以互换的。

### 初始化

```c++
int units_sold = 0;
int units_sold(0);
int units_sold = {0};//列表初始化
int units_sold{0};//列表初始化
//如果使用列表初始化，且初始值存在丢失信息的风险，则编译器将报错
```

默认初始化：如果定义变量没有定义初始值，则变量被赋予默认值；默认值是由变量类型决定的，同时定义变量的位置也会有影响；内置类型由定义的位置决定，**函数体之外初始化为0**。每个类各自决定其初始化对象的方式（构造函数？）

应该避免未初始化变量。

### 变量声明与定义

只声明不定义：用extern关键字

```c++
extern double pi = 3.14; //定义，不能放在函数体内部
int main()
{
    extern int i;//只声明不定义
    int j;//声明+定义
}
```

变量能且只能定义一次，但可以被声明多次。

==extern不是定义，是**声明在其他源文件中定义的非static全局变量**==

### 作用域

C++中大部分作用域都用花括号分离

作用域分为**全局作用域**和**块作用域**（在花括号内的），对应全局变量和局部变量

如果函数有可能用到某全局变量，则不宜再定义一个同名的局部变量；否则在局部变量的生命周期结束之前，局部变量会覆盖全局变量的值。也可以使用全局访问符::显式地访问全局变量(::variable)



## 复合类型：引用、指针

### 引用

为对象起的别名，把引用和它的初始值（对象）绑定在一起，而不是将初始值拷贝给引用。**引用本身并不是对象**，（没有物理空间？）所以不能定义引用的引用。引用必须初始化。

### 左值引用

```c++
int ival = 1024;
int& refVal = ival; //引用必须初始化
refVal = 2; //等同于ival = 2;
int& refVal2 = refVal; //等同于int& refVal2 = ival;
```

==C++新增右值引用==

### 指针

对地址的封装，本身就是一个对象。引用不是对象，所以不存在指向引用的指针。

取地址符（&）：获取指针所封装的地址

解引用符（*）：利用指针访问对象

```c++
int* ip1;
int* ip2;//指针定义
int ival = 42;
int* p = &ival; //p是指向ival的指针
*p = 2; //等同于ival = 2
```

### void*指针

纯粹的地址封装，**与类型无关**。可以用于存放任意对象的地址。

```c++
double obj = 3.14, *pd = &obj;
void* pv = &obj;
pv = pd;
```

### 指向指针的指针

```c++
int ival = 1024;
int* pi = &ival;
int** ppi = &pi;
```

### 指针的引用

```c++
int ival = 1024;
int* pi = &ival;
int*& r = pi; // r = &ival;

*r = 0; //等同于ival = 0；
```



## const限定符

const把变量变成一个常量，对变量的类型加以限定，变量的值不能被改变。 

**const对象必须初始化。**

如果想在多个文件之间共享const对象，必须在变量的定义之前添加**extern**关键字。

### ==const引用==

对常量的引用。不能通过一个非const引用指向一个const。

```c++
const int ival = 4;
const int& refVal = ival;
```

### ==常量指针==：

```c++
double pi = 3.14;
const double* ptr = &pi;
//ptr可变，*ptr不可变
```

### ==指针常量==：

```c++
double pi = 3.14;
double* const pip = &pi;
//pip不可变，*pip可变
```

### 常量表达式

值不会改变并且在编译过程就能得到计算结果的表达式。

```c++
const int max_files = 20;
const int limit = max_files + 1;
```

### constexpr变量

C++11规定允许将变量声明为constexpr类型，以便编译器来验证变量的值是否是一个常量表达式。

```c++
constexpr int max_files = 20;
constexpr int limit = max_files + 1;
```



## ==typedef、auto、decltype==

### typedef

类型别名：提高可读性

```c++
typedef double wages;
wages hourly, weekly;

typedef wages base, *p;//base是double的同义词，p是double*的同义词
```

==using ： C++11别名声明==

```c++
using SI = Sales_Item;
SI Item;
```

### auto

C++11新特性，让编译器通过初始值推断变量的类型

### decltype

选择并返回操作数的数据类型；只要数据类型，不要其值



## 自定义数据结构

类定义：类定义可以使用关键字class或struct，最后要加上分号

==二者默认的继承访问权限不同：struct默认是public的，class默认是private的==

数据成员定义了类的对象的具体内容，每个对象有自己的一份拷贝

编写头文件：

预处理变量有两个状态：已定义和未定义

#ifndef, #ifdef, #define, #endif是预处理器在编译之前执行的代码，在这里的作用是==**头文件保护**==

```c++
#ifndef SALES_DATA_H
#define SALES_DATA_H

#include <string>

struct Sales_data
{
      std::string bookNo;
      unsigned units_sold = 0;
      double revenue = 0.0;
};

#endif
```



## 命名空间的using声明

using namespace nameSpaceName;

头文件不应该包含using声明，因为会被拷贝到引用该头文件的文件中。



## 标准库类型string（STL）

可以当作容器，装char型。最后一位装的是'\0'。

string内存是连续的，大小是可变的，可以用下标访问。

初始化：

```c++
string s1;
string s2 = s1;
string s3 = "hiya";
string s4(10,'c');
```

 cin.ignore(std::numeric_limits < std::streamsize > ::max(), '\n');可以忽略掉之前留在输入流中的换行符

### ==string操作==

==C++中，字符串字面值并不是string对象==

| 代码            | 操作                                                         |
| --------------- | ------------------------------------------------------------ |
| cout<<st        | 将st写到输出流中                                             |
| cin>>st         | 输入到st中（碰见空字符时候停止）                             |
| getline(cin,st) | 读取一行赋值给st，返回st（碰见换行符时候停止）               |
| st.empty()      | st为空返回true，否则返回false                                |
| st.size()       | 返回st中字符个数                                             |
| st[n]           | 返回st中下表为n的字符的引用                                  |
| s1+s2           | 返回s1和s2连接后的结果。注意等号两边不能同时是字面值"xxx"，必须有一边是string定义的变量，借助string中==加号的重载==进行连接。 |
| s1=s2           | 用s2的副本代替s1中原来的字符                                 |
| s1==s2          | 判断s1和s2是否完全一样                                       |
| s1!=s2          | 判断s1和s2是否不完全一样                                     |
| <,<=,>=,>       | 利用字符在字典中的顺序进行比较                               |



## 标准库类型vector（STL）

### ==vector操作==

| vector操作                   |                                                              |
| ---------------------------- | ------------------------------------------------------------ |
| vector<T> v1;                | v1是一个空vector，潜在元素是T类型的                          |
| vector<T> v2(v1);            | v2包含有v1所有元素的副本                                     |
| vector<T> v2 = v1;           | 等价于v2(v1)                                                 |
| vector<T> v3(n, val);        | v3包含n个重复个元素，每个元素值都是val                       |
| vector<T> v4(n)              | v4包含n个重复地执行了值初始化的对象                          |
| vector<T> v5{a, b, c ...}    | v5包含了初始值个数的元素，每个元素都被赋予相应的初始值       |
| vector<T> v5 = {a, b, c ...} | 同上                                                         |
| vector<vector<T>> v6         | 二维数组                                                     |
| vec.empty()                  | 判断vec是否为空                                              |
| vec.size()                   | 判断vec元素个数                                              |
| vec.push_back(t)             | 向vec尾端添加一个值为t的元素                                 |
| vec[n]                       | 返回vec中第n个位置元素的引用                                 |
| vec1 = vec2                  | 用v2中的元素拷贝替换v1中的元素                               |
| vec1 = { a, b, c…}           | 用列表中的元素替换v1中的元素                                 |
| vec1 == vec2                 | v1、v2相等当且仅当他们的元素数量相同且对应位置的元素值都相同 |
| vec1 != vec2                 |                                                              |
| <,<=,>=.>                    | 以字典顺序进行比较                                           |



## 迭代器

使用迭代器可以访问某个元素，迭代器也能从一个元素移动到另一个元素

有迭代器的类型都拥有begin和end成员

begin：返回指向第一个元素（或字符）的迭代器

end：**尾后迭代器**，即尾元素的下一个位置

如果容器为空，则begin和end返回的是同一个迭代器

| 代码         | 操作                                                    |
| ------------ | ------------------------------------------------------- |
| *iter        | 返回迭代器iter所指元素的引用                            |
| iter->mem    | 解引用iter并获取该元素的名为mem的成员，等价于(iter.mem) |
| /   ++iter   | 令iter指示容器中的下一个元素（尾后迭代器除外）          |
| /   --iter   | 令iter指示容器中的上一个元素                            |
| iter1==iter2 | 如果两个迭代器指示的是同一个元素则相等，否则不等        |
| iter1!=iter2 |                                                         |

尾后迭代器并不实际指示某一个元素，所以不能对其进行递增或解引用

```c++
vector<int>::iterator it;
string::iterator it2; //迭代器类型，定义在每个容器里面

vector<string> v;
auto it = v.begin();
(*it).empty();//成员访问
it->empty();//把解引用和成员访问两个操作合在一起
```

 任何一种可能改变vector对象容量的操作，都会使得相应的迭代器失效



## 数组

### 一维数组

声明： arrayType arrayName[num];

可以使用列表初始化，但必须指定数组类型，不允许使用auto

元素个数必须是常量表达式

字符数组的特殊性：字符串字面值的结尾处还有一个空字符'\0'

==数组不允许拷贝和赋值==，因为等号右边的数组名字默认为一个指向首元素的指针了，只能用for循环一个一个赋值元素

p[num]相当于指针p向后移动num个位置对应的值

### 多维数组

声明： arrayType arrayName   [num1] [num2];

```c++
int arr[3][4] = {0};// 全部元素初始化为0
int arr[3][4] = {0,3,6,9}; // {0,3,6,9,0,0,0,0,0,0,0,0}

```

size_t大部分时候是unsigned int的别名

```c++
for (auto& row : ia) //取出每一行
{
    for (auto& col : row) //取出每个数组
    {
        
    }
}
```

```c++
for (auto row : ia) //取出的数组会被编译器转换为指针
{
    for (auto col : row) //错误， int* row没有合适的begin函数
    {
        
    }
}
```



## 表达式

一元运算符：作用于一个运算对象的运算符，如取地址符（&）和解引用符（*）

二元运算符：作用于两个运算对象的运算符，如相等和乘法

三元运算符：a?b:c

运算符重载。运算对象的个数、运算符的优先级、结合律都是无法改变的。

C++表达式要么是左值，要么是右值

==左值：能取到地址的表达式==

==右值：取不到地址的表达式==（&a）

> 某些表达式的求值结果是对象，但它们是右值

==当一个对象被作用右值的时候，用的是对象的值（内存中的内容）==

==当一个对象当作左值的时候，用的是对象的身份（内存中的位置）==

如果表达式的求值结果是左值，decltype作用于该表达式（不是变量）得到一个==引用==类型。

> 例如：对于int* p:
>
> 因为解引用生成左值，所有decltype(*p)的结果是int&
>
> 因为取地址符生成右值，所有decltype(&p)的结果是int **

对于没有指定求值顺序的运算符来说，如果表达式修改了同一个对象，将会引发错误并产生未定义行为。

> 负号的求模和取余：
>
> (-m)/n和m/(-n)都等于-(m/n)
>
> m%(-n)等于m%n，(-m)%n等于-m%n

赋值运算符左边必须是一个可修改的左值。初始化并非赋值。

### 成员访问、条件、位运算符

> 点运算符和成员运算符都可以访问成员

ptr->mem等价于(*ptr).mem

条件运算符： cond ? expr1 : expr2

> 嵌套：finalgrade == (grade > 90) ? "high pass" : (grade<60) ? "fail" : "pass"

==位运算符（左结合律）==：（没怎么听懂）

| 运算符 | 功能   | 用法         |
| ------ | ------ | ------------ |
| ~      | 位求反 | ~expr        |
| <<     | 左移   | expr1<<expr2 |
| >>     | 右移   | expr1>>expr2 |
| &      | 位与   | expr&expr    |
| ^      | 位异或 | expr^expr    |
| \|     | 位或   | expr\|expr   |

建议仅仅将位运算符用于处理无符号类型

### sizeof运算符

sizeof：返回所占的字节数

```c++
constexpr size_t sz = sizeof(ia) / sizeof(*ia); //sizeof(ia)是数组在内存中占的总字节数，sizeof(*ia)是数组第一个元素在内存中占的总字节数
```

数组名在大多数情况下会被当作指向其第一个元素的指针，但在`sizeof`、`&`以及`decltype`这类运算符的上下文中，数组名并不会退化为指针，而是代表整个数组。

## 类型转换

### 隐式转换

算术转换

指针的转换：0或字面值nullptr能够转换成任意指针类型

指向任意非常量的指针能够转换为void*，指向任意对象的指针能够转换成const void *

### ==显式转换==

强制转换 cast-name< type > (expression)

static_cast

dynamic_cast

const_cast

reinterpret_cast

```c++
int i,j;
double slope = static_cast<double>(j) /i; //static_cast:静态强制转换，只要不包含底层const，都可以使用
//动态强制转换更安全，而静态强制转换使用更快

double d;
void* p = &d;
double* dp = static_cast<double*>(p);

const char* pc;
char* p = const_cast<char*>(pc);
char* cpc;
const char* pc2 = const_cast<const char*>(cpc);
//const_cast只能改变运算对象的底层const

int* ip;
char* pc = reinterpret_cast<>char*>(ip);//类似于C风格的强制转换，char* pc = (char*) ip;
```



## ==try语句块和异常处理==

==throw表达式==：异常检测部分使用throw表达式来表示它遇到了无法解决的问题

```c++
throw runtime_error("Data must refer to same ISBN");
//抛出一个一场，终止当前的函数，并把控制权交给异常处理的代码
//runtime_error是标准库异常类型的一种，定义在stdexcept头文件
```

==try语句块==：异常处理部分使用try语句块处理异常，可以有一个或多个catch

```c++
while (cin >> item1 >> item2)
{
    try
    {
        if (item1.isbn()!=item2.isbn())
        {
            throw runtime_error("Data must refer to same ISBN");
        }
        //如果失败，代码抛出一个runtime_error异常
    }
    catch (runtime_error err)
    {
        cout<<err.what()<<endl;
    }
}
```

一套异常类：

exception头文件：最通用的异常类exception，只报告异常的发生，不提供额外信息

stdexcept头文件：定义了几种常用的异常类

new头文件：bad_alloc异常类

typeinfo头文件：bad_cast异常类



## 函数基础

### 局部对象

自动对象：生命周期从变量声明开始，到函数块末尾结束

==局部静态对象（static）==：生命周期从变量声明开始，直到程序结束才销毁

### 参数传递

传值参数

```c++
void reset(int* ip)
{
    *ip = 0;//改变指针ip所指对象的值
    ip = 0;//只改变了ip的局部拷贝，实参未被改变
}

int main()
{
    int i = 42;
    reset(&i);
    cout<<"i="<<i<<endl;
    return 0;
}
```

传引用参数，==使用引用可以避免拷贝==。如果函数无需改变引用形参的值，最好将其声明为常量引用。

```c++
void reset(int& j)
{
    j = 0;//改变了实参的值
}

int main()
{
    int j = 42;
    reset(j);
    cout<<"j="<<j<<endl;
    return 0;
}
```

const形参和实参

形参的顶层const会被忽略掉（如const int等），底层const不会（指针、引用等）

如果函数无需改变引用形参的值，最好将其声明为常量引用。

### 数组形参

C++允许将变量定义成数组的引用

```c++
void print (int (&arr)[20])//括号不能少
{
    
}

void print(int (*matrix)[10], int rowSize){};
void print(int matrix[][10], int rowSize){};//传递多维数组，实际上是指针，第一个维度可以不写，第二个维度必须写
```

如果所有实参类型相同，可以传递一个名为initializer_list的标准库类型（操作类似于vector）

### 返回类型与return

不要返回**局部对象**的引用或指针

列表初始化返回值：C++11

```c++
vector<string> process()
{
    if (expected.empty())
    {
        return{};
    }
    else if (expected == actual)
    {
        return {"functionX","okay"};
    }
    else
    {
        return {"functionX",expected.actual};
    }
}
```

返回数组指针：数组不能拷贝，所以函数不能直接返回数组

```c++
typedef int arrT[10];//arrT是一个类型别名，using arr = int[10]
arrT* func(int i);
```

### 函数重载

函数重载：函数名称相同但形参列表不同

const_cast和重载

```c++
const string& shorterString(const string& s1, const string& s2)
{
    return s1.size()<s2.size() ? s1 : s2;
}

string& shorterString(string& s1, string& s2)
{
    auto& r = shorterString(const_cast<const string&>(s1), const_cast<const string&>(s2));
    //强制转换不能省略，否则就成了递归（最佳匹配原则）
    return const_cast<string&> r;
}
```

重载与作用域

一旦在当前作用域找到了所需的名字，编译器就会忽略掉外层作用域中的同名实体

### 默认实参

一旦某个形参被赋予了默认值，它后面的所有形参都必须有默认值 

```c++
void func(int a, int b = 3, string c = "abc")
```

调用函数的时候，只能省略尾部的实参

```c+
func(5);  //相当于func(5,3,"abc")
```

多次声明同一个函数也是合法的

**constexpr函数**

能用于常量表达式的函数：函数的返回类型以及所有的形参都是字面值类型

### 调试帮助

assert预处理宏：cassert头文件中

```c++
//如果表达式为假，assert输出信息并终止程序的执行
//如果表达式为真，assert什么也不做
assert(word.size()>threshold);
```

NDEBUG预处理变量：

assert的行为依赖NDEBUG预处理变量的状态，如果定义了NDEBUG，则assert无效

```c++
#define NDEBUG //关闭调试状态，必须在cassert头文件上面
#include <cassert>

int main(void)
{
#ifdef NDEBUG
    cerr<<__func__<<": array size is"<<size<<endl;
#endif
    int x = 0;
    assert(x);
}
```

### 函数匹配

寻找最佳匹配，不能具有二义性

精确匹配->通过const转换实现的匹配->通过类型提升实现的匹配->通过算术类型转换实现的匹配->通过类类型转换实现的匹配

所有算术类型转换的级别都一样

### 函数指针

```c++
bool (*pf)(const string&, const string&); //括号不能少
```



## 抽象数据类型

类的基本思想是数据抽象（接口与实现分离）和封装（把实现藏起来）

常量成员函数：类的成员函数后面加const，表明这个函数不会修改这个类对象的数据成员

当调用一个对象的某一个成员函数的时候，会包含这个对象的地址this。this是一个指针常量。

### 类作用域和成员函数

成员体可以随意使用类中的其他成员而无需在意这些成员出现的次序

定义一个返回this对象的函数

```c++
Sales_data& Sales_data::combine(const Sales_Data &rhs)
{
    units_sold+=rhs.units_sold;
    revenue+=rhs.revenue;
    return *this;
}
```

### 构造函数

构造函数与类名同名，没有返回值，它的任务是初始化类对象的数据成员

类可以包括多个构造函数，和重载函数差不多

只有当类没有声明任何构造函数，且所有类类型的成员都有默认构造函数时，编译器才会自动地生成默认构造函数

构造函数不能声明为const

```c++
struct Sales_data
{
    Sales_data() = default; //有另外的构造函数，所以不能少
    Sales_data(const std::string &s) : bookNo(s){};
    Sales_data(const std::string &s, unsigned n, double p): bookNo(s), units_sold(n), revenue(p*n){};
    
    //之前已有的其他成员函数
    std::string isbn const{return bookNo;}//前面加const表示返回常量，后面加const表示函数不能修改class的成员
    Sales_data& combine(const Sales_data&);    
        
        
    std::string bookNo;
    unsigned units_sold = 0;
    double revenue = 0.0;
        
};
```

#### 构造函数赋值

如果成员是const、引用、或者属于某种未提供默认构造函数的类类型，必须通过构造函数初始列表提供初始值，而不能直接在构造函数函数体中赋值

#### 委托构造函数

```c++
class Sales_data
{
	Sales_data(int d, int e, int f) : a(d), b(e), c(f){}
    Sales_data() : Sales_data(0,0,0){}//把自己的一些职责给了其他的构造函数
        
private:
    int a;
    int b;
    int c;
};
```

#### 默认构造函数

默认初始化、值初始化时默认构造函数被自动调用；

如果定义了其它构造函数，最好也提供一个默认构造函数。

#### 隐式的类类型转换

如果构造函数支持一个实参的调用，那么也就定义了从参数类型向类类型隐式转换的规则。只允许一步类类型转换。

抑制构造函数定义的隐式转换：explicit



### 拷贝、赋值和析构

如果没有定义，编译器将会提供合成的默认版本

### 访问控制与封装

public: 类的接口，在整个程序内可以被访问

private：封装（即隐藏）类的实现细节

==class和struct定义类唯一的区别就是默认的访问权限不同。class默认是private的，struct默认是public的。==

友元：允许其它类或函数访问自己的非公有成员

```c++
friend Sales_Data add(const Sales_data&, const Sales_data&);//为Sales_data的非成员函数所做的友元声明
```

在类的内部和类的外面都声明一次



### 类的其他特性

#### 定义一个类型成员

```c++
class Screen
{
public:
    typedef std::string::size_type pos;
    
private:
    pos cursor = 0;
    pos height = 0, width = 0;
    std::string contents;
};
```

#### ==inline函数：隐式内联、显式内联==

在类的内部进行函数的定义：隐式内联

在声明前指定inline ：显式内联

#### 可变数据成员mutable

```c++
class Screen()
{
private:
    mutable size_t access_ctr;//即使在一个const对象内也能被修改
};
```

#### 返回*this的成员函数

```c++
inline Screen &Screen::set(char c)
{
    contents[cursor] = c;
    return *this;
}
myScreen.move(4,0).set('#');//move()返回的也是*this
```

不完整类型（class Name;）可以定义指向该类型的指针或引用，也可以作为函数声明中的参数或返回类型，但不能初始化一个对象

#### 类之间的友元关系

每个类负责控制自己的友元类或友元函数

```c++
class Screen
{
    friend class Window_mgr;//可以在Window_mgr类访问Screen的私有成员
private:
    int height= 0;
};
```

令成员函数作为友元

```c++
class Screen
{
    friend void Window_mgr::clear(ScreenIndex);
};
//1. 定义Window_mgr类，声明clear函数但不能定义
//2. 定义Screen，包括对clear函数的友元声明
//3. 定义clear，此时才能使用Screen的成员
```

### 类的作用域

一个类就是一个作用域。一旦遇到类名Name::定义函数，直到定义结束都是类的作用域内

类型名称的定义应该放在类的开始处

成员定义中的名字查找顺序：成员函数作用域->类的作用域->全局作用域（*this->xxx，ClassName::->xxx可以得到类作用域变量，::xxx可以得到全局作用域变量）

### 类的静态成员

static函数不包含this指针，所以不能定义为const函数

静态成员存在于任何对象之外，所有对象共享。static成员的定义只能放在类的外面，类里面只能放static成员的声明。（特殊情况：如果是常量表达式，可以用字面值赋值替换）

```c++
static constexpr int period = 30;
```

static关键字只出现在类内部的声明语句中，在外面定义的时候就不能重复加static关键字

静态数据类型可以是不完全类型，可以使用静态成员作为默认实参，因为它本身并不是对象的一部分



## 容器

### 顺序容器

C++容器分为：顺序容器、关联容器

顺序容器提供了控制元素存储和访问的能力。不依赖于元素的值，而是与加入容器时的位置相对应。每种容器都是性能和功能的权衡（添加、删除、非顺序访问）。

==顺序容器类型==：

| 头文件       | 类型                                                         |
| ------------ | ------------------------------------------------------------ |
| vector       | 可变大小数组。支持快速随机访问。在尾部之外的位置插入或删除元素可能很慢 |
| deque        | 双端队列。支持快速随机访问。在头尾位置插入/删除速度很快      |
| list         | 双向链表。只支持双向顺序访问。在list中任何位置进行插入/删除操作速度都很快 |
| forward_list | 单向链表。只支持单向顺序访问。在链表任何位置进行插入/删除操作速度都很快 |
| array        | 固定大小数组。支持快速随机访问。不能添加或删除元素           |
| string       | 与vector相似的容器，但专门用于保存字符。随机访问快。在尾部插入/删除速度快 |

如果不确定要用哪种容器，那么可以在程序中只使用vector和list公共的操作：使用迭代器，不使用下标操作，避免随机访问

#### 容器库概述

容器均定义为模板类：

```c++
list<Sales_data>
deque<int>
vector<TypeName> a(num) //TypeName要有默认构造函数，否则要加上初始值vector<TypeName> a(num,init)
```

容器也可以装容器：

```c++
vector<vector<int>>
```

#### 迭代器：iterator

所有容器的迭代器接口的实现方式都相同：

​	访问元素（使用解引用实现），递增运算符（从当前元素移动到下一个元素）

迭代器范围由一对迭代器表示（左闭右开区间） ： [begin, end)

```c++
list<string>::iterator iter; //必须显式使用其类型
list<string> a ={'a','b','c'};
auto it1 = a.begin();// list<string>::iterator
auto it2 = a.rbegin();// list<string>::reverse_iterator
auto it3 = a.cbegin();// list<string>::const_iterator
auto it4 = a.crbegin();// list<string>::const_reverse_iterator
it1 = it3;//错误
it3 = it1;//正确
```

#### 容器定义和初始化

| 代码                | 功能                                                         |
| ------------------- | ------------------------------------------------------------ |
| C c;                | 默认构造函数。如果C是一个array，则c中元素按默认方式初始化，否则c为空 |
| C c1(c2);           | c1初始化为c2的拷贝，c1和c2必须是相同类型                     |
| C c1 = c2;          | 同上                                                         |
| C c{a, b, c ...}    | c初始化为初始化列表中元素的拷贝。对于array类型，列表中元素数目必须小于等于array大小，任何遗漏的元素都进行值初始化 |
| C c = {a, b, c ...} | 同上                                                         |
| C c(b, e);          | c初始化为迭代器b和e指定范围中（不包括e）的元素的拷贝。范围中元素的类型必须与C的元素类型相容（array不适用） |
| C seq(n);           | seq包括n个元素，这些元素进行了值初始化，string\array不适用。只有顺序容器的构造函数才能接受大小参数 |
| C seq(n,t);         | seq包括n个初始化为值t的元素                                  |

array的特殊操作

```c++
array<int,5> ia1; //初始化全0
array<int,5> ia2 = {0, 1, 2, 3, 4};
array<int,5> ia3 = {42};//{42, 0, 0, 0, 0}
```

#### 容器赋值运算

| 代码            | 功能                                              |
| --------------- | ------------------------------------------------- |
| c1 = c2         |                                                   |
| c = {a,b,c...}  | //array不适用                                     |
| swap(c1, c2)    | 交换c1和c2中的元素，c1和c2必须具有相同的类型      |
| c1.swap(c2)     |                                                   |
| seq.assign(b,e) | 将seq中的元素替换为迭代器b和e所表示的范围中的元素 |
| seq.assign(il)  | 将seq中的元素替换为初始化列表il中的元素           |
| seq.assign(n,t) | 将seq中的元素替换为n个值为t的元素                 |

赋值相关操作会导致左边容器内部的迭代器、引用和指针失效。而swap操作将容器内容交换不会导致指向容器的迭代器、引用和指针失效（array和string除外）

array不支持assign，也不允许花括号包围的值列表进行赋值

assign允许从一个不同但是相容的类型赋值，或是从容器的一个子序列赋值

#### 顺序容器操作

只要是改变容器大小的操作，array都不支持。

forward_list有自己专有的insert和emplace，不支持push_back和emplace_back。

vector和string不支持push_front和emplace_front。

向顺序容器**添加元素**的操作：

| 代码                  | 操作                                                         |
| --------------------- | ------------------------------------------------------------ |
| c.push_back(t)        | 在c的尾部创建一个值为t或由args创建的元素，返回void           |
| c.emplace_back(args)  | 同上                                                         |
| c.push_front(t)       | 在c的头部创建一个值为t或由args创建的元素，返回void           |
| c.emplace_front(args) | 同上                                                         |
| c.insert(p,t)         | 在迭代器p指向的元素之前创建一个值为t或由args创建的元素，返回指向新添加的元素的迭代器 |
| c.emplace(p,args)     | 同上                                                         |
| c.insert(p,n,t)       | 在迭代器p指向的元素之前插入n个值为t的元素，返回指向新添加第一个元素的迭代器 |
| c.insert(p,b,e)       | 将迭代器b和e指定范围内的元素插入到迭代器p指向的元素之前，返回指向新添加第一个元素的迭代器 |
| c.insert(p,il)        | il是一个花括号包围的元素值列表                               |

在顺序容器中**访问元素**的操作：

at和下标操作只适用于string，vector，deque和array

back不适用于forward_list

| 代码      | 操作                                                         |
| --------- | ------------------------------------------------------------ |
| c.back()  | 返回c中尾元素的**引用**。若c为空，函数行为未定义             |
| c.front() | 返回c中首元素的**引用**。若c为空，函数行为未定义             |
| c.at(n)   | 返回下标为n的元素的**引用**，如果下标越界，则抛出异常out_of_range |
| c[n]      | 返回下表为n的元素的**引用**，如果越界，则函数行为未定义      |

顺序容器的**删除元素**操作：

改变容器大小，不适用于array。forward_list有特殊版本的erase。forward_list不支持pop_back, vector和string不支持pop_front。

| 代码          | 操作                                                         |
| ------------- | ------------------------------------------------------------ |
| c.pop_back()  | 删除c中尾元素，返回void                                      |
| c.pop_front() | 删除c中首元素，返回void                                      |
| c.erase(p)    | 删除迭代器p所指定的元素，返回指向被删元素之后的元素的迭代器  |
| c.erase(b,e)  | 删除迭代器b和e所指定范围内的元素，返回指向最后一个被删元素之后的元素的迭代器 |
| c.clear()     | 删除c中所有元素，返回void                                    |

顺序容器的**大小操作**：

| 代码          | 操作                                                         |
| ------------- | ------------------------------------------------------------ |
| c.resize(n)   | 调整c的大小为n个元素，可能丢弃旧元素或添加新元素，新元素进行值初始化 |
| c.resize(n,t) | 调整c的大小为n个元素，任何新添加的元素都初始化为值t          |

不要缓存end迭代器，更安全的方法是每个循环重新计算end

#### ==vector对象是如何增长的==

如果没有空间容纳新元素，就必须分配新的空间来保存已有元素和新元素。

shrink_to_fit()只适用于vector、string和deque

capacity和reserve只适用于vector和string

| 代码              | 操作                                      |
| ----------------- | ----------------------------------------- |
| c.shrink_to_fit() | 将capacity()减少为与size()相同大小        |
| c.capacity()      | 不重新分配内存空间的话，c可以保存多少元素 |
| c.reserve(n)      | 分配至少能容纳n个元素的内存空间           |

reserve并不改变容器中的元素的数量，仅影响vector预分配多大的内存空间

#### 额外的string操作

| 代码                    | 操作                                                         |
| ----------------------- | ------------------------------------------------------------ |
| string s(cp,n)          | s是cp指向的数组中前n个字符的拷贝                             |
| string s(s2, pos2)      | s是string s2从下标pos2开始的字符的拷贝                       |
| string s(s2,pos2,len2)  | s是string s2从下标pos2开始的len2个字符的拷贝                 |
| s.substr(pos,n)         | 返回一个string，包含s中从pos开始的n个字符的拷贝。默认为所有字符 |
| s.append(s2)            | 在string末尾进行插入操作                                     |
| s.erase(index,num)      | 删除index开始的num个元素                                     |
| s.replace(index,num,s2) | 替换index开始的num个元素为s2                                 |
| s.find(args)            | 查找s中args第一次出现的位置                                  |
| s.rfind(args)           | 查找s中args最后一次出现的位置                                |

| args   | 含义                      |
| ------ | ------------------------- |
| c,pos  | 从位置pos开始查找字符c    |
| s2,pos | 从位置pos开始查找字符串s2 |

string和数值之间的转换：to_string(val), stoi, stol, stoul, stoll, stoull, stof, stod, stold

#### 容器适配器：queue, stack，priority_queue

stack和queue默认基于deque（双端队列）实现，priority_queue默认基于vector实现。

stack特有的操作：

| 代码             | 操作                                      |
| ---------------- | ----------------------------------------- |
| st.pop()         | 弹出栈顶元素，但不返回该值                |
| st.push(x)       | 将值为x的新元素或由args创建的新元素压入栈 |
| st.emplace(args) |                                           |
| st.top()         | 返回栈顶元素，但不将元素弹出栈            |

queue和priority_queue特有的操作：

| 代码            | 操作                                                         |
| --------------- | ------------------------------------------------------------ |
| q.pop()         | 返回queue的首元素或priority_queue的最高优先级的元素，但不删除此元素 |
| q.front()       | 返回首元素，但不删除此元素                                   |
| q.back()        | 只适用于queue，返回尾元素，但不删除此元素                    |
| q.top()         | 只适用于priority_queue，返回最高优先级元素，但不删除元素     |
| q.push(item)    | 在queue末尾或priority_queue中恰当位置插入元素                |
| q.emplace(args) | 同上                                                         |

#### 关联容器

关联容器：元素是按关键字来保存和访问的

关联容器类型：

​	有序（按照关键字顺序保存）：map（键值对），set（关键字），multimap（关键字可重复出现的map），multiset（关键字可重复出现的set）

​	无序：unordered_map, unordered_set, unordered_multimap, unordered_multiset

```c++
map<string, size_t> word_count;
for (const auto& w : word_count)
{
    cout<<w.first<<"occurs"<<w.second<<((w.second>1) ? "times" :"time")<<endl;
}
```

map、set、multimap、multiset迭代器按关键字升序遍历元素

#### pair类型

```c++
pair<string,string> anon;
```

## 泛型算法

大多数算法都定义在头文件algorithm中。

```c++
auto result = find(vec.begin(),vec.end(),val);
//返回迭代器
```

sort：默认使用元素类型的<运算符排序（升序排序）

### ==lambda表达式==

==[capture list] (parameter list) -> return type {function body}==

捕获列表和函数体不可省略

```c++
bool isShorter(const string &s1, const string &s2)
{
    return s1.size() < s2.size();
}
sort(words.begin(), words.end(), isShorter);
```

```c++
sort(words.begin(),words.end(),[](const string &s1,const string &s2)-> bool {return s1.size()<s2.size();});
```

[=] : 用拷贝的方式进行捕获

[&] : 用引用的方式进行捕获

```c++
void fcn4()
{
    size_t v1 = 42;
    auto f2 = [&v1]{return ++v1;}; //对于非const变量的引用，可以通过f2中的引用修改
    v1 = 0;
    auto j = f2();//j is 1
}
```

## 动态内存和智能指针

栈对象：仅在其定义的程序块运行时才存在

堆对象：动态分配的对象，在程序运行过程中可以随时建立或删除的对象。

static对象：在使用前分配，在程序结束时销毁。



在一个函数中定义vector，变量本身在栈里面，但是它所引用的空间在堆里面。





13.1

















