shell脚本编程视频 总共25集

| 视频名称                   | 时间  |
| :------------------------- | :---- |
| 01-shell的介绍             | 22:58 |
| 02-shell的内建命令         | 4:18  |
| 03-shell脚本执行的几种方法 | 18:40 |
| 04-变量的使用              | 6:08  |
| 05-变量的使用              | 20:18 |
| 06-文件名代换和参数拓展    | 13:01 |
| 07-命令代换                | 09:17 |
| 08-算数代换                | 04:39 |
| 09-shell中的转义           | 04:29 |
| 10-引号                    | 08:14 |
| 11-复习                    | 09:24 |
| 12-条件测试                | 21:37 |
| 13-if分支结构              | 16:35 |
| 14-case分支结构            | 10:36 |
| 15-for循环                 | 09:25 |
| 16-while循环               | 07:33 |
| 17-位置参数以及shift       | 11:42 |
| 18-shell中的输出           | 02:49 |
| 19-复习                    | 15:58 |
| 20-管道1                   | 04:02 |
| 21-管道2                   | 13:02 |
| 22-重定向                  | 10:19 |
| 23-函数                    | 10:20 |
| 24-函数2                   | 06:08 |
| 25-脚本调试的集中方法      | 12:03 |

4小时 45分钟 30秒,今天肯定是能看完并且做完笔记，还行吧，加油。

# 01-shell的介绍

简单的工作用简单语言来开发。

==对Linux有一个更深层次的认识==

Shell在交互式模式下，用户可以逐行输入命令，Shell会立即解释执行并输出结果，这种方式称为交互式Shell。这样用户可以根据需要逐步操作和获取结果。

另一种执行命令的方式是批处理模式，用户事先编写好一个Shell脚本（也称为脚本文件），其中包含多条命令。用户只需执行该脚本，Shell会按顺序读取脚本文件中的命令，并一次性执行完所有命令，而无需手动逐行输入。这种方式称为批处理Shell。

Shell脚本类似于编程语言，它可以包含变量、流程控制语句（如条件判断和循环），以及其他功能。然而，与编程语言不同的是，Shell脚本是解释执行的，不需要进行编译过程。Shell程序会逐行读取脚本中的命令，并将其解释执行，就好像用户一行一行地在Shell提示符下输入并执行这些命令一样。

通过编写Shell脚本，用户可以将一系列常用的命令组合起来，实现自动化、批量化的操作，提高工作效率。

 不同的bash版本：

1. sh (Bourne Shell): 由Steve Bourne开发，几乎所有UNIX系统都默认配备了sh。它是一种简单的Shell，不支持一些高级功能，如作业控制、命令历史和命令行编辑。
2. csh (C Shell): 由Bill Joy开发，随BSD UNIX发布。它的流程控制语句类似于C语言，支持Bourne Shell不支持的一些功能。然而，csh也有一些限制，并不是在所有UNIX系统上都广泛使用。
3. ksh (Korn Shell): 由David Korn开发，旨在向后兼容sh，并添加了csh引入的新功能。ksh是许多UNIX系统的标准配置Shell，因此在这些系统上，/bin/sh通常是指向/bin/ksh的符号链接。
4. tcsh (TENEX C Shell): 是csh的增强版本，引入了命令补全等功能。在FreeBSD、MacOS X等系统上，tcsh替代了csh。
5. bash (Bourne Again Shell): 由GNU开发的Shell，目标是与POSIX标准保持一致，并兼容sh。bash从csh和ksh借鉴了许多功能。它是各种Linux发行版的标准配置Shell，因此在Linux系统上，/bin/sh通常是指向/bin/bash的符号链接。尽管如此，bash和sh仍然存在一些差异。一方面，bash扩展了某些命令和参数，另一方面，bash并不完全兼容sh，某些行为可能不一致。因此，当以sh为程序名启动bash时，bash可以模拟sh的行为，不识别扩展命令，并保持与sh的行为一致。



echo $SHELL 查看当前用户使用什么shell

# 2 shell内建命令

在命令行中，用户输入的命令通常由Shell执行。但是Shell的内建命令是一个例外，它们不会创建新的进程，而是在Shell进程中直接执行，类似于调用Shell内部的一个函数。

