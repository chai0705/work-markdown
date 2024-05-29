摆脱一份幻觉比发现一个真理更能使人明智

当你在凝视深渊的时候深渊也在凝视你

前情提要：在之前的时候，简单的修改和复现了TF卡启动相关的内容，目前看起来倒是还行，现在要做的就是复现一下完整的内容，并且使用上github。

## 1.环境使用和搭建

v2ray

tabby

在tabby里面默认是没有http那些本地网络设置的，所以需要加入一些环境变量才行，具体如下所示：

~~~shell
export ftp_proxy=http://127.0.0.1:8889/
export https_proxy=http://127.0.0.1:8889/
export FTP_PROXY=http://127.0.0.1:8889/
export HTTPS_PROXY=http://127.0.0.1:8889/
export HTTP_PROXY=http://127.0.0.1:8889/
export http_proxy=http://127.0.0.1:8889/
~~~

## 2.推送

现在确认没问题的地方就是rkbin和uboot，这两个基本上就是一个地方，我之前已经通过香橙派搞了一个确认能用的uboot了，所以以后也就根据这个改就行了，现在将这个版本的uboot推送上去。

~~~shell
echo "# uboot" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:chai0705/uboot.git
git push -u origin main
~~~

没一句命令的具体内容为

1. `echo "# uboot" >> README.md`
   - 这条命令在当前目录下创建一个名为 `README.md` 的文件,并在其中写入标题 `# uboot`。这通常用于创建项目的说明文档。
2. `git init`
   - 这条命令初始化一个新的 Git 仓库。这会在当前目录下创建一个隐藏的 `.git` 目录,用于保存 Git 仓库的元数据。
3. `git add README.md`
   - 这条命令将 `README.md` 文件添加到 Git 的暂存区。暂存区是 Git 用于跟踪文件变更的一个概念。
4. `git commit -m "first commit"`
   - 这条命令将暂存区的文件提交到 Git 仓库,并添加提交说明 `"first commit"`。提交是 Git 的基本操作,用于记录项目的历史变更。
5. `git branch -M main`
   - 这条命令将当前分支重命名为 `main`。之前 Git 默认使用 `master` 作为主分支的名称,但现在更多的项目使用 `main` 作为主分支的名称。
6. `git remote add origin git@github.com:chai0705/uboot.git`
   - 这条命令将当前 Git 仓库关联到一个远程 Git 仓库,即 GitHub 上的 `chai0705/uboot.git` 仓库。`origin` 是这个远程仓库的默认名称。
7. `git push -u origin main`
   - 这条命令将当前 `main` 分支的提交推送到远程 `origin` 仓库。`-u` 选项用于将当前分支与远程分支关联起来,以后可以直接使用 `git push` 命令推送。

![image-20240529134321288](https://chai-1301855619.cos.ap-beijing.myqcloud.com/image-20240529134321288.png)

## 3.具体编译

git下两个库，分别为rkbin和uboot，具体命令如下所示：

~~~shell
git clone git@github.com:chai0705/rkbin.git
git clone git@github.com:chai0705/uboot.git
~~~

git完成如下所示：

![image-20240529134934395](https://chai-1301855619.cos.ap-beijing.myqcloud.com/image-20240529134934395.png)

然后进入uboot，运行以下命令编译idbloader和uboot。

~~~shell

# uboot
make CROSS_COMPILE=aarch64-linux-gnu- ARCH=arm  -j32  topeet_rk3588_defconfig 
	  make CROSS_COMPILE=aarch64-linux-gnu- -j32 
	  make CROSS_COMPILE=aarch64-linux-gnu- ARCH=arm  -j32 \
	  BL31=../rkbin/bin/rk35/rk3588_bl31_v1.45.elf \
	  spl/u-boot-spl.bin u-boot.dtb u-boot.itb

# idbloader
./tools/mkimage -n rk3588 -T rksd -d \
	../rkbin/bin/rk35/rk3588_ddr_lp4_2112MHz_lp5_2400MHz_v1.16.bin:spl/u-boot-spl.bin \
	idbloader.img
~~~

编译完成之后如下所示：

![image-20240529135517987](https://chai-1301855619.cos.ap-beijing.myqcloud.com/image-20240529135517987.png)

生成了idbloader.img和u-boot.itb这两个二进制文件，这两个文件的具体作用我只是简单的知道是什么，但并不知道他们详细的内容，甚至我连他们为啥叫这个名字都不知道，这一点问题就挺大的，等第一轮搞完就详细的钻研一下根本。

## 4.烧录

~~~shell
sudo dd if=idbloader.img of=/dev/sdc seek=64
sudo dd if=u-boot.itb of=/dev/sdc seek=16384 conv=notrunc
sync
~~~



5.分区





























