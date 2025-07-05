# **lab0**

### 思考题

#### thinking 0.1

题目：

![image-20250313082921861](C:\Users\hp\Desktop\Agarwood\题源\image-20250313082921861.png)

指令模拟过程：

![image-20250313083239378](C:\Users\hp\Desktop\Agarwood\题源\image-20250313083239378.png)

![image-20250313083311377](C:\Users\hp\Desktop\Agarwood\题源\image-20250313083311377.png)

**思考**：git status 可以查看当前文件的状态（未追踪，已暂存未提交，已提交）

| 文件            | 状态变化                                          |
| --------------- | ------------------------------------------------- |
| `Untracked.txt` | `README.txt` 处于 Untracked（未追踪）状态         |
| `Stage.txt`     | `README.txt` 处于 Staged（已暂存） 状态           |
| `Modified.txt`  | `README.txt` 处于 Modified（已修改但未提交） 状态 |

指令分析：

- `git add` 将文件从 Untracked（未追踪）变为 Staged（已暂存）
- `git commit` 将 Staged 文件提交到 Git 历史记录
- 重新修改文件后，它从 Tracked（已追踪）变为 Modified（已修改），需要重新 `git add` 和 `git commit`

#### thinking 0.2

题目：

![image-20250313082407081](C:\Users\hp\Desktop\Agarwood\题源\image-20250313082407081.png)

git 工作模式示意图：

![image-20250313082554284](C:\Users\hp\Desktop\Agarwood\题源\image-20250313082554284.png)

**总结**：add the file 和 stage the file 对应 git add 指令，add 本质上就是 staging 的过程，"staging" 是指将文件放入 Git 的暂存区（Staging Area），等待提交；commit the file 对应 git commit 指令，会将暂存区中的文件保存到 Git 本地仓库，形成一个新的提交（commit）

#### thinking 0.3

题目：

![image-20250313081640742](C:\Users\hp\Desktop\Agarwood\题源\image-20250313081640742.png)

①如果 `print.c` 还存在于 Git 的版本管理中（即 `git rm` 未执行），可以使用以下命令恢复：

```shell
git checkout -- print.c
```

`git checkout -- print.c` 可以从最新的提交版本中恢复 `print.c`

但这个方法**仅适用于** `print.c` 已被 Git 追踪过，并且仍然存在于 Git 历史记录中

②如果已经执行了 `git rm print.c`，但还**未提交**（即 `git commit` 还没有执行），可以使用：

```Shell
git checkout -- print.c
```

③如果 `git commit` 也已经执行了，则需要先回退版本，再进行恢复：

```shell
git reset HEAD~  # 撤销最近的一次提交
git checkout -- print.c  # 恢复文件
```

或者如果不想撤销整个提交，而只是恢复 `print.c`：

```shell
git checkout HEAD^ -- print.c
```

`git reset HEAD~`：撤销最近的一次提交，回到 `git commit` 之前的状态

`git checkout HEAD^ -- print.c` ：从前一次提交恢复 `print.c`，但不会影响其他文件

④如果 `hello.txt` 只是被 `git add` 了，还没有 `commit`，可以用：

```shell
git reset HEAD hello.txt
```

`git reset HEAD hello.txt`：将 `hello.txt` **从暂存区移除**，但不会删除本地文件，之后 `hello.txt` 仍然存在于工作目录中，不会影响其他提交

**示例**：

![image-20250313082305564](C:\Users\hp\Desktop\Agarwood\题源\image-20250313082305564.png)

#### thinking 0.4

题目：

![image-20250313080845910](C:\Users\hp\Desktop\Agarwood\题源\image-20250313080845910.png)

三次修改以及提交：

![image-20250313080902436](C:\Users\hp\Desktop\Agarwood\题源\image-20250313080902436.png)

 git log 可以显示历次的提交信息，而使用 git log –all –abbrev-commit –graph –decorate 则可以精简显示信息如下：

![image-20250313081034338](C:\Users\hp\Desktop\Agarwood\题源\image-20250313081034338.png)

使用 git reset –hard HEAD^ 可以回到当前提交的上一次提交状态，即从 3 修改回到 2  修改状态：

![image-20250313081141492](C:\Users\hp\Desktop\Agarwood\题源\image-20250313081141492.png)

使用 git reset –gard <hash> 可以回退到任何一个提交状态，也可以在回退之后再次回到后面的提交状态，即可以从 3 回到 1，也可以再从 1 回到 3，这里的 <hash> 值只需要前 7 位即可：

![image-20250313081357877](C:\Users\hp\Desktop\Agarwood\题源\image-20250313081357877.png)

**总结**：本例介绍了 git reset –hard 的用法，可以用以下两种形式

git reset –hard HEAD^ 回退到上一个提交状态

git reset –hard <hash> 回退到任意一个哈希值为 hash 的提交状态

#### thinking 0.5

题目：

![image-20250312233259198](C:\Users\hp\Desktop\Agarwood\题源\image-20250312233259198.png)

执行结果：

![image-20250312233335505](C:\Users\hp\Desktop\Agarwood\题源\image-20250312233335505.png)

**总结**：‘>’ 会用新的标准输出覆盖被输出文件的原有内容，‘>>’ 会把新的标准输出拼接到被输出文件的原有内容之后

#### thinking 0.6

![image-20250312233508722](C:\Users\hp\Desktop\Agarwood\题源\image-20250312233508722.png)

