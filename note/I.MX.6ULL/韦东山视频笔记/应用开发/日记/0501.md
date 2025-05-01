
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



