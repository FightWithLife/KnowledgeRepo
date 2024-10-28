# Shell语法



## 获取命令输出

```shell
value=$(command)
```



## 函数

**函数定义**

```
function_name(){

}
```

**函数调用**

使用以上方式定义函数，使用以下方式调用函数

```
function_name
```

**函数传参与参数调用**

shell中函数传参与参数获取的方式，跟shell脚本本身类似

```shell
function_name(){
	para1=$1#获取参数1
	para2=$2#获取参数2
	
	echo "$para1 $para2"
}

function_name "Hello" "World"
```





## 变量



**变量定义**

```shell
i=1
#注意，这里不要有空格
```

**变量使用**

```
$i
${i}
```

**环境变量**

```
#!/bin/bash

# 定义环境变量
export MY_VAR="Hello, World!"

# 调用子脚本
./another_script.sh
```

在子脚本中，可以使用$MY_VAR环境变量



## 循环



### **while**

**基本语法**

```shell
while [ condition ]; do
    # 循环体
done
```

基本使用方法：

```shell
#!/bin/bash

# 初始化变量
count=1

# 使用 while 循环
while [ $count -le 5 ]; do
    echo "当前计数: $count"
    ((count++))  # 增加计数
done
```

无限循环：

```shell
#!/bin/bash

# 无限循环
while true; do
    echo "请输入一个数字 (输入 0 退出): "
    read number

    if [ "$number" -eq 0 ]; then
        echo "退出循环"
        break  # 退出循环
    fi

    echo "您输入的数字是: $number"
done
```

**逐行处理命令输出**

```
while IFS= read -r line; do
    FmcPingRetParse "$line"
done <<< "$pingRet"
```

1. **`while IFS= read -r line; do ... done`**

- **`while`**：用于开始一个循环，直到没有更多的输入。
- **`IFS=`**：`IFS` 是内部字段分隔符（Internal Field Separator）的缩写。将其设置为空意味着在读取输入时，`read` 命令不会对输入进行分割。这样可以保留输入行中的所有空格和特殊字符。
- **`read -r line`**：`read` 命令用于从输入中读取一行。`-r` 选项用于防止 `read` 命令处理反斜杠（`\`），确保原始输入被读取。每次读取一行，赋值给变量 `line`。
- **`do ... done`**：在 `do` 和 `done` 之间的代码块是在每次读取一行后要执行的操作。

2. **`FmcPingRetParse "$line"`**

- 在 `do` 代码块中，调用 `FmcPingRetParse` 函数，并将读取的每一行作为参数传递给它。这样就可以在 `FmcPingRetParse` 中处理这行数据。

3. **`<<< "$pingRet"`**

- **`<<<`**：这是一个重定向操作符，称为“这里字符串”（here string）。它将右侧的字符串（在这个例子中是变量 `pingRet`）作为标准输入传递给左侧的命令（在这个例子中是 `while` 循环）。
- **`"$pingRet"`**：这是包含 `ping` 命令输出的变量。通过这里字符串，将 `pingRet` 的内容传递给 `while` 循环进行逐行处理。

> [!caution]
>
> 这里的IFS实际上是被赋值为空，也就是说这里`while IFS= read -r line;`进行了两个操作：
>
> - 将IFS赋值为空格
> - 读取一行read(不进行任何转译，保留原始数据`-r`)并赋值给变量line



### for循环

在 Shell 脚本中，`for` 循环用于重复执行一段代码，直到指定的条件不再满足。`for` 循环可以通过多种方式进行迭代，以下是一些常见的用法。

#### 使用列表进行迭代

这种方式适用于循环访问一组预定义的值。

```
for variable in value1 value2 value3; do
    # 循环体
done
```

示例：

```
#!/bin/bash

# 使用列表进行迭代
for fruit in apple banana cherry; do
    echo "I like $fruit"
done
```

输出为：

```
I like apple
I like banana
I like cherry
```

#### 使用范围进行迭代

可以使用 `seq` 命令或 `{}` 语法来指定一个范围。

```
for variable in $(seq start end); do
    # 循环体
done
```

或者

```
for variable in {start..end}; do
    # 循环体
done
```

示例：

```
#!/bin/bash

# 使用 seq 进行范围迭代
for number in $(seq 1 5); do
    echo "Number: $number"
done

# 使用 {} 进行范围迭代
for number in {1..5}; do
    echo "Number: $number"
done
```

输出：

```
Number: 1
Number: 2
Number: 3
Number: 4
Number: 5
Number: 1
Number: 2
Number: 3
Number: 4
Number: 5
```

#### 遍历数组元素

你可以使用 `for` 循环遍历数组元素。

```
#!/bin/bash

# 定义一个数组
fruits=("apple" "banana" "cherry")

# 遍历数组
for fruit in "${fruits[@]}"; do
    echo "I like $fruit"
done
```

#### 使用c风格的for循环

```
for (( initialization; condition; increment )); do
    # 循环体
done
```

示例：

```
#!/bin/bash

# C 风格的 for 循环
for (( i = 1; i <= 5; i++ )); do
    echo "Count: $i"
done
```







## 数学运算

```shell
可以使用 expr 或双小括号 (( )) 进行数学运算：

