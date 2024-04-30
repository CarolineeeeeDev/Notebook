# C++面经

[TOC]

## 智能指针

### **内存泄露与智能指针**

内存泄露简单地说就是申请了一块内存空间，使用完毕后没有释放掉。内存泄漏发生在已经分配的内存未能被正确释放回操作系统或可用内存池的情况下，导致程序无法再次使用那部分内存。内存泄露可以导致程序运行效率下降，并且随着程序的运行时间增加，可能最终耗尽系统的所有可用内存，引起程序崩溃或系统性能下降。内存泄漏的原因可能有：

（1）未释放的动态内存：new和malloc申请资源使用后，没有用delete和free释放；

（2）子类继承父类时，父类析构函数不是虚函数。

（3）Windows句柄资源使用后没有释放。

（4）循环引用

怎么解决？
使用**智能指针**，确保每次分配与释放匹配，避免循环引用。

### **智能指针有什么类型，各自的原理有什么区别 / 解释下智能指针的实现原理**

智能指针在 C++ 中是一种用于自动化资源管理的类模板，主要是用来管理动态分配（堆分配）的内存，以避免内存泄漏和其他与资源管理相关的错误。C++ 标准库提供了几种智能指针，如`std::unique_ptr`、`std::shared_ptr` 和 `std::weak_ptr`。这些智能指针各自有不同的管理策略和使用场景。下面是三种主要智能指针的实现原理：

1. `std::unique_ptr`

`std::unique_ptr` 提供了对单一对象的独占所有权语义。其核心原理和特点包括：

- **独占所有权**：每个 `std::unique_ptr` 对象管理一个指针，并保证没有其他智能指针同时指向同一个对象。这意味着 `std::unique_ptr` 不能被复制，只能被移动。移动语义允许所有权从一个 `unique_ptr` 转移到另一个。
- **自动释放**：当 `std::unique_ptr` 的实例被销毁（例如，离开作用域）时，它会自动删除其管理的对象。
- **自定义删除器**：用户可以指定自定义删除器，以便在 `unique_ptr` 被销毁时执行特定的清理操作。

2. `std::shared_ptr`

`std::shared_ptr` 提供共享所有权的智能指针，多个 `shared_ptr` 实例可以指向同一个对象，其核心原理和特点包括：

- **共享所有权**：`std::shared_ptr` 使用引用计数机制来确保多个指针可以安全地管理同一个对象。每当新的 `shared_ptr` 拷贝或赋值自另一个 `shared_ptr`，引用计数会增加；当 `shared_ptr` 被销毁时，引用计数减少。
- **自动释放**：当最后一个 `shared_ptr`（引用计数变为0）被销毁时，所管理的对象会被自动删除。
- **线程安全**：`shared_ptr` 的引用计数操作是线程安全的，但用户需要自行保证所指向的对象的线程安全性。
- **弱引用**：`std::shared_ptr` 可以和 `std::weak_ptr` 配合使用，以解决潜在的循环引用问题。

3. `std::weak_ptr`

`std::weak_ptr` 是一种非拥有（非独占）的智能指针，用来指向由 `std::shared_ptr` 管理的对象，但不会增加引用计数，其核心原理和特点包括：

- **监视而不拥有**：`std::weak_ptr` 允许访问 `std::shared_ptr` 管理的对象，而不延长其生命周期。这对于防止 `shared_ptr` 之间的循环引用非常有用。
- **临时访问**：`std::weak_ptr` 需要通过调用 `lock()` 方法来创建一个临时的 `std::shared_ptr` 实例，以安全地访问对象（如果原始 `shared_ptr` 仍存在）。



### **shared_ptr怎么实现多指针指向同一个地址** 

拷贝或者赋值另一个shared_ptr

```c++
//拷贝
shared_ptr<int> sp = make_shared<int>(100);
shared_ptr<int> sp1(sp);
//赋值
shared_ptr<int> sp = make_shared<int>(100);
shared_ptr<int> sp1 = sp;
```



### ==**引用计数如何保证不同类实例的指针之间共享同步**== 

不同shared_ptr指针需要共享相同的内存对象，因此**引用计数的存储是在堆上的**。



