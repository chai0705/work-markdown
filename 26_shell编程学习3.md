## 案例1：inpath

~~~shell
#!/bin/sh
# inpath - 验证指定的程序是否有效或者是否存在于PATH目录列表中。

in_path()
{
  # 给定一个命令和PATH路径，尝试查找该命令。如果找到并且可执行，返回0；否则返回1。
  # 需要注意的是，这个函数会临时修改IFS（输入字段分隔符），但在完成后会恢复原值。

  cmd=$1        # 命令
  path=$2       # PATH路径
  retval=1      # 返回值，默认为1
  oldIFS=$IFS   # 保存旧的IFS值
  IFS=":"       # 设置IFS为冒号，用于分隔路径列表

  for directory in $path
  do
    if [ -x $directory/$cmd ] ; then
      retval=0      # 如果找到了$cmd在$directory中，将返回值设为0
    fi
  done
  IFS=$oldIFS     # 恢复IFS为旧值
  return $retval  # 返回结果
}

checkForCmdInPath()
{
  var=$1

  # 下面的条件语句中的变量切片表示法需要一些解释：
  # ${var#expr} 返回变量值中匹配'expr'之后的内容（如果有），而
  # ${var%expr} 返回变量值中不匹配的部分（在本例中只有第一个字符）。
  # 在Bash中也可以使用${var:0:1}来实现，还可以使用cut命令：cut -c1

  if [ "$var" != "" ] ; then
    if [ "${var%${var#?}}" = "/" ] ; then
      if [ ! -x $var ] ; then
        return 1  # 如果$var不是空字符串且以'/'开头，且不可执行，则返回1
      fi
    elif ! in_path $var $PATH ; then
      return 2  # 如果$var不是空字符串且不在PATH中，则返回2
    fi 
  fi
}

if [ $# -ne 1 ] ; then  # 检查脚本的参数个数是否为1，如果不是，则输出错误消息并退出脚本。
 echo "Usage: $0 command" >&2 ; exit 1
fi

checkForCmdInPath "$1"
case $? in
  0 ) echo "$1 在PATH中找到"			;;
  1 ) echo "$1 未找到或不可执行"	;;
  2 ) echo "$1 未在PATH中找到"		;;
esac

exit 0
~~~



## 案例2：validAlphaNum

~~~shell
#!/bin/sh

# validAlphaNum - 确保输入只包含字母和数字字符。
validAlphaNum()
{
  # 验证参数，如果参数中包含除大写字母、小写字母和数字以外的字符，返回1，否则返回0。
  # 删除所有不可接受的字符。
  compressed="$(echo $1 | sed -e 's/[^[:alnum:]]//g')"

  if [ "$compressed" != "$input" ] ; then
    return 1  # 如果压缩后的字符串与原始输入不相等，则返回1。
  else
    return 0  # 如果压缩后的字符串与原始输入相等，则返回0。
  fi
}

# 脚本示例中validAlphaNum函数的使用
echo -n "请输入输入内容: "
read input

if ! validAlphaNum "$input" ; then
  echo "您的输入必须只包含字母和数字。" >&2
  exit 1  # 如果输入不符合要求，输出错误消息并退出脚本。
else
  echo "输入有效。"  # 如果输入符合要求，输出验证通过的消息。
fi

exit 0
~~~



## 案例3：normdate 

~~~shell
#!/bin/sh
# normdate - 将日期中的月份字段规范化为首字母大写的三个字母缩写。
# 这是hack #7，validdate的一个辅助函数。如果没有错误，退出状态为零。

monthnoToName()
{
  # 将变量'month'设置为适当的值
  case $1 in
    1 ) month="Jan"    ;;  2 ) month="Feb"    ;;
    3 ) month="Mar"    ;;  4 ) month="Apr"    ;;
    5 ) month="May"    ;;  6 ) month="Jun"    ;;
    7 ) month="Jul"    ;;  8 ) month="Aug"    ;;
    9 ) month="Sep"    ;;  10) month="Oct"    ;;
    11) month="Nov"    ;;  12) month="Dec"    ;;
    * ) echo "$0: 未知的数字月份值 $1" >&2; exit 1
   esac
   return 0
}

## 开始主脚本

