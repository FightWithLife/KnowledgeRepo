
![[嵌入式Linux应用开发完全手册V5.2_IMX6ULL_Pro开发板.pdf#page=86&rect=38,124,557,337|嵌入式Linux应用开发完全手册V5.2_IMX6ULL_Pro开发板, p.86]]
![[嵌入式Linux应用开发完全手册V5.2_IMX6ULL_Pro开发板.pdf#page=87&rect=30,396,561,669|嵌入式Linux应用开发完全手册V5.2_IMX6ULL_Pro开发板, p.87]]

下面是图中的代码命令：

```
git clone https://e.coding.net/codebug8/repo.git

mkdir -p 100ask_imx6ull-sdk && cd 100ask_imx6ull-sdk

../repo/repo init -u https://gitee.com/weidongshan/manifests.git -b linux-sdk -m  mx6ull/100ask_imx6ull_linux4.9.88_release.xml --no-repo-verify

../repo/repo sync -j4
```