# build.sh 脚本分析

> `build.sh` 是一个构建脚本，通过命令行参数来执行不同的构建任务。根据你提供的输出信息，以下是每个选项的简要说明：
>
> - `lunch`：选择 defconfig（默认配置），可以用于选择构建目标。
> - `*_defconfig`：切换到指定的 defconfig（配置文件），用于选择特定的板级配置。
> - `olddefconfig`：解决 `.config` 中的未解析符号。
> - `savedefconfig`：将当前配置保存为 defconfig（配置文件）。
> - `menuconfig`：基于 curses 的交互式配置工具，用于进行配置。
> - `kernel-5.10`：构建 5.10 版本的内核。
> - `kernel`：构建内核。
> - `modules`：构建内核模块。
> - `loader`：构建引导加载程序（uboot 或 spl）。
> - `uboot`：构建 u-boot 引导加载程序。
> - `spl`：构建 spl（二级引导加载程序）。
> - `uefi`：构建 UEFI。
> - `wifibt`：构建 Wifi/BT 模块。
> - `rootfs`：构建根文件系统，默认使用 buildroot。
> - `buildroot`：构建 buildroot 根文件系统。
> - `yocto`：构建 Yocto 根文件系统。
> - `debian`：构建 Debian 根文件系统。
> - `recovery`：构建恢复镜像。
> - `pcba`：构建 PCBA（Printed Circuit Board Assembly）。
> - `security_check`：检查安全功能的条件。
> - `createkeys`：生成安全启动根密钥。
> - `security_uboot`：使用安全参数构建 u-boot。
> - `security_boot`：使用安全参数构建引导加载程序。
> - `security_recovery`：使用安全参数构建恢复镜像。
> - `security_rootfs`：使用安全参数构建根文件系统和相关镜像（仅用于 dm-v）。
> - `updateimg`：构建更新镜像。
> - `otapackage`：构建 OTA 更新镜像。
> - `sdpackage`：构建 SD 卡更新镜像。
> - `firmware`：生成和检查固件。
> - `all`：构建所有基本镜像。
> - `save`：保存镜像和构建信息。
> - `allsave`：构建所有内容、固件、更新镜像并保存。
> - `cleanall`：清理构建过程中生成的文件。
> - `post-rootfs`：触发 post-rootfs 钩子脚本。
> - `shell`：设置用于开发的 shell。
> - `help`：显示使用说明。

## 1.BASH_SOURCE

~~~shell
#!/bin/bash

# 这个脚本检查是否在 Bash shell 中运行。
# 如果不是，则切换到 Bash shell 并在其中执行脚本。

if [ -z "$BASH_SOURCE" ]; then
	echo "Not in bash, switching to it..."

	# 检查传递给脚本的命令行参数
	case "${@:-shell}" in
		shell) 
			# 如果参数是 "shell"，在一个新的 Bash shell 中执行脚本
			./build.sh shell ;;
		*)
			# 如果参数是其他任何值，或者没有提供参数，
			# 使用提供的参数执行脚本，然后启动一个新的 Bash shell
			./build.sh $@
			bash
			;;
	esac
fi
~~~

昨天晚上学习了一下，这个BASH_SOURCE实际上是和$0一样的效果，都可以指待脚本名，但如果使用的是source或者.命令，就会发现`$0`已经变成了-bash，这肯定是不对的，所以使用BASH_SOURCE可以避免很多麻烦

## 2.usage

~~~shell
usage()
{
	echo "Usage: $(basename $BASH_SOURCE) [OPTIONS]"
	echo "Available options:"

	run_build_hooks usage

	# Global options
	echo -e "cleanall                          \tcleanup"
	echo -e "post-rootfs <rootfs dir>          \ttrigger post-rootfs hook scripts"
	echo -e "shell                             \tsetup a shell for developing"
	echo -e "help                              \tusage"
	echo ""
	echo "Default option is 'allsave'."
	exit 0
}
~~~

具体运行打印下所示：

![image-20240411104238213](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202404111042262.png)

$BASH_SOURCE 已经转换成了build.sh，这个没有任何问题，然后有个

~~~shell
run_build_hooks usage
~~~

run_build_hooks是一个函数，它的参数为usage，这个函数有点复杂，分析一下：
~~~shell
run_build_hooks()
{
	# 不记录这些钩子的日志
	case "$1" in
		init | pre-build | make-* | usage | support-cmds)
			run_hooks "$RK_BUILD_HOOK_DIR" $@ || true
			return 0
			;;
	esac

	LOG_FILE="$(start_log "$1")"

	echo -e "# run hook: $@\n" >> "$LOG_FILE" # 添加钩子名称到日志文件
	run_hooks "$RK_BUILD_HOOK_DIR" $@ 2>&1 | tee -a "$LOG_FILE" # 运行钩子并将输出写入日志文件
	HOOK_RET=${PIPESTATUS[0]}
	if [ $HOOK_RET -ne 0 ]; then
		err_handler $HOOK_RET "${FUNCNAME[0]} $*" "$@" # 处理错误，并传递相关参数
		exit $HOOK_RET # 钩子执行出错，退出脚本并返回钩子的返回码
	fi
}
~~~

