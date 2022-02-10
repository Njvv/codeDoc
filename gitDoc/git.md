# Git



## Git文件状态

已修改（modified）`工作区`：修改了文件，但是还没有存到数据库中；

已暂存（committed）`暂存区`：对一个已修改的文件的当前版本做了标记，使之包含在下次提交的快照当中；

已提交（staged）`git目录`：数据已经安全的保存在本地数据库当中；



## Git配置

### 配置目录

系统`/etc/gitconfig`：系统上每一个用户的通用配置；

```bash
git config --system
```



用户`~/.gitconfig or ~/.config/git/config`：只针对当前用户；

```bash
git config --global
```



仓库`.git/config`：只针对当前选择的仓库；

```bash
git config --local
```



每一个级别会覆盖上一个级别的配置；

可以通过以下命令查看所有的配置，以及他们所在的文件；

```bash
git config --list --show-origin
```

### 用户信息

安装完git之后，第一件事情就是配置git的用户信息，每一个git提交都会用到这些信息，他们会写入到每一次提交中，不可更改；

```bash
git config --global user.name "user_name"
git config --global user.email ****@exampel.com
```

### 检查配置

如果需要检查配置情况，可以通过以下命令检查当前的配置信息；

```bash
git config --list
```

如果需要检索某一项配置，可以执行以下命令；

```bash
git config <key>
# git config user.name
```



以上命令会输出重复的变量名，因为会输出所有配置目录（系统、用户）中的配置信息；

可以通过以下命令查询哪个配置文件最后设置了该值；

```bash
git config --show-origin <key>
```



## 获取Git仓库

### 获取类型

1. 将尚未进行版本控制的本地目录转换为Git目录；
2. 从其他服务器克隆一个已经存在的Git仓库

### 在已存在的目录中初始化仓库

通过以下命令初始化一个空白的仓库

```bash
cd /User/user/my_project
git init
```

通过以下命令将当前文件夹中的既有文件进行版本控制

```bash
git add *.c
git add LICENSE
git commit -m 'initial project version'
```

### 克隆现有仓库

如果想获取一个已有仓库的拷贝，需要用到`git clone`命令，当执行`git clone`命令时，默认会拉取仓库中的每一个文件的每一个版本；

克隆仓库，并将其在本地建立一个对应名字的仓库，可以执行以下命令；

```bash
git clone <url>
```

克隆仓库，并在其在本地命名为自定义的名字，可以执行以下命令；

```bash
git clone <url> new_name
```

Git支持多种协议（https，git，ssh），如下

```bash
git clone https://***
git clone git://***.git
git clone user@server:path/to/repo.git
```



## 使用Git

### 检查文件状态

```bash
git status
```

### 跟踪文件状态

跟踪：Git会记录文件的变更情况；

```bash
git add file_name/path
```

### 暂存已修改的文件

```bash
git add file_name/path
```

`git add`是一个多功能命令：

1. 跟踪新文件；
2. 已跟踪的文件放入暂存区；
3. 合并时，把有冲突的文件标记为已解决状态；

`git add`命令可以理解为精确的将内容添加到下一次提交当中；

注：`git add`在前两项作用中，均可以理解为将文件放入暂存区，并标记跟踪，只是对于已跟踪的文件不存在再跟踪这种说法；其中放入暂存区就代表着文件被跟踪；

### 修改已暂存的文件

如果将修改的文件暂存后，再进行修改，运行`git status`此时该文件会同时出现在暂存区和非暂存区，因为git记录了两个版本的文件：暂存版本、暂存后修改的版本，如果此时进行提交，那么提交的会是暂存版本；

### 状态简览

`git status`输出的结果过于繁琐，可以调整命令为如下

```bash
git status -s
```

```bash
$ git status -s
>>
   M README
  MM Rakefile
  A  lib/git.rb
  M  lib/simplegit.rb
  ?? LICENSE.txt
```

左侧表示暂存区，右侧表示工作区，`A`表示新添加到暂存区域，`？？`表示新添加的未跟踪文件，`M`表示修改过，`MM`表示文件在暂存区后又被进行了修改；

### 忽略文件

通过管理`.gitignore`文件，可以让指定文件不受git控制；

- 可以使用标准的glob模式匹配，他会递归的应用在整个工作区；
- 匹配模式可以以`\`开头，防止递归；
- 匹配模式可以以`\`结尾，指定目录；
- 要忽略指定模式以外的文件或目录，可以在模式前加上`!`;

### 提交更新

提交更新至暂存区

```bash
git commit -m 'msg'
```

跳过暂存直接提交更新

```bash
git commit -a -m 'msg'
```

### 移除文件

从Git中移除文件，就必须要从跟踪文件清单`暂存区`中移除；

```bash
git rm file/path
```

强制删除已经处于暂存区或者之前已经修改过的文件，需要增加`-f`;

```bash
git rm -f file/path
```

仅删除版本管理，而不从本地磁盘删除，需要增加`--cached`;

```bash
git rm --cached file/path
```

删除文件支持glob模式匹配，但是对于通配符号需要注意加入`\`；

### 移动文件

Git不跟踪文件的移动、重命名；

可以通过以下命令进行移动

```bash
git mv file_from file_to

# 等效于
mv file_from file_to
git rm file from
git add file_to

```

### 查看历史

可以通过以下命令查看提交历史；

```bash
git log
```

### 撤销操作

在git中有些操作是不可逆的，以下说明部分撤回操作；

> 替换提交

```bash
git add file
git commit -m 'msg'

# 修改操作

git add file
git commit --amend -m 'msg'  # 此时该提交会替代第一次提交 
```

> 取消暂存

```bash
git reset HEAD file # 取消对于file的暂存
```

> 撤销修改

```bash
git checkout -- file # 还原至上一次提交的样子（有风险）
```