if [ $# -eq 1 ] ; then  # 尝试处理/或-格式的输入
  set -- $(echo $1 | sed 's/[\/\-]/ /g')
fi

if [ $# -ne 3 ] ; then
  echo "用法: $0 月份 日 年份" >&2
  echo "常见的输入格式为 August 3 1962 和 8 3 2002" >&2
  exit 1
fi

if [ $3 -lt 1000 ] ; then
  echo "$0: 预期四位数的年份值。" >&2; exit 1
fi

if [ -z $(echo $1|sed 's/[[:digit:]]//g') ]; then
  monthnoToName $1
else
  # 规范化为首字母大写的三个字母缩写
  month="$(echo $1|cut -c1|tr '[:lower:]' '[:upper:]')"
  month="$month$(echo $1|cut -c2-3 | tr '[:upper:]' '[:lower:]')"
fi

echo $month $2 $3

exit 0
~~~



## 案例4：nicenumber

~~~shell
#!/bin/sh

# nicenumber - 给定一个数字，以逗号分隔的形式显示它
#    期望 DD 和 TD 已经被赋值。instantiates nicenum
#    或者，如果指定了第二个参数，则将输出回显到标准输出

nicenumber()
{
  # 注意，我们在解析传递给脚本的 INPUT 值时，使用 '.' 作为小数分隔符。
  # 输出值由用户使用 -d 标志指定，如果与 '.' 不同的话。

  integer=$(echo $1 | cut -d. -f1)   # 小数点左边的部分
  decimal=$(echo $1 | cut -d. -f2)   # 小数点右边的部分

  if [ $decimal != $1 ]; then
    # 存在小数部分，我们将其包含进来。
    result="${DD:="."}$decimal"
  fi

  thousands=$integer

  while [ $thousands -gt 999 ]; do
    remainder=$(($thousands % 1000))  # 最低的三位数

    while [ ${#remainder} -lt 3 ] ; do  # 根据需要强制添加前导零
      remainder="0$remainder"
    done

    thousands=$(($thousands / 1000))  # 左边的部分，如果有余数的话
    result="${TD:=","}${remainder}${result}"  # 从右向左构建
  done

  nicenum="${thousands}${result}"
  if [ ! -z $2 ] ; then
    echo $nicenum
  fi
}

DD="."  # 小数点分隔符，分隔整数和小数部分
TD=","  # 千位分隔符，每三位数分隔一次

while getopts "d:t:" opt; do
  case $opt in
    d ) DD="$OPTARG"  ;;
    t ) TD="$OPTARG"  ;;
  esac
done

shift $(($OPTIND - 1))

if [ $# -eq 0 ] ; then
  cat << "EOF" >&2
用法: $(basename $0) [-d c] [-t c] 数值
       -d 指定小数点分隔符 (默认为 '.')
       -t 指定千位分隔符 (默认为 ',')
EOF
  exit 1
fi

nicenumber $1 1    # 第二个参数强制将输出作为 'echo'

exit 0
~~~



## 案例5：validint

~~~shell
#!/bin/sh
# validint - 验证整数输入，允许负整数

validint()
{
  # 验证第一个字段。可选择针对最小值 $2 和/或最大值 $3 进行测试：
  # 如果你想跳过这些测试，请将值设为空字符串。
  # 返回 1 表示错误，返回 0 表示成功。

  number="$1";    min="$2";    max="$3"

  if [ -z $number ] ; then
    echo "你没有输入任何内容。不可接受。" >&2 ; return 1
  fi

  if [ "${number%${number#?}}" = "-" ] ; then  # 第一个字符为 '-' ？
    testvalue="${number#?}"  # 除了第一个字符的所有字符
  else
    testvalue="$number"
  fi

  nodigits="$(echo $testvalue | sed 's/[[:digit:]]//g')"

  if [ ! -z $nodigits ] ; then
    echo "无效的数字格式！只允许数字，不能包含逗号、空格等。" >&2
    return 1
  fi

  if [ ! -z $min ] ; then
    if [ "$number" -lt "$min" ] ; then
       echo "你的值太小了：最小可接受值为 $min" >&2
       return 1
    fi
  fi
  if [ ! -z $max ] ; then
     if [ "$number" -gt "$max" ] ; then
       echo "你的值太大了：最大可接受值为 $max" >&2
       return 1
     fi
  fi
  return 0
}

# 解除以下几行的注释进行测试，但要注意这将破坏 Hack #6
# 因为 Hack #6 希望引入此文件以获取 validint() 函数。:-)

# if validint "$1" "$2" "$3" ; then
#   echo "该输入是一个在你的约束范围内的有效整数值"
# fi
~~~



## 案例6：validfloat

~~~shell
#!/bin/sh

# validfloat - 检测一个数值是否为有效的浮点数。
# 注意，该脚本不能接受科学计数法表示的浮点数（如 1.304e5）。

# 要测试输入的值是否为有效的浮点数，我们需要将值在小数点处分割，
# 然后测试第一部分是否为有效的整数，再测试第二部分是否为有效的 >=0 整数。
# 因此，-30.5 是有效的，但 -30.-8 不是。

. 005-validint.sh		# 引入 validint 函数

validfloat()
{
  fvalue="$1"

  if [ ! -z $(echo $fvalue | sed 's/[^.]//g') ] ; then  # 测试是否有小数点

    decimalPart="$(echo $fvalue | cut -d. -f1)"
    fractionalPart="$(echo $fvalue | cut -d. -f2)"

    if [ ! -z $decimalPart ] ; then
      if ! validint "$decimalPart" "" "" ; then  # 测试整数部分是否有效
        return 1
      fi 
    fi

    if [ "${fractionalPart%${fractionalPart#?}}" = "-" ] ; then
      echo "无效的浮点数：小数点后不允许出现 '-' 符号" >&2 
      return 1
    fi 
    if [ "$fractionalPart" != "" ] ; then 
      if ! validint "$fractionalPart" "0" "" ; then  # 测试小数部分是否有效
        return 1
      fi
    fi

    if [ "$decimalPart" = "-" -o -z $decimalPart ] ; then
      if [ -z $fractionalPart ] ; then
        echo "无效的浮点数格式。" >&2 ; return 1
      fi 
    fi

  else
    if [ "$fvalue" = "-" ] ; then
      echo "无效的浮点数格式。" >&2 ; return 1
    fi

    if ! validint "$fvalue" "" "" ; then  # 测试整数部分是否有效
      return 1
    fi
  fi

  return 0
}

if validfloat $1 ; then
  echo "$1 是一个有效的浮点数"
fi

exit 0
~~~

## 案例7：valid-date

~~~shell
#!/bin/sh
# valid-date - 验证日期，考虑闰年规则

normdate="./003-normdate.sh"	 # 规范化月份名称的脚本

exceedsDaysInMonth()
{
  # 给定一个月份名称，如果指定的日期值小于等于该月份的最大天数，则返回 0，否则返回 1

  case $(echo $1|tr '[:upper:]' '[:lower:]') in
    jan* ) days=31    ;;  feb* ) days=28    ;;
    mar* ) days=31    ;;  apr* ) days=30    ;;
    may* ) days=31    ;;  jun* ) days=30    ;;
    jul* ) days=31    ;;  aug* ) days=31    ;;
    sep* ) days=30    ;;  oct* ) days=31    ;;
    nov* ) days=30    ;;  dec* ) days=31    ;;
    * ) echo "$0: 未知的月份名称 $1" >&2; exit 1
   esac
   
   if [ $2 -lt 1 -o $2 -gt $days ] ; then
     return 1
   else
     return 0	# 一切正常
   fi 
}