一些常见的Shell内建命令包括umask、exit、cd、alias、man等。这些命令在执行时不会启动新的进程，而是直接在当前Shell进程中执行相应的功能。

对于一些不是内建命令的普通命令，可以使用`which`命令来查找其可执行文件的位置。而内建命令没有对应的可执行文件，因此无法用`which`命令查找到它们的位置。

要查看Shell内建命令的详细信息，可以使用`man bash-builtins`命令（对于Bash Shell）。这将显示有关Shell内建命令的手册页面，包括命令的用法、选项和示例。

虽然内建命令不创建新的进程，但它们执行结束后也会有一个退出状态码（Exit Status）。通常，执行成功的内建命令会返回0作为状态码，而执行失败的则返回非零值。这样的状态码可以通过特殊变量`$?`来读取，以便在Shell脚本中进行后续的处理。

# 3 执行脚本

可以看到一个简单的脚本test.sh，其中包含以下内容：

```shell
#!/bin/sh
echo HelloWorld
cd ..
```

这是一个简单的Shell脚本示例，使用了Shebang（#!）来指定解释器为`/bin/sh`。脚本的功能是输出"HelloWorld"并尝试切换到上一级目录。

要执行这个脚本，可以通过以下方式之一：

给脚本文件添加可执行权限并执行：

```shell
$ chmod +x test.sh
$ ./test.sh
```

这样Shell会fork一个子进程并调用exec执行`./test.sh`，由于指定了Shebang，子进程会用`/bin/sh`解释器的代码段替换当前进程，并从解释器的开始执行。因此，脚本中的命令会被执行。

直接使用解释器执行脚本：

```shell
$ /bin/sh ./test.sh
```

这种方式不需要脚本文件具有可执行权限，直接通过指定解释器执行脚本。无论使用哪种方式执行脚本，都会输出"HelloWorld"并尝试切换到上一级目录。

另外，提到了使用括号和`source`命令来执行Shell脚本。这种方式不会创建子Shell，而是直接在当前交互式Shell中逐行执行脚本中的命令。例如：

```shell
$ (cd ..; ls -l)
```

这将在当前Shell中执行括号内的命令，不会影响当前Shell的PWD。而使用`source`命令可以直接在当前Shell中执行脚本，例如：

```shell
$ source ./test.sh
```

这种方式也不会创建子Shell，脚本中的命令会在当前Shell中逐行执行。

source 和.的作用以及最终效果相同：
~~~shell
. test.sh
~~~

==在Linux中我明明没有添加#!/bin/bash 这个脚本为什么也能执行呢？==

在Linux中，脚本文件是否能够执行，并不仅仅取决于文件的扩展名或者文件中是否包含 `#!/bin/bash` 这样的解释器指令。Linux系统通过文件的权限来确定是否可以执行该文件。

如果一个文件的权限被设置为可执行（例如设置了执行权限 `chmod +x script.sh`），那么即使文件中没有指定解释器，Linux系统也会尝试使用默认的解释器来执行该文件。通常情况下，默认的解释器是由系统配置文件 `/etc/bashrc` 或者 `/etc/profile` 中的 `SHELL` 环境变量来确定的。

因此，如果你在Linux中没有添加 `#!/bin/bash` 这个脚本开头的指令，但是文件的权限被设置为可执行，并且系统默认的解释器是Bash，那么系统会默认使用Bash解释器来执行该文件。

需要注意的是，对于其他类型的脚本文件，可能需要在文件开头指定相应的解释器，例如Python脚本需要在开头指定 `#!/usr/bin/python` 或者 `#!/usr/bin/env python`。这样可以确保脚本能够正确地被对应的解释器执行。



在Linux中，`#!/bin/bash` 是一种特殊的注释，称为"shebang"或"hashbang"，用于指定脚本文件的解释器。

当执行一个脚本文件时，操作系统会读取文件的第一行，如果以 `#!` 开头，后面跟着解释器的路径，就会使用该解释器来执行脚本。因此，`#!/bin/bash` 表示使用Bash作为脚本文件的解释器。

为什么需要添加 `#!/bin/bash` 呢？

