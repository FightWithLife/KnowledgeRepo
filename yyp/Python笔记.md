# Python语法



## 变量定义：

在 Python 中，变量定义非常简单，不需要指定类型，Python 会自动根据赋值来推断变量的类型。以下是 Python 变量定义的基本规则和示例：

### 1. **基本变量定义**

- 直接将值赋给变量即可，无需声明类型：

  ```
  x = 10       # 整数类型 (int)
  y = 3.14     # 浮点数类型 (float)
  name = "Alice"  # 字符串类型 (str)
  is_active = True  # 布尔类型 (bool)
  ```

### 2. **变量命名规则**

- 变量名必须以字母（`a-z` 或 `A-Z`）或下划线（`_`）开头，不能以数字开头。
- 变量名只能包含字母、数字和下划线（`_`）。
- 变量名区分大小写（`myVar` 和 `myvar` 是不同的变量）。
- 不要使用 Python 的保留字作为变量名（如 `and`、`class`、`def` 等）。

示例：

```
user_age = 25
_total = 100.5
is_valid = False
```

### 3. **多变量赋值**

- Python 支持在一行中给多个变量赋值：

  ```
  a, b, c = 1, 2.5, "Hello"
  ```

- 所有变量都赋相同的值：

  ```
  x = y = z = 0
  ```

### 4. **定义不同类型的变量**

- Python 变量的类型是动态的，可以根据赋的值自动推断，并且可以随时更改类型。

  ```
  x = 10        # x 是整数类型
  x = "ten"     # 现在 x 是字符串类型
  ```

### 5. **Python 常见数据类型**

- **整数**（`int`）：整数值，如 `10`, `-5`
- **浮点数**（`float`）：带小数点的数值，如 `3.14`, `-2.5`
- **字符串**（`str`）：一组字符，用单引号或双引号包裹，如 `"Hello"` 或 `'World'`
- **布尔值**（`bool`）：表示真或假，值为 `True` 或 `False`
- **列表**（`list`）：可以存储多个值的集合，如 `[1, 2, 3]`
- **字典**（`dict`）：键值对的集合，如 `{"name": "Alice", "age": 25}`
- **元组**（`tuple`）：不可变的值集合，如 `(1, 2, 3)`
- **集合**（`set`）：无序不重复的集合，如 `{1, 2, 3}`

### 6. **变量类型检查**

- 使用 

  ```
  type()
  ```

   函数查看变量的类型：

  ```
  x = 10
  print(type(x))  # 输出: <class 'int'>
  ```

### 7. **变量删除**

- 可以使用 

  ```
  del
  ```

   关键字删除变量：

  ```
  x = 5
  del x
  ```

## 关键字

Python 关键字（Keywords）是 Python 语言中保留的词汇，它们具有特定的意义，不能作为变量名、函数名或其他标识符使用。这些关键字定义了 Python 的语法规则和结构。

以下是 Python 3 中的所有关键字（截至最新版本，关键字可能会随版本更新有所变化）：

下面的关键字还需要进一步完善信息才可以。

### Python 关键字列表

```
False      await      else       import     pass
None       break      except     in         raise
True       class      finally    is         return
and        continue   for        lambda     try
as         def        from       nonlocal   while
assert     del        global     not        with
async      elif       if         or         yield
```

### 关键字的作用和用法

1. **`False` / `True`**：布尔值，用于表示假和真。

   ```
   is_active = True
   ```

2. **`None`**：表示空值或无值的对象。

   ```
   value = None
   ```

3. **`and` / `or` / `not`**：逻辑运算符，用于逻辑表达式。

   ```
   if a and b:
       print("Both are true")
   ```

4. **`if` / `elif` / `else`**：条件语句，用于控制程序的执行流。

   ```
   if condition:
       print("Condition is true")
   elif another_condition:
       print("Another condition is true")
   else:
       print("Neither is true")
   ```

5. **`for` / `while`**：循环语句，用于重复执行某些代码块。

   ```
   for i in range(5):
       print(i)
   ```

6. **`break` / `continue`**：控制循环的执行。

   - `break`：终止循环。
   - `continue`：跳过当前循环的剩余部分，进入下一次迭代。

   ```
   for i in range(10):
       if i == 5:
           break
       print(i)
   ```

7. **`def` / `return`**：定义函数并返回值。

   ```
   def add(x, y):
       return x + y
   ```

8. **`class`**：定义类的关键字。

   ```
   class Person:
       def __init__(self, name):
           self.name = name
   ```

9. **`try` / `except` / `finally` / `raise`**：异常处理机制。

   ```
   try:
       x = 1 / 0
   except ZeroDivisionError:
       print("Cannot divide by zero")
   ```