### **循环引用会在什么情况下产生，如何解决，解决的原理**

循环引用在使用 `std::shared_ptr` 时常见于两个或多个对象互相持有对方的 `std::shared_ptr` 引用，这会阻止引用计数达到零，导致内存泄漏。

```c++
#include <iostream>
#include <memory>
using namespace std;

class B; 
class A {
public:
    shared_ptr<B> b_ptr;
    ~A() {
        cout << "A destructor called" << endl;
    }
};

class B {
public:
    shared_ptr<A> a_ptr;
    ~B() {
        cout << "B destructor called " << endl;
    }
};

int main() {
    shared_ptr<A> a = make_shared<A>();
    shared_ptr<B> b = make_shared<B>();
    a->b_ptr = b;
    b->a_ptr = a;
    return 0;
}
```

`std::weak_ptr` 用于解决循环引用问题。它是一种智能指针，不会增加对象的引用计数。

```c++
#include <iostream>
#include <memory>

class B; 
class A {
public:
    std::weak_ptr<B> b_ptr; // 使用 weak_ptr 代替 shared_ptr
    ~A() {
        std::cout << "A destructor called" << std::endl;
    }
};

class B {
public:
    std::weak_ptr<A> a_ptr; // 使用 weak_ptr 代替 shared_ptr
    ~B() {
        std::cout << "B destructor called" << std::endl;
    }
};

int main() {
    std::shared_ptr<A> a = std::make_shared<A>();
    std::shared_ptr<B> b = std::make_shared<B>();
    a->b_ptr = b;
    b->a_ptr = a;
	return 0;
}
```



### **shared_ptr的代码实现（主要是构造、赋值和析构）weak_ptr呢**

```c++
template<typename T>
class shared_ptr {
public:
// 构造函数
shared_ptr(T* ptr = nullptr) : m_ptr(ptr), m_refCount(new int(1)) {}

// 拷贝
shared_ptr(const shared_ptr& other) : m_ptr(other.m_ptr), m_refCount(other.m_refCount) {
    (*m_refCount)++;
}

// 析构函数
~shared_ptr() {
    (*m_refCount)--;

    if (*m_refCount == 0) {
        delete m_ptr;
        delete m_refCount;
    }
}

//赋值操作，运算符=重载
shared_ptr& operator=(const shared_ptr& other) {
    //被新的shared_ptr覆盖
    if (this != &other) {
        // 旧shared_ptr的count减一
        (*m_refCount)--;

        if (*m_refCount == 0) {
            delete m_ptr;
            delete m_refCount;
        }
        
        m_ptr = other.m_ptr;
        m_refCount = other.m_refCount;
        (*m_refCount)++;
    }
    return *this;
}

private:
    T* m_ptr;            // points to the actual data
    int* m_refCount;     // reference count
};

```



### **智能指针构造与析构时间**

1. 构造时间：

   **`std::unique_ptr`**：当你创建一个 `unique_ptr` 时，它会接管一个原始指针，并负责该指针指向的对象的生命周期。构造时间通常与创建该原始指针的对象的时间相同。

   **`std::shared_ptr`**：`shared_ptr` 的构造可以通过直接接管（移动赋值）一个原始指针或复制（拷贝赋值）另一个 `shared_ptr` 来完成。复制 `shared_ptr` 时，内部的引用计数会增加，以表明现在有多个 `shared_ptr` 实例共享同一个对象。

2. 析构时间：

   **`std::unique_ptr`**：当 `unique_ptr` 离开其作用域时，它会自动释放它所拥有的对象。如果它是函数中的局部变量，那么在函数返回时析构。如果它是类的成员，那么在其所属的对象被销毁时析构。

   **`std::shared_ptr`**：与 `unique_ptr` 不同，`shared_ptr` 会跟踪有多少个 `shared_ptr` 实例共享同一个对象。只有**当最后一个 `shared_ptr` 被销毁或被赋予新的对象时**，它才会释放原来管理的对象。这意味着析构时间是不确定的，取决于所有共享该对象的 `shared_ptr` 的生命周期。



### **野指针的产生原因，解决方法**

产生原因：指针没有初始化；释放资源之后没有将指针置空；对象的生命周期结束之后仍尝试访问它（作用域外使用）