1. 指定解释器：通过添加 `#!/bin/bash`，你明确地告诉操作系统应该使用Bash来解释执行脚本文件。这对于确保脚本在正确的环境中运行非常重要。
2. 可移植性：不同的操作系统可能使用不同的默认解释器路径。通过指定 `#!/bin/bash`，你可以确保脚本在不同的Linux系统上都能够正常执行，而不依赖于系统默认的解释器路径。
3. 脚本可执行性：添加 `#!/bin/bash` 并赋予脚本文件执行权限 (`chmod +x script.sh`)，可以使脚本文件直接执行，而不需要显式地调用解释器。这样可以方便地在终端中执行脚本，提高了脚本的使用便捷性。

==我倒是认为现在所处的就是bash环境，所以最终是使用bash运行的，所以就算不指定第一行的/bin/bash也可以正常执行==



# 4.变量的使用

​	在Shell中，变量通常以字母加下划线开头，并由字母、数字和下划线组成。变量的定义或赋值可以使用等号（=）进行，例如`VARNAME=value`。需要注意的是，等号两边不能有空格，否则空格会被解释成命令和参数的一部分。

在使用变量时，可以使用美元符号（$）加上变量名来引用变量的值，例如`echo $VARNAME`。如果变量名后面紧跟着其他字符（例如后缀），为了避免将变量名和后缀当作一个整体，可以使用花括号将变量名分隔出来，例如`echo ${VARNAME}suffix`。

# 5.变量的分类

可以将Shell中的变量分为两种不同的分类：

1. 环境变量（Environment Variables）：

   环境变量是操作系统自带的变量，每个进程都有自己的环境变量集合。当启动一个子进程时，子进程会从父进程继承一份相同的环境变量副本。这意味着子进程拥有与父进程相同的初始环境变量。

   子进程对环境变量的修改不会影响父进程的环境变量。环境变量是单向传递的，子进程可以修改自己的环境变量，但不会影响到父进程或其他兄弟进程的环境变量。

   在Shell中，可以使用`export`命令将一个变量导出为环境变量，例如`export varname=value`。另外，也可以直接在当前Shell进程中定义一个变量，并将其同时导出为环境变量，例如`varname=value`和`export varname`两个命令组合使用。

2. 本地变量（Local Variables）：

   **全局变量（Global Variables）:**
   全局变量是在Shell的解析环境中存在的变量，不需要任何修饰符进行声明。无论是在函数内部还是函数外部，全局变量的作用范围都是整个Shell进程。全局变量的生命周期从声明语句开始，一直持续到Shell脚本结束。

   **局部变量（Local Variables）:**
   局部变量使用`local`关键字进行修饰，只能在函数内部声明。局部变量的作用范围仅限于声明它的函数内部，在函数结束后，局部变量将不再可用。局部变量的生命周期从声明语句开始，一直持续到函数执行结束。

   Shell内部变量只能在当前Shell进程中使用，如果跨越了进程边界，例如在子进程中或从子进程返回到父进程，那么变量的可见性将受到限制。

环境变量是进程间共享的概念，而本地变量是Shell特有的概念。在Shell中，环境变量和本地变量的定义和使用方式相似。

可以使用`export`命令将本地变量导出为环境变量。一般情况下，定义和导出环境变量可以一步完成，例如`export VARNAME=value`。也可以分两步完成，先定义本地变量，然后使用`export`命令将其导出为环境变量。



3. 删除环境变量
   使用`unset`命令来删除Shell中的变量，无论是环境变量还是普通的Shell内部变量。

使用`unset`命令的语法是：`unset 变量名`。

例如，如果要删除一个环境变量，可以执行如下命令：

```
unset VARNAME
```

如果要删除一个普通的Shell内部变量，同样可以使用`unset`命令：

```
unset varname
```

执行`unset`命令后，相应的变量将被从当前Shell进程中移除，不再可用。

需要注意的是，`unset`命令只能删除当前Shell进程中的变量，不会影响其他Shell进程或操作系统级别的环境变量。

# 6.文件名替换和参数扩展

文件名代换（Globbing）是一种在Shell中用于匹配文件名的机制，通常使用通配符来指定匹配模式。以下是一些常用的	意字符。

- `?`：匹配一个任意字符。
- `[]`：匹配方括号中的任意一个字符，可以指定多个字符或字符范围。

下面是一些示例说明如何使用这些通配符：

