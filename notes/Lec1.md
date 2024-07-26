# lec0

## Linux历史

### 溯源

- 1969 **Unix操作系统** 贝尔实验室 Ken Thompson & Dennis Ritchie
- 1980年代 **Minix操作系统** Andrew S.Tanenbaum 用于教学
- 1991 **linux操作系统** Linus Torvalds开发

## Linux 和Linux发行版

### Linux

> 指操作系统内核，用于管理硬件资源，提供基本服务

#### Linux发行版

> 将Linux内核与应用程序、库程序、用户界面等打包，形成一个完整的操作系统

### 主流

- 最早：redhat debian
- 目前：ubuntu Debian

## Shell prompt

```bash
ubuntu@ubuntu2204:~$
#用户名  主机名   当前位置 当前身份
```

- ~ 代表用户目录
- / 代表根目录
- . 代表当前目录
- ..代表上层目录

### 快捷键

- `ctrl + l` 清屏
- `ctrl + shift + c` 复制
- `shift + insert ` 粘贴

### 常见指令

- `echo`

  > echo 是一个用于在终端或命令行界面中打印文本的命令。它常用于输出消息或变量的值。允许空格，可以使用\来多行输入

- `which`

  > 用于查找并显示可执行文件的路径。它会显示你输入的命令在系统中的实际位置。
  >
  > which [command]
  >
  > 输出绝对路径

- `type`

  >用于显示指定命令的类型以及其位置。它比 `which` 更加详细，因为它不仅可以显示命令的路径，还可以告诉你命令是内建命令、别名还是外部命令。
  >
  >type [command]

- `printenv`
  
  > 用于打印当前用户环境变量的值。环境变量是系统和应用程序用来配置环境的变量，它们包含有关系统配置、用户设置等信息
  >
  > 没有参数则打印所有环境变量及其值
  
- `echo $PATH` 

  >  显示环境变量,其中$用于解析参数

- `grep`

  > 用于在文件或标准输入中搜索符合指定模式的行，并将这些行输出。`grep` 可以使用正则表达式来进行模式匹配。
  >
  > grep [options] pattern [file..]

- `pwd`

  > 显示当前工作目录完整路径

#### 路径相关指令

> 路径是一组使用正斜杠/分隔的目录

- 绝对路径
  - /开头
- 相对路径
  - 相对于当前目录的路径
- 切换路径
  - 使用cd
  - .表示当前目录
  - ..表示上层目录
  - cd ~ 进入用户目录 /home/usr
  - cd - 进入上一个的目录

`ls`

#### 帮助

- `help`

  > [指令] --help/-h

- `man`

  >  man + 指令名
  
- `tldr`

  > tldr + command

### 文件信息

例如在ls -lh指令下 有

`-rwsr-xr-x 1 root root 63K Apr  9 15:01 /usr/bin/passwd`

`文件权限 硬链接数 文件所有者 文件所属组 大小 修改时间 文件名 （->指向实际的文件数据块）`

#### 权限

> 如drwxr-xr--
>
> 一个十位，首位代表文件类型
>
> - d——目录
>
> - \- ——普通文件
>
> - l——符号链接
>
> 后九位三个一组
>
> - 文件**所有者**权限
> - 与文件所有者**相同组**的权限
> - 其他用户权限
>
> 三个分别为
>
> - r：可读
> - w：可写
> - x：可执行
>
> 特殊：
>
> `drwxrwxrwt 15 root root 4.0K Jul 24 12:44 tmp`
>
> t代表**粘滞位**（sticky bit），通常用于目录，确保只有文件所有者、目录所有者、root用户可以删除或重命名目录中的文件
>
> 粘滞位通常用于 `/tmp` 目录，这个目录通常是所有户都可以写入的公共目录。通过设置粘滞位，管理员可以确保用户不能删除或修改其他用户在 `/tmp` 中创建的文件。
>
> `-rwsr-xr-x 1 root root 63K Apr  9 15:01 /usr/bin/passwd`
>
> s代表（Setuid/Setgid)
>
> 表示表示为 `s` 出现在文件的执行权限位置（`rws`）时，表示该文件在执行时会以文件所有者的权限运行，而不是执行者的权限。
>
> 对于可执行文件，`s` 位设置后，该文件在运行时将以其所有者的权限执行。