isLeapYear()
{    
  # 如果是闰年，该函数返回 0，否则返回 1
  # 检查是否是闰年的公式如下：
  # 1. 能被 4 整除的年份是闰年，除非...
  # 2. 能被 100 整除的年份不是闰年，除非...
  # 3. 能被 400 整除的年份是闰年

  year=$1
  if [ "$((year % 4))" -ne 0 ] ; then
    return 1 # 不是闰年
  elif [ "$((year % 400))" -eq 0 ] ; then
    return 0 # 是闰年
  elif [ "$((year % 100))" -eq 0 ] ; then
    return 1
  else
    return 0
  fi 
}

## 开始主脚本

if [ $# -ne 3 ] ; then
  echo "用法: $0 月份 日  年份" >&2
  echo "常见的输入格式为 August 3 1962 和 8 3 2002" >&2
  exit 1
fi

# 规范化日期并拆分返回的值

newdate="$($normdate "$@")"

if [ $? -eq 1 ] ; then
  exit 1	# 错误已经由 normdate 报告过了
fi

month="$(echo $newdate | cut -d\  -f1)"
  day="$(echo $newdate | cut -d\  -f2)"
 year="$(echo $newdate | cut -d\  -f3)"

# 现在我们有了一个规范化的日期，让我们检查一下日期值是否合理

if ! exceedsDaysInMonth $month "$2" ; then
  if [ "$month" = "Feb" -a $2 -eq 29 ] ; then
    if ! isLeapYear $3 ; then
      echo "$0: $3 不是闰年，所以二月不可能有 29 天" >&2
      exit 1
    fi
  else 
    echo "$0: 错误的日期值: $month 不能有 $2 天" >&2
    exit 1
  fi
fi

echo "有效日期: $newdate"

exit 0
~~~

## 案例8：echon

~~~shell
#!/bin/sh

# echon - 一个用于在不具备 '-n' 选项的 Unix 系统上模拟 'echo' 中 '-n' 功能的脚本
#       -n 选项用于禁止输出结尾的换行符

echon()
{
  echo "$*" | tr -d '\n'  # 将所有传入的参数连接起来，并通过管道传递给 'tr' 命令以删除输出中的换行符
}

echon "这是一个测试: "
read answer

echon "这也是一个测试" " "
read answer2
~~~

## 案例9：scriptbc

~~~shell
#!/bin/sh

# scriptbc - 一个对 'bc' 进行封装的脚本，用于返回公式的计算结果

if [ $1 = "-p" ] ; then
  precision=$2
  shift 2
else
  precision=2		# 默认精度为 2
fi

bc -q -l << EOF
scale=$precision  # 设置计算结果的小数精度
$*                # 执行传入的公式
quit              # 退出 bc
EOF

exit 0
~~~

## 案例10:filelock

~~~shell
#!/bin/sh

# filelock - 一个灵活的文件锁定机制

retries="10"          # 默认的重试次数：10
action="lock"         # 默认操作为锁定
nullcmd="/bin/true"   # 空命令，用于 lockf

while getopts "lur:" opt; do
  case $opt in
    l ) action="lock"      ;;
    u ) action="unlock"    ;;
    r ) retries="$OPTARG"  ;;
  esac