1. `ls /dev/ttyS*`：匹配以`/dev/ttyS`开头的文件名，后面可以是任意字符。
2. `ls ch0?.doc`：匹配以`ch0`开头，后面跟着一个任意字符，然后以`.doc`结尾的文件名。
3. `ls ch0[0-2].doc`：匹配以`ch0`开头，后面跟着一个字符，该字符是0、1或2，然后以`.doc`结尾的文件名。
4. `Is ch[012] [0-9].doc`：这个示例可能存在一些打字错误。如果将其理解为`Is ch[012] [0-9].doc`，那么它将匹配以`ch0`、`ch1`或`ch2`开头，后面跟着一个数字，然后以空格和一个数字，最后以`.doc`结尾的文件名。

需要注意的是，Globbing所匹配的文件名是Shell在参数传递给命令之前进行展开的。因此，在执行诸如`ls`或`Is`这样的命令之前，Shell会将匹配的文件名展开为实际的文件名，并将这些文件名作为命令的参数传递。例如，在使用`ls ch0[012].doc`命令时，如果当前目录下存在`ch00.doc`和`ch02.doc`这两个文件，那么实际传递给`ls`命令的参数将是这两个文件名，而不是一个匹配字符串。 

# 7.命令代换

命令代换（Command Substitution）是一种在Shell中执行命令并将其输出结果直接嵌入到另一个命令或上下文中的机制。在Shell中，可以使用反引号（`）或美元符号加圆括号（$()）来表示命令代换。

以下是一些示例说明如何使用命令代换：

使用反引号（`）表示命令代换：

```bash
DATE=`date`
echo $DATE
```

在上述示例中，`date`命令被执行，并将其输出结果赋给变量`DATE`。然后，使用`echo`命令打印出`DATE`变量的值，即当前的日期和时间。

使用美元符号加圆括号（$()）表示命令代换：

```bash
DATE=$(date)
echo $DATE
```

这个示例与前一个示例的功能相同，只是使用了不同的语法形式。`$(date)`会执行`date`命令，并将输出结果赋给变量`DATE`。

```shell
#!/bin/bash
# 获取当前日期和时间
dateTime=$(date)
echo "dateTime is $dateTime"

# 在当前路径下创建1.txt文件
touch 1.txt

# 获取当前脚本所在路径
curPath=$(cd "$(dirname "$0")" && pwd)
touch "$curPath/1.txt"
```

`dateTime=$(date)`使用命令代换获取当前日期和时间，并将结果存储在`dateTime`变量中，然后使用`echo`命令打印出该变量的值。

在创建文件部分，`touch 1.txt`直接在当前路径下创建了1.txt文件。

获取当前脚本所在路径的部分，使用了`cd`命令结合命令代换和`pwd`命令来实现。`cd "$(dirname "$0")"`将当前路径切换到脚本所在路径，然后使用`pwd`命令获取该路径，并将结果存储在`curPath`变量中。最后，使用`touch`命令在该路径下创建1.txt文件。

# 8.算数代换

算术代换（Arithmetic Substitution）是一种在Shell中进行数值计算的机制，使用双圆括号`((...))`来表示。在算术代换中，Shell会将双圆括号中的表达式作为数值进行计算，并返回计算结果。

以下是一些示例说明如何使用算术代换：

使用双圆括号进行算术计算：

```bash
VAR=45
echo $((VAR + 3))
```

在上述示例中，`$((VAR + 3))`会将变量`VAR`的值（45）与3相加，并返回计算结果。

使用不同进制进行数值解释：

```bash
echo $((8#10 + 11))
echo $((16#10 + 11))
```

在上述示例中，`8#10`表示将后面的数字按照八进制进行解释，`16#10`表示将后面的数字按照十六进制进行解释。然后，进行相应的数值计算并返回结果。

需要注意的是，算术代换中只能使用`+`、`-`、`*`、`/`和`()`等算术运算符，且只能进行整数运算。

在示例中，`s((SVAR+3))`和`[VAR+3]`是不正确的写法。正确的写法应该是`((VAR+3))`或`echo $((VAR+3))`。

# 9.转义字符