#### 权限修改

`chmod`

##### 符号模式

- 'r'：读权限
- 'w'：写权限
- 'x'：执行权限

三类用户

- 'u'：文件所有者(user)
- 'g'：文件所属组(grou)
- 'o'：其他用户(others)
- 'a'：所有用户(all)

添加

`chmod u+x file`

删除

`chomd o-x file`

设置

`chmod u=rwx,o=rw,o=r file`

##### 八进制模式

- r：4
- w：2
- x：1

组合

- rwx：7
- rw：6
- rx：5
- r：4

设置

`chmod 755 file`

`chmod 644 file`

#### Passwd文件

> 储存的是用户信息，包括用哈希值进行加密的密码信息

### 文件操作

- `mv`

  > 重命名和移动文件指令
  >
  > - mv [options] source destination
  >
  > 选项
  >
  > -i 覆盖时询问确认
  >
  > -u 只在源文件更新或目标不存在才移动
  >
  > -v 显示详细操作过程

  - mv a.txt b.txt
  - mv dir-1 dir-2
  - mv a.txt dir/

- `cp`

  > 用于复制文件或目录
  >
  > - cp [options] source destination

  - cp a.txt b.txt 

    复制并重命名副本名

  - cp a.txt ../

  - 复制并将副本储存在上层目录

- `rm`

  > 用于删除文件和目录。使用时需要小心，因为删除的文件或目录通常无法恢复。
  >
  > rm [options] file
  >
  > -r 递归操作
  >
  > -f 强制删除
  >
  > 可以用通配符
  >
  > rm *

- `rmdir`

  > 用于删除空目录。与 `rm` 不同，`rmdir` 仅能删除空目录，如果目录中有文件或子目录，则无法删除。
  >
  > rmdir [options] directory
  >
  > -p 可以递归删除目录及其所有父目录

- mkdir

  > 用于创建新目录
  >
  > mkdir directory

### 重定向

- 输入流

  - 默认键盘

- 输出流

  - 默认屏幕

- 重定向流到文件

  - \> file

    > 将输入流输出到hello.txt

    - echo hello > hello.txt
    - cat hello.txt

  - < file

    > 将文件内容作为参数输入到前面的指令

    - cat < hello.txt
    - cat < hello.txt > hello2.txt

  - \>\>

    > 将新内容追加到现有文件中，不存在也会创建新文件夹

    - cat < hello.txt \>\> hello2.txt

### 管道

`|`

> 将一个程序的输出和另一个程序的输入连接起来

- `ls -l / | tail -n1` 显示根目录文件信息输出最后一行

  >  注意：有的指令并不能直接从标准输出读取内容

- `ls -l / | rm` 无法执行，rm没有参数

- `ls -l / | xargs rm`

  > 通过xargs读取标准输出的内容，传给rm

### sudo命令

- `sudo -i`

  > 模拟root用户环境，以root用户身份启动一个新的shell会话

- `sudo -su`

  > 以当前用户权限运行su，再切换到root用户，但是不模拟root用户环境设置，适用于提升权限的操作

### 软件包更新

`apt-cache -n search 软件包名`

- 搜索软件包

`apt install 软件包名`

- 安装软件包

`apt --purge remove 软件包名`

- 卸载软件包

`apt list --installed | grep 软件包名`

`dpkg -l 软件包名`

- 查看软件包是否安装

`dpkg -L 软件包名`

- 查看已安装软件包中包含的文件

`dpkg -S command`

- 查看某个命令是由哪个软件包提供