done
shift $(($OPTIND - 1))

if [ $# -eq 0 ] ; then
  cat << EOF >&2
用法：$0 [-l|-u] [-r 重试次数] 锁定文件名
其中，-l 请求锁定（默认操作），-u 请求解锁，-r X 指定在失败之前的最大重试次数（默认为 $retries）。
EOF
  exit 1
fi

# 确定是否存在 lockf 或 lockfile 系统应用程序

if [ -z "$(which lockfile | grep -v '^no ')" ] ; then
  echo "$0 失败：在 PATH 中找不到 'lockfile' 工具。" >&2
  exit 1
fi

if [ "$action" = "lock" ] ; then
  if ! lockfile -1 -r $retries "$1" 2> /dev/null; then
    echo "$0: 失败：无法及时创建锁定文件。" >&2
    exit 1
  fi
else  # action = unlock
  if [ ! -f "$1" ] ; then
    echo "$0: 警告：要解锁的锁定文件 $1 不存在。" >&2
    exit 1
  fi
  rm -f "$1"
fi

exit 0
~~~

## 案例11:011-colors.sh

~~~shell
#!/bin/sh

# ANSI Color -- 使用这些变量可以轻松地输出不同的颜色和格式。
#    确保在颜色之后输出重置序列（f = 前景色，b = 背景色），
#    并使用 'off' 特性关闭任何打开的设置。

initializeANSI()
{
  esc=""  # 转义序列的起始字符

  blackf="${esc}[30m";   redf="${esc}[31m";    greenf="${esc}[32m"
  yellowf="${esc}[33m"   bluef="${esc}[34m";   purplef="${esc}[35m"
  cyanf="${esc}[36m";    whitef="${esc}[37m"
  
  blackb="${esc}[40m";   redb="${esc}[41m";    greenb="${esc}[42m"
  yellowb="${esc}[43m"   blueb="${esc}[44m";   purpleb="${esc}[45m"
  cyanb="${esc}[46m";    whiteb="${esc}[47m"

  boldon="${esc}[1m";    boldoff="${esc}[22m"
  italicson="${esc}[3m"; italicsoff="${esc}[23m"
  ulon="${esc}[4m";      uloff="${esc}[24m"
  invon="${esc}[7m";     invoff="${esc}[27m"

  reset="${esc}[0m"  # 重置所有颜色和格式设置的序列
}

# 注意，在第一次使用时切换颜色不需要先进行重置。
# 新的颜色会覆盖旧的颜色。

initializeANSI

cat << EOF
${yellowf}这是黄色的文字${redb}和红色的背景${reset}
${boldon}这是粗体${ulon}这是斜体${reset}再见
${italicson}这是斜体${italicsoff}这是常规字体
${ulon}这是下划线${uloff}这是常规字体
${invon}这是反显${invoff}这是常规字体
${yellowf}${redb}警告 I${yellowb}${redf}警告 II${reset}
EOF
~~~

## 012-library-test.sh*

~~~shell
#!/bin/bash

# nicenumber - 格式化数字，以逗号分隔
# 参数arg1为要格式化的数字，如果指定了arg2，则直接打印输出，否则返回格式化后的结果
nicenumber()
{
  # 注意：我们使用'.'作为小数点分隔符来解析输入值。
  # 如果用户指定了-d选项，则输出值将使用-d指定的小数点分隔符。

  integer=$(echo $1 | cut -d. -f1)    # 小数点左边的整数部分
  decimal=$(echo $1 | cut -d. -f2)    # 小数点右边的小数部分

  if [ $decimal != $1 ]; then
    # 存在小数部分，将其包含在结果中
    result="${DD:="."}$decimal"
  fi

  thousands=$integer

  while [ $thousands -gt 999 ]; do
    remainder=$(($thousands % 1000))    # 取最低的三位数字

    while [ ${#remainder} -lt 3 ] ; do    # 需要时添加前导零
      remainder="0$remainder"
    done

    thousands=$(($thousands / 1000))    # 左边的数字（如果有的话）
    result="${TD:=","}${remainder}${result}"    # 从右到左构建结果
  done

  nicenum="${thousands}${result}"

  if [ ! -z $2 ] ; then
     echo $nicenum
  fi
}

# validint - 验证整数输入，允许负数
validint()
{
  # 验证第一个字段是否为整数。
  # 可选地测试是否大于最小值$2和/或小于最大值$3：如果你不想进行这些测试，请将其值设为""。
  # 返回1表示错误，返回0表示成功。

  number="$1"
  min="$2"
  max="$3"

  if [ -z "$number" ] ; then
    echo "您没有输入任何内容。不可接受。" >&2 ; return 1
  fi

  if [ "${number%${number#?}}" = "-" ] ; then    # 第一个字符是'-'吗？
    testvalue="${number#?}"    # 除第一个字符外的所有字符
  else
    testvalue="$number"
  fi

  nodigits="$(echo $testvalue | sed 's/[[:digit:]]//g')"

  if [ ! -z "$nodigits" ] ; then
    echo "无效的数字格式！只能包含数字，不能包含逗号、空格等。" >&2
    return 1
  fi

  if [ ! -z "$min" ] ; then
    if [ "$number" -lt "$min" ] ; then
       echo "您的值太小：最小可接受值为 $min" >&2
       return 1
    fi
  fi
  if [ ! -z "$max" ] ; then
     if [ "$number" -gt "$max" ] ; then
       echo "您的值太大：最大可接受值为 $max" >&2
       return 1
     fi
  fi
  return 0
}

# validfloat - 验证浮点数的有效性
# 注意，该函数不能接受科学计数法（如1.304e5）的表示方式。
# 要测试输入值是否为有效的浮点数，我们需要将值在小数点处分割，
# 然后测试第一部分是否为有效的整数，然后测试第二部分是否为有效的大于等于0的整数。
# 因此，-30.5是有效的，而-30.-8则不是。返回0表示成功，返回1表示失败。

validfloat()
{
  fvalue="$1"

  if [ ! -z "$(echo $fvalue | sed 's/[^.]//g')" ] ; then
~~~



## 012-library.sh*

~~~shell
#!/bin/sh

# 脚本演示使用shell函数库
# 导入012-library.sh脚本
. 012-library.sh

# 初始化ANSI颜色
initializeANSI

# 提示用户是否在PATH环境变量中有echo命令
echon "首先，请问你的PATH环境变量中是否包含echo命令？（1=是，2=否）"
read answer

# 验证用户输入是否为1或2，直到输入有效的值
while ! validint $answer 1 2 ; do
    echon "${boldon}请再试一次${boldoff}。你的PATH环境变量中是否包含echo命令？（1=是，2=否）"
    read answer
done

# 检查PATH环境变量中是否存在echo命令
if ! checkForCmdInPath "echo" ; then
    echo "找不到echo命令。"
else
    echo "echo命令存在于PATH环境变量中。"
fi

echo ""

# 提示用户输入一个可能是闰年的年份
echon "请输入你认为可能是闰年的年份："
read year

# 验证用户输入的年份是否有效，直到输入有效的值
while ! validint $year 1 9999 ; do
    echon "请输入一个${boldon}正确${boldoff}格式的年份："
    read year
done

# 判断输入的年份是否为闰年
if isLeapYear $year ; then
    echo "${greenf}你是对的！$year年是闰年。${reset}"
else
    echo "${redf}不对，那不是闰年。${reset}"
fi

exit 0
~~~

## 013-guessword.sh*

~~~shell
#!/bin/sh
# guessword - 一个简单的单词猜测游戏，类似于猜词游戏

blank=".................."	# 必须比最长的单词长

getword() 
{
  case $(( $$ % 8 )) in
    0 ) echo "pizzazz"    ;; 	1 ) echo "delicious"	;;
    2 ) echo "gargantuan" ;;	3 ) echo "minaret"	;;
    4 ) echo "paparazzi"  ;;    5 ) echo "delinquent"   ;;
    6 ) echo "zither"     ;;    7 ) echo "cuisine"	;;
  esac
}

