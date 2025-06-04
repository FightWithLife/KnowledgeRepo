# Makefile的引入与规则

如前面gcc介绍的时候所说的，gcc在编译的时候使用普通的方式去进行编译生成可执行文件的话
需要将每个文件都编译一次，哪怕没有进行修改
```
gcc -o main mian.c a.c b.c
```

对于这种由于编译导致的效率上的降低，我们有新的办法，即使用如下方式：
*先生成`.o`文件，然后再通过链接生成可执行文件*
这样子每次就只需要对有经过修改的文件执行编译就可以了

我们的makefile引入也是为了方便类似的效果，即可以像大多数ide一样直接编译你的工程，不需要一个个去筛选哪个进行过修改

**Makefile用于分辨文件是否经过修改的方法，是使用修改时间去分辨**

## Makefile的规则

Makefile的语法规则如下：
	目标文件：依赖文件
		(Tab)命令

下面为一个基本的makefile文件示例：
```makefile
App:main.o a.o b.o
	gcc -o App main.o a.o b.o
a.o：a.c
	gcc -c -o a.o a.c
b.o: b.c
	gcc -c -o b.o b.c
```

***注意，这里的makefile写法里面，tab是作为分隔符存在的，不是通过缩进去进行判断***
***因此使用vscode写makefile的时候需要注意相关的事项***


# Makefile语法

## 通配符
- %.o 表示所有以.o作为结尾的目标文件
- $@  表示目标
- $<  表示第一个依赖文件
- $^  表示所有依赖文件

## 假想目标

![[Pasted image 20250529223805.png]]
该选项关系到make的使用方法

直接执行make命令的时候，会选择规则文件中的第一个目标，进行生成。

若是make后面带目标，比如`all`、`clean`
则会单独执行该规则

**上图中的写法，若是当前目录下存在`clean`文件，则无法执行`make clean`**
此时可以使用假想目标符号：`.PHONY`
其操作如下：
![[Pasted image 20250529224256.png]]

## 变量

赋值符号：
- `:=` 
	- 即时变量
- `=`
	- 延时变量
- `?=`
	- 延时变量(第一次赋值起效，若是前面赋值过则不起效)
- `+=`
	- 附加，它是即时变量还是延时变量取决于前面的定义

变量的引用方法：`$(var)`


### 即时变量

即时变量定义方法：A := Var
说明：
	即时变量会在定义赋值的一瞬间直接赋值

### 延时变量

定义方法：B = Var
说明：
	延时变量会在使用到的时候才进行赋值


# Makefile 常用函数

Makefile中存在一些内置的常用函数，下面介绍几个比较常用的。

## foreach

**作用**：
	对list中的每个变量执行text中的公式

**用法**

```makefile
$(foreach var,list,text)
```

使用示例：
![[Pasted image 20250604220609.png]]

## filter

**作用**：
	在text中取出符合patten格式的值

**用法**：
	$(filter patten..., text)

## filter-out

**作用**：
	在text中取出不符合patten格式的值

**用法**：
	同filter

**用法示例**:
![[Pasted image 20250604225947.png]]

## wildcard

**作用**：
	取出目录下符合pattern格式的文件

**用法**：
	$(wildcard pattern)
**用法示例**：
![[Pasted image 20250604230312.png]]
使用示例2
![[Pasted image 20250604231521.png]]

## patsubst

**作用**：
	把var中pattern格式的变量修改为replacement格式

**用法**：
	$(patsubst pattern, replacement, $(var))

**使用示例**：
![[Pasted image 20250604232341.png]]


# Makefile 解决头文件更新可执行文件不更新问题

通过在.o文件的依赖中添加.h头文件部分，用以更新头文件
![[Pasted image 20250604234607.png]]

# gcc编译器打印相关依赖（调试技巧）

![[Pasted image 20250604234939.png]]