在4-9行有一个case判断，下安装输入的是usage，所以会进入，后面的11-19是不执行的，可以不用理会，所以现在的重点在第六行，又运行了一个函数，这个函数为run_hooks，参数为RK_BUILD_HOOK_DIR变量，这个变量在后面定义的

~~~shell
export RK_BUILD_HOOK_DIR="$COMMON_DIR/build-hooks"
~~~

 具体内容如下所示：

![image-20240411110404714](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202404111104741.png)

run_hooks函数内容如下所示：

~~~shell
run_hooks()
{
	DIR="$1" # 传入的目录路径
	shift

	for dir in "$CHIP_DIR/$(basename "$DIR")/" "$DIR"; do # 遍历两个目录："$CHIP_DIR/传入目录的基本名称/" 和 "$DIR"
		[ -d "$dir" ] || continue # 如果目录不存在，则跳过当前循环

		for hook in $(find "$dir" -maxdepth 1 -name "*.sh" | sort); do # 遍历目录中的以 ".sh" 结尾的脚本文件
			"$hook" $@ && continue # 执行脚本文件，并继续下一次循环
			HOOK_RET=$? # 存储脚本文件的退出状态码
			err_handler $HOOK_RET "${FUNCNAME[0]} $*" "$hook $*" # 调用错误处理函数，传递错误码和相关参数
			exit $HOOK_RET # 退出脚本并返回脚本文件的退出状态码
		done
	done
}
~~~

这个软链接很有用，我现在才算是理解了瑞芯微的意思，瑞芯微的脚本写的确实也还行，我收回之前对瑞芯微的轻视。

![image-20240411110934708](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202404111109737.png)



~~~shell
# 错误处理函数
err_handler()
{
	ret=${1:-$?} # 获取错误码，如果未提供参数，则使用上一个命令的退出状态码
	[ "$ret" -eq 0 ] && return # 如果错误码为零，表示没有错误，直接返回

	echo "ERROR: Running $BASH_SOURCE - ${2:-${FUNCNAME[1]}} failed!" # 输出错误信息，包括脚本文件路径和失败的函数或命令名称
	echo "ERROR: exit code $ret from line ${BASH_LINENO[0]}:" # 输出错误码和导致错误的行号
	echo "    ${3:-$BASH_COMMAND}" # 输出导致错误的命令或函数调用

	echo "ERROR: call stack:" # 输出调用堆栈信息，即函数调用的层次关系
	for i in $(seq 1 $((${#FUNCNAME[@]} - 1))); do # 遍历函数调用堆栈
		SOURCE="${BASH_SOURCE[$i]}" # 获取调用的脚本文件路径
		LINE=${BASH_LINENO[$(( $i - 1 ))]} # 获取调用发生的行号
		echo "    $(basename "$SOURCE"): ${FUNCNAME[$i]}($LINE)" # 输出调用的脚本文件名、函数名称和行号
	done

	exit $ret # 退出脚本，并返回错误码
}
~~~

现在的报错是这样的：

![image-20240411112646979](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202404111126024.png)

其实还是有些东西没有导入进来，将那些导入之后就没问题了，但是我总得知道要导入的是哪个才行吧，这我应该要分析00-config.sh脚本了。

## 3. 00-config.sh

不管是哪个脚本，都要从它的实际执行开始看起，而不是它的那些真正函数，因为有些函数是真的作用不大，而且会阻碍你的判断，所以最靠谱的地方就是从真正的使用出发。	

该脚本的实际执行的内容为：

~~~shell
MAKE="make ${DEBUG:+V=1} -C $(realpath --relative-to="$SDK_DIR" "$COMMON_DIR")"
echo $MAKE
INIT_CMDS="chip defconfig lunch .*_defconfig olddefconfig savedefconfig menuconfig config default"
source "${BUILD_HELPER:-$(dirname "$(realpath "$0")")/../build-hooks/build-helper}"

init_hook $
~~~

第四行语法的意思是：`BUILD_HELPER` 是一个环境变量，用于指定辅助脚本文件的路径。如果该环境变量为空或未设置，那么将使用后面的路径作为默认值，这里会执行一下build-helper，这也是一个脚本，但主要是为了提供一些特定的帮助函数，这个脚本先放放，等我们有需要了再说。但要注意的是，需要指定一个变量，否则不会向下执行，有个报错：
~~~shell
# 检查 DEBUG 变量是否为空。如果非空，则启用调试模式。
[ -z "$DEBUG" ] || set -x

# 确保我们是通过源码方式调用并在 RK 构建脚本内部调用的。
if [ "$BASH_SOURCE" = "$0" -o -z "$RK_SESSION" ]; then
    echo "$(realpath "$0") 不应直接执行"
    exit 1
fi
~~~

所以要添加下面这一个环境变量：
~~~shell
export RK_SESSION="${RK_SESSION:-$(date +%F_%H-%M-%S)}"
~~~

将使用当前日期和时间作为默认值。

这样就执行成功了。

![image-20240411155842190](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202404111558279.png)

但我仍旧不知道这个打印是怎么来的，所以还需要向下分析build-helper，仍旧是看主要的几个内容，要执行的内容如下所示：
~~~shell
cd "$SDK_DIR"

LOG_FILE_NAME="$(basename "${0%.sh}")-$1_$(date +"%F_%H-%M-%S")"

case "$1" in
	help | h | -h | --help | \?) usage ;;
	make-targets) make_targets; exit 0 ;;
	make-usage) make_usage; exit 0 ;;
	usage) usage_hook; exit 0 ;;
	support-cmds)
		shift
		{
			ALL_CMDS="$INIT_CMDS $PRE_BUILD_CMDS $BUILD_CMDS \
				$POST_BUILD_CMDS"
			for stage in ${@:-all}; do
				case $stage in
					init) echo "$INIT_CMDS" ;;
					pre-build) echo "$PRE_BUILD_CMDS" ;;
					build) echo "$BUILD_CMDS" ;;
					post-build) echo "$POST_BUILD_CMDS" ;;
					all) echo "$ALL_CMDS" ;;
				esac
			done
		} | xargs -n 1 | grep -v "^default$" | xargs || true
		exit 0
		;;
	clean)
		try_func clean_hook
		exit 0
		;;
	init)
		shift
		try_hook init_hook "$INIT_CMDS" $@
		exit 0
		;;
	pre-build)
		shift
		try_hook pre_build_hook "$PRE_BUILD_CMDS" $@
		exit 0
		;;
	build)
		shift
		try_hook build_hook "$BUILD_CMDS" $@
		exit 0
		;;
	post-build)
		shift
		try_hook post_build_hook "$POST_BUILD_CMDS" $@
		exit 0
		;;
