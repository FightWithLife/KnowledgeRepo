
![[嵌入式Linux应用开发完全手册V5.2_IMX6ULL_Pro开发板.pdf#page=86&rect=38,124,557,337|嵌入式Linux应用开发完全手册V5.2_IMX6ULL_Pro开发板, p.86]]
![[嵌入式Linux应用开发完全手册V5.2_IMX6ULL_Pro开发板.pdf#page=87&rect=30,396,561,669|嵌入式Linux应用开发完全手册V5.2_IMX6ULL_Pro开发板, p.87]]

下面是图中的代码命令：

```
git clone https://e.coding.net/codebug8/repo.git

mkdir -p 100ask_imx6ull-sdk && cd 100ask_imx6ull-sdk

../repo/repo init -u https://gitee.com/weidongshan/manifests.git -b linux-sdk -m  mx6ull/100ask_imx6ull_linux4.9.88_release.xml --no-repo-verify

../repo/repo sync -j4
```


> repo是一个仓库管理工具
> 上面的这个repo命令用于解析https://gitee.com/weidongshan/manifests.git仓库下的mx6ull/100ask_imx6ull_linux4.9.88_release.xml文件
> 将里面的仓库路径以及其中的文件进行下载

由于教程自带的命令下载的repo版本比较老，可以使用git仓库https://gitee.com/weidongshan/manifests.git中的命令进行下载
比如：
```
git clone https://gerrit.googlesource.com/git-repo  (谷歌官方源)
git clone https://mirrors.tuna.tsinghua.edu.cn/git/git-repo (国内清华源)
git clone https://gerrit-googlesource.lug.ustc.edu.cn/git-repo (国内中科大源)
```

同时下载过程中会出现类似如下情况的报错
```
ubuntu-20@ubuntu:~/code/100ask_imx6ull-sdk$ ../git-repo/repo sync -j4 Fetching: 30% (3/10) 3:43 | 4 jobs | 3:43 ST-Buildoot-dl/ST-Buildoot-dl @ Buildroot_2020.02.x/dlInvalid clone.bundle file; ignoring. Fetching: 40% (4/10) 18:00 | 4 jobs | 18:00 ST-Buildoot-dl/ST-Buildoot-dl @ Buildroot_2020.02.x/dlInvalid clone.bundle file; ignoring.
```
这种情况可以无视，具体原因可以查看下面deepseek的回答
![[Pasted image 20250411002143.png]]
在之后如果出现了解压错误之类的报错
类似下面这种：
```
error: RPC failed; curl 18 transfer closed with outstanding read data remaining error: 11977 bytes of body are still expected fetch-pack: unexpected disconnect while reading sideband packet fatal: early EOF fatal: fetch-pack: invalid index-pack output
```
可以重新执行命令：
`repo sync -j4`
