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

- `ctrl + l` 粘贴
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
> t代表**粘滞位**（sticky bit），确保只有文件所有者、目录所有者、root用户可以删除或重命名
>
> 粘滞位通常用于 `/tmp` 目录，这个目录通常是所有用户都可以写入的公共目录。通过设置粘滞位，管理员可以确保用户不能删除或修改其他用户在 `/tmp` 中创建的文件。
>
> `-rwsr-xr-x 1 root root 63K Apr  9 15:01 /usr/bin/passwd`

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