esac

~~~

有了上面这些选择，其他就没了，build-helper 先分析到这里，等等，还有一个

~~~shell
export DEVICE_DIR="$SDK_DIR/device/rockchip" # 瑞芯微脚本和配置文件存放总目录
export CHIP_DIR="$DEVICE_DIR/.chip" # 存放分区文件、常用的配置文件
~~~

这两个定义之后，这里的打印也就正常了。

~~~shell
usage_hook()
{
	echo -e "chip[:<chip>[:<config>]]          \tchoose chip"
	echo -e "defconfig[:<config>]              \tchoose defconfig"
	echo -e " *_defconfig                      \tswitch to specified defconfig"
	echo "    available defconfigs:"
	echo "$(ls "$CHIP_DIR/" | grep "defconfig$" | sed "s/^/\t/")"
	echo -e " olddefconfig                     \tresolve any unresolved symbols in .config"
	echo -e " savedefconfig                    \tsave current config to defconfig"
	echo -e " menuconfig                       \tinteractive curses-based configurator"
	echo -e "config                            \tmodify SDK defconfig"
}
~~~

最终的显示效果如下所示：
![image-20240411165321429](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202404111653488.png)

> chip[:<chip>[:<config>]]       choose chip
>
> defconfig[:<config>]         choose defconfig
>
>  *_defconfig             switch to specified defconfig
>
>   available defconfigs:
>
>   rockchip_defconfig
>
>   rockchip_rk3562_dictpen_test3_v20_defconfig
>
>   rockchip_rk3562_evb1_lp4x_v10_defconfig
>
>   rockchip_rk3562_evb2_ddr4_v10_defconfig
>
>   rockchip_rk3562_robot_evb1_lp4x_v10_defconfig
>
>   rockchip_rk3562_robot_evb2_ddr4_v10_defconfig
>
>  olddefconfig            resolve any unresolved symbols in .config
>
>  savedefconfig            save current config to defconfig
>
>  menuconfig             interactive curses-based configurator
>
> config  

上面的这些我感觉可以学习一下，确实有点用

这样就会跳回到00-config.sh脚本，运行最后一条指令

~~~shell
init_hook()
{
	case "${1:-default}" in
		chip) shift; choose_chip $@ ;;
		lunch|defconfig) shift; choose_defconfig $@ ;;
		*_defconfig) switch_defconfig "$1" ;;
		olddefconfig | savedefconfig | menuconfig) $MAKE $1 ;;
		config)
			$MAKE menuconfig
			$MAKE savedefconfig
			;;
		default) prepare_config ;; # End of init
		*) usage ;;
	esac
}
~~~

说有用也有用，说没用也没用，我肯定是给他改掉的先。

## 4. 简单的函数1

~~~shell

# 将变量自动导出为环境变量
set -a

# 编译完成打印函数
finish_build()
{
	echo -e "\e[35mRunning $(basename "${BASH_SOURCE[1]}") - ${@:-${FUNCNAME[1]}} succeeded.\e[0m"
	cd "$SDK_DIR"
}

# 导入config配置函数
load_config()
{
	[ -r "$RK_CONFIG" ] || return 0

	for var in $@; do
		export $(grep "^$var=" "$RK_CONFIG" | \
			tr -d '"' || true) &>/dev/null
	done
}

# 检测config配置函数
check_config()
{
	unset missing
	for var in $@; do
		eval [ \$$var ] && continue

		missing="$missing $var"
	done

	[ -z "$missing" ] && return 0

	echo "Skipping $(basename "${BASH_SOURCE[1]}") - ${FUNCNAME[1]} for missing configs: $missing."
	return 1
}


kernel_version_real()
{
	[ -d kernel ] || return 0

	VERSION_KEYS="VERSION PATCHLEVEL"
	VERSION=""

	for k in $VERSION_KEYS; do
		v=$(grep "^$k = " kernel/Makefile | cut -d' ' -f3)
		VERSION=${VERSION:+${VERSION}.}$v
	done
	echo $VERSION
}

