# QT学习笔记

> Qt的界面里面有示例功能，可以作为参考学习使用

## 界面解析

![image-20241017004359409](image-20241017004359409.png)

## 项目创建

- 编译系统，可以选择编译器

![image-20241018222217841](image-20241018222217841.png)

- 类信息配置

![image-20241018222703119](image-20241018222703119.png)

类信息的配置可以帮助我们直接生成一个对应的代码框架与配置头文件

可以配置的三个类信息

`QWidget QMainWindow QDiaglog`

其中，`Qwidget`为父类，会提供一个最基本的页面

它的两个子类分别会有以下作用:

- `QMainWindow`：生成一个基础界面，涵盖选项框、工具栏、状态栏等等，以我们的QT编辑器为参考，有如下图：

  ![image-20241018223657951](image-20241018223657951.png)

- `QDiaglog`：如名称所示，会生成一个基础的对话框，涵盖对话按钮等，以我们的QT界面为参考，有如下图：

  ![image-20241018223819309](image-20241018223819309.png)

图中的`Generate form`选项，可以创建一个基础的界面，可以在QT的设计界面中使用拖拽的方式来创建UI

![image-20241018224327069](image-20241018224327069.png)

![image-20241018225904002](image-20241018225904002.png)

![image-20241020203808276](image-20241020203808276.png)

### Qt基本模块

![image-20241020202803472](image-20241020202803472.png)

### Qt快捷键

![image-20241020205155151](image-20241020205155151.png)

##  API介绍

Qt有许多API可以使用，当有时候不知道这个API如何调用的时候可以查看帮助

下面以`QPushButton`为例子：

![image-20241026215017495](image-20241026215017495.png)

### 信号槽

信号槽的创建使用`connect`函数

`#include <QObject>`

```
QMetaObject::Connection QObject::connect	\
	(const QObject *sender, const char *signal, const QObject *receiver, const char *method,	\
    Qt::ConnectionType type = Qt::AutoConnection)
```

实际使用起来如下

```
QObject::connect(btn,&QPushButton::clicked,this,&Widget::close);
```

其中btn为控件指针，this为接收者指针

另外两个参数为信号，需要传递指针过去

### 按钮控件

`#include <QPushButton>`

![image-20241020224414519](image-20241020224414519.png)

### `QMainWindow`类

`QMainWindow`是一个为用户提供主窗口程序的类，包含一个菜单栏(`menu bar`)、多个工具栏(`tool bars`)、多个链接部件(`dock widgets`)、一个状态栏(`status bar`)以及一个中心部件(`central widget`)，是许多应用程序的基础，如文本编辑器，图片编辑器等。

![image-20241026203757688](image-20241026203757688.png)

以`word`为例：

![image-20241026204138013](image-20241026204138013.png)

#### 常用API

![image-20241026224850735](image-20241026224850735.png)

```
//创建菜单栏
    QMenuBar *MenuBar = menuBar();
    //设置菜单栏到主窗口
    setMenuBar(MenuBar);

    //添加菜单
    QMenu *FileMenu = MenuBar->addMenu("文件");
    //工具栏  可以有多个
    QToolBar *toolBar = new QToolBar(this);
    //创建按钮
    QPushButton *Button = new QPushButton("按钮",this);

    //创建菜单项
    FileMenu->addAction("新建");
    //添加分隔符
    FileMenu->addSeparator();
    FileMenu->addAction("打开");



    addToolBar(Qt::LeftToolBarArea,toolBar);

    //后期设置成允许上下左右停靠
    toolBar->setAllowedAreas((Qt::ToolBarArea)0xF);
    //总开关，允许移动
    toolBar->setMovable(true);
    //设置浮动
    toolBar->setFloatable(true);

    //工具栏中可以设置内容
    toolBar->addAction("打开");
    toolBar->addSeparator();
    toolBar->addAction("新建");
    toolBar->addWidget(Button);

    //创建状态栏
    QStatusBar *stBar = statusBar();
    setStatusBar(stBar);
    //创建标签
    QLabel *label = new QLabel("Caution",this);
    QLabel *label2 = new QLabel("Caution",this);
    //添加标签
    stBar->addWidget(label);
    //添加右侧便签
    stBar->addPermanentWidget(label2);

    //创建铆接部件(浮动窗口) 可以有多个
    QDockWidget *dock = new QDockWidget("浮动",this);
    addDockWidget(Qt::RightDockWidgetArea,dock);

    //设置中心部件 只有一个
    QTextEdit *textedit = new QTextEdit("Text",this);
    setCentralWidget(textedit);
```

#### 添加资源文件

![image-20241026233731811](image-20241026233731811.png)

使用类似该方式进行添加：`ui->actionNew_File->setIcon(QIcon(":/image-20240926172413577.png"));`









## 对象树

