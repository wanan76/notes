## git 常用命令
#### 查看Git本地用户信息
```
git config --global -l
```
#### 撤销commit
撤销并保留修改：
```
// 会将改动放在缓存区
git reset --soft <commit_id>
```
```
// 不会将改动放在缓存区
git reset --soft <commit_id>
```
> 缓冲区：add的代码就在缓冲区

不保留修改撤销：
```
git reset –hard <commit_id>
```
#### 修改最后一次commit
```
git commit --amend
```
#### 撤销add
```
git reset HEAD <file>
```
#### 丢弃工作文件的改动
```
git checkout -- <file>
```
#### 撤销merge/pull操作
```
git reset --merge
```
> pull操作实际上包含了fetch+merge操作
#### stash操作
```
git stash //能够将所有未提交的修改（工作区和暂存区）保存至堆栈中，用于后续恢复当前工作目录
```
```
git stash save "remark" //作用等同于git stash，区别是可以加一些注释
```
```
git stash list //查看当前stash中的内容
```
```
git stash pop //将当前stash中的内容弹出，并应用到当前分支对应的工作目录上。
```
> 该命令将堆栈中最近保存的内容删除（栈是先进后出）
```
git stash apply //将堆栈中的内容应用到当前目录
```
```
git stash apply <stash_name> //指定恢复哪个stash到当前的工作目录
```
> 不同于git stash pop，该命令不会将内容从堆栈中删除，也就说该命令能够将堆栈的内容多次应用到工作目录中，适应于多个分支的情况
```
git stash drop <stash_name> //从堆栈中移除某个指定的stash
```
```
git stash clear //清除堆栈中的所有内容
```
#### .gitignore中添加忽略文件
```
git rm -r --cached .
git add .
git commit -m 'update .gitignore'
```
> 把某些目录或文件加入忽略规则，按照上述方法定义后发现并未生效，原因是.gitignore只能忽略那些原来没有被追踪的文件，如果某些文件已经被纳入了版本管理中，则修改.gitignore是无效的。那么解决方法就是先把本地缓存删除（改变成未被追踪状态），然后再提交，这样就不会出现忽略的文件了
#### 与远程仓库同步
```
git fetch origin -p
```
#### checkout远程分支
```
git checkout -b dev（本地分支名） origin/dev（远程分支名）
```
---
## 项目上传到Github
### 1.配置 ssh
#### 终端生成 ssh key
```
ssh-keygen -t rsa -C "[email address]"
```
```
cnte@cntedeMac-mini flutter_solid_ui % ssh-keygen -t rsa -C "670074760@qq.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/cnte/.ssh/id_rsa): /Users/cnte/Documents/github/ssh/id_rsa
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /Users/cnte/Documents/github/ssh/id_rsa.
Your public key has been saved in /Users/cnte/Documents/github/ssh/id_rsa.pub.
The key fingerprint is:
SHA256:cWLH4uFI6sHU30COF6PSKcKSgD3ANE0Ju1sPH+rRgb0 670074760@qq.com
The key's randomart image is:
+---[RSA 3072]----+
|**+..   +        |
|o+=o o * +       |
|o.o.+ B X +      |
| ..+o= B X       |
| . +++. S .      |
|  o.*.+          |
| . o.E           |
|  . .            |
|   .             |
+----[SHA256]-----+
```
> 它会在你选择的路径下上生成 ssh key，如果你直接点击回车，会在默认路径下创建 ssh 

> 输入密码，直接回车则是不设置密码。直接回车就可以。然后会让你重复密码，也是直接回车
#### 将生成的 ssh 配置到 github
```
Settings / SSH and GPG keys / New SSH key
```
> Title：随便取一个

> Key: 把上一步生成的id_rsa.pub文件里的内容复制到这里
#### 验证是否添加ssh成功
终端执行：
```
ssh -T git@github.com
```
如果失败，执行：
```
ssh-add /Users/cnte/Documents/github/ssh/id_rsa
```
```
cnte@cntedeMac-mini flutter_solid_ui % ssh -T git@github.com
The authenticity of host 'github.com (20.205.243.166)' can't be established.
ECDSA key fingerprint is SHA256:p2QAMXNIC1TJYWeIOttrVc98/R1BUFWu3/LiyKgUfQM.
Are you sure you want to continue connecting (yes/no/[fingerprint])? 
Host key verification failed.
cnte@cntedeMac-mini flutter_solid_ui % ssh-add /Users/cnte/Documents/github/ssh/id_rsa 
Identity added: /Users/cnte/Documents/github/ssh/id_rsa (670074760@qq.com)
cnte@cntedeMac-mini flutter_solid_ui % ssh -T git@github.com
The authenticity of host 'github.com (20.205.243.166)' can't be established.
ECDSA key fingerprint is SHA256:p2QAMXNIC1TJYWeIOttrVc98/R1BUFWu3/LiyKgUfQM.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'github.com,20.205.243.166' (ECDSA) to the list of known hosts.
Hi wanan76! You've successfully authenticated, but GitHub does not provide shell access.
```
### 2. Github上生成access token
```
Settings/Developer settings/Personal access tokens/
```
### 3. 上传项目
- Github上创建仓库
- 本地项目根目录执行
  ```
  git init
  git add .
  git commit -m "Initial commit"
  git remote add origin https://[access token]@github.com/z-flutter/flutter_solid_ui.git
  git push --set-upstream origin master
  ```
