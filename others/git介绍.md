# git教程

[git简介](https://www.liaoxuefeng.com/wiki/896043488029600/900937935629664)

## git简介

### git初始配置

> ```
> //指定你的位置
> $ git config --global user.name "Your Name"
> $ git config --global user.email "email@example.com"
> ```

### 创建respository

> 也就是创建一个文件夹，这个文件夹下面的所有文件都可以由git进行增删减改

> //如下命令使得当前文件夹可以由git控制
>
> git init

### 本地的基本操作

[工作区和缓冲区的基本操作](https://www.liaoxuefeng.com/wiki/896043488029600/897271968352576)

> //提交到暂存区
>
> git add 文件
>
> //提交到仓库
>
> git commit -m "message"
>
> //查看状态
>
> git status

### 撤销以及修改命令

> //假设A文件在工作区被修改了，如何让它回到上一个版本
>
> git restore A
>
> //假设A文件被修改了，并且提交到暂存区，那么如何让暂存区中修改后的A回到修改前的状态
>
> //下面的命令仍不会撤销A的修改，如果想撤销的话，还需要再次执行上面的:git restore A
>
> git restore --staged A

### 删除操作

> //明确以及操作的异同，并且可以撤销
>
> git rm 文件
>
> rm 文件

### 版本回退

[简介](https://www.liaoxuefeng.com/wiki/896043488029600/897013573512192)

> - `HEAD`指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令`git reset --hard commit_id`。
> - 穿梭前，用`git log`可以查看提交历史，以便确定要回退到哪个版本。
> - 要重返未来，用`git reflog`查看命令历史，以便确定要回到未来的哪个版本

## 远程仓库

### 远程仓库

> //关联远程库
>
> git remote add origin git@github.com:XtangEver/git_learning.git
>
> //推送mater内容
>
> git push -u origin master
>
> //后续的推送
>
> git push origin master

### 克隆远程仓库

 >//你在哪里使用当前目录，便会将git克隆到哪里
 >
 >git clone 地址

## 分支管理

[分支的基本操作](https://www.liaoxuefeng.com/wiki/896043488029600/900003767775424)

## SSH密钥问题

### 检查现有的SSH密钥

> 1. 打开 Git Bash。
>
> 2. 输入 `ls -al ~/.ssh` 以查看是否存在现有 SSH 密钥：
>
>    ```shell
>    $ ls -al ~/.ssh
>    # Lists the files in your .ssh directory, if they exist
>    ```
>
> 3. 检查目录列表以查看是否已经有 SSH 公钥。 默认情况下，公钥的文件名是以下之一：
>
>    - *id_rsa.pub*
>    - *id_ecdsa.pub*
>    - *id_ed25519.pub*

#### 若没有密钥，需要产生SSH密钥

1. 打开 Git Bash。

2. 粘贴下面的文本（替换为您的 GitHub 电子邮件地址）。

   ```shell
   $ ssh-keygen -t ed25519 -C "your_email@example.com"
   ```

   **注：**如果您使用的是不支持 Ed25519 算法的旧系统，请使用以下命令：

   ```shell
   $ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
   ```

   这将创建以所提供的电子邮件地址为标签的新 SSH 密钥。

   ```shell
   > Generating public/private ed25519 key pair.
   ```

3. 提示您“Enter a file in which to save the key（输入要保存密钥的文件）”时，按 Enter 键。 这将接受默认文件位置。

   ```shell
   > Enter a file in which to save the key (/c/Users/you/.ssh/id_ed25519):[Press enter]
   ```

4. 在提示时输入安全密码。 更多信息请参阅[“使用 SSH 密钥密码”](https://docs.github.com/cn/articles/working-with-ssh-key-passphrases)。

   ```shell
   > Enter passphrase (empty for no passphrase): [Type a passphrase]
   > Enter same passphrase again: [Type passphrase again]
   ```

### 添加SSH密钥添加到ssh_agent

1. 确保 ssh-agent 正在运行。 您可以根据“[使用 SSH 密钥密码](https://docs.github.com/cn/articles/working-with-ssh-key-passphrases)”中的“自动启动 ssh-agent”说明，或者手动启动它：

   ```shell
   # start the ssh-agent in the background
   $ eval `ssh-agent -s`
   > Agent pid 59566
   ```

2. 将 SSH 私钥添加到 ssh-agent。 如果您创建了不同名称的密钥，或者您要添加不同名称的现有密钥，请将命令中的 *id_ed25519* 替换为您的私钥文件的名称。

   ```shell
   $ ssh-add ~/.ssh/id_ed25519
   ```

### 将SSH密钥添加到github账户

```
clip < ~/.ssh/id_ed25519.pub
```