在Shell中，反斜杠（`\`）可以用作转义字符，用于去除紧跟其后的单个字符的特殊意义。换句话说，反斜杠告诉Shell将紧跟其后的字符视为字面值而不是特殊字符。

以下是关于反斜杠的一些示例：

1. 转义特殊字符：

   ```bash
   #!/bin/bash
   echo \$SHELL
   ```
   
   
   
   ~~~bash
   echo \\
   ~~~
   
   
   
   在上述示例中，`\$SHELL`和`\\`使用反斜杠进行转义，将其后的字符视为字面值。因此，`\S`被解释为"S"，而`\)`被解释为")"。
   
2. 创建文件名包含特殊字符的文件：

   ```
   touch \s\ \S
   ```

   在上述示例中，通过使用反斜杠转义空格字符，可以创建一个文件名为"S "（S后面有一个空格）的文件。

# 10 单引号和双引号

在Shell脚本中，单引号（'）和双引号（"）都用作字符串的界定符，但它们有不同的行为方式。

1. 单引号（'）：

   单引号用于创建保持字符串的字面值的字符串。在单引号字符串中，所有字符都被视为普通字符，不进行变量扩展、命令替换或特殊字符转义。

   例如：

   ```bash
   echo 'SHELL'
   # 输出：SHELL
   
   echo 'ABC\'
   # 输出：ABC\
   ```

   在单引号字符串中，无法直接嵌入单引号字符。如果需要在单引号字符串中使用单引号，可以通过拼接字符串或转义字符的方式实现。

2. 双引号（"）：

   双引号用于创建字符串，并支持变量扩展和特殊字符转义。

   在双引号字符串中，变量会被展开为其对应的值，命令替换会执行替换操作，而特殊字符可以通过转义字符进行转义。

   例如：

   ```bash
   VAR="World"
   echo "Hello, $VAR!"
   # 输出：Hello, World!
   
   echo "ABC\$"
   # 输出：ABC$
   ```

   在双引号字符串中，变量会被展开为其对应的值（通过`$`进行标识），而特殊字符可以通过反斜杠进行转义。

总结起来，单引号保持字符串的字面值，不进行变量扩展、命令替换和特殊字符转义。双引号支持变量扩展和特殊字符转义。

作为有经验的Shell程序员，确实在使用变量作为参数传递时，习惯性地将变量用双引号括起来是一个很好的做法，特别是当变量的值中包含空格或其他特殊字符时。

双引号的使用可以确保传递的参数被当作一个整体进行处理，而不会被解析为多个独立的片段。这对于保留变量值中的空格或其他特殊字符的完整性非常重要。

​	以下是一些示例来说明这个问题：

```bashz
var='a b'
rm  $var        # 假设这是一个命令，参数是变量var的值
rm "$var"   # 假设这是一个命令，参数是变量var的值
```

在上述示例中，如果没有使用双引号括起变量`$var`，那么Shell会将其解析为两个独立的参数："a"和"b"。这可能导致命令无法按预期工作，或者产生错误。

通过使用双引号将变量括起来，Shell会将整个变量作为一个参数传递给命令，确保参数的完整性。在上述示例中，`Svar`和`rm`命令将正确处理变量`var`的值。

# 11 条件测试

在Shell中，test命令用于测试条件是否成立，并返回相应的退出状态码。如果测试结果为真，则该命令的退出状态为0，如果测试结果为假，则退出状态为1。

方括号（[）是test命令的等效形式，只是使用了不同的语法。方括号命令的参数与test命令相同，只是需要在方括号前后加上空格，并在方括号内部使用空格将各个参数分隔开。

以下是对您提供的示例进行解释：

```
var=2
test $var -gt 1
echo $?
```

在这个示例中，`test $var -gt 1`用于测试变量`var`是否大于1。如果是，则`test`命令返回退出状态码0，否则返回退出状态码1。接下来，`echo $?`用于打印上一条命令的退出状态码。

同样地，`[ $var -gt 3 ]`使用方括号形式进行条件测试，判断变量`var`是否大于3。如果是，则方括号命令返回退出状态码0，否则返回退出状态码1。

总结起来，test命令和方括号（[）用于在Shell中进行条件测试。它们可以用于检查各种条件，包括数值比较、字符串比较、文件检查等。请注意保持参数之间的空格，并根据测试结果检查命令的退出状态码。

- `(EXPRESSION)`：表达式为真。
- `!EXPRESSION`：表达式为假。
- `EXPRESSION1 -a EXPRESSION2`：同时满足EXPRESSION1和EXPRESSION2。
- `EXPRESSION1 -o EXPRESSION2`：满足EXPRESSION1或EXPRESSION2中的任意一个。
- `-n STRING`：字符串STRING的长度非零。
- `STRING`：等同于`-n STRING`，即字符串STRING的长度非零。
- `-z STRING`：字符串STRING的长度为零。
- `STRING1 = STRING2`：字符串STRING1和STRING2相等。
- `STRING1 != STRING2`：字符串STRING1和STRING2不相等。
- `INTEGER1 -eq INTEGER2`：整数INTEGER1等于INTEGER2。
- `INTEGER1 -ge INTEGER2`：整数INTEGER1大于或等于INTEGER2。
- `INTEGER1 -gt INTEGER2`：整数INTEGER1大于INTEGER2。
- `INTEGER1 -le INTEGER2`：整数INTEGER1小于或等于INTEGER2。
- `INTEGER1 -lt INTEGER2`：整数INTEGER1小于INTEGER2。
- `INTEGER1 -ne INTEGER2`：整数INTEGER1不等于INTEGER2。
- `FILE1 -ot FILE2`：判断FILE1是否比FILE2旧（修改时间早于文件2）。
- `-b FILE`：判断FILE是否为块设备。
- `-C FILE`：判断FILE是否为字符设备。
- `-d FILE`：判断FILE是否为目录。
- `-e FILE`：判断FILE是否存在（存在则为真）。
- `-f FILE`：判断FILE是否为普通文件。
- `-h FILE` 或 `-L FILE`：判断FILE是否为符号链接。
- `-k FILE`：判断FILE的粘着位是否已设置。
- `-O FILE`：判断当前用户是否为FILE的所有者。
- `-0 FILE`：判断FILE是否存在（存在则为真）。

中括号是test的一个等效命令，所以[ ]两端要有空格，后面的参数都是该命令的参数，

# 12 if分支结构

在Shell编程中，条件判断是非常常见和重要的部分，而if语句是一种用于实现条件判断和分支控制的结构。if语句允许根据条件的真假执行不同的代码块。下面我将详细讲解Shell编程中的if分支结构。

if语句的基本语法如下：

```bash
if condition
then
    # 代码块1，条件为真时执行的代码
