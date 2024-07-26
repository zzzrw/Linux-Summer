# Lec2

## Vim

### 历史

- 1976 Bill Joy发布vi编辑器
- 1991 Bram Moolenaar 发布Vim
- Vim是个有“模式”的编辑器

### 模式

`Normal`

- 默认情况，esc返回该模式

`Insert`

- 输入文本使用，使用`i`/`a`进入

`Replace`

- 替换文本使用，使用`r/R`进入

`Command-line`

- 执行命令，`:`进入。使用`/`或`?`搜索也算命令模式。按`enter`结束

`Visual`

- 选定文本块，按`v`进入，`shift-v`按行，`ctrl-v`按列

`Select`

### 基本操作

- `esc`返回正常模式

- `:wq`保存并退出
- `help key | command` 查询某个按键或命令的帮助

### 缓存、标签页和窗口

#### 缓存

> Vim可以打开多个标签页，每个标签页可以包含多个窗口，每个窗口对应某个缓存，但并不是一一对应，可能多对一

#### 窗口

`:sp` 水平分隔

`:vsp`垂直分隔

`ctrl-w +[motion]/w` 切换窗口

#### 标签操作

`tabnew [+file]` 打开新标签

`tabnext`/`tabn`/快捷键`gt`  切换标签

`tabclose`/`tabc` 关闭

### 自定义

> 使用~/.vimrc这个配置文件，实现自定义vim

## Shell脚本

### 变量

- **赋值**
  - **foo=bar **中间不能加空格

- **获取变量值**

  - $foo
  - echo $foo

- **单引号和双引号**

  > 双引号存在转义和变量替换，而单引号表示纯文本

  - echo "$foo"
  - echo '$foo'

### 函数

```bash
mcd () {
	mkdir -p "$1"
	cd "$1"
}
```

#### 执行函数的方法

- 直接在shell中输入函数内容

  之后调用函数

- 将脚本保存

  利用`source script`加载脚本后调用

#### 退出码结合 && ||

```bash
false || echo "Oops, fail"
true || echo "Will not be printed"
true && echo "Things went well"
false || echo "Will not be printed"
false ; echo "This will always run" 
```

#### 命令替换、进程替换

- 命令替换

  `$(CMD)` 将命令输出插入另一个命令

  - foo=$(pwd)
  - echo $foo
  - echo "We are in $(pwd)"

- 进程替换 <(CMD)
  - 是一种将命令的输出作为输入传递给另一个命令的机制。这在 shell 编程中非常有用，特别是在 Bash 和 Zsh 中。它允许你在不实际创建临时文件的情况下，将一个命令的输出传递给另一个命令作为输入。
  - `diff <(ls) <(ls..)`
  - `cat <(date)`

## 查找

#### find

`find [path] [cond] [op]`

常见条件

-name

#### grep

> 用于在文件或标准输入中搜索符合指定模式的行，并将这些行输出。`grep` 可以使用正则表达式来进行模式匹配。

`grep [options] pattern [file]`

##### 常见参数

- `-i`：忽略大小写

- `-r` / `-R` 递归搜索目录

- `-v` 反转匹配

- `-l`：仅显示包含匹配模式的文件名

- `-n`：显示匹配行的行号

  ```bash
  zzzrw@zzzrw:~$ cat time.log | grep -n "29"
  1:29.258
  5:290.944
  ```

- -c 显示匹配行的计数

### Shell命令

#### history

- `history`

  > 查看历史命令
  >
  > 通常HISTSIZE=1000 shell 会话保存历史记录最大行数为1000
  >
  > HISTFILESIZE保存历史记录

  - `history | grep / find` 用于查找
  - 利用!找到先前1条指令
    - `!!` ：上一条指令
    - `!cd`：上一条cd指令
    - `!?cd?`：任何包含cd的指令

- `ctrl + r`

  - 对命令历史记录进行回溯搜索
  - 连续使用`ctrl + r`来寻找不断上一条

- 基于历史命令自动补全

  - zsh
    - 根据最近使用过的开头相同的命令，动态地对当前的shell命令进行补全

- 命令保护

  如果不希望历史记录保存文件，可以使用空格开。这个设定由.bashrc中HISTCONTROL=ignorespace来实现 即忽略空格开头的命令