对象树用于管理Qt窗口各个控件的生命周期，当我们结束程序的时候，各个控件的指针会依次从最底层开始进行析构释放

![image-20241020233130730](image-20241020233130730.png)

注意此处是对象树，而非继承树，因此哪怕不是继承自父对象的类，也可以添加进这个对象树中

只要是继承自QObject的子类即可，因此在Qt中，尽量在构造的时候指定parent对象，并且大胆在堆上创建

## 信号和槽

以创建按钮关闭窗口的需求为例

```
flowchart LR
	Button --Click-->Window-->Close
```

而这里的例子可以拟合成如下步骤

```
flowchart LR
	SignalSender--Signal-->SignalAccepter-->SignalProc
```

这里的`SignalProc`就是`信号槽`，**具体创建与实现可以查看API调用部分**

这里的***一个信号可以连接多个槽函数，多个信号可以连接同一个槽函数，彼此松散耦合***

> [!caution]
>
> ***信号和槽的参数类型必须要一一对应***，同时**信号的个数可以多于槽的参数个数**
>
> 不过`void`可以匹配任何类型的参数（仅限槽）
>
> 即信号为`void`不能匹配带参数的槽，但是槽为`void`可以匹配带参数的信号

> [!NOTE]
>
> 信号槽的优点可以综合为以下几点：
>
> - 松散耦合
> - 发送端与接收端本身没有关联，通过`connect`将两端耦合在一起

### 自定义的信号和槽

创建一个新的类之后，会在头文件出现以下内容：

其中信号的创建如下：

![image-20241023235304394](image-20241023235304394.png)

槽的创建有如下要求：

![image-20241023235408916](image-20241023235408916.png)

**信号的触发**：

触发信号需要调用对应函数，这里可以这样实现：

![image-20241024001202936](image-20241024001202936.png)

![image-20241024000835533](image-20241024000835533.png)

也就是**使用关键字`emit`触发对应信号**





### 信号与槽的重载

当自定义的信号和槽出现重载的情况，可以使用以下两种方式来进行`connect`函数的传参：

- ![image-20241025004710564](image-20241025004710564.png)

  

- ![image-20241025004832629](image-20241025004832629.png)

  其中代码的详细内容为：

  ```
  connect(sender, QOverload<>::of(&SenderClass::hungry), receiver, &ReceiverClass::slotFunction);
  connect(sender, QOverload<QString>::of(&SenderClass::hungry), receiver, &ReceiverClass::slotFunction);
  ```


### 信号连接信号

可以使用`connect`函数连接信号，但是得注意信号与信号之间的参数要一致

(`Reciver`的参数可以为`void`适配所有参数)

### 断开信号

调用函数`disconnect`，使用方式与`connect`是一样的。





## C/C++



### Lambda表达式

Lambda 表达式是 C++11 引入的一种简洁方式，用于定义匿名函数（即没有名字的函数），通常用于需要短小函数的地方，比如排序、过滤等操作。它的形式简洁，且可以直接在代码中嵌入函数逻辑，特别适用于回调、算法函数或需要简洁表达的场合。

Lambda 表达式在 C++ 中就像“**临时工**”——它们可以在需要的时候，快速创建一个小型函数来执行一些临时性任务，而不需要专门为它起个名字和单独定义。

Lambda表达式的基本结构如下：

```
[capture](parameters) -> return_type {
    // 函数体
};
```

各个部分的含义如下：

- capture

  （捕获列表）：定义 Lambda 表达式可以访问的外部变量。可以是 

  ```
  []
  ```

  、

  ```
  [=]
  ```

   或 

  ```
  [&]
  ```

   等。

  - `[]`：不捕获任何外部变量。
  - `[=]`：按值捕获所有外部变量。
  - `[&]`：按引用捕获所有外部变量。
  - `[x, &y]`：按值捕获变量 `x`，按引用捕获变量 `y`。

- **parameters**（参数列表）：和普通函数的参数列表类似，定义 Lambda 表达式接受的参数。

- **return_type**（返回类型，可选）：指定返回类型。可以省略，编译器会自动推断返回类型。

- **函数体**：具体的函数实现代码。

捕获列表可以帮助lambda获取作用域内的对应值，例如

```
[=](int a,int b){return a+b;}
```

可以获取定义lambda函数的作用域的值进行使用

> [!caution]
>
> 值传递使用，必须添加关键字`mutable`才能修改传递进来的值变量，否则传递进来的值变量为只读变量

```
[&](int a,int b)->int{return a+b;}
```

可以获取在lambda内修改外部作用域的值

类似的可以使用

```
[a]()->int{return a;}//只能识别a
[&a](){}//只能识别修改a
[this](){}//可以使用对应类中的成员变量
[a,&b](){}//可以获取a的值，可以修改b的值
[=,&a,&b](){}//除了a，b使用引用传递外，其他的使用值传递
[&,a,b](){}//除了a、b使用值传递，其他的使用引用传递
```

