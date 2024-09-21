## `Linux`内核源码下载编译

这部分内容为`GPT`生成，暂时未进行实践，待完善

### `Linux`内核源码下载

- 更新系统并下载编译依赖项

  - ```
    #更新软件包的本地索引，即软件包列表。它从你系统配置的所有软件源（也称为存储库）中获取最新的软件包信息。
    sudo apt update
    #实际执行软件包的更新操作。它会基于 sudo apt update 获取的最新包索引，升级系统中已经安装的软件包到它们的最新版本。
    sudo apt upgrade
    #安装内核编译需要的依赖项
    sudo apt install build-essential libncurses-dev bison flex libssl-dev libelf-dev
    ```

  - 依赖项各自的作用
    - `build-essential`
      - **功能**: 包含了一组用于编译软件的基本工具，包括 `gcc`（GNU C 编译器）、`g++`（GNU C++ 编译器）、`make`、`dpkg-dev` 等。
      - **用途**: 在编译内核和其他软件时提供基础的编译工具。
    - `libncurses-dev`
      - **功能**: 提供 `ncurses` 库的开发头文件。`ncurses` 是一个用于在终端中创建文本界面（`TUI`）的库。
      - **用途**: 在配置内核时（例如使用 `make menuconfig`）会用到 `ncurses` 库来生成用户友好的菜单界面。
    - `bison`
      - **功能**: 一个语法分析器生成器（解析器生成器），通常用于从上下文无关文法生成语法解析器。
      - **用途**: 在编译过程中处理内核的各种代码生成任务，尤其是解析 C 语言中的复杂语法结构。
    - `flex`
      - **功能**: 一个词法分析器生成器，它用于从词法分析规则生成词法解析器。
      - **用途**: 与 `bison` 一起使用，用于处理内核代码中的词法分析阶段。
    - `libssl-dev`
      - **功能**: 提供用于加密操作的 `OpenSSL `库的开发头文件。`libssl` 是 `OpenSSL `的库，广泛用于加密、`SSL/TLS` 通信等。
      - **用途**: 在编译内核时，某些加密模块或功能（例如内核中对 `SSL/TLS` 的支持）需要这个库。
    - `libelf-dev`
      - **功能**: 提供 `ELF（Executable and Linkable Format）` 文件格式的开发库和头文件。`ELF` 是 `Linux` 系统上可执行文件、共享库和目标文件的标准格式。
      - **用途**: 内核在编译过程中需要处理 `ELF` 文件，尤其是在生成内核模块和处理相关调试信息时。

这些依赖项负责提供编译内核时所需的基础工具和库支持。`build-essential` 提供了基本的编译器工具链，`libncurses-dev` 用于生成内核配置菜单，`bison` 和 `flex` 是用于生成语法和词法解析器的工具，而 `libssl-dev` 和 `libelf-dev` 分别提供加密支持和 `ELF `文件格式支持。



-------------------------------------

这里更新的时候出现过一个问题：

```
study@study-virtual-machine:~/code$ sudo apt upgrade
正在等待缓存锁：无法获得锁 /var/lib/dpkg/lock-frontend。锁正由进程 3701（unattended-upgr）持有... 13秒
```

无法获取该缓存锁，这个进程一直运行没有结束

这里通过查阅发现该进程为`sudo apt update`命令执行后的后台更新进程，一般等待几分钟可以让其完成更新，之后就会释放缓存锁了

这里使用命令`ps aux | grep -i unattended-upgr`查看进程是否正在运行

发现长时间没有结束后选择直接杀死进程：

`sudo kill -9 3701`

之后再次运行`sudo upgrade`没有再出现缓存锁无法获取的问题

关于杀死进程可以使用的几个`Shell`命令:

```
1- kill
kill命令的使用一般要搭配PID进行，此处可以使用
ps aux | grep process_name
获取pid号
用法：kill PID
有时候会遇到该进程是系统某些比较重要的组件的情况，这时候如果想杀死该进程可以使用
kill -9 PID
强制杀死进程

2- killall
killall命令可以杀死所有包含指定名称的进程
用法:killall process_name

3- pkill
pkill与killall类似，可以根据进程的名称杀死进程
用法: pkill process_name
```



-----------------------------------------------



- 使用`git`拉取`linux`内核源码：`git clone https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git`

- 编译

  - 配置内核模块

    - 使用当前系统配置作为基础进行选择

    ```
    cp /boot/config-$(uname -r) .config
    make oldconfig
    ```

    - 手动配置内核模块

    ```
    make menuconfig
    ```

    - 编译内核模块

    ```
    #-j$(nproc) 命令会根据你的 CPU 核心数并行编译，加快编译速度。$(nproc) 会返回你的 CPU 核心数。
    make -j$(nproc)
    ```

编译完成后可以使用以下命令

`sudo make install`

将内核安装至系统中运行

安装完成后可以重启使用`uname -r`查看内核版本是否与你安装的一致

若是不一致可以尝试手动更新引导程序

```
sudo update-grub
```































