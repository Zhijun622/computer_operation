# Git 用法



### 工作流程



```mermaid
graph LR
A[工作区]-->|add|B[暂存区]-->|commit|C[本地仓库]-->|push|D[远程仓库];
D-->|pull|C-->|reset|B-->|checkout|A;

```



### 1.开始一个项目

```bash
git init
```

```bash
git clone <远程仓库地址>
```



### 2.添加到暂存区

``` bash
#添加指定文件
git add filename.py

# 添加当前目录下的所有文件（最常用）
git add .
```



### 3.提交到本地仓库

```bash
# 提交并附带注释（必须写清楚你做了什么） 
git commit -m "修复了登录页面的 Bug"
```



### 4.远程协作

```bash
# 1. 关联远程仓库（如果是本地 init 的项目）
git remote add origin <远程仓库地址>

# 2. 拉取最新代码（防止冲突，推送前最好先拉取）
git pull origin <分支名>
# 例如: git pull origin main

# 3. 推送代码到远程
git push origin <分支名>
# 第一次推送时通常需要关联: git push -u origin main

# 4. 查看远程仓库
git remote -v
```



### 5.撤销操作

```bash
# 撤销工作区的修改（未 add）
git checkout -- 文件名
git restore 文件名      # 新命令

# 撤销暂存（已 add 未 commit）
git reset HEAD 文件名
git restore --staged 文件名  # 新命令

# 撤销提交（已 commit）
git reset --soft HEAD~1     # 保留更改
git reset --hard HEAD~1     # 丢弃更改（危险！）
```



### 6..gitignore 文件

#### 创建 .gitignore

```bash
# 创建 .gitignore 文件
nano .gitignore
```

#### 常用配置示例

```bash
# macOS 系统文件
.DS_Store

# 编辑器配置
.vscode/
.idea/

# 依赖文件夹
node_modules/
venv/

# 环境变量文件
.env

# 日志文件
*.log

# 编译文件
*.pyc
*.class
```



### 7.常见问题解决

#### 7.1忘记提交信息

```bash
# 修改最后一次提交信息
git commit --amend -m "新的提交信息"
```



#### 7.2不小心提交了错误的文件

```bash
# 撤销最后一次提交，但保留更改
git reset --soft HEAD~1

# 移除不需要的文件
git reset HEAD 文件名

# 重新提交
git add 正确的文件
git commit -m "正确的提交"
```



#### 3.查看某个文件的修改历史

```bash
# 查看文件的提交历史
git log -- 文件名

# 查看文件的详细修改
git log -p 文件名
```



#### 4.比较不同版本

```bash
# 比较工作区和暂存区
git diff

# 比较暂存区和最后一次提交
git diff --staged

# 比较两个提交
git diff 提交ID1 提交ID2
```



 #### 5.关联远程仓库时，报错 **fatal: not a git repository...**

##### 1.去一个干净的文件夹

```bash
# 例如：切换到桌面
cd Desktop
```

##### 2.直接克隆 (推荐)

```bash
git clone https://github.com/Zhijun622/computer_operation.git
```

##### 3.进入项目文件夹

```bash
cd computer_operation
```



#### 6.推送代码到远程时，报错

报错信息 **`fatal: The current branch main has no upstream branch`**的意思是：“你让我把代码推送到远端（push），但我不知道要把你本地的 `main` 分支推给远端的哪个分支。我们还没建立‘绑定’关系呢。”

#### 情况一：最直接的尝试（先试这个）

```bash
git push -u origin main
```

`-u` 的意思是 `set-upstream`（设置上游），这就相当于告诉 Git：“以后我输入 `git push`，你就默认往 `origin` 的 `main` 分支推。”

 #### 情况二：如果报错 "Updates were rejected"（极大概率发生）

如果你运行上面的命令后，出现了类似下面的红色报错：**error: failed to push some refs to ...**

**hint: Updates were rejected because the remote contains work that you do not have locally.**

**原因：** 因为你是在本地新建的仓库（`git init`），而远程仓库（GitHub）里已经有文件了（比如 README 或你之前上传的文件）。Git 发现这两边的历史记录“毫无瓜葛”，属于“非亲非故”的关系，所以它拒绝合并，怕覆盖掉远程的东西。

##### 第一步：允许合并不相关的历史

```bash
git pull origin main --allow-unrelated-histories
```

##### 第二步：再次推送

```bash
git push -u origin main
```