# 获取内核版本，我肯定不需要这个函数
kernel_version()
{
	[ -d kernel ] || return 0

	KERNEL_DIR="$(basename "$(realpath kernel)")"
	case "$KERNEL_DIR" in
		kernel-*)
			echo ${KERNEL_DIR#kernel-}
			return 0
			;;
	esac

	kernel_version_real
}

# 打印log的文件，这个可以留下
start_log()
{
	LOG_FILE="$RK_LOG_DIR/${2:-$1_$(date +%F_%H-%M-%S)}.log"
	ln -rsf "$LOG_FILE" "$RK_LOG_DIR/$1.log"
	echo "# $(date +"%F %T")" >> "$LOG_FILE"
	echo "$LOG_FILE"
}

# 返回源码根目录
rroot()
{
	cd "$SDK_DIR"
}

# 返回源码output目录
rout()
{
	cd "$RK_OUTDIR"
}

# 返回源码 common目录
rcommon()
{
	cd "$COMMON_DIR"
}

# 返回源码脚本存放目录
rscript()
{
	cd "$SCRIPTS_DIR"
}

# 返回源码板级配置文件目录
rchip()
{
	cd "$(realpath "$CHIP_DIR")"
}

~~~

## 5.钩子函数

~~~shell
# 钩子脚本运行函数
run_hooks()
{
	DIR="$1" # 传入的目录路径
	shift

	for dir in "$CHIP_DIR/$(basename "$DIR")/" "$DIR"; do # 遍历两个目录："$CHIP_DIR/传入目录的基本名称/" 和 "$DIR"
		[ -d "$dir" ] || continue # 如果目录不存在，则跳过当前循环

		for hook in $(find "$dir" -maxdepth 1 -name "*.sh" | sort); do # 遍历目录中的以 ".sh" 结尾的脚本文件
			"$hook" $@ && continue # 执行脚本文件，并继续下一次循环
			HOOK_RET=$? # 存储脚本文件的退出状态码
			err_handler $HOOK_RET "${FUNCNAME[0]} $*" "$hook $*" # 调用错误处理函数，传递错误码和相关参数
			exit $HOOK_RET # 退出脚本并返回脚本文件的退出状态码
		done
	done
}
~~~



~~~shell
# 编译钩子运行函数
run_build_hooks()
{
	case "$1" in
		init | pre-build | make-* | usage | support-cmds)
			run_hooks "$RK_BUILD_HOOK_DIR" $@ || true
			return 0
			;;
	esac

	LOG_FILE="$(start_log "$1")"

	echo -e "# run hook: $@\n" >> "$LOG_FILE" # 添加钩子名称到日志文件
	run_hooks "$RK_BUILD_HOOK_DIR" $@ 2>&1 | tee -a "$LOG_FILE" # 运行钩子并将输出写入日志文件
	HOOK_RET=${PIPESTATUS[0]}
	if [ $HOOK_RET -ne 0 ]; then
		err_handler $HOOK_RET "${FUNCNAME[0]} $*" "$@" # 处理错误，并传递相关参数
		exit $HOOK_RET # 钩子执行出错，退出脚本并返回钩子的返回码
	fi
}

~~~



~~~shell
# 事件发生之后的钩子
run_post_hooks()
{
	LOG_FILE="$(start_log post-rootfs)"  # 启动日志记录

	echo -e "# run hook: $@\n" >> "$LOG_FILE"  # 在日志文件中记录正在运行的钩子
	run_hooks "$RK_POST_HOOK_DIR" $@ 2>&1 | tee -a "$LOG_FILE"  # 运行 post 钩子脚本并将输出同时追加到日志文件中
	HOOK_RET=${PIPESTATUS[0]}  # 获取钩子脚本的返回码

	if [ $HOOK_RET -ne 0 ]; then  # 如果钩子脚本返回非零值
		err_handler $HOOK_RET "${FUNCNAME[0]} $*" "$@"  # 调用错误处理函数，并传递错误码和相关参数
		exit $HOOK_RET  # 退出脚本，并返回钩子脚本的返回码
	fi
}
~~~



## 6.简单函数2

~~~shell
# 参数检测函数
option_check()
{
	CMDS="$1"  # 接收命令列表作为参数
	shift

	for opt in $@; do  # 迭代处理传入的选项参数
		for cmd in $CMDS; do  # 迭代处理命令列表
			# 注意：命令可能包含通配符
			echo "${opt%%:*}" | grep -q "^$cmd$" || continue  # 使用正则表达式匹配检查选项是否匹配命令
			return 0  # 如果选项匹配命令，则返回 0 表示匹配成功
		done
	done

	return 1  # 如果没有匹配的选项和命令，则返回 1 表示匹配失败
}
~~~

- `${opt%%:*}` 删除 `opt` 变量值中冒号及其后面的部分，得到一个处理后的字符串。
- `grep -q "^$cmd$"` 使用正则表达式 `^$cmd$` 进行匹配，尝试在处理后的字符串中查找完全匹配的内容。
- 如果匹配成功（即 `grep` 命令返回退出状态为 0），则表达式返回真（非零），`continue` 语句会跳过当前迭代，继续下一次迭代。
- 如果匹配失败（即 `grep` 命令返回退出状态为非零），则表达式返回假（零），`continue` 语句不会执行，继续执行接下来的代码。