解决方法：对指针进行初始化，释放资源后将指针置空，用智能指针代替裸指针



### **智能指针如何实现weak_ptr? 引用计数存储的位置？weak_ptr如何知道返回的是一个空对象？引用计数什么时候销毁？**



引用计数存储在与 std::shared_ptr 共享的控制块中。这个控制块通常是在首次创建 shared_ptr 时动态分配的，而所有复制或移动生成的 shared_ptr 和 weak_ptr 都会指向同一个控制块。

std::weak_ptr 通过调用 .lock() 方法尝试获取一个 std::shared_ptr。如果相关的 shared_ptr 已经不存在（即强引用计数为 0），.lock() 会返回一个空的 std::shared_ptr 对象。

当最后一个shared_ptr被销毁的时候，引用计数被销毁。



### **共享指针的底层实现**

```c++
element_type*    _M_ptr;         // Contained pointer.
__shared_count<_Lp>  _M_refcount;    // Reference counter.
```

std::shared_ptr在内部维护一个引用计数，其只有两个指针成员，一个指针是所管理的数据的地址；还有一个指针是控制块的地址，包括引用计数、weak_ptr计数、删除器(Deleter)、分配器(Allocator)。因为不同shared_ptr指针需要共享相同的内存对象，因此引用计数的存储是在**堆**上的。而**unique_ptr只有一个指针成员**，指向所管理的数据的地址。因此一个shared_ptr对象的大小是raw_pointer大小的两倍。

智能指针主要用于管理在堆上分配的内存，它将普通的指针封装为一个栈对象 。 当栈对象的生存周期结束后，会在析构函数中释放掉申请的内存，从而防止内存泄漏 。注意，当智能指针在全局作用域里定义时将被存放在全局/静态存储区



### **智能指针判空**

直接比较：可以直接使用 `==` 或 `!=` 运算符来比较智能指针和 `nullptr`。

使用 `bool` 转换：智能指针重载了 `bool` 类型的转换运算符，当指针为空时，转换结果为 `false`；当指针非空时，转换结果为 `true`



### **weak_ptr原理**

1. **引用计数和弱引用计数：**

   当你使用 `std::shared_ptr` 管理一个对象时，这个智能指针会维护一个引用计数（用来记录有多少个 `shared_ptr` 实例共享同一个对象）。

   当你创建一个 `std::weak_ptr` 并将其与 `std::shared_ptr` 关联时，除了维护原有的引用计数外，还会**增加一个弱引用计数**。弱引用计数记录有多少个 `weak_ptr` 实例指向同一个对象。

   2. 访问管理

      - ```
        std::weak_ptr
        ```

         不能直接访问其指向的对象，因为它不拥有对象。要访问对象，你必须先将 

        ```
        weak_ptr
        ```

         转换为 

        ```
        std::shared_ptr
        ```

        。这通常通过调用 

        ```
        std::weak_ptr
        ```

         的 

        ```
        lock()
        ```

         方法实现，该方法检查关联的 

        ```
        shared_ptr
        ```

         是否仍存在：

        - 如果关联的 `shared_ptr` 仍然存在（即对象尚未被删除），`lock()` 方法会创建并返回一个新的 `std::shared_ptr` 实例。
        - 如果关联的 `shared_ptr` 已经不存在，`lock()` 方法将返回一个空的 `std::shared_ptr`。



### **解释下智能指针的实现原理**

智能指针在 C++ 中是一种用于自动化资源管理的类模板，主要是用来管理动态分配（堆分配）的内存，以避免内存泄漏和其他与资源管理相关的错误。C++ 标准库提供了几种智能指针，如`std::unique_ptr`、`std::shared_ptr` 和 `std::weak_ptr`。这些智能指针各自有不同的管理策略和使用场景。下面是三种主要智能指针的实现原理：

1. `std::unique_ptr`

`std::unique_ptr` 提供了对单一对象的独占所有权语义。其核心原理和特点包括：