a=5
b=3
result=$((a + b))#注意这里要加$表示引用
echo "Sum: $result"  # 输出: Sum: 8
```



## 条件判断



### case in

**基本使用语法**

```shell
case variable in
    pattern1)
        # 当 variable 匹配 pattern1 时执行的代码
        ;;
    pattern2)
        # 当 variable 匹配 pattern2 时执行的代码
        ;;
    *)
        # 默认情况（可选）
        ;;
esac
```

注意这里是**esac**

> [!caution]
>
> case语句记得每种情况后面都要加`;;`同时末尾还要添加`esac`作为结尾，否则会报错

### if then











# 开发经验



## 脚本参数解析

脚本参数解析可以将发送的参数存储到数组当中，例如下面的例子：

```shell
#目标ip或者域名
gTarget=""
#发送用的ip或者端口
gSource=""

#定义函数
FmcPingParmParse(){
    i=0
    #将参数赋值给param数组
    param=("$@")
    #使用一个while循环
    while [ $i -lt $# ];do
    	#使用case in作为条件判断
        case ${param[$i]} in
        #参数符合条件
        "-t")
        	#把下一个参数赋值给变量
            gTarget="${param[$((i+1))]}"
            echo "Target:${gTarget}"
            #参数递增两位，继续解析后面的参数
            i=$((i+2))
            ;;
        "-s")
            gSource="${param[$((i+1))]}"
            echo "Source:${gSource}"
            i=$((i+2))
            ;;
        *)
            echo "异常参数"
            i=$((i+1))
            ;;
        esac
    done
}


FmcPingParmParse "$@"

```

## Sleep命令使用

在 Bash 脚本中，`sleep` 命令用于暂停执行一段时间，通常用于控制脚本的运行节奏或在某些条件下进行延迟。`sleep` 命令的基本用法非常简单。

```
sleep 1 #休眠1s
sleep 1m #休眠1min
sleep 1h #休眠1h
sleep 1d #休眠1天

注：上面也可以使用小数来进行更精准的控制
```

## 参数检查

用来检查某个参数为空的时候，可以使用如下语句

```
if [ -n "$Param" ];then
	dosomething
fi
```

执行命令获取命令输出



## shell中的关联数组（c：结构体）

关联数组（Associative Array）是一种数据结构，它允许使用字符串作为索引（键）来存储和访问数据，而不是使用整数索引。这使得关联数组非常灵活和强大，尤其适用于需要通过名称而非数字索引来管理数据的场景。

### 关联数组的特点

1. **键值对存储**：每个元素由一个唯一的键（字符串）和一个值（可以是任意类型）组成。例如，`person["name"]="Alice"`。
2. **动态大小**：关联数组的大小不固定，可以在运行时根据需要动态添加或删除键值对。
3. **快速查找**：通过键可以快速访问相应的值。

### 在 Bash 中使用关联数组

在 Bash 脚本中，关联数组可以使用 `declare` 命令声明，并且键是字符串。以下是使用 Bash 关联数组的基本示例：

声明和初始化数组：

```
#!/bin/bash

# 声明一个关联数组
declare -A person

# 初始化关联数组
person["name"]="Alice"
person["age"]=30
person["city"]="New York"
```

访问和输出关联数组的值：

```
# 输出关联数组的值
echo "Name: ${person["name"]}"   # 输出: Name: Alice
echo "Age: ${person["age"]}"     # 输出: Age: 30
echo "City: ${person["city"]}"   # 输出: City: New York
```

遍历关联数组：

```
# 遍历所有键
for key in "${!person[@]}"; do
    echo "$key: ${person[$key]}"
done
```

> [!note]
>
> `declare`解析：在 Bash 中，`declare` 和 `-A` 是用于声明变量和数据结构的命令和选项。以下是对它们的详细解释：
>
> ### `declare`
>
> `declare` 是一个内置命令，用于声明变量并为其设置属性。它可以用于定义普通变量、数组（包括关联数组）、只读变量等。
>
> **声明变量**：
>
> ```
> declare varname
> ```
>
> **赋值变量**：
>
> ```
> declare varname=value
> ```
>
> **显示变量类型**：可以使用 `declare -p` 来显示变量的属性和当前值
>
> `-A`选项专门用于声明关联数组，关联数组允许数组使用字符串作为索引来访问数组元素



## grep在实际编程中的使用

```
if echo "$ping_output" | grep -q "time="; then
    echo "Ping 成功，以下是结果:"
else
    echo "Ping 失败，可能出现了错误:"
    echo "$ping_output" | grep -i "error"  # 如果输出中包含错误信息
fi
```

**检查每一条响应**：

- ```
  if echo "$ping_output" | grep -q "time="; then
  ```

  - 这一行将 `ping_output` 的内容通过管道传递给 `grep`。

  - `grep -q "time="` 检查 `ping_output` 中是否有包含 `time=` 的行。
  - 如果找到了匹配的行，`grep` 会返回状态码 `0`，`if` 条件为真，执行 `then` 后的语句。
  - 如果没有找到匹配，`grep` 返回状态码 `1`，`else` 后的语句将被执行。

**输出结果**：

- 如果 `ping` 成功并且找到了有效的响应，输出 `"Ping 成功，以下是结果:"`。
- 如果没有找到有效响应，输出 `"Ping 失败，可能出现了错误:"`，并进一步检查 `ping_output` 中是否有错误信息。







