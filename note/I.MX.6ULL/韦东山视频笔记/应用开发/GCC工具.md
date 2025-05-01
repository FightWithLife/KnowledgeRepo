
# GCC编译器

编程发展史：
![[Pasted image 20250427222126.png]]

编译过程：
![[Pasted image 20250427222327.png]]

上述编译过程可以通过gcc -o hello hello.c **-v**
来进行查看

通过上述命令可以得到许多信息，这里只贴简化后的关键步骤：
```
 /usr/lib/gcc/x86_64-linux-gnu/11/cc1  -imultiarch x86_64-linux-gnu hello.c  -o /tmp/ccoMft7N.s
```
可以看到这一步由ccl将hello.c文件由`.c`进行预处理+编译生成`.s`文件

这一步通过as命令，生成`.o`文件
```
 as -v --64 -o /tmp/ccu3fQF4.o /tmp/ccoMft7N.s
```


```
collect2  -o hello .../Scrt1.o .../crti.o .../crtbeginS.o .../crtn.o
```

通过上面四步生成二进制可执行文件
即：
- ccl：预处理+编译生成`.s`文件
- as：汇编生成`.o`文件
- collect：链接生成`.elf`文件

手动执行下面几个命令可以查看这些编译步骤：
![[Pasted image 20250427225057.png]]

>代码中的include代码，编译器搜寻头文件的逻辑是这样：
>使用尖括号`<>`包括的头文件，编译器会去到工具链的目录下进行查看
>使用双引号`""`包括的头文件，编译器会在同级目录下与设定好的文件目录中进行搜索

## GCC常用编译选项

```
 gcc -E main.c //查看预处理结果
 gcc -E -dM main.c > 1.txt //把所有宏展开，存在1.txt里面
 gcc -Wp,-MD,abc.dep -c -o main.o main.c //生成依赖文件adc.dep
 echo 'main(){}' | gcc -E -v - //列出头文件目录、库目录(LIBRARY_PATH)
```
 
 ***`-c`选项***：

这个选项用于进行预处理、编译、汇编，但是不进行链接
>由于gcc生成的时候每个文件都是编译+链接
>因此每次代码有改动的时候，每个`.c`文件都要从头开始执行一次编译
>但是这个会严重降低我们的编译效率，特别是大型工程里面
>因此就会考虑使用`-c`选项，将每个`.c`文件都生成`.o`状态
>**每次代码改动只需要重新编译被改动的`.c`文件就可以，其他文件只需要链接`.o`就可以了**
>当前慧翰的代码编译就是采用这样的方式进行



## 使用GCC生成库文件

### 静态库：

静态库是以`.a`为后缀的库文件
静态库在编译的时候，会被编译进去程序中，可以在没有库函数的条件下去执行
**但是相对来说占用空间会更大**
编译一个静态库文件有以下步骤：
1. 编写源代码和头文件
2. 生成目标文件(`.o`文件)
	1. `gcc -c file1.c file2.c`
	    > 生成file1.o和file2.o
3. 打包静态库：
	1. `ar rcs libmylib.a file1.o file2.o`
		1. 命令参数内容如下：![[Pasted image 20250427234245.png]]
4. 使用静态库：
	1. `gcc main.c -I./include -L. -lmylib -o main`
		1. 命令参数解析如下：![[Pasted image 20250427234420.png]]
#### 注意事项：
![[Pasted image 20250427234455.png]]

### 动态库

使用 GCC 编译动态库（共享库）的步骤如下，与静态库的流程类似但有关键区别（需生成位置无关代码，动态链接）：

---

**1. 编写源代码和头文件**
假设文件与静态库相同：
• `file1.c` 和 `file2.c`：动态库的源文件。

• `mylib.h`：头文件，声明库中的函数。


---

**2. 生成位置无关的目标文件（`.o` 文件）**
编译时添加 `-fPIC` 选项，生成位置无关代码（Position-Independent Code）：
```bash
gcc -c -fPIC file1.c file2.c
```
• `-fPIC`：强制编译器生成可在内存任意位置加载的代码（动态库必需）。

• 生成 `file1.o` 和 `file2.o`。


---

**3. 生成动态库（`.so` 文件）**
使用 GCC 的 `-shared` 选项将目标文件打包成动态库：
```bash
gcc -shared -o libmylib.so file1.o file2.o
```
• `-shared`：明确告诉 GCC 生成动态库。

