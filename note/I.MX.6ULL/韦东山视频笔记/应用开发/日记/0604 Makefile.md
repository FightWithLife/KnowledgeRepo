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
	`$(filter patten..., text)`









