# Lec1

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