addLetterToWord()
{
  # 此函数将模板中的所有'.'替换为猜测的字母
  # 然后更新remaining为剩余的空槽数量

  letter=1
  while [ $letter -le $letters ] ; do
    if [ "$(echo $word | cut -c$letter)" = "$guess" ] ; then
      before="$(( $letter - 1 ))";  after="$(( $letter + 1 ))"
      if [ $before -gt 0 ]  ; then
        tbefore="$(echo $template | cut -c1-$before)"
      else
	tbefore=""
      fi
      if [ $after -gt $letters ] ; then
        template="$tbefore$guess"
      else
        template="$tbefore$guess$(echo  $template | cut -c$after-$letters)"
      fi
    fi
    letter=$(( $letter + 1 ))
  done

  remaining=$(echo $template|sed 's/[^\.]//g'|wc -c|sed 's/[[:space:]]//g')
  remaining=$(( $remaining - 1 ))	# 修复忽略'\n'
}

word=$(getword)
letters=$(echo $word | wc -c | sed 's/[[:space:]]//g')
letters=$(( $letters - 1 ))	# 修复字符计数，忽略\n
template="$(echo $blank | cut -c1-$letters)"
remaining=$letters ; guessed="" ; guesses=0; badguesses=0

echo "** 你正在尝试猜一个有 $letters 个字母的单词 **"

while [ $remaining -gt 0  ] ; do
  echo -n "单词为: $template  请猜下一个字母："; read guess
  guesses=$(( $guesses + 1 ))
  if echo $guessed | grep -i $guess > /dev/null ; then
    echo "你已经猜过这个字母了。请重新猜！"
  elif ! echo $word | grep -i $guess > /dev/null ; then
    echo "抱歉，字母 \"$guess\" 不在单词中。"
    guessed="$guessed$guess"
    badguesses=$(( $badguesses + 1 ))
  else
    echo "很棒！字母 $guess 在单词中！"
    addLetterToWord $guess
  fi
