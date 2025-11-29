好的！我来给您一个从零开始的 Git 详细使用教程：

## 📚 Git 完整使用教程（macOS）

------

## 第一部分：验证和配置 Git

### 1. 验证 Git 是否安装成功

打开终端（Terminal），输入：

```bash
git --version
```

应该显示类似：`git version 2.x.x`

### 2. 配置 Git 用户信息（必须做！）

```bash
# 设置用户名（用于标识您的提交）
git config --global user.name "您的名字"

# 设置邮箱
git config --global user.email "your.email@example.com"

# 例如：
git config --global user.name "Zhang San"
git config --global user.email "zhangsan@gmail.com"
```

### 3. 验证配置

```bash
# 查看所有配置
git config --list

# 或单独查看
git config user.name
git config user.email
```

### 4. 配置默认编辑器（可选）

```bash
# 使用 nano（简单）
git config --global core.editor "nano"

# 或使用 vim
git config --global core.editor "vim"
```

------

## 第二部分：Git 基础操作

### 场景一：创建新项目并使用 Git

#### 1. 创建项目文件夹

```bash
# 创建一个新文件夹
mkdir my-first-project

# 进入文件夹
cd my-first-project
```

#### 2. 初始化 Git 仓库

```bash
# 初始化 Git（让这个文件夹被 Git 管理）
git init
```

您会看到提示：`Initialized empty Git repository`

#### 3. 创建第一个文件

```bash
# 创建一个测试文件
echo "# 我的第一个项目" > README.md

# 查看文件
cat README.md
```

#### 4. 查看状态

```bash
# 查看 Git 状态
git status
```

会显示 `README.md` 是未跟踪的文件（红色）

#### 5. 添加文件到暂存区

```bash
# 添加单个文件
git add README.md

# 或添加所有文件
git add .

# 再次查看状态
git status
```

现在文件应该变成绿色（已暂存）

#### 6. 提交更改

```bash
# 提交更改（第一次提交）
git commit -m "初始提交：添加 README 文件"

# -m 后面是提交信息，描述这次改了什么
```

#### 7. 查看提交历史

```bash
# 查看提交记录
git log

# 简洁查看
git log --oneline
```

------

### 场景二：日常使用流程

#### 完整工作流程：

```bash
# 1. 修改文件（用任何编辑器编辑文件）
echo "添加一些新内容" >> README.md

# 2. 查看改动
git status
git diff        # 查看具体改了什么

# 3. 添加到暂存区
git add README.md

# 4. 提交
git commit -m "更新 README：添加新内容"

# 5. 查看历史
git log --oneline
```

------

## 第三部分：Git 分支操作

### 1. 查看分支

```bash
# 查看所有分支
git branch

# 当前分支前面有 * 号
```

### 2. 创建新分支

```bash
# 创建新分支
git branch feature-new

# 查看分支
git branch
```

### 3. 切换分支

```bash
# 切换到新分支
git checkout feature-new

# 或使用新命令
git switch feature-new
```

### 4. 创建并切换分支（快捷方式）

```bash
# 一步完成创建和切换
git checkout -b feature-login

# 或
git switch -c feature-login
```

### 5. 在新分支上工作

```bash
# 创建新文件
echo "登录功能代码" > login.txt

# 添加并提交
git add login.txt
git commit -m "添加登录功能"
```

### 6. 合并分支

```bash
# 1. 切回主分支
git checkout main
# 或 git checkout master（取决于您的默认分支名）

# 2. 合并分支
git merge feature-login

# 3. 删除已合并的分支（可选）
git branch -d feature-login
```

------

## 第四部分：与 GitHub 配合使用

### 1. 在 GitHub 创建仓库

1. 访问 https://github.com
2. 登录账号
3. 点击右上角 "+" → "New repository"
4. 填写仓库名称，点击 "Create repository"

### 2. 连接本地仓库到 GitHub

```bash
# 添加远程仓库（复制 GitHub 上显示的命令）
git remote add origin https://github.com/您的用户名/仓库名.git

# 查看远程仓库
git remote -v
```

### 3. 推送代码到 GitHub

```bash
# 第一次推送（设置上游分支）
git push -u origin main

# 之后的推送
git push
```

### 4. 从 GitHub 克隆项目

```bash
# 克隆别人的或自己的项目
git clone https://github.com/用户名/仓库名.git

# 进入克隆的文件夹
cd 仓库名
```