~~~shell
# 编译器设置函数
get_toolchain()
{
	TOOLCHAIN_ARCH="${1/arm64/aarch64}"  # 将参数中的 'arm64' 替换为 'aarch64'，并赋值给 TOOLCHAIN_ARCH 变量

	MACHINE=$(uname -m)  # 获取当前机器的架构信息
	if [ "$MACHINE" = x86_64 ]; then  # 如果当前架构是 x86_64
		# RV1126 使用自定义工具链
		if [ "$RK_CHIP_FAMILY" = "rv1126_rv1109" ]; then  # 如果 RK_CHIP_FAMILY 变量等于 "rv1126_rv1109"
			TOOLCHAIN_OS=rockchip  # 设置 TOOLCHAIN_OS 变量为 rockchip
		else
			TOOLCHAIN_OS=none  # 否则设置 TOOLCHAIN_OS 变量为 none
		fi

		TOOLCHAIN_DIR="$(realpath prebuilts/gcc/*/$TOOLCHAIN_ARCH)"  # 根据 TOOLCHAIN_ARCH 变量的值构建 TOOLCHAIN_DIR 变量的路径
		GCC="$(find "$TOOLCHAIN_DIR" -name "*$TOOLCHAIN_OS*-gcc" | \
			head -n 1)"  # 在 TOOLCHAIN_DIR 目录下查找以 "$TOOLCHAIN_OS-gcc" 结尾的文件，并取第一个结果，赋值给 GCC 变量
		if [ ! -x "$GCC" ]; then  # 如果 GCC 变量不是可执行文件
			echo "No prebuilt GCC toolchain!"  # 输出错误信息
			exit 1  # 退出脚本，返回状态码 1
		fi
	elif [ "$TOLLCHAIN_ARCH" = aarch64 -a "$MACHINE" != aarch64 ]; then  # 如果 TOOLCHAIN_ARCH 变量为 aarch64 且 MACHINE 变量不为 aarch64
		GCC=aarch64-linux-gnu-gcc  # 设置 GCC 变量为 aarch64-linux-gnu-gcc
	elif [ "$TOLLCHAIN_ARCH" = arm -a "$MACHINE" != armv7l ]; then  # 如果 TOOLCHAIN_ARCH 变量为 arm 且 MACHINE 变量不为 armv7l
		GCC=arm-linux-gnueabihf-gcc  # 设置 GCC 变量为 arm-linux-gnueabihf-gcc
	else
		GCC=gcc  # 否则设置 GCC 变量为 gcc
	fi

	echo "${GCC%gcc}"  # 输出 GCC 变量的值，并删除结尾的 'gcc' 部分
}
~~~

华丽花哨，我现在其实就只有一个板子，所以也只有一个编译器

## 7.main函数

### 第一部分

~~~shell
	[ -z "$DEBUG" ] || set -x
	# 在发生错误时调用名为 err_handler 的函数来处理错误
	trap 'err_handler' ERR
	# 启用错误处理机制
	set -eE

	# 保存初始环境
	INITIAL_ENV=$(mktemp -u)
	if [ -z "$RK_SESSION" ]; then
		env > "$INITIAL_ENV"
	fi
	
	export LC_ALL=C # 设置本地化环境为C
	
	export SCRIPTS_DIR="$(dirname "$(realpath "$BASH_SOURCE")")" # build.sh脚本路径
	export COMMON_DIR="$(realpath "$SCRIPTS_DIR/..")" # common目录路径
	export SDK_DIR="$(realpath "$COMMON_DIR/../../..")" # SDK源码根目录路径
	export DEVICE_DIR="$SDK_DIR/device/rockchip" # 脚本和板级别配置文件路径
	export CHIPS_DIR="$DEVICE_DIR/.chips"  # .chips路径,里面其实也只有一个rk3562
	export CHIP_DIR="$DEVICE_DIR/.chip" # .chip路径也就是rk3562

	export RK_DATA_DIR="$COMMON_DIR/data" # 存放了一些调试工具和开发板可执行脚本
	export RK_IMAGE_DIR="$COMMON_DIR/images" # 存放了ome userdata PCBA等镜像或者分区文件
	export RK_CONFIG_IN="$COMMON_DIR/configs/Config.in" # 存放了一些配置文件，推测根目录的menuconfig就是来自这里

	export RK_BUILD_HOOK_DIR="$COMMON_DIR/build-hooks" # 存放编译钩子脚本的目录
	export BUILD_HELPER="$RK_BUILD_HOOK_DIR/build-helper" # 编译时钩子的帮助函数
	export RK_POST_HOOK_DIR="$COMMON_DIR/post-hooks" # 存放编译完成后的钩子脚本目录
	export POST_HELPER="$RK_POST_HOOK_DIR/post-helper" # 编译完成后的钩子帮助函数

	export PARTITION_HELPER="$SCRIPTS_DIR/partition-helper" # 文件分区函数

	export RK_OUTDIR="$SDK_DIR/output" # 文件输出保存目录
	export RK_LOG_BASE_DIR="$RK_OUTDIR/log"	#log日志保存总目录
	export RK_SESSION="${RK_SESSION:-$(date +%F_%H-%M-%S)}" #日志时间定义
	export RK_LOG_DIR="$RK_LOG_BASE_DIR/$RK_SESSION" # 根据时间保存的日志目录
	export RK_FIRMWARE_DIR="$RK_OUTDIR/firmware" # 固件存放目录
	export RK_INITIAL_ENV="$RK_OUTDIR/initial.env" # 保存的最初环境
	export RK_CUSTOM_ENV="$RK_OUTDIR/custom.env" 
	export RK_FINAL_ENV="$RK_OUTDIR/final.env"	#最终的环境变量
	export RK_CONFIG="$RK_OUTDIR/.config" # 保存的Menuconfig配置
	export RK_DEFCONFIG_LINK="$RK_OUTDIR/defconfig"  # 默认配置