**可以使用Lambda表达式解决connect传参必须一致的问题。**

```
connect(&sender,&signal,&reciver,[=](){a->slot();})
```





### 静态成员与非静态成员

静态成员可以理解为类似全局函数的东西，只不过为了管理方便我们将其划分到了类里面

它并不依赖类的实例创建，**不论你这个类创建了多少个，被多少个子类继承，静态成员永远就只有那一个**。

#### 成员

| 特性                     | 静态成员                                       | 非静态成员                                     |
| ------------------------ | ---------------------------------------------- | ---------------------------------------------- |
| 是否属于具体对象         | 否（属于类本身）                               | 是（属于具体对象）                             |
| 内存分配                 | 类级别，全局唯一                               | 对象级别，每个对象都有自己的副本               |
| 访问方式                 | 通过类名或对象访问（推荐类名访问）             | 必须通过对象访问                               |
| 生命周期                 | 随类的生命周期（类加载时创建，程序结束时销毁） | 随对象的生命周期（对象创建时存在，销毁时结束） |
| 是否共享                 | 所有对象共享同一份                             | 每个对象拥有独立的一份                         |
| 能否被静态成员函数访问   | 可以                                           | 不可以                                         |
| 能否被非静态成员函数访问 | 可以                                           | 可以                                           |



#### 成员函数

| 特性               | 静态成员函数                           | 非静态成员函数               |
| ------------------ | -------------------------------------- | ---------------------------- |
| 是否依赖对象       | 不依赖（属于类本身）                   | 依赖（属于类的具体对象）     |
| 调用方式           | 通过类名直接调用 `AClass::Function();` | 通过对象调用 `A.Function();` |
| 能否访问静态成员   | 可以                                   | 可以                         |
| 能否访问非静态成员 | 不可以                                 | 可以                         |
| 是否有 `this` 指针 | 没有                                   | 有                           |
| 内存分配           | 类级别，全局唯一                       | 对象级别，不同对象独立       |

简单来讲，静态成员函数类似我们普通定义的函数，只是为了扩展我们将其定义到了类里面，其使用方式、各方面特性都与普通函数类似

> [!NOTE]
>
> 比较特殊的是静态成员函数只能访问类中的静态成员，这也是合理的，因为我们可以在没有实例的情况下调用该函数，实例都没有，那里面的变量也没有初始化，如何访问。



### 类的权限与封装性

在C++中，类的权限控制主要有三种：`public`、`protected` 和 `private`，它们定义了类成员（包括成员变量和成员函数）的可访问性。这种设计旨在提供数据封装和继承的灵活性，确保代码的安全性、可维护性以及灵活性。以下是对这三种访问权限的详细说明及其使用区别：

#### 1. `public` 权限

- **说明**：`public` 成员可以在类的内部和外部访问。换句话说，任何代码都可以直接访问类的 `public` 成员（包括其他类的对象或函数）。

- 使用场景

  ：

  - 适合那些需要对外公开的接口，如构造函数、`getter` 和 `setter` 方法，以及一些用户需要直接调用的成员函数。
  - 不推荐将成员变量声明为 `public`，因为这会破坏类的封装性和数据安全性。

- **设计意图**：`public` 权限是为了提供类的接口和功能，使外部代码可以与类进行交互。

```
cpp复制代码class MyClass {
public:
    int publicVar;  // 公有成员变量
    void publicMethod();  // 公有成员函数
};
```

#### 2. `protected` 权限

- **说明**：`protected` 成员可以在类的内部和子类中访问，但不能在类的外部访问。即使是类的对象或其他非继承的类也无法访问它。

- 使用场景

  ：

  - 适合那些希望在子类中使用但不希望被外部访问的成员变量或方法。通常在类的继承关系中，用于子类需要访问的父类数据。
  - 例如，父类可能有一些辅助函数或内部状态，子类需要访问这些信息来实现特定功能，但外部不应直接操作这些数据。

- **设计意图**：`protected` 使得类的继承结构更加灵活，允许子类在继承父类的同时保留对某些成员的访问权，但又避免了外部代码直接访问这些成员，从而保护数据的完整性。

```
cpp复制代码class BaseClass {
protected:
    int protectedVar;  // 受保护的成员变量
};

class DerivedClass : public BaseClass {
public:
    void accessProtectedVar() {
        protectedVar = 10;  // 在子类中访问受保护的成员
    }
};
```

#### 3. `private` 权限

- **说明**：`private` 成员只能在类的内部访问，外部代码或子类都无法直接访问它们。这是访问限制最严格的一种。

- 使用场景

  ：

  - 适用于那些仅限类内部使用的成员，例如内部状态、辅助函数或敏感数据。这些数据和函数不希望被外部直接访问或修改，因此设置为 `private` 以确保类的安全性和完整性。
  - 通过 `private`，类可以对外界隐藏实现细节，只有通过 `public` 方法（接口）才能访问或修改这些数据。