done

echo -n "恭喜你！你在 $guesses 次猜测中猜到了 $word"
echo "，其中有 $badguesses 次错误猜测"

exit 0
~~~

## 013-hilow.sh*

~~~shell
#!/bin/sh
# hilow - 一个简单的猜数字游戏

biggest=100                             # 最大可能的数字
guess=0                                 # 玩家猜测的数字
guesses=0                               # 猜测次数
number=$(( $$ % $biggest ))             # 随机数，范围为 1 到 $biggest

while [ $guess -ne $number ] ; do
  echo -n "猜测数字是多少？" ; read guess
  if [ "$guess" -lt $number ] ; then
    echo "... 更大！"
  elif [ "$guess" -gt $number ] ; then
    echo "... 更小！"
  fi
  guesses=$(( $guesses + 1 ))
done

echo "正确！在 $guesses 次猜测中猜到了 $number。"

exit 0
~~~

## 014-nfmt.sh*

~~~shell
#!/bin/sh

# nfmt - 一个使用nroff的fmt版本。添加了两个有用的选项：-w X 用于设置行宽，-h 用于启用连字以获得更好的换行效果。

while getopts "hw:" opt; do
  case $opt in
    h ) hyph=1    	    ;;  # 如果选项为 -h，则将 hyph 变量设置为 1，表示启用连字
    w ) width="$OPTARG"    ;;  # 如果选项为 -w，则将 width 变量设置为选项参数的值，表示设置行宽
  esac
done
shift $(($OPTIND - 1))

nroff << EOF
.ll ${width:-72}  # 设置行宽为 width 变量的值（如果未设置则为72）
.na  # 禁用自动换行，不允许单词在行末被截断
.hy ${hyph:-0}  # 如果 hyph 变量为 1，则启用连字（连字符）以获得更好的换行效果，否则禁用连字
.pl 1  # 设置段落间距为 1
$(cat "$@")  # 使用 cat 命令读取文件内容并传递给 nroff
EOF

exit 0
~~~

## 015-newrm.sh*

~~~shell
#!/bin/sh

# newrm - 一个替代现有 rm 命令的脚本，通过在用户的主目录中创建一个新的目录，
# 实现了一个简单的还原删除的功能。它可以处理目录及其内容，以及单个文件，
# 如果用户指定了 -f 标志，则不会将文件归档，而是直接删除。

# 重要警告：你需要设置一个 cron 作业或类似的机制来保持各个垃圾目录的管理，
# 否则实际上系统上的文件将永远不会被删除，你的磁盘空间将会耗尽！

mydir="$HOME/.deleted-files"  # 存储被删除文件的目录路径
realrm="/bin/rm "  # 真正的 rm 命令路径
copy="/bin/cp -R"  # 复制命令路径，用于归档文件

if [ $# -eq 0 ] ; then  # 如果没有输入参数，则让 'rm' 输出使用错误
  exec $realrm  # 替换当前 shell 进程为 /bin/rm
fi

# 解析所有选项，查找 '-f' 标志

flags=""

while getopts "dfiPRrvW" opt
do
  case $opt in
    f ) exec $realrm "$@"     ;;  # 使用 exec 直接退出本脚本并执行 /bin/rm
    * ) flags="$flags -$opt"  ;;  # 其他选项是给 'rm' 使用的，不是给我们的
  esac
done
shift $(( $OPTIND - 1 ))

# 确保 $mydir 存在

if [ ! -d $mydir ] ; then
  if [ ! -w $HOME ] ; then
    echo "$0 失败：无法在 $HOME 中创建 $mydir" >&2
    exit 1
  fi
  mkdir $mydir
  chmod 700 $mydir  # 一点点隐私，请
fi

for arg 
do
  newname="$mydir/$(date "+%S.%M.%H.%d.%m").$(basename "$arg")"  # 生成新的文件名
  if [ -f "$arg" ] ; then  # 如果是文件
    $copy "$arg" "$newname"  # 复制文件到垃圾目录
  elif [ -d "$arg" ] ; then  # 如果是目录
    $copy "$arg" "$newname"  # 复制目录及其内容到垃圾目录
  fi
done

exec $realrm $flags "$@"  # 使用真正的 rm 命令删除文件/目录
~~~



## 016-unrm.sh*

~~~shell
#!/bin/sh

# unrm - 在删除的文件归档中搜索指定的文件。如果有多个匹配项，则显示按时间戳排序的列表，并允许用户指定要恢复的文件。

# 重要警告：你需要设置一个 cron 作业或类似的机制来保持各个垃圾目录的管理，
# 否则实际上系统上的文件将永远不会被删除，你的磁盘空间将会耗尽！

mydir="$HOME/.deleted-files"  # 存储被删除文件的目录路径
realrm="/bin/rm"  # 真正的 rm 命令路径
move="/bin/mv"  # 移动命令路径，用于恢复文件