else
    # 代码块2，条件为假时执行的代码（可选）
fi
```

在这个语法中，`condition`是一个条件表达式，用于判断真假。如果`condition`为真，则执行`then`后的代码块1，否则执行可选的`else`后的代码块2。

另一种形式的if语句是使用elif（即else if）来实现多个条件判断，例如：

```bash
if condition1
then
    # 代码块1，条件1为真时执行的代码
elif condition2
then
    # 代码块2，条件2为真时执行的代码
else
    # 代码块3，以上条件都为假时执行的代码（可选）
fi
```

在这个语法中，首先判断`condition1`，如果为真则执行代码块1；如果为假，则继续判断`condition2`，如果为真则执行代码块2；如果以上条件都为假，则执行可选的代码块3。

下面是一个示例，演示了if语句的使用：

```bash
#!/bin/bash

score=80

if [ $score -ge 90 ]; then
    echo "优秀"
elif [ $score -ge 80 ]; then
    echo "良好"
elif [ $score -ge 60 ]; then
    echo "及格"
else
    echo "不及格"
fi
```

在这个示例中，根据变量`score`的值进行成绩判断。根据条件的真假，分别输出不同的结果。

在if语句中，条件表达式可以使用各种比较运算符（如`-eq`、`-ne`、`-lt`、`-gt`、`-le`、`-ge`）来比较数字，也可以使用字符串比较运算符（如`=`、`!=`）来比较字符串。此外，还可以使用逻辑运算符（如`-a`、`-o`）进行多个条件的组合。

在if语句中，代码块可以包含任意Shell命令、其他条件语句、循环结构等。

需要注意的是，if语句的每个代码块都需要以关键字`then`开头，并以关键字`fi`结尾。`then`和`fi`之间的代码块可以是单行语句，也可以是多行语句。另外，if语句中的方括号`[]`用于表示条件判断，需要注意在方括号内外使用适当的空格。

![image-20240319170500405](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202403191705482.png)

&&：逻辑与运算符

- `command1 && command2`：表示如果 `command1` 成功执行（退出状态为零），则执行 `command2`。
- `command1` 和 `command2` 可以是任意的命令或命令序列。
- 如果 `command1` 的退出状态为非零（表示执行失败），则 `command2` 不会被执行，并且整个命令序列的退出状态也将是非零。
- `&&` 具有 short-circuit 特性，即如果前一个命令返回非零退出状态，后续的命令将被跳过。
- `&&` 可以用于串联多个命令，只有前一个命令成功执行后，才会执行后续的命令。

示例：

```shell
make clean && make
```

如果 `make clean` 成功执行（退出状态为零），则执行 `make` 命令。

||：逻辑或运算符

- `command1 || command2`：表示如果 `command1` 执行失败（退出状态非零），则执行 `command2`。
- `command1` 和 `command2` 可以是任意的命令或命令序列。
- 如果 `command1` 的退出状态为零（表示执行成功），则 `command2` 不会被执行，并且整个命令序列的退出状态也将是零。
- `||` 也具有 short-circuit 特性，即如果前一个命令返回零退出状态，后续的命令将被跳过。
- `||` 可以用于根据命令执行结果选择不同的处理路径。

示例：

```
make install || echo "Installation failed"
```

如果 `make install` 执行失败（退出状态非零），则输出 "Installation failed"。

这些逻辑运算符可以帮助您根据命令执行的成功或失败状态来控制命令之间的执行流程。它们常用于自动化脚本和条件执行的场景中，以便根据命令执行结果采取相应的操作。

# 13.case 分支结构

在Shell编程中，`case`语句用于根据模式匹配执行不同的操作。`case`语句类似于其他编程语言中的`switch`语句，可以根据不同的条件执行不同的代码块。

`case`语句通常具有以下结构：

```shell
case expression in
    pattern1)
        # 执行 pattern1 匹配的操作
        ;;
    pattern2)
        # 执行 pattern2 匹配的操作
        ;;
    pattern3)
        # 执行 pattern3 匹配的操作
        ;;
    *)
        # 如果没有匹配任何模式，则执行默认操作
        ;;