- **设计意图**：`private` 权限是为了实现封装（Encapsulation），将数据和操作封装在类内部，防止外部代码随意修改数据的状态，确保数据的一致性和安全性。

```
cpp复制代码class MyClass {
private:
    int privateVar;  // 私有成员变量

public:
    void setPrivateVar(int value) {  // 公有方法来访问私有成员
        privateVar = value;
    }
};
```

#### **4.总结**

不论是哪一种权限，在定义的类内部进行实现都是可以直接调用的，不需要使用`this->function`或者`this->var`的方式，不过要使用也可以。

对于`public`里面的成员和函数，可以理解成这个类创建实例后，提供给外部接口使用的。

`private`和`protected`的区别其实就在于`private`只能由类内部的函数进行调用，而`protected`为子类也提供了调用的接口。

这种类的实现和创建其实应该是为了我们的封装更加方便来进行的，最后提供给外部的API应该是一个子类，而重要的部分经过层层封装写入在`private`里面，防止了数据篡改的发生



### 函数重载

**函数重载**（Function Overloading）是C++中一种多态性的实现方式，它允许在同一个作用域中定义多个**同名但参数列表不同**的函数。编译器通过**函数参数的类型和数量**来区分这些函数，从而决定调用哪一个版本。这种机制使得代码更加简洁、灵活，并提高了代码的可读性。

#### 函数重载的条件

函数重载的实现有以下几个条件：

1. 同一个作用域

   ：重载的函数必须在同一个类或同一个命名空间中。

2. 同名函数

   ：函数的名字必须相同。

3. 参数列表不同

   ：参数的数量不同，或参数的类型不同。例如：

   - ```
     cpp复制代码void print(int value);
     void print(double value);
     void print(int value1, int value2);
     ```

   - 上述三个`print`函数是合法的重载，因为它们的参数类型和数量都不相同。

#### 函数重载的好处

1. **代码简洁**：可以用同一个函数名处理不同类型的数据。
2. **可读性强**：调用时通过函数名即可知道其功能，而参数的类型和数量决定了具体调用哪个版本。
3. **提高灵活性**：可以针对不同的输入类型设计不同的处理逻辑。



### 类中函数指针的定义

普通的函数指针定义：

```
返回类型 (*指针名称)(参数类型1, 参数类型2, ...);
int (*func_ptr)(int, float);

//使用
(*func_ptr)(1,1.0);
```

`C++`类中成员函数的函数指针定义：

```
返回类型 (类名::*指针名称)(参数列表);
void (MyClass::*funcPtr)() = &MyClass::display;
```

`C++`中的使用调用比较复杂，这里使用下面的例子展示如何使用：

```
//定义类
#include <iostream>
using namespace std;

class MyClass {
public:
    void display() {
        cout << "Display function called!" << endl;
    }

    int add(int a, int b) {
        return a + b;
    }
};

//定义和使用无参成员函数
int main() {
    MyClass obj;

    // 定义一个指向 MyClass 中 void display() 函数的指针
    void (MyClass::*funcPtr)() = &MyClass::display;

    // 使用成员函数指针调用函数（通过对象）
    (obj.*funcPtr)();  // 输出：Display function called!

    // 使用成员函数指针调用函数（通过对象指针）
    MyClass* ptr = &obj;
    (ptr->*funcPtr)();  // 输出：Display function called!

    return 0;
}

//定义和使用带参成员函数
int main() {
    MyClass obj;

    // 定义一个指向 MyClass 中 int add(int, int) 函数的指针
    int (MyClass::*addPtr)(int, int) = &MyClass::add;

    // 使用成员函数指针调用函数（通过对象）
    int result = (obj.*addPtr)(3, 4);
    cout << "Result: " << result << endl;  // 输出：Result: 7

    // 使用成员函数指针调用函数（通过对象指针）
    MyClass* ptr = &obj;
    result = (ptr->*addPtr)(5, 6);
    cout << "Result: " << result << endl;  // 输出：Result: 11

    return 0;
}
```

> [!important]
>
> ### 成员函数指针的注意事项
>
> 1. **必须使用对象或对象指针来调用**：
>    - 成员函数指针不能像普通函数指针那样直接调用，必须使用一个具体的对象或对象指针，并使用`.*`或`->*`操作符。
> 2. **静态成员函数不需要使用成员函数指针**：
>    - 静态成员函数和普通的全局函数类似，可以直接使用普通函数指针来指向它们，不需要包含类的类型信息。
> 3. **成员函数指针不支持绑定到对象**：
>    - C++标准中的成员函数指针只包含函数的地址，不包括对象本身。因此，调用时必须显式地提供对象或对象指针。































































