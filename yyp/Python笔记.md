# Python语法





## 其他



### 返回值类型指定

python中可以指定函数的返回值类型，帮助IDE确定返回值的类型，例如

```
def relative_to_assets(path: str) -> Path:
    return fmc_eth_tool.ASSETS_PATH / Path(path)
```

里面的`->`就是用于指定函数返回值类型为`Path`

与静态类型检查工具配合：

- 工具如 `mypy` 可以使用类型提示来在运行前检查代码中是否存在类型不匹配的问题。
- 例如，如果你尝试将 `relative_to_assets` 的返回值赋值给一个变量，且该变量被声明为非 `Path` 类型，`mypy` 会发出警告。



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



# Python编程



## Cve处理脚本代码解析及API调用记录



### CveCompareTool.py

```python
import pandas as pd

# 读取文件A和文件B
file_a = 'FLC_ALL_CVE_Handle_Report-V1.0.xlsx'  # Excel文件路径
file_b = 'cve_unique.csv'   # CSV文件路径

# 读取文件A (Excel)
df_a = pd.read_excel(file_a)

# 读取文件B (CSV)，并指定编码以避免读取错误
df_b = pd.read_csv(file_b, encoding='utf-8')  # 根据需要修改编码，如 'gbk'

# 确保文件A和文件B中存在 "漏洞ID" 这一列
if '漏洞ID' not in df_a.columns or '漏洞ID' not in df_b.columns:
    raise ValueError("两个文件都必须包含 '漏洞ID' 列")

# 处理空值，删除 "漏洞ID" 列为空的行
df_a = df_a.dropna(subset=['漏洞ID'])
df_b = df_b.dropna(subset=['漏洞ID'])

# 获取 "漏洞ID" 列，并找到匹配的行
matching_rows = pd.merge(df_a, df_b, on='漏洞ID', how='inner')  # 找到ID相同的行

# 写入到 Processed.xlsx 文件
matching_rows.to_excel('Processed.xlsx', index=False)

# 找到在文件B中没有匹配的行
untreated_rows = df_b[~df_b['漏洞ID'].isin(df_a['漏洞ID'])]

# 写入到 untreated.xlsx 文件
untreated_rows.to_excel('untreated.xlsx', index=False)

print("处理完成，结果已保存到 'Processed.xlsx' 和 'untreated.xlsx'。")

```

#### `read_excel`/`read_csv`

其中`pd.read_excel(file_a)`将通过`read_excel`读取文件`A`，将其内容加载到一个`pandas DataFrame`对象里

这个对象将成为一个二维的表格，每一列都可以通过列名访问。

上面两个函数功能类似，只不过针对的文件格式不同。

```
read_excel:xls.xlsx
read_csv:csv
```

在 `pandas` 中，可以通过列名来访问 DataFrame 中的某一列或某个元素。以下是一些常用的操作：

##### 1. **访问某一列的所有数据**
你可以通过列名来访问 DataFrame 中的某一列，这会返回该列的数据作为 `pandas` Series 对象。

假设 `df_a` 是你读取的 DataFrame，且有一列名为 `漏洞ID`，你可以通过以下方法来访问该列的所有数据：

```python
# 访问 "漏洞ID" 列的所有数据
漏洞ID列 = df_a['漏洞ID']
```

这会返回 `df_a` 中 `漏洞ID` 列的所有数据，类型是 `pandas.Series`。你可以像处理列表一样对其进行操作。

##### 2. **访问某个元素**
如果你想访问某一行和某一列的交点元素，可以使用 `.loc[]` 或 `.iloc[]` 来按行列索引进行访问。

- 使用 `.loc[]` 根据标签（行名和列名）访问：
  ```python
  # 获取第1行 "漏洞ID" 列的值
  value = df_a.loc[0, '漏洞ID']
  ```

  这里，`0` 是行的标签，`'漏洞ID'` 是列的标签。`loc[]` 用于通过标签定位。

- 使用 `.iloc[]` 根据行号和列号（位置索引）访问：
  ```python
  # 获取第1行第1列的值
  value = df_a.iloc[0, 0]
  ```

  `iloc[]` 用于基于整数位置进行定位，`0` 是行和列的索引位置（从0开始）。

##### 3. **访问多列的数据**
你也可以通过一个列名列表来访问多个列的数据，返回一个新的 DataFrame：

```python
# 访问 "漏洞ID" 和 "其他列" 两列的数据
多列数据 = df_a[['漏洞ID', '其他列']]
```

##### 4. **通过条件过滤数据**
你还可以通过条件来访问特定行的数据。例如，获取 `漏洞ID` 列中值等于某个特定值的行：

```python
# 访问 "漏洞ID" 列等于某个值的行
filtered_data = df_a[df_a['漏洞ID'] == 'CVE-2020-12345']
```

##### 总结：
- 通过 `df['列名']` 获取某一列的数据。
- 通过 `df.loc[行标签, 列名]` 获取某一特定单元格的数据。
- 通过 `df.iloc[行索引, 列索引]` 通过整数索引获取某一特定单元格的数据。
- 通过条件过滤 `df[df['列名'] == '某个值']` 获取符合条件的行数据。

#### **匹配列中相同的行`pd.merge`**

```
matching_rows = pd.merge(df_a, df_b, on='漏洞ID', how='inner')
```

- matching_rows = pd.merge(df_a, df_b, on='漏洞ID', how='inner')：使用`pandas` 的`merge` 函数，按 "漏洞ID" 列将两个 `DataFrame`

  （`df_a` 和`df_b`）进行合并：

  - `on='漏洞ID'` 表示合并时要根据 "漏洞ID" 列进行匹配。
  - `how='inner'` 表示使用 **内连接**（`inner join`），即只保留两个文件中都有的 "漏洞ID" 行（即匹配的行）。

- `matching_rows` 将包含文件A和文件B中都有的 "漏洞ID" 行。

#### 将对应的内容保存到`excel`

```python
matching_rows.to_excel('Processed.xlsx', index=False)
```

`matching_rows.to_excel('Processed.xlsx', index=False)`：将 `matching_rows` 中的内容写入到一个新的 Excel 文件 `Processed.xlsx`。`index=False` 表示在输出时不保存行索引。

> 此处不保存行索引指的是写入的时候不保存对应的索引信息
>
> 也就是程序中的`DataFrame`原本的数据应该是：1、a 2、b
>
> 此时不保存索引就是将1、2这种信息去掉，只留下a、b这样的信息，然后写入。

#### 在文件B中寻找未匹配的行

```python
untreated_rows = df_b[~df_b['漏洞ID'].isin(df_a['漏洞ID'])]
```

`untreated_rows = df_b[~df_b['漏洞ID'].isin(df_a['漏洞ID'])]`：从文件B（`df_b`）中筛选出那些 "漏洞ID" 列的值没有出现在文件A（`df_a`）中的行。

- `df_b['漏洞ID'].isin(df_a['漏洞ID'])` 会返回一个布尔系列（`True` 或 `False`），表示文件B中的 "漏洞ID" 是否存在于文件A的 "漏洞ID" 列中。
- `~` 是逻辑取反操作符，表示选择文件B中没有匹配的行。





