esac
```

解释上述结构中的各个部分：

- `expression`：要进行匹配的表达式或变量。
- `pattern1`、`pattern2`、`pattern3`：不同的模式，用于匹配`expression`的值。
- `)`：每个模式的结束标记。
- `# 执行 pattern 匹配的操作`：在匹配到相应的模式时，执行对应的操作。
- `;;`：每个模式操作的结束标记。它表示一个模式的操作结束，并开始匹配下一个模式。
- `*`：通配符，表示其他未匹配到的情况。
- `# 如果没有匹配任何模式，则执行默认操作`：在没有匹配到任何模式时，执行的默认操作。
- `esac`：`case`语句的结束标记。

下面是一个示例，演示如何使用`case`语句根据不同的条件执行不同的操作：

```shell
#!/bin/bash

fruit="apple"

case $fruit in
    "apple")
        echo "Selected fruit is apple"
        ;;
    "banana")
        echo "Selected fruit is banana"
        ;;
    "orange")
        echo "Selected fruit is orange"
        ;;
    *)
        echo "Unknown fruit"
        ;;
esac
```

在上述示例中，根据变量`fruit`的值，`case`语句进行模式匹配。如果`fruit`的值是"apple"，则执行第一个模式下的操作，输出"Selected fruit is apple"。如果`fruit`的值是"banana"，则执行第二个模式下的操作，输出"Selected fruit is banana"。如果`fruit`的值是"orange"，则执行第三个模式下的操作，输出"Selected fruit is orange"。如果`fruit`的值不匹配任何模式，则执行默认操作，输出"Unknown fruit"。

`case`语句还支持使用模式匹配的特殊符号和正则表达式，使匹配更加灵活和强大。您可以在模式中使用通配符（`*`、`?`）和正则表达式来进行更复杂的匹配。

![image-20240319174939315](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202403191749451.png)



# 14 for循环

在Shell脚本中，`for`循环用于遍历列表或范围，并执行一系列的操作。它是一种常用的控制流程结构，用于重复执行相同或类似的任务。

Shell中的`for`循环有多种语法形式，包括遍历列表、遍历范围和遍历命令输出等。下面将详细介绍这些形式。