**command 内容**：command 为具有可执行权限的 sh 文件

![image-20250313001340479](C:\Users\hp\Desktop\Agarwood\题源\image-20250313001340479.png)

**test内容**：test 为具有可执行权限的 sh 文件

![image-20250313001422294](C:\Users\hp\Desktop\Agarwood\题源\image-20250313001422294.png)

**总结**：关键在于 echo 输出内容加单引号，不加引号，加双引号的区别，不加引号或加双引号的时候，echo 输出内容的所有 $ 变量会被解析，有值的赋值后输出，空变量输出空串；加单引号的时候，不进行任何变量解析， 会把字面量原样输出

①两次执行命令的区别：

![image-20250313000915146](C:\Users\hp\Desktop\Agarwood\题源\image-20250313000915146.png)

第一条命令：直接输出 echo Shell Start 这个字符串的内容到标准输出

第二条命令：把 echo Start Shell 这条命令的标准输出捕获，并且输出到标准输出，即为 Shell Start

②两次执行命令的区别：

![image-20250313000455794](C:\Users\hp\Desktop\Agarwood\题源\image-20250313000455794.png)

第一条命令：把 echo $c 这个字符串重定向输出到 file1 文件中，其中 c 的值会被代入，因为 c 本身是空，所以 file1 文件中只有 echo 这个字符串

第二条命令：同理，用双引号引起来和不用双引号都会把字符串中的变量代入相应的引用值

第三条命令：用单引号引起来的内容不会进行任何变量值引用，而是把字符串的内容原样输出，所以 file1 的文件就是 echo $c 这个字符串

第四条命令：echo 捕获并输出 echo $c > file1 这条命令的标准输出，而这条命令没有标准输出，所以输出为空

③其他例子：

![image-20250313001251981](C:\Users\hp\Desktop\Agarwood\题源\image-20250313001251981.png)

**总结**：echo 捕获的是某条命令的**标准输出**，无特殊情况时，会把其捕获到的标准输出输出到 stdout 中，可以用 echo 来捕获函数的返回值（这里的返回值指 stdout 而不是 exit code）

### 作业难点

#### T1

（1）完成一个简单的 C 语言判断回文数即可

（2）使用 Makefile 编译并链接形成可执行文件

（3）简单的 Shell 语法，提取文件的某些特定行并且重定向输出到目标文件中，后者可以用 sed p 参数结合管道符来实现

**思考**：

区别传参和标准输入，本例要求的是传参，即来自参数 $

```shell
input=$1
outut=$2
```

标准输入是来自 stdin：

```shell
read input
read outuput
```

（4）文件的复制，使用 cp 指令即可

**思考**：区别 mv 和 cp，前者是剪切，后者是复制

#### T2

完成简单的 shell 脚本，考察对 if 语句，判断语句，循环语句的掌握，代码如下：

```shell
#! /bin/bash                                                                  
for((i=1;i<=100;i++))
do
    if [ $i -ge '71' ]
    then
        rm "file${i}" -r     
    fi  
    if [ $i -ge '41' ] && [ $i -lt '71' ]
    then
        mv "file${i}" "newfile${i}"
    fi  
done
```

**总结**：test 指令可以用 [] 来简单代替，也可以用更加安全的 [[]] 来代替

#### T3

提取文件中包含特定内容的某些行，只输出行号到目标文件中，可以使用 grep，管道，结合 awk 命令实现，因为 C 文件中行号和正文中以：分开，因此我们可以规定 awk 中的输入分隔符为：，取第一列输出即可，代码如下：

```shell
grep -n "int" $input | awk -v FS=':' '{print $1}' > $output
```

#### T4

（1）修改文件中的某个字符串为新内容，并把修改后内容写回原文件，可以用 sed 命令结合其内置参数 s 配合 g 实现，代码如下：

```shell
sed -i "s/$old/$new/g" $input
```

（2）完成 Makefile 文件的递归调用

**总结**：递归调用 Makefile 文件的格式如下

我们可以在一个 makefile 文件中调用其他目录下的 makefile 文件

| 命令                      | 作用                                        |
| ------------------------- | ------------------------------------------- |
| `$(MAKE) -C subdir`       | 进入 `subdir` 目录，执行该目录的 `Makefile` |
| `$(MAKE) -C subdir clean` | 在 `subdir` 目录执行 `clean` 目标           |

示例：

```makefile
all:
	$(MAKE) -C src
```

递归调用也是一条命令（command），最好写在 all 的内部

### 实验感想

本次上机，exam 部分并未出现太大问题，主要问题出在 extr 部分，有以下需要改进的地方：

1. 对于 shell 的扩展指令理解不够全面，比如替换文件后缀，如何遍历一个目录下的所有文件等常用操作，不能第一时间想到对应的指令，导致思路不连贯；同时对于 sed 替换，grep 截取等语法记忆不牢，需要经常翻阅 help 文档，耽误大量调试时间
2. 知识面不够宽，对于 sort 函数，软链接等知识没有提前接触，现场学习耗费太多时间

### 参考文献

【黑马程序员Git全套教程，完整的git项目管理工具教程，一套精通git】 https://www.bilibili.com/video/BV1MU4y1Y7h5/?share_source=copy_web&vd_source=069a61898eba498b92493563cbd57459 ————其中有关 git 的理解和部分示意图来自此教程



![image-20250315095505430](../题源/image-20250315095505430.png)