~~~

### 第二部分

~~~shell
# 如果命令行参数为 "make-targets" 或 "make-usage"
# 执行 run_build_hooks 函数并退出脚本

case "$@" in
	make-targets | make-usage)
		run_build_hooks "$@"
		exit 0 ;;
esac

# 日志文件设置
# 如果 $RK_LOG_DIR 目录不存在创建目录 $RK_LOG_DIR
# 删除 $RK_LOG_BASE_DIR/latest 的符号链接，然后创建 $RK_LOG_DIR 的符号链接到 $RK_LOG_BASE_DIR/latest
# 打印日志保存的路径信息
if [ ! -d "$RK_LOG_DIR" ]; then
	mkdir -p "$RK_LOG_DIR"
	rm -rf "$RK_LOG_BASE_DIR/latest"
	ln -rsf "$RK_LOG_DIR" "$RK_LOG_BASE_DIR/latest"
	echo -e "\e[33mLog saved at $RK_LOG_DIR\e[0m"
	echo
fi

# 删除 $RK_LOG_BASE_DIR 目录下按时间排序的前 10 个文件或目录
cd "$RK_LOG_BASE_DIR"
rm -rf $(ls -t | sed '1,10d')

# 创建目录 $RK_FIRMWARE_DIR
# 删除 $SDK_DIR/rockdev 目录
# 创建 $RK_FIRMWARE_DIR 的符号链接到 $SDK_DIR/rockdev    原来根目录的rockdev 是output目录下的fimeware，软链接
mkdir -p "$RK_FIRMWARE_DIR"
rm -rf "$SDK_DIR/rockdev"
ln -rsf "$RK_FIRMWARE_DIR" "$SDK_DIR/rockdev"

# 进入 $SDK_DIR 目录
# 如果不存在 README.md 文件，则创建 README.md 的符号链接到 $COMMON_DIR/README.md
cd "$SDK_DIR"
[ -f README.md ] || ln -rsf "$COMMON_DIR/README.md" .

# 删除 envsetup.sh 文件
rm -f envsetup.sh

~~~

​	make-targets | make-usage 这两个选项的作用还不知道，经过实验就是打印目前实现的功能列表

### 第三部分

~~~shell
# 将命令行参数赋值给变量 OPTIONS，如果没有提供命令行参数，则默认为 "allsave"
OPTIONS="${@:-allsave}"


# 获取支持的命令列表，并存储到变量 CMDS 中
CMDS="$(run_build_hooks support-cmds all | xargs)"

for opt in $OPTIONS; do
	case "$opt" in
		help | h | -h | --help | usage | \?) # 如果选项为 help、h、-h、--help、usage 或 ?，则显示使用说明并退出
			usage
			;;
		shell | cleanall)
			# 如果选项为 shell 或 cleanall，并且它是唯一的选项（没有其他选项），则跳出循环
			# 否则，显示错误消息，说明该选项不能与其他选项组合使用
			if [ "$opt" = "$OPTIONS" ]; then
				break
			fi
			echo "ERROR: $opt cannot combine with other options!"
			;;
		post-rootfs)
		# 如果选项为 post-rootfs，并且它是第一个选项，并且后面跟着一个 rootfs 目录，则隐藏其他参数并跳出循环
		# 否则，显示错误消息，说明 post-rootfs 应该是第一个选项，后面跟着 rootfs 目录
			if [ "$opt" = "$1" -a -d "$2" ]; then
				OPTIONS=$opt
				break
			fi
			echo "ERROR: $opt should be the first option followed by rootfs dir!"
			
			;;
		*)# 对于其他选项，确保所有选项都被处理了，如果没有处理，则显示错误消息，说明该选项未被处理
			if option_check "$CMDS" $opt; then
				continue
			fi
			echo "ERROR: Unhandled option: $opt"
			
			;;
	esac

	usage
	# 显示使用说明
done
~~~

### 第4部分

~~~shell
# 运行 init 钩子函数，并传递选项参数
run_build_hooks init $OPTIONS

# 删除 $RK_OUTDIR 目录下的 .tmpconfig* 文件
rm -f "$RK_OUTDIR/.tmpconfig*"

# 获取支持的命令列表，并存储到变量 CMDS 中，包括 pre-build、build、post-build 钩子函数返回的命令列表
# 还包括 shell、cleanall、post-rootfs 命令
CMDS="$(run_build_hooks support-cmds pre-build build \
	post-build | xargs) shell cleanall post-rootfs"

# 检查选项是否在支持的命令列表中，如果不在列表中，则返回 0，终止脚本执行
option_check "$CMDS" $OPTIONS || return 0