1. 遍历列表：

   ```bash
   for variable in list
   do
       # 执行循环体操作
   done
   ```

   在这种形式中，`list` 是一个由空格分隔的值列表，可以是字符串、变量、命令的输出结果等。循环将迭代`list`中的每个值，每次迭代将把当前值赋给`variable`，然后执行循环体中的操作。

   示例：

   ```bash
   fruits="apple orange banana"
   for fruit in $fruits
   do
       echo "I like $fruit"
   done
   ```

   在上述示例中，`fruits`变量包含了三个水果名称。`for`循环遍历`fruits`中的每个水果，将当前水果赋值给`fruit`变量，并输出"I like <水果名称>"。

2. 遍历范围：

   ```bash
   for variable in {start..end}
   do
       # 执行循环体操作
   done
   ```

   这种形式中，`start` 和 `end` 是起始和结束的整数值。循环将从`start`值迭代到`end`值（包括边界值），每次迭代将把当前值赋给`variable`，然后执行循环体中的操作。

   示例：

   ```bash
   for num in {1..5}
   do
       echo "Number: $num"
   done
   ```

   在上述示例中，循环将从1到5迭代，将当前数字赋值给`num`变量，并输出"Number: <当前数字>"。

3. 遍历命令输出：

   ```bash
   for variable in $(command)
   do
       # 执行循环体操作
   done
   ```

   在这种形式中，`command` 是一个命令或命令序列，它的输出将作为循环的列表。循环将迭代命令输出中的每个值，每次迭代将把当前值赋给`variable`，然后执行循环体中的操作。

   示例：

   ```bash
   for file in $(ls *.txt)
   do
       echo "Processing file: $file"
   done
   ```

   在上述示例中，`$(ls *.txt)` 执行了一个列出所有以 `.txt` 结尾的文件的命令，并将文件列表作为循环的输入。循环遍历文件列表，将当前文件名赋值给`file`变量，并输出"Processing file: <文件名>"。

`for`循环还支持使用`continue`和`break`语句来控制循环的执行流程。`continue`语句用于跳过当前迭代并继续下一次迭代，而`break`语句用于提前终止循环。

注意，在Shell脚本中，`for`循环的变量是局部变量，只在循环体内部有效。如果需要在循环外部使用循环变量的值，可以在循环外部定义相应的变量，并在循环内部赋值。

# 15 while 循环

在Shell脚本中，`while`循环用于重复执行一系列操作，直到给定的条件不再满足为止。`while`循环是一种常见的控制流程结构，用于处理需要基于条件进行迭代的任务。

Shell中的`while`循环有以下语法形式：

```shell
while condition
do
    # 执行循环体操作
done
```

在这种形式中，`condition` 是一个用于判断循环是否继续执行的条件表达式。只要`condition`的结果为真（非零），循环体就会被执行；一旦`condition`的结果为假（零），循环就会终止。

循环体中的操作将被重复执行，直到`condition`的结果为假。在每次循环迭代时，会先判断`condition`的值，然后根据判断结果决定是否执行循环体。

示例：

```shell
count=1
while [ $count -le 5 ]
do
    echo "Count: $count"
    count=$((count + 1))
done
```

在上述示例中，循环从1开始，每次迭代输出当前的计数值，并将计数器`count`递增。循环将持续执行，直到`count`的值大于5，此时条件`$count -le 5`不再满足，循环终止。

`while`循环中可以使用各种条件表达式来判断循环是否继续执行。条件表达式可以使用比较运算符（如 `-lt`、`-gt`、`-eq` 等）进行数值比较，也可以使用逻辑运算符（如 `-a`、`-o`）进行逻辑判断。此外，还可以通过命令的执行结果来判断条件。

示例：

```shell
counter=10
while [ $counter -gt 0 -a -f "file.txt" ]
do
    echo "Counter: $counter"
    counter=$((counter - 1))
done
```

在上述示例中，循环将持续执行，只要`counter`的值大于0且文件`file.txt`存在。每次迭代时，输出当前计数值，并将计数器递减。

`while`循环还支持使用`continue`和`break`语句来控制循环的执行流程。`continue`语句用于跳过当前迭代并继续下一次迭代，而`break`语句用于提前终止循环。

需要注意的是，在`while`循环中，如果循环条件一开始就为假，循环体内的操作将不会执行，即循环体可能根本不执行。