• 动态库命名格式为 `lib<库名>.so`（如 `libmylib.so`）。


---

**4. 使用动态库**
假设主程序为 `main.c`，编译并链接动态库：
```bash
gcc main.c -I./include -L. -lmylib -o main
```
• `-I./include`：指定头文件路径（若头文件在 `include` 目录下）。

• `-L.`：指定库文件路径（当前目录）。

• `-lmylib`：链接名为 `libmylib.so` 的库（省略 `lib` 和 `.so`）。


---

**5. 运行程序前设置动态库路径**
动态库在运行时需要被系统找到，需以下操作之一：
**方法 1：临时指定路径（开发调试）**
```bash
export LD_LIBRARY_PATH=.:$LD_LIBRARY_PATH  # 将当前目录加入库搜索路径
./main
```

在命令 `export LD_LIBRARY_PATH=.:$LD_LIBRARY_PATH` 中，`.:` 的作用是将​**​当前目录​**​添加到 `LD_LIBRARY_PATH` 环境变量中。具体解释如下：

​**​1. `:` 的作用​**​

- `:` 是 Linux 环境变量中的路径分隔符，类似于 Windows 中的分号 `;`。
- 例如，若 `LD_LIBRARY_PATH` 原本是 `/usr/lib:/home/user/libs`，添加 `.:` 后变为：  
    `.:/usr/lib:/home/user/libs`  
    （当前目录 + 原有路径）。

​**​2. `.` 的含义​**​

- `.` 表示​**​当前工作目录​**​（即执行命令时所在的目录）。
- 通过将 `.` 添加到 `LD_LIBRARY_PATH`，系统在运行程序时会在当前目录下搜索动态库（`.so` 文件）。

**​3. 命令的作用​**​

- ​**​目的​**​：告诉操作系统，除了默认的系统库路径（如 `/lib`、`/usr/lib`）外，还要在​**​当前目录​**​中查找动态库。
- ​**​典型场景​**​：开发调试时，动态库（如 `libmylib.so`）通常直接放在项目目录下，而不是安装到系统目录（如 `/usr/lib`），此时需要临时指定当前目录为库搜索路径。


**方法 2：永久配置路径（生产环境）**
```bash
# 将动态库复制到系统库目录（如 /usr/lib）
sudo cp libmylib.so /usr/lib

# 更新动态库缓存
sudo ldconfig
```

---

**6. 验证动态库**
• 查看动态库依赖：

  ```bash
  ldd main  # 检查主程序依赖的动态库
  ```
• 查看符号表：

  ```bash
  nm -D libmylib.so  # 显示动态库中的符号（函数/变量）
  ```

---

**完整示例**
```bash
# 生成位置无关的目标文件
gcc -c -fPIC file1.c file2.c

# 生成动态库
gcc -shared -o libmylib.so file1.o file2.o

# 编译主程序并链接动态库
gcc main.c -I./include -L. -lmylib -o main

# 运行程序（临时指定路径）
export LD_LIBRARY_PATH=.:$LD_LIBRARY_PATH
./main
```

---

**动态库 vs 静态库关键区别**

| 特性               | 静态库（`.a`）                 | 动态库（`.so`）                  |
|--------------------|-------------------------------|----------------------------------|
| 编译时         | 代码嵌入可执行文件             | 仅记录库的引用                   |
| 运行时         | 无需外部文件                  | 需动态库文件存在且路径正确       |
| 内存占用       | 占用更多内存（多进程重复加载） | 共享内存，节省空间               |
| 更新           | 需重新编译程序                | 替换库文件即可生效               |
| 性能           | 无加载开销                    | 首次加载有轻微开销               |
| 依赖管理       | 无依赖问题                    | 需确保版本兼容性和路径正确       |

---

**注意事项**
1. 命名规范：动态库名格式为 `lib<name>.so`，链接时使用 `-l<name>`。
2. 版本控制：建议为动态库添加版本号（如 `libmylib.so.1.0`），通过符号链接管理。
3. 调试符号：开发时可用 `-g` 选项保留调试信息：
   ```bash
   gcc -shared -g -o libmylib.so file1.o file2.o
   ```
4. 优化选项：生产环境可添加 `-O2` 优化：
   ```bash
   gcc -shared -O2 -o libmylib.so file1.o file2.o
   ```

通过以上步骤，你可以成功编译和使用动态库！