# 强制导出配置环境变量
set -a

# 加载配置环境变量文件 $RK_CONFIG
source "$RK_CONFIG"

# 复制 $RK_CONFIG 文件到 $RK_LOG_DIR 目录
cp "$RK_CONFIG" "$RK_LOG_DIR"

# 保存init环境变量
if [ -e "$INITIAL_ENV" ]; then	# 如果文件 $INITIAL_ENV 存在
	# 将文件 $INITIAL_ENV 的内容复制到文件 $RK_INITIAL_ENV
	cat "$INITIAL_ENV" > "$RK_INITIAL_ENV"
	
	# 删除文件 $RK_CUSTOM_ENV
	rm -f "$RK_CUSTOM_ENV"

	# 查找自定义环境变量
	for cfg in $(grep "^RK_" "$RK_INITIAL_ENV" || true); do
		# 在文件 $RK_INITIAL_ENV 中查找以 "RK_" 开头的行，并将结果存储到变量 cfg 中
		env | grep -q "^${cfg//\"/}$" || \
			echo "$cfg" >> "$RK_CUSTOM_ENV"
		# 检查环境变量中是否存在与 cfg 值相同的变量名，如果不存在，则将 cfg 写入文件 $RK_CUSTOM_ENV
	done

	# 允许自定义环境变量覆盖
	if [ -e "$RK_CUSTOM_ENV" ]; then
		# 如果文件 $RK_CUSTOM_ENV 存在

		echo -e "\e[31mWARN: Found custom environments: \e[0m"
		# 显示警告消息，指示发现自定义环境变量
		cat "$RK_CUSTOM_ENV"
		# 显示文件 $RK_CUSTOM_ENV 的内容

		echo -e "\e[31mAssuming that is expected, please clear them if otherwise.\e[0m"
		# 显示提示消息，告知用户如果不需要自定义环境变量，请清除它们
		read -t 10 -p "Press enter to continue."
		# 等待用户按下回车键继续执行脚本

		source "$RK_CUSTOM_ENV"
		# 加载文件 $RK_CUSTOM_ENV 中定义的环境变量
		cp "$RK_CUSTOM_ENV" "$RK_LOG_DIR"
		# 复制文件 $RK_CUSTOM_ENV 到目录 $RK_LOG_DIR

		if grep -q "^RK_KERNEL_VERSION=" "$RK_CUSTOM_ENV"; then
			# 如果文件 $RK_CUSTOM_ENV 中存在以 "RK_KERNEL_VERSION=" 开头的行

			echo -e "\e[31mCustom RK_KERNEL_VERSION ignored!\e[0m"
			# 显示警告消息，指示自定义的 RK_KERNEL_VERSION 被忽略
			load_config RK_KERNEL_VERSION
			# 载入配置变量 RK_KERNEL_VERSION 的值
		fi

		if grep -q "^RK_ROOTFS_SYSTEM=" "$RK_CUSTOM_ENV"; then
			# 如果文件 $RK_CUSTOM_ENV 中存在以 "RK_ROOTFS_SYSTEM=" 开头的行

			echo -e "\e[31mCustom RK_ROOTFS_SYSTEM ignored!\e[0m"
			# 显示警告消息，指示自定义的 RK_ROOTFS_SYSTEM 被忽略
			load_config RK_ROOTFS_SYSTEM
			# 载入配置变量 RK_ROOTFS_SYSTEM 的值
		fi
	fi
fi
~~~



### 第5部分

~~~shell
# 导入分区帮助脚本
source "$PARTITION_HELPER"

# 运行分区初始化函数
rk_partition_init

# 停止强制导出环境变量
set +a

# 导出环境变量 PYTHON3，指定为 /usr/bin/python3
export PYTHON3=/usr/bin/python3

# 如果变量 RK_KERNEL_CFG 存在
if [ "$RK_KERNEL_CFG" ]; then

	# 导出环境变量 RK_KERNEL_TOOLCHAIN，设置为根据 RK_KERNEL_ARCH 获取的工具链
	export RK_KERNEL_TOOLCHAIN="$(get_toolchain "$RK_KERNEL_ARCH")"
	
	# 显示内核的工具链，如果未设置则显示默认值 gcc
	echo "Toolchain for kernel:"
	echo "${RK_KERNEL_TOOLCHAIN:-gcc}"
	
	# 获取可用的 CPU 核心数
	CPUS=$(getconf _NPROCESSORS_ONLN 2>/dev/null || echo 1)
	
	# 导出环境变量 KMAKE，设置为用于编译内核的 make 命令及其参数
	export KMAKE="make -C kernel/ -j$(( $CPUS + 1 )) \
		CROSS_COMPILE=$RK_KERNEL_TOOLCHAIN ARCH=$RK_KERNEL_ARCH"
	
	# 导出环境变量 RK_KERNEL_VERSION_REAL，设置为实际内核版本
	export RK_KERNEL_VERSION_REAL=$(kernel_version_real)
fi

# 如果变量 RK_UBOOT_CFG 存在
if [ "$RK_UBOOT_CFG" ]; then

	# 导出环境变量 RK_UBOOT_TOOLCHAIN，设置为根据 RK_UBOOT_ARCH 获取的工具链
	export RK_UBOOT_TOOLCHAIN="$(get_toolchain "$RK_UBOOT_ARCH")"
	
	# 显示引导加载程序（u-boot）的工具链，如果未设置则显示默认值 gcc
	echo "Toolchain for loader (u-boot):"
	echo "${RK_UBOOT_TOOLCHAIN:-gcc}"
