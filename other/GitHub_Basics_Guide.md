## GitHub 基础使用指南

### 1. **什么是 GitHub？**

GitHub 是一个基于 Git 的版本控制平台，主要用于代码托管和协作开发。它不仅帮助开发者管理代码的版本，还支持多人协作、代码审核、问题追踪（Issues）、静态网站托管（GitHub Pages）等功能，是全球开发者最常用的协作平台之一。

### 2. **如何创建一个 GitHub 账号**

- 访问 [GitHub 官网](https://github.com/)。

- 点击右上角的 “Sign Up” 按钮。

- 输入你的电子邮件、创建用户名和密码（密码需包含字母、数字和特殊字符）。

- 完成人机验证后，根据提示选择使用目的（如 “For myself” 个人使用或 “For my team” 团队使用）。

- 完成邮箱验证后，账号创建成功。

### 3. **如何创建一个新的仓库**

1. 登录 GitHub 账号。
2. 在页面右上角，点击 “+” 图标，选择 “New repository”。
3. 在创建页面填写信息：

- **Repository name**：仓库名称（需唯一，建议用小写字母 + 连字符，如 my-project）。

- **Description**：仓库描述（可选，简要说明项目用途）。

- **Visibility**：选择 “Public”（公开，所有人可见）或 “Private”（私有，仅授权用户可见，免费账号有数量限制）。

- 可选配置：

- 勾选 “Add a README file”（自动生成 README 文档，用于项目说明）。

- 勾选 “Add .gitignore”（选择对应语言的忽略文件模板，避免提交无用文件）。

- 勾选 “Choose a license”（添加开源许可证，如 MIT、Apache 等，明确代码使用规则）。

4. 点击 “Create repository” 完成创建。

### 4. **如何使用 Git 命令行上传代码到 GitHub**

#### 4.1 **安装 Git**

- 下载并安装 Git：访问 [Git 官网](https://git-scm.com/)，根据操作系统（Windows/macOS/Linux）选择安装包。

- 安装完成后，打开终端（Windows 用 PowerShell 或 Git Bash，macOS/Linux 用 Terminal），输入 git --version，若显示版本号则安装成功。

#### 4.2 **配置 Git 身份（首次使用必做）**

Git 需要知道你的身份才能记录提交者信息，执行以下命令（替换为你的 GitHub 用户名和邮箱）：

```bash
git config --global user.name "your-username"  # 你的 GitHub 用户名
git config --global user.email "your-email@example.com"  # 你的 GitHub 注册邮箱
```

#### 4.3 **初始化本地仓库**

进入你的项目目录（通过 cd 项目路径 命令），执行：

```bash
git init  # 初始化本地 Git 仓库（生成隐藏的 .git 文件夹，存储版本信息）
```

#### 4.4 **关联远程仓库（HTTPS 或 SSH）**

将本地仓库与 GitHub 仓库关联，支持两种方式：

- **HTTPS 方式**（简单但可能需要频繁输入密码，推荐新手）：

```bash
git remote add origin https://github.com/your-username/your-repository.git
```

- **SSH 方式**（需配置密钥，一次配置后免密码推送，推荐常用场景）：

1. 生成 SSH 密钥（终端执行，一路回车默认配置）：

```bash
ssh-keygen -t ed25519 -C "your-email@example.com"  # 生成密钥文件
```

2. 查看公钥内容（Windows 路径：C:\Users\用户名\.ssh\id_ed25519.pub；macOS/Linux 路径：~/.ssh/id_ed25519.pub）：

```bash
# Windows Git Bash 或 macOS/Linux
cat ~/.ssh/id_ed25519.pub
```

3. 复制公钥内容，打开 GitHub → 点击头像 → “Settings” → “SSH and GPG keys” → “New SSH key”，粘贴公钥并保存。

4. 关联远程仓库：

```bash
git remote add origin git@github.com:your-username/your-repository.git
```

#### 4.5 **添加文件到暂存区**

本地修改或新增文件后，需先添加到暂存区（临时存储待提交的更改）：

```bash
git add 文件名  # 添加单个文件（如 git add index.js）
git add .       # 添加当前目录所有更改（新增、修改、删除的文件）
git add -u      # 只添加已跟踪文件的修改/删除（不包含新增文件）
```

#### 4.6 **提交更改到本地仓库**

用描述信息记录本次更改的目的（必填，建议清晰简洁，如 “修复登录按钮样式 bug”）：

```bash
git commit -m "描述信息"  
```

若需修改最近一次的提交信息（未推送到远程时）：

```bash
git commit --amend -m "新的描述信息"  
```

#### 4.7 **推送代码到 GitHub**

将本地提交推送到远程仓库的指定分支（首次推送需加 -u 关联分支，后续可直接 git push）：

```bash
# 推送到 main 分支（GitHub 新建仓库默认分支为 main，旧仓库可能为 master）
git push -u origin main  
```

### 5. **如何克隆一个 GitHub 仓库**

将远程仓库完整复制到本地（包括所有分支和提交历史）：

```bash
git clone 仓库地址  # 地址可在 GitHub 仓库页面点击 "Code" 获取（HTTPS 或 SSH）
# 示例：git clone git@github.com:your-username/your-repository.git
```

克隆后会自动创建本地仓库，并关联远程仓库（可通过 git remote -v 查看关联信息）。

### 6. **如何管理分支（Branches）**

分支用于并行开发（如功能开发、bug 修复），避免直接修改主分支代码。

#### 6.1 **创建并切换到新分支**

```bash
git checkout -b 分支名  # 等价于 git branch 分支名 + git checkout 分支名
# 示例：git checkout -b feature/login （功能分支，命名建议：feature/xxx、bugfix/xxx）
```

#### 6.2 **查看分支列表**

```bash
git branch          # 查看本地分支（当前分支前有 * 标记）
git branch -r       # 查看远程分支
git branch -a       # 查看本地+远程所有分支
```

#### 6.3 **切换分支**

```bash
git checkout 分支名  # 切换到已存在的分支（如 git checkout main）
# 新版 Git 可使用 git switch 分支名，更直观
```

#### 6.4 **合并分支**

将开发完成的分支（如 feature/login）合并到主分支（如 main）：

```bash
# 1. 先切换到目标分支（如 main）
git checkout main  
# 2. 拉取远程最新代码（避免冲突）
git pull origin main  
# 3. 合并分支
git merge feature/login  
```

#### 6.5 **删除分支**

```bash
git branch -d 分支名   # 删除本地已合并的分支（未合并会提示错误）
git branch -D 分支名   # 强制删除本地未合并的分支（谨慎使用）
git push origin --delete 分支名  # 删除远程分支
```

#### 6.6 **处理合并冲突**

当两个分支修改了同一文件的同一部分时，会产生冲突。解决步骤：

1. Git 会提示冲突文件（如 Auto-merging index.js CONFLICT (content)）。

2. 打开冲突文件，找到冲突标记并修改：

```bash
<<<<<<< HEAD       # 当前分支（main）的代码
欢迎登录           # main 分支的内容
=======
请登录             # feature/login 分支的内容
>>>>>>> feature/login  # 待合并分支的代码
```

3. 保留需要的代码，删除冲突标记（<<<<<<<、=======、>>>>>>>）。

4. 标记为已解决并提交：

```bash
git add 冲突文件   # 如 git add index.js
git commit -m "解决登录文案冲突"  
```

### 7. **如何拉取（Pull）远程代码**

拉取远程最新代码到本地，并自动合并（避免本地代码过时）：

```bash
git pull origin 分支名  # 如 git pull origin main（拉取远程 main 分支到本地当前分支）
```

若拉取时冲突，解决方式同 “合并冲突”（修改文件 → git add → git commit）。

### 8. **如何提交 Pull Request（PR）**

PR 是多人协作的核心工具，用于请求将你的分支代码合并到目标分支（如主分支），方便团队审核。

1. 先将你的分支推送到远程：

```bash
git push -u origin 你的分支名  # 如 git push -u origin feature/login
```

2. 打开 GitHub 仓库页面，点击 “Compare & pull request”（或进入 “Pull requests” 标签页 → “New pull request”）。
3. 选择 “base”（目标分支，如 main）和 “compare”（你的分支，如 feature/login）。
4. 填写 PR 信息：

- **Title**：PR 标题（如 “新增登录功能”）。

- **Description**：详细说明修改内容、解决的问题等（可关联 Issues，如 “Fixes #123” 表示解决 #123 问题）。

5. 点击 “Create pull request” 提交。

6. 等待团队审核，审核通过后由管理员点击 “Merge pull request” 完成合并。

### 9. **常用进阶操作**

#### 9.1 **.gitignore 文件：忽略无需提交的文件**

用于指定不需要被 Git 跟踪的文件（如依赖包、日志、IDE 配置等），避免仓库冗余。

- 在项目根目录创建 .gitignore 文件，添加规则（支持通配符）：

```bash
# 忽略 node_modules 文件夹（npm 依赖）
node_modules/
# 忽略 .env 环境变量文件
.env
# 忽略所有 .log 日志文件
*.log
# 忽略 VS Code 配置（但保留 .vscode/settings.json）
.vscode/*
!.vscode/settings.json
```

- GitHub 提供多种语言的 .gitignore 模板，创建仓库时可直接选择。

#### 9.2 **标签（Tags）：标记版本**

用于标记重要版本（如 v1.0.0），方便后续回溯。

```bash
# 创建标签（轻量标签，仅记录版本号）
git tag v1.0.0  
# 创建带描述的标签（推荐，类似提交信息）
git tag -a v1.0.0 -m "第一个正式版本"  
# 推送标签到远程
git push origin v1.0.0  
# 推送所有本地标签到远程
git push origin --tags  
# 查看所有标签
git tag  
```

#### 9.3 **撤销操作**

- **撤销工作区修改**（未 git add 的文件）：

```bash
git checkout -- 文件名  # 如 git checkout -- index.js（恢复到最近一次提交的状态）
```

- **撤销暂存区修改**（已 git add 但未 git commit）：

```bash
git reset HEAD 文件名  # 如 git reset HEAD index.js（将文件从暂存区移回工作区）
```

- **撤销本地提交**（已 git commit 但未 git push）：

```bash
# 方式1：保留修改，回到提交前状态（推荐，安全）
git reset --soft HEAD~1  # HEAD~1 表示撤销最近1次提交，~2 撤销最近2次，以此类推
# 方式2：丢弃修改，回到提交前状态（谨慎，修改会丢失）
git reset --hard HEAD~1  
```

- **撤销远程提交**（已 git push，需创建新提交覆盖）：

```bash
git revert 提交ID  # 提交ID可通过 git log 查看，如 git revert a1b2c3d
# 执行后会生成一个新提交，描述为“Revert "原提交信息"”，推送即可
git push origin 分支名  
```

#### 9.4 **暂存工作区（git stash）**

当需要切换分支但不想提交当前修改时，可暂存工作区：

```bash
git stash  # 暂存当前工作区所有修改（未提交的内容）
git stash list  # 查看所有暂存记录（如 stash@{0}: WIP on main: ...）
git stash apply stash@{0}  # 恢复指定暂存记录（0 为序号）
git stash drop stash@{0}  # 删除指定暂存记录
git stash pop  # 恢复最近一次暂存并删除该记录（常用）
```

#### 9.5 **查看远程仓库信息**

```bash
git remote -v  # 查看关联的远程仓库地址（fetch 拉取地址，push 推送地址）
git remote show origin  # 查看远程仓库详细信息（如分支、提交记录）
git remote remove origin  # 移除关联的远程仓库
```

### 10. **GitHub Pages：托管静态网站**

GitHub 支持将仓库中的静态文件（HTML/CSS/JS）部署为网站，免费且无需服务器。

1. 新建仓库（仓库名建议为 用户名.[github.io](http://github.io)，如 [octocat.github.io](http://octocat.github.io)，此时网站地址即为该名称）。

2. 克隆仓库到本地，添加静态文件（如 index.html）。
3. 推送代码到 main 分支。
4. 打开仓库 “Settings” → “Pages” → “Build and deployment” → “Source” 选择 “Deploy from a branch”，分支选择 main，点击 “Save”。
5. 几分钟后，即可通过 https://用户名.[github.io](http://github.io) 访问网站。

### 11. **Issues：追踪任务与 Bug**

Issues 用于记录项目中的任务、Bug、建议等，是团队协作的重要工具。

- **创建 Issues**：仓库页面 → “Issues” → “New issue” → 填写标题、描述（支持 Markdown 格式），可添加标签（Labels，如 bug、enhancement）、里程碑（Milestones）、指派负责人（Assignees）。

- **管理 Issues**：可通过评论交流、关闭（解决后点击 “Close issue”）、关联 PR（如在 PR 描述中写 “Fixes #123”，合并后自动关闭 #123 Issues）。

### 12. **其他实用功能**

- **Star（星标）**：点击仓库右上角 “Star” 可收藏仓库，方便后续查找（在个人主页 “Stars” 中查看）。

- **Fork（分叉）**：点击 “Fork” 可复制他人仓库到自己账号下（用于修改开源项目，之后可通过 PR 向原仓库提交修改）。

- **分支保护**：仓库 “Settings” → “Branches” → “Add rule”，可设置主分支保护（如禁止直接推送、必须通过 PR 且审核后才能合并）。

### 13. **常见问题解答（FAQ）**

#### 13.1 **推送失败：****error: failed to push some refs to ...**

- 原因：本地分支落后于远程分支（远程有新提交）。

- 解决：先拉取远程代码合并，再推送：

```bash
git pull origin main  # 拉取远程 main 分支
# 若有冲突，解决后提交
git push origin main  
```

#### 13.2 **忘记添加文件到提交：已** **git commit** **但漏了文件**

- 解决：添加文件后，用 --amend 补充到最近一次提交：

```bash
git add 漏加的文件  
git commit --amend --no-edit  # --no-edit 表示不修改提交信息
git push --force origin 分支名  # 若已推送，需强制推送（谨慎，多人协作时避免）
```

#### 13.3 **误删本地分支 / 文件**

- 误删分支：通过提交历史恢复（找到分支最后一次提交的 ID）：

```bash
git log --oneline  # 查看提交历史，找到分支最后一次提交的 ID（如 a1b2c3d）
git checkout -b 恢复的分支名 a1b2c3d  # 基于该提交重建分支
```

- 误删文件（已提交过）：通过 git checkout 恢复：

```bash
git checkout 分支名 -- 文件名  # 如 git checkout main -- index.js
```

#### 13.4 **SSH 连接错误：****Permission denied (publickey)**

- 原因：SSH 密钥未添加到 GitHub 或本地密钥配置错误。

- 解决：

1. 检查本地密钥是否存在：ls ~/.ssh（看是否有 id_ed25519 和 id_ed25519.pub）。
2. 重新添加公钥到 GitHub（步骤见 4.4  SSH 方式）。
3. 测试连接：ssh -T [git@github.com](mailto:git@github.com)，显示 “Hi 用户名！You've successfully authenticated...” 即成功。

通过以上内容，可覆盖 GitHub 日常使用的绝大多数场景，从基础操作到协作工具，帮助快速上手并规范使用流程。