dest=$(pwd)  # 当前工作目录作为恢复文件的目标目录

if [ ! -d $mydir ] ; then
  echo "$0: 没有删除文件目录：无法进行还原操作" >&2 ; exit 1
fi

cd $mydir

if [ $# -eq 0 ] ; then # 没有参数，仅显示列表
  echo "你的已删除文件归档内容（按日期排序）："
  ls -FC | sed -e 's/\([[:digit:]][[:digit:]]\.\)\{5\}//g' \
    -e 's/^/  /' 
  exit 0
fi

# 否则，我们必须有一个要匹配的模式。让我们看看用户指定的模式是否与归档中的多个文件或目录匹配。

matches="$(ls *"$1" 2> /dev/null | wc -l)"

if [ $matches -eq 0 ] ; then
  echo "在已删除文件归档中找不到 \"$1\" 的匹配项。" >&2
  exit 1
fi

if [ $matches -gt 1 ] ; then
  echo "归档中有多个文件或目录匹配项："
  index=1
  for name in $(ls -td *"$1")
  do
    datetime="$(echo $name | cut -c1-14| \
       awk -F. '{ print $5"/"$4" at "$3":"$2":"$1 }')"
    if [ -d $name ] ; then
      size="$(ls $name | wc -l | sed 's/[^0-9]//g')"
      echo " $index)   $1  (内容 = ${size} 项, 删除时间 = $datetime)"
    else
      size="$(ls -sdk1 $name | awk '{print $1}')"
      echo " $index)   $1  (大小 = ${size}KB, 删除时间 = $datetime)"
    fi
    index=$(( $index + 1))
  done
  
  echo "" 
  echo -n "您想要恢复哪个版本的 $1（输入 '0' 退出）？[1] : "
  read desired

  if [ ${desired:=1} -ge $index ] ; then
    echo "$0: 用户取消恢复操作：索引值过大。" >&2
    exit 1
  fi

  if [ $desired -lt 1 ] ; then
    echo "$0: 用户取消恢复操作。" >&2 ; exit 1
  fi

  restore="$(ls -td1 *"$1" | sed -n "${desired}p")"
  
  if [ -e "$dest/$1" ] ; then
    echo "此目录中已存在 \"$1\"。无法覆盖。" >&2
    exit 1
  fi

  echo -n "正在恢复文件 \"$1\" ..."
  $move "$restore" "$dest/$1"
  echo "完成。"

  echo -n "删除其他副本？[y] " 
  read answer
  
  if [ ${answer:=y} = "y" ] ; then
    $realrm -rf *"$1"
    echo "已删除。"
  else
    echo "保留其他副本。"
  fi
else
  if [ -e "$dest/$1" ] ; then
    echo "此目录中已存在\"$1\"。无法覆盖。" >&2
    exit 1
  fi

  restore="$(ls -d *"$1")"

  echo -n "正在恢复文件 \"$1\" ... " 
  $move "$restore" "$dest/$1"
  echo "完成。"
fi

exit 0
~~~

## 017-logrm.sh*

~~~shell
#!/bin/sh

# logrm - 记录所有的文件删除请求，除非使用了 "-s" 标志

removelog="/tmp/removelog.log"  # 保存删除请求日志的文件路径

if [ $# -eq 0 ] ; then  # 检查是否没有传入任何参数
  echo "用法: $0 [-s] 文件或目录列表" >&2  # 输出用法信息到标准错误
  exit 1
fi

if [ "$1" = "-s" ] ; then  # 检查第一个参数是否为 "-s"
  # 请求静默操作...不记录日志
  shift  # 移除第一个参数
else
  echo "$(date): ${USER}: $@" >> $removelog  # 将删除请求的时间戳、用户名和文件列表写入日志文件
fi

/bin/rm "$@"  # 调用真正的 rm 命令删除文件

exit 0
~~~

## 018-formatdir.sh*

~~~shell
#!/bin/sh

# formatdir - 以友好和有用的格式输出目录列表

gmk()
{
  # 根据输入的大小（以KB为单位），输出最佳显示格式，单位为KB、MB或GB
  if [ $1 -ge 1000000 ] ; then
    echo "$(scriptbc -p 2 $1 / 1000000)Gb"
  elif [ $1 -ge 1000 ] ; then
    echo  "$(scriptbc -p 2 $1 / 1000)Mb"
  else 
    echo "${1}Kb"
  fi
}

if [ $# -gt 1 ] ; then
  echo "用法: $0 [目录名]" >&2; exit 1
elif [ $# -eq 1 ] ; then
  cd "$@"  # 切换到指定的目录
fi

for file in *
do 
  if [ -d "$file" ] ; then  # 判断文件是否为目录
    size=$(ls "$file" | wc -l | sed 's/[^[:digit:]]//g')  # 统计目录中的文件数量
    if [ $size -eq 1 ] ; then
      echo "$file ($size 个条目)|"  # 输出目录名称和文件数量（单数形式）
    else
      echo "$file ($size 个条目)|"  # 输出目录名称和文件数量（复数形式）
    fi
  else
    size="$(ls -sk "$file" | awk '{print $1}')"  # 获取文件大小（以KB为单位）
    echo "$file ($(gmk $size))|"  # 输出文件名称和格式化后的文件大小
  fi
done | \
  sed 's/ /^^^/g'  | \
  xargs -n 2     | \
  sed 's/\^\^\^/ /g' | \
  awk -F\| '{ printf "%-39s %-39s\n", $1, $2 }'  # 格式化输出目录列表

exit 0
~~~

## 019-locate.sh*

~~~shell
#!/bin/sh

# locate - 在 locate 数据库中搜索指定的模式

locatedb="/var/locate.db"  # locate 数据库文件路径

exec grep -i "$@" $locatedb  # 在 locate 数据库中执行不区分大小写的 grep 命令搜索指定模式
~~~

## 019-mklocatedb.sh*

~~~shell
#!/bin/sh

# mklocatedb - 使用 find 命令构建 locate 数据库。必须以 root 用户身份运行此脚本

locatedb="/var/locate.db"  # locate 数据库文件路径

if [ "$(whoami)" != "root" ] ; then
  echo "必须以 root 用户身份运行此命令。" >&2
  exit 1
fi

find / -print > $locatedb

exit 0
~~~

## 020-DIR.sh*

~~~shell
~~~

## 021-findman.sh*

~~~shell
~~~

## 022-timein.sh*

~~~shell
~~~

## 023-remember.sh*

~~~shell
~~~



## 023-remindme.sh*

~~~shell
~~~

## 024-calc.sh*

~~~shell
~~~

## 025-checkspelling.sh*

~~~shell
~~~

## 026-shpell.sh*

~~~shell
~~~

## 027-spelldict.sh*

~~~shell
~~~

## 028-convertatemp.sh*

~~~shell
~~~

## 029-loancalc.sh*

~~~shell
~~~

## 030-addagenda.sh*

~~~shell
~~~

## 030-agenda.sh*

~~~shell
~~~

## 031-numberlines.sh*

~~~shell
~~~

## 032-showfile.sh*

~~~shell
~~~

## 033-toolong.sh*

~~~shell
~~~

## 034-quota.sh*

~~~shell
~~~

## 035-mysftp.sh*

~~~shell
~~~

## 036-cgrep.sh*

~~~shell
~~~

## 037-zcat.sh*

~~~shell
~~~

## 038-bestcompress.sh*

~~~shell
~~~

## 039-fquota.sh*

~~~shell
~~~

## 040-diskhogs.sh*

~~~shell
~~~

## 041-diskspace.sh*

~~~shell
~~~

## 042-newdf.sh*

~~~shell
~~~

## 043-mkslocate.sh*

~~~shell
~~~

## 043-slocate.sh*

~~~shell
~~~

## 044-adduser.sh*

~~~shell
~~~

## 045-suspenduser.sh*

~~~shell
~~~

## 046-deleteuser.sh*

~~~shell
~~~

## 047-validator.sh*

~~~shell
~~~

## 048-fixguest.sh*

~~~shell
~~~

## 049-findsuid.sh*

~~~shell
~~~

## 050-set-date.sh*

~~~shell
~~~

## 051-enabled.sh*

~~~shell
~~~

## 052-killall.sh*

## 053-verifycron.sh*

## 054-docron.sh*

## 055-rotatelogs.sh*

## 056-backup.sh*

## 057-archivedir.sh*

## 058-connecttime.sh*

## 059-ftpget.sh*

## 060-bbcnews.sh*

## 061-getlinks.sh*

## 062-define.sh*

## 063-weather.sh*

## 064-checklibrary.sh*

## 065-moviedata.sh*

## 066-exchangerate.sh*

## 066-getexchrate.sh*

## 067-getstock.sh*

## 067-portfolio.sh*

## 068-changetrack.sh*

## 069-showcgienv.sh*

## 071-getdope.sh*

## 075-counter.sh*

## 075-updatecounter.sh*

## 076-randomquote.sh*

## 077-checklinks.sh*

## 078-checkexternal.sh*

## 079-webspell.sh*

## 081-ftpsyncup.sh*

## 082-ftpsyncdown.sh*

## 083-sftpsync.sh*

## 083-ssync.sh*

## 084-webaccess.sh*

## 085-enginehits.sh*

## 085-searchinfo.sh*

## 086-weberrors.sh*

## 087-remotebackup.sh*

## 087-trimmailbox.sh*

## 088-unpacker.sh*

## 089-xferlog.sh*

## 090-getstats.sh*

## 090-netperf.sh*

## 091-renicename.sh*

## 091-watch-and-nice.sh*

## 092-addvirtual.sh*

## 093-listmacusers.sh*

## 094-addmacuser.sh*

## 095-addmacalias.sh*

## 096-titleterm.sh*

## 097-itunelist.sh*

## 098-open2.sh*

## 099-unscramble.sh*

## 100-hangman.sh*

## 101-states.sh*