fi

# 处理特殊命令
case "$OPTIONS" in
	shell)
		# 显示警告消息，指示该操作仅用于开发，具有一定的危险性
		# 开发 Shell 中没有错误处理。
		echo -e "\e[35mDoing this is dangerous and for developing only.\e[0m"
		
		# 停止设置错误检测和错误处理
		set +e; trap ERR
		
		# 进入交互式 Shell
		/bin/bash
		
		# 显示消息，指示退出 Shell
		echo -e "\e[35mExit from $BASH_SOURCE shell.\e[0m"
		exit 0 ;;
	cleanall)
		# 运行 clean 钩子函数
		run_build_hooks clean
		
		# 删除目录 $RK_OUTDIR
		rm -rf "$RK_OUTDIR"

		# 完成构建，清理所有内容
		finish_build cleanall
		exit 0 ;;
	post-rootfs)
		# 移除第一个参数（命令本身），将后续参数向前移动
		shift
		
		# 运行 post-rootfs 钩子函数，并传递参数
		run_post_hooks $@
		
		# 完成构建的 post-rootfs 阶段
		finish_build post-rootfs
		exit 0 ;;
esac

# 保存最终的环境变量，将当前环境变量保存到文件 $RK_FINAL_ENV
env > "$RK_FINAL_ENV"

# 复制文件 $RK_FINAL_ENV 到目录 $RK_LOG_DIR
cp "$RK_FINAL_ENV" "$RK_LOG_DIR"

~~~



### 第6部分

~~~shell
# 日志记录配置信息
echo
echo "=========================================="
echo "          Final configs"
echo "=========================================="
# 显示以 "RK_" 开头的配置变量，排除以 "PARTITION_[0-9]" 开头的变量，
# 排除值为空或默认为 "y" 的变量，排除以 "RK_CONFIG"、"_BASE_CFG"、"_LINK"、"DIR"、"_ENV"、"_NAME" 开头的变量，并按字母顺序排序
env | grep -E "^RK_.*=.+" | grep -vE "PARTITION_[0-9]" | \
	grep -vE "=\"\"$|_DEFAULT=y" | \
	grep -vE "^RK_CONFIG|_BASE_CFG=|_LINK=|DIR=|_ENV=|_NAME=" | sort
echo

# 预构建阶段（子模块配置等）
# 运行 pre-build 钩子函数，并传递选项参数
run_build_hooks pre-build $OPTIONS

# 运行 support-cmds、build 和 post-build 钩子函数，并将命令结果存储在变量 CMDS 中，
CMDS="$(run_build_hooks support-cmds build post-build | xargs)"

# 检查选项参数是否在 CMDS 中存在，如果不存在则不需要继续执行后续步骤，直接返回
option_check "$CMDS" $OPTIONS || return 0

# 运行 build 钩子函数，并传递选项参数
run_build_hooks build $OPTIONS

# 运行 support-cmds 和 post-build 钩子函数，并将命令结果存储在变量 CMDS 中，
CMDS="$(run_build_hooks support-cmds post-build | xargs)"

# 检查选项参数是否在 CMDS 中存在，如果不存在则不需要继续执行后续步骤，直接返回
option_check "$CMDS" $OPTIONS || return 0

# 运行 post-build 钩子函数，并传递选项参数
run_build_hooks post-build $OPTIONS
~~~

## 8.build.sh 实际运行

~~~shell

if [ "$0" != "$BASH_SOURCE" ]; then
	# 如果当前脚本是通过 `source` 命令被引用执行的
	# 直接执行脚本本身
	"$BASH_SOURCE" ${@:-shell} # 使用当前脚本路径作为命令执行，传递参数 ${@:-shell}
elif [ "$0" == "$BASH_SOURCE" ]; then
	# 如果当前脚本是直接执行的
	# 执行主函数 main，并传递所有参数
	main $@
fi
~~~









~~~shell
sudo apt-get install -y --no-install-recommends whiptail dialog psmisc acl uuid uuid-runtime curl gpg gnupg gawk git acl aptly aria2 bc binfmt-support bison btrfs-progs build-essential ca-certificates ccache cpio cryptsetup curl debian-archive-keyring debian-keyring debootstrap device-tree-compiler dialog dirmngr dosfstools dwarves f2fs-tools fakeroot flex gawk gcc-arm-linux-gnueabihf gdisk gpg imagemagick jq kmod libbison-dev libc6-dev-armhf-cross libelf-dev libfdt-dev libfile-fcntllock-perl libfl-dev liblz4-tool libncurses-dev  libssl-dev libusb-1.0-0-dev linux-base locales lzop ncurses-base ncurses-term nfs-kernel-server ntpdate p7zip-full parted patchutils pigz pixz pkg-config pv python3-dev  qemu-user-static rsync swig systemd-container u-boot-tools udev unzip uuid-dev wget whiptail zip zlib1g-dev distcc lib32ncurses-dev lib32stdc++6 libc6-i386 python3 expect expect-dev cmake vim openssh-server net-tools
~~~

