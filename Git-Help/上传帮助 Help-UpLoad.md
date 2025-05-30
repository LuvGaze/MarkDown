
# GitHub 仓库上传本地项目完整指南

## 目录
1. [准备工作](#一、准备工作)
2. [HTTPS上传方式](#二、HTTPS上传方式)
3. [SSH上传方式](#三、ssh上传方式)
4. [命令行操作全流程](#四、命令行操作全流程)
5. [常见问题](#五、常见问题)

---

## 一、准备工作
### 必需工具
- [Git安装包](https://git-scm.com/downloads)
- GitHub账号

### 初始化设置
```bash
# 配置全局用户信息（重要！）
git config --global user.name "YourName"
git config --global user.email "your@email.com"
```

---

## 二、HTTPS上传方式
### 操作流程
1. 在GitHub创建新仓库
   - 不要初始化README/.gitignore
   - 记录提供的HTTPS地址

2. 本地项目初始化
```bash
cd /your/project/path
git init
git add .
git commit -m "Initial commit"
```

3. 关联远程仓库
```bash
git remote add origin https://github.com/username/repo.git
```

4. 首次推送
```bash
git push -u origin main
# 需要输入账号密码（2021年后需用个人访问令牌）
```

---

## 三、SSH上传方式
### 配置步骤
1. 检查现有SSH密钥
```bash
ls -al ~/.ssh
```

2. 生成新密钥（若无）
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

3. 添加公钥到GitHub
   - 复制`id_ed25519.pub`内容
   - GitHub → Settings → SSH and GPG keys → New SSH key

### 上传命令
```bash
git remote set-url origin git@github.com:username/repo.git
git push origin main
```

---

## 四、命令行操作全流程
### 完整示例
```bash
# 1. 进入项目目录
cd ~/projects/my-app

# 2. 初始化仓库
git init

# 3. 添加所有文件
git add .

# 4. 提交更改
git commit -m "First commit"

# 5. 关联远程仓库（HTTPS示例）
git remote add origin https://github.com/username/repo.git

# 6. 推送代码
git push -u origin main
```

### 文件状态管理
```diff
# 查看状态
git status

# 添加特定文件
+ git add index.html style.css

# 排除文件
- 创建.gitignore文件
```

---

## 五、常见问题
### 1. 推送被拒绝
```bash
# 强制推送（谨慎使用）
git push -f origin main

# 推荐方案：先拉取最新代码
git pull origin main
```

### 2. 认证失败
```bash
# 检查远程地址类型
git remote -v

# HTTPS切换SSH
git remote set-url origin git@github.com:username/repo.git
```

### 3. 大文件上传
```bash
# 安装Git LFS
git lfs install
git lfs track "*.psd"
git add .gitattributes
```

---

## 六、图形化工具推荐
```bash
# 对于常用git功能者，建议掌握以下其中一个工具
```
1. [GitHub Desktop](https://desktop.github.com)
2. [Sourcetree](https://www.sourcetreeapp.com)
3. VS Code、Pycharm等工具内置Git功能

> 提示：所有路径需替换为你的实际项目路径