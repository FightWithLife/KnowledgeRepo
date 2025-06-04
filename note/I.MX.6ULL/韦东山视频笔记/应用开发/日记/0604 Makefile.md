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



