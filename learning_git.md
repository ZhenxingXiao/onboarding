## 1. 安装Git

下载地址：[Git for Windows](https://gitforwindows.org/)

安装时，一路下一步即可。

## 2. 配置Git

安装完成后，打开Git Bash，输入以下命令：

```bash
git config --global user.name "Your Name"
git config --global user.email "Your Email"
```

## 3. 创建版本库

版本库又名仓库，英文名repository，可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。

创建一个版本库非常简单，首先，选择一个合适的地方，创建一个空目录：

```bash
mkdir learngit
cd learngit
pwd
```

pwd命令用于显示当前目录。在我的机器上，这个仓库位于`/c/Users/lenovo/learngit`。

第二步，通过`git init`命令把这个目录变成Git可以管理的仓库：

```bash
git init
```

Git就会告诉你，这是一个空的Git仓库，而且当前目录下多了一个`.git`的目录，这个目录是Git来跟踪管理版本库的，千万不要手动修改这个目录里面的文件，否则，会把Git仓库给破坏了。

如果你没有看到`.git`目录，那是因为这个目录默认是隐藏的，用`ls -ah`命令就可以看见。

也不一定必须在空目录下创建Git仓库，选择一个已经有东西的目录也是可以的。不过，不建议你使用自己正在开发的公司项目来学习Git，否则造成的一切后果概不负责。

## 4. Git基本操作

### 4.1 添加文件

编写一个`readme.txt`文件，内容如下：

```txt
Git is a version control system.
Git is free software.
```

第一步，用命令`git add`告诉Git，把文件添加到仓库：

```bash
git add readme.txt
```

执行上面的命令，没有任何显示，这就对了，Unix的哲学是“没有消息就是好消息”，说明添加成功。

第二步，用命令`git commit`告诉Git，把文件提交到仓库：

```bash
git commit -m "wrote a readme file"
```

`-m`后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的，这样你就能从历史记录里方便地找到改动记录。

`git commit`命令执行成功后会告诉你，`1 file changed`：1个文件被改动（我们新添加的readme.txt文件）；`2 insertions`：插入了两行内容（readme.txt有两行内容）。

为什么Git添加文件需要`add`，`commit`一共两步呢？因为`commit`可以一次提交很多文件，所以你可以多次`add`不同的文件，比如：

```bash
git add file1.txt
git add file2.txt file3.txt
git commit -m "add 3 files."
```

### 4.2 查看状态

用`git status`命令可以让我们时刻掌握仓库当前的状态：

```bash
git status
```

`git status`命令可以让我们时刻掌握仓库当前的状态，上面的命令输出告诉我们，`readme.txt`被修改过了，但还没有准备提交的修改。

### 4.3 查看修改内容

如果`git status`告诉你有文件被修改过，用`git diff`可以查看修改内容：

```bash
git diff readme.txt
```

`git diff`顾名思义就是查看difference，显示的格式正是Unix通用的diff格式，可以从上面的命令输出看到，我们在第一行添加了一个`Git is a distributed version control system.`，第二行添加了一个`Git is free software.`。

### 4.4 查看历史记录

如果`git status`告诉你有文件被修改过，用`git diff`可以查看修改内容：

```bash
git log
```

`git log`命令显示从最近到最远的提交日志，我们可以看到3次提交，最近的一次是`append GPL`，上一次是`add distributed`，最早的一次是`wrote a readme file`。

如果嫌输出信息太多，看得眼花缭乱的，可以试试加上`--pretty=oneline`参数：

```bash
git log --pretty=oneline
```

### 4.5 版本回退

在Git中，用`HEAD`表示当前版本，也就是最新的提交`1094adb...`（注意我的提交ID和你的肯定不一样），上一个版本就是`HEAD^`，上上一个版本就是`HEAD^^`，当然往上100个版本写100个`^`比较容易数不过来，所以写成`HEAD~100`。

现在，我们要把当前版本`append GPL`回退到上一个版本`add distributed`，就可以使用`git reset`命令：

```bash
git reset --hard HEAD^
```

也可以指定回退到某个版本：

```bash
git reset --hard 1094a
```

### 4.6 查看命令历史

如果你用的是Windows系统，还需要告诉Git一个东西，以防Git使用了Windows自带的另一个命令`cmd`，而不是Git Bash。

确保你的电脑上有一个文本编辑器可以打开文本文件，如果没有，请自行安装。我们推荐[VS Code](https://code.visualstudio.com/)，它是一个开源的、跨平台的现代化文本编辑器。

在Git中，我们用`git reflog`查看命令历史，以便确定要回到未来的哪个版本。

```bash
git reflog
```

### 4.7 撤销修改

`git checkout -- file`可以丢弃工作区的修改：

```bash
git checkout -- readme.txt
```

`git checkout -- file`命令中的`--`很重要，没有`--`，就变成了“切换到另一个分支”的命令，我们在后面的分支管理中会再次遇到`git checkout`命令。

`git reset HEAD <file>`可以把暂存区的修改撤销掉（unstage），重新放回工作区：

```bash
git reset HEAD readme.txt
```

### 4.8 删除文件

`git rm`命令用于删除一个文件：

```bash
git rm test.txt
```

## 5. 远程仓库

### 5.1 添加远程仓库

要关联一个远程库，使用命令`git remote add origin git@server-name:path/repo-name.git`；

关联后，使用命令`git push -u origin master`第一次推送master分支的所有内容；

此后，每次本地提交后，只要有必要，就可以使用命令`git push origin master`推送最新修改；

### 5.2 克隆远程仓库

要克隆一个仓库，首先必须知道仓库的地址，然后使用`git clone`命令克隆。

Git支持多种协议，包括`https`，但通过`ssh`支持的原生`git`协议速度最快。

### 5.3 分支管理

Git分支十分强大，在团队开发中应该充分应用。

创建与合并分支

查看分支：`git branch`

创建分支：`git branch <name>`

切换分支：`git checkout <name>`

创建+切换分支：`git checkout -b <name>`

合并某分支到当前分支：`git merge <name>`

删除分支：`git branch -d <name>`

### 5.4 解决冲突

当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。

用`git log --graph`命令可以看到分支合并图。


## 6. 盛安德沈阳团队分支管理策略

|No.|Branch Name|Permission|Protected|Push|Merge|Note|
|:---:|:---|:---:|:---:|:---:|:---:|:---|
|1|main|Owner|✔️|❌|✔️|To release product version，version format x.xx.x.\<Alpha\|Beta\|Release\>|
|2|test|Master|✔️|❌|✔️|UAT Testing version|
|3|dev|Master|✔️|✔️|✔️|development|
|4|dev_\<username\>|Developer|✔️|✔️|✔️|personal branch|
|4|dev_\<username\>_\<datetime\>|Developer|✔️|✔️|✔️|personal temporary version|

## 7. 盛安德沈阳团队代码提交规范

### 7.1 提交信息格式

每次提交，Commit message 都包括三个部分：Header，Body 和 Footer。

```bash
<type>(<scope>): <subject>
<body>
<footer>
```

其中，Header 是必需的，Body 和 Footer 可以省略。

### 7.2 Header

Header 部分只有一行，包括三个字段：type（必需）、scope（可选）和 subject（必需）。

#### 7.2.1 type

type 用于说明 commit 的类别，只允许使用下面7个标识。

- feat：新功能（feature）
- fix：修补bug
- docs：文档（documentation）
- style： 格式（不影响代码运行的变动）
- refactor：重构（即不是新增功能，也不是修改bug的代码变动）
- test：增加测试
- chore：构建过程或辅助工具的变动

#### 7.2.2 scope

scope 用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同。

#### 7.2.3 subject

subject 是 commit 目的的简短描述，不超过50个字符。

- 以动词开头，使用第一人称现在时，比如change，而不是changed或changes
- 第一个字母小写
- 结尾不加句号（.）

### 7.3 Body

Body 部分是对本次 commit 的详细描述，可以分成多行。

### 7.4 Footer

Footer 部分只用于两种情况。

#### 7.4.1 不兼容变动

如果当前代码与上一个版本不兼容，则 Footer 部分以`BREAKING CHANGE`开头，后面是对变动的描述、以及变动理由和迁移方法。

#### 7.4.2 关闭 Issue

如果当前 commit 针对某个issue，那么可以在 Footer 部分关闭这个 issue 。

```bash
Closes #234
```

也可以一次关闭多个 issue 。

```bash
Closes #123, #245, #992
```

## 8. 盛安德沈阳团队代码提交流程

### 8.1 代码提交流程

1. 从远程仓库拉取最新代码
2. 创建个人分支
3. 在个人分支上开发
4. 提交代码到个人分支
5. 合并个人分支到开发分支
6. 测试通过后，合并开发分支到测试分支
7. 测试通过后，合并测试分支到主分支
8. 发布版本

## 9. 盛安德沈阳团队代码提交示例

### 9.1 代码提交示例

```bash
git commit -m "feat: add xxx feature"
```

### 9.2 代码提交示例

```bash
git commit -m "fix: xxx bug"
```

### 9.3 代码提交示例

```bash
git commit -m "feat: add xxx feature
- xxx
- xxx
- xxx
BREAKING CHANGE: xxx"
```