- **独占所有权**：每个 `std::unique_ptr` 对象管理一个指针，并保证没有其他智能指针同时指向同一个对象。这意味着 `std::unique_ptr` 不能被复制，只能被移动。移动语义允许所有权从一个 `unique_ptr` 转移到另一个。
- **自动释放**：当 `std::unique_ptr` 的实例被销毁（例如，离开作用域）时，它会自动删除其管理的对象。
- **自定义删除器**：用户可以指定自定义删除器，以便在 `unique_ptr` 被销毁时执行特定的清理操作。

2. `std::shared_ptr`

`std::shared_ptr` 提供共享所有权的智能指针，多个 `shared_ptr` 实例可以指向同一个对象，其核心原理和特点包括：

- **共享所有权**：`std::shared_ptr` 使用引用计数机制来确保多个指针可以安全地管理同一个对象。每当新的 `shared_ptr` 拷贝或赋值自另一个 `shared_ptr`，引用计数会增加；当 `shared_ptr` 被销毁时，引用计数减少。
- **自动释放**：当最后一个 `shared_ptr`（引用计数变为0）被销毁时，所管理的对象会被自动删除。
- **线程安全**：`shared_ptr` 的引用计数操作是线程安全的，但用户需要自行保证所指向的对象的线程安全性。
- **弱引用**：`std::shared_ptr` 可以和 `std::weak_ptr` 配合使用，以解决潜在的循环引用问题。

3. `std::weak_ptr`

`std::weak_ptr` 是一种非拥有（非独占）的智能指针，用来指向由 `std::shared_ptr` 管理的对象，但不会增加引用计数，其核心原理和特点包括：

- **监视而不拥有**：`std::weak_ptr` 允许访问 `std::shared_ptr` 管理的对象，而不延长其生命周期。这对于防止 `shared_ptr` 之间的循环引用非常有用。
- **临时访问**：`std::weak_ptr` 需要通过调用 `lock()` 方法来创建一个临时的 `std::shared_ptr` 实例，以安全地访问对象（如果原始 `shared_ptr` 仍存在）。

智能指针的这些实现原理主要是通过类模板和运算符重载实现的。它们通过管理指针的生命周期和确保资源正确释放来帮助程序员避免内存泄漏和其他资源管理错误。



### **`shared_ptr`什么情况下引用计数增加、什么时候减少**

增加：新的 `shared_ptr` 拷贝或赋值自另一个 `shared_ptr`

减少：`shared_ptr` 被销毁时



### **独占所有权是什么含义**

每个 `std::unique_ptr` 对象管理一个指针，并保证没有其他智能指针同时指向同一个对象。这意味着 `std::unique_ptr` 不能被复制，只能被移动。移动语义允许所有权从一个 `unique_ptr` 转移到另一个。



### **`unique_ptr`可以放在标准库的容器中吗**

在 C++ 中，`unique_ptr` 是一个智能指针，它拥有其所管理对象的唯一所有权。这意味着不能有两个 `unique_ptr` 同时指向同一个对象。这个特性使得 `unique_ptr` 不能被拷贝，只能被移动。

当你想要将 `unique_ptr` 放入标准库的容器中时，你需要注意以下几点：
1. **容器操作的兼容性**：由于 `unique_ptr` 只能被移动，而不能被拷贝，所以任何需要拷贝元素的容器操作（比如插入、删除、排序等）都必须确保操作是通过移动而非拷贝进行的。
2. **使用适当的容器方法**：例如，使用 `emplace_back` 而不是 `push_back` 来添加元素到 `vector` 中，因为 `emplace_back` 可以直接在容器内部构造元素，避免不必要的拷贝或移动。
3. **容器选择**：任何可以存储移动构造对象的容器都可以存储 `unique_ptr`。例如，`std::vector`, `std::list`, `std::deque` 都是合适的选择。

总的来说，`unique_ptr` 可以放在标准库的容器中，只要确保使用适合移动语义的操作和方法。这样做可以使你有效地管理动态分配的资源，同时享受容器带来的灵活性和功能。



### **如何实现对象的函数返回this指针的share_ptr**

```c++
class T : public enable_shared_from_this<T>
{
    public:
    shared_ptr<T> self()
    {
        return shared_from_this();
    }
}
```

类继承自 `std::enable_shared_from_this<类名>`。通过这种方式，Test 类的对象可以安全地获取自身的 `shared_ptr`。

