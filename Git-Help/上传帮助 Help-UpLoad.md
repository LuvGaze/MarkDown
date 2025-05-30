
# 🚀 GitHub 仓库上传本地项目完整指南

## 📚 目录
1. [🛠️ 准备工作](#一、🛠️准备工作)
2. [🔗 HTTPS上传方式](#二、🔗HTTPS上传方式)
3. [🔐 SSH上传方式](#三、🔐SSH上传方式)
4. [⌨️ 命令行操作全流程](#四、⌨️命令行操作全流程)
5. [❗ 常见问题](#五、❗常见问题)
6. [🖥️ 图形化工具推荐](#六、🖥️图形化工具推荐)

---

## 一、🛠️准备工作
### 📦 必需工具
- [Git官方安装包](https://git-scm.com/downloads)  
- [GitHub账号注册](https://github.com/signup)

### ⚙️ 初始化设置
```bash
# 配置全局用户信息（必须！）
git config --global user.name "YourName"
git config --global user.email "your@email.com"

# 查看配置是否生效
git config --list
```

---

## 二、🔗HTTPS上传方式
### 📌 操作流程
1. **创建GitHub仓库**  
   - 不要勾选"Initialize this repository with a README"
   - 复制提供的HTTPS地址（如：`https://github.com/username/repo.git`）

2. **本地项目初始化**  
```bash
cd /your/project/path
git init
git add .
git commit -m "Initial commit"
```

3. **关联远程仓库**  
```bash
git remote add origin https://github.com/username/repo.git
```

4. **首次推送**  
```bash
git push -u origin main
# 弹出窗口输入GitHub账号密码（或PAT令牌）
```

> 💡 2021年后GitHub已禁用密码验证，需使用[Personal Access Token](https://github.com/settings/tokens)

---

## 三、🔐SSH上传方式
### 🔑 配置步骤
1. **检查现有密钥**  
```bash
ls -al ~/.ssh
```

2. **生成新密钥**  
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
# 连续回车使用默认设置
```

3. **添加公钥到GitHub**  
   - 复制`~/.ssh/id_ed25519.pub`内容
   - GitHub → Settings → SSH and GPG keys → New SSH key

4. **测试连接**  
```bash
ssh -T git@github.com
# 看到"Hi username!"表示成功
```

### 🚀 上传命令
```bash
git remote set-url origin git@github.com:username/repo.git
git push origin main
```

---

## 四、⌨️命令行操作全流程
### 🎯 完整示例
```bash
# 1. 进入项目目录
cd ~/projects/my-app

# 2. 初始化仓库
git init

# 3. 添加所有文件（排除.gitignore中文件）
git add .

# 4. 提交更改
git commit -m "First commit"

# 5. 关联远程仓库
git remote add origin https://github.com/username/repo.git

# 6. 推送代码
git push -u origin main
```

### 📂 文件状态管理
```diff
# 查看状态
git status

# 添加特定文件
+ git add index.html src/

# 排除文件
- echo "node_modules/" >> .gitignore
```

---

## 五、❗常见问题
### 1. 推送被拒绝
```bash
# 先拉取最新代码（推荐）
git pull origin main

# 强制推送（慎用！）
git push -f origin main
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
git lfs track "*.psd" "*.zip"
git add .gitattributes
git commit -m "Add LFS tracking"
```

---

## 六、🖥️图形化工具推荐
| 工具 | 适用场景 | 下载链接 |
|------|----------|----------|
| GitHub Desktop | 新手友好 | [下载](https://desktop.github.com) |
| Sourcetree | 高级功能 | [下载](https://www.sourcetreeapp.com) |
| VS Code | 内置Git支持 | [下载](https://code.visualstudio.com) |

> 💡 提示：所有路径需替换为你的实际项目路径  
> ⚠️ 注意：执行`git push -f`前请确保了解风险