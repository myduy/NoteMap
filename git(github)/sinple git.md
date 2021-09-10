#### 如果你是一个新项目使用

```bash
echo "# arabic" >> README.md # 编写自述
git init # 初始化当前项目
git add README.md #将 README.md 提交到缓冲区
git commit -m "first commit" #提交到工作区
git branch -M main # 移动/重命名分支，即使目标存在
git remote add origin <https://github.com/myduy/arabic.git> # 为远程github添加别名
git push -u origin main #将mian推送到github
```

#### 如果这个项目已经存在

```bash
git remote add origin <https://github.com/myduy/arabic.git> # 为远程github添加别名
git branch -M main  # 移动/重命名分支，即使目标存在
git push -u origin main # 将mian推送到github
```

#### 获取

~~~bash
git clone  # 克隆仓库
git pull # 拉回远程版本库的提交

git branch -a # 查看所有的分支
git branch -r # 查看远程所有分支

git checkout dev # 切换到本地dev分支
git merge # 分支合并
git pull # 拉回远程版本库的提交
git remote -v # 查看远程仓库
git remote show #查看远程仓库
git pull [remoteName] [localBranchName] # 拉取远程仓库
~~~

### 密钥

```bash
 ssh-keygen -t rsa -C "sfgdxv@163.com"
```

### 查看远程所有分支

```bash
git branch -r 查看远程所有分支
```