### 5. 拉取最新代码

```bash
# 拉取远程仓库的最新代码
git pull
```

------

## 第五部分：常用命令速查表

### 基础命令

```bash
# 初始化仓库
git init

# 查看状态
git status

# 添加文件
git add 文件名          # 添加单个文件
git add .              # 添加所有文件

# 提交
git commit -m "提交信息"

# 查看历史
git log
git log --oneline      # 简洁版
git log --graph        # 图形化显示分支
```

### 分支命令

```bash
# 查看分支
git branch

# 创建分支
git branch 分支名

# 切换分支
git checkout 分支名
git switch 分支名       # 新命令

# 创建并切换
git checkout -b 分支名
git switch -c 分支名

# 合并分支
git merge 分支名

# 删除分支
git branch -d 分支名
```

### 远程仓库命令

```bash
# 添加远程仓库
git remote add origin URL

# 查看远程仓库
git remote -v

# 推送
git push
git push -u origin main  # 第一次推送

# 拉取
git pull

# 克隆
git clone URL
```

### 撤销操作

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

------

## 第六部分：实战练习

### 练习1：创建一个简单项目

```bash
# 1. 创建项目
mkdir git-practice
cd git-practice
git init

# 2. 创建文件
echo "# Git 练习项目" > README.md
echo "console.log('Hello Git');" > index.js

# 3. 提交
git add .
git commit -m "初始提交"

# 4. 查看历史
git log --oneline
```

### 练习2：使用分支开发新功能

```bash
# 1. 创建开发分支
git checkout -b develop

# 2. 修改文件
echo "console.log('新功能');" >> index.js

# 3. 提交
git add index.js
git commit -m "添加新功能"

# 4. 切回主分支
git checkout main

# 5. 合并
git merge develop

# 6. 查看历史
git log --oneline --graph
```

------

## 第七部分：.gitignore 文件

### 什么是 .gitignore？

用于告诉 Git 哪些文件不需要跟踪（比如临时文件、系统文件等）

### 创建 .gitignore

```bash
# 创建 .gitignore 文件
nano .gitignore
```

### 常用配置示例

```
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

------

## 第八部分：常见问题解决

### 问题1：忘记提交信息怎么办？

```bash
# 修改最后一次提交信息
git commit --amend -m "新的提交信息"
```

### 问题2：不小心提交了错误的文件

```bash
# 撤销最后一次提交，但保留更改
git reset --soft HEAD~1

# 移除不需要的文件
git reset HEAD 文件名

# 重新提交
git add 正确的文件
git commit -m "正确的提交"
```

### 问题3：查看某个文件的修改历史

```bash
# 查看文件的提交历史
git log -- 文件名

# 查看文件的详细修改
git log -p 文件名
```

### 问题4：比较不同版本

```bash
# 比较工作区和暂存区
git diff

# 比较暂存区和最后一次提交
git diff --staged

# 比较两个提交
git diff 提交ID1 提交ID2
```

------

## 🎯 学习路径建议

### 第1周：基础操作

- 熟悉 `git init`, `git add`, `git commit`, `git status`
- 每天练习创建提交

### 第2周：分支操作

- 学习 `git branch`, `git checkout`, `git merge`
- 练习创建和合并分支

### 第3周：远程仓库

- 学习使用 GitHub
- 练习 `git push`, `git pull`, `git clone`

### 第4周：进阶技巧

- 学习 `.gitignore`
- 学习撤销操作
- 学习解决冲突

------

## 📖 推荐资源

1. **官方文档**：https://git-scm.com/doc
2. **交互式教程**：https://learngitbranching.js.org/?locale=zh_CN
3. **可视化工具**：
   - GitKraken（图形界面）
   - Sourcetree（图形界面）
   - VS Code 内置 Git 功能

------

## 💡 实用技巧

### 1. 创建别名（快捷命令）

```bash
# 设置常用命令的别名
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.cm commit
git config --global alias.lg "log --oneline --graph"

# 之后就可以用：
git st      # 相当于 git status
git co main # 相当于 git checkout main
```

### 2. 美化 Git 输出

```bash
# 彩色输出
git config --global color.ui auto
```

### 3. 查看图形化历史

```bash
git log --oneline --graph --all --decorate
```

------

现在您可以开始使用 Git 了！建议先从**第六部分的实战练习**开始，动手操作几遍就能掌握基础了。

有任何具体问题随时问我！🚀