10. **`import` / `from` / `as`**：用于导入模块。

    ```
    import math
    from datetime import datetime as dt
    ```

11. **`lambda`**：用于定义匿名函数。

    ```
    square = lambda x: x * x
    ```

12. **`global`** / `nonlocal`：声明变量的作用域。

    - `global` 用于声明全局变量。
    - `nonlocal` 用于声明嵌套函数中的非本地变量。

    ```
    x = 10
    def modify():
        global x
        x = 20
    ```

13. **`with`**：上下文管理，用于简化资源管理。

    ```
    with open('file.txt', 'r') as file:
        content = file.read()
    ```

14. **`assert`**：用于调试，断言某个条件为 `True`。

    ```
    assert x > 0, "x must be positive"
    ```

15. **`yield`** / `async` / `await`**：用于生成器和异步编程。

    ```
    async def fetch_data():
        await some_async_function()
    ```

### 如何查看关键字

可以使用 Python 内置的 `keyword` 模块来查看当前 Python 版本的关键字列表：

```
import keyword
print(keyword.kwlist)
```



## API调用



### 常用API



#### `print`

`print()` 函数在 Python 中用于向控制台输出信息，是最常用的内置函数之一。它可以打印各种类型的内容，如字符串、数字、变量、表达式的结果等。以下是 `print()` 函数的用法和示例。

##### 基本用法

```
print("Hello, World!")
```

这会在控制台输出：

```
Hello, World!
```

##### 详细用法和示例

1. **打印多个值**

   - 可以使用逗号分隔多个值，`print()` 会在输出时自动插入空格。

   ```
   print("Hello", "World", 123)
   ```

   输出：

   ```
   Hello World 123
   ```

2. **打印变量**

   - 直接将变量放在 `print()` 中，它会输出变量的值。

   ```
   name = "Alice"
   age = 25
   print("Name:", name, "Age:", age)
   ```

   输出：

   ```
   Name: Alice Age: 25
   ```

3. **打印表达式结果**

   - `print()` 可以直接打印表达式的结果。

   ```
   print(3 + 5)
   ```

   输出：

   ```
   8
   ```

4. **不换行打印**

   - 默认情况下，`print()` 在每次输出后会自动换行。如果不想换行，可以使用 `end` 参数指定结束符。

   ```
   print("Hello", end=" ")
   print("World")
   ```

   输出：

   ```
   Hello World
   ```

   （这里没有换行，而是用空格连接了两次输出）

5. **自定义分隔符**

   - 使用 `sep` 参数来自定义多个值之间的分隔符。

   ```
   print("apple", "banana", "cherry", sep=", ")
   ```

   输出：

   ```
   apple, banana, cherry
   ```

6. **格式化输出**

   - `print()` 支持多种字符串格式化方式，例如使用 **f-string**（推荐）：

     ```
     name = "Bob"
     age = 30
     print(f"My name is {name} and I am {age} years old.")
     ```

     输出：

     ```
     My name is Bob and I am 30 years old.
     ```

   - 也可以使用 `str.format()` 方法：

     ```
     print("My name is {} and I am {} years old.".format(name, age))
     ```

7. **打印带特殊字符的字符串**

   - 可以使用转义字符，例如 `\n`（换行符）和 `\t`（制表符）：

   ```
   print("Line1\nLine2")
   print("Column1\tColumn2")
   ```

   输出：

   ```
   Line1
   Line2
   Column1    Column2
   ```

8. **打印到文件**

   - 可以使用 `file` 参数将输出重定向到文件：

   ```
   with open('output.txt', 'w') as f:
       print("This will be written to the file.", file=f)
   ```

9. **刷新输出缓冲区**

   - `print()` 默认是缓冲输出的，如果需要立即刷新，可以设置 `flush=True`：

   ```
   print("Flushing output", flush=True)
   ```

##### `print()` 函数的完整语法

```
print(*objects, sep=' ', end='\n', file=sys.stdout, flush=False)
```

- `*objects`：要打印的一个或多个对象，可以是字符串、数字、变量等。
- `sep`：指定多个对象之间的分隔符，默认为空格。
- `end`：指定打印结束后的字符，默认为换行符 `\n`。
- `file`：指定输出目标，默认为控制台（`sys.stdout`）。
- `flush`：是否立即刷新输出缓冲区，默认为 `False`。

##### 总结

`print()` 是一个灵活且功能强大的函数，可以满足几乎所有的输出需求。了解其参数和使用方法有助于编写更高效、简洁的代码。

















































