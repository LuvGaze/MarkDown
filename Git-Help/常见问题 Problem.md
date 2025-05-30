
# 🚀 GitHub 使用常见问题解决方案大全

## 📚 目录
1. [🔧 仓库操作问题](#一、🔧仓库操作问题)
2. [🔐 认证与权限问题](#二、🔐认证与权限问题)
3. [🌿 分支与合并问题](#三、🌿分支与合并问题)
4. [⚙️ 配置与优化问题](#四、⚙️配置与优化问题)
5. [🎯 特殊场景处理](#五、🎯特殊场景处理)
6. [✨ 实用技巧](#六、✨实用技巧)

---

## 一、🔧仓库操作问题

### 1. ❗ 误删本地仓库如何恢复？
```bash
# 🔄 重新克隆远程仓库
git clone https://github.com/username/repo.git
```

### 2. 🗑️ 如何彻底删除提交历史？
```bash
# ✨ 创建新分支
git checkout --orphan new_branch
git add .
git commit -m "Initial commit"
git branch -D main
git branch -m main
git push -f origin main
```

### 3. ✏️ 如何修改最近提交信息？
```bash
git commit --amend -m "新的提交信息"
git push -f origin branch_name
```

---

## 二、🔐认证与权限问题

### 1. 🔒 HTTPS 认证失败（403错误）
```bash
# 🔑 解决方案：
# 1. 生成个人访问令牌（PAT）
#    GitHub → Settings → Developer settings → Personal access tokens
# 2. 使用令牌代替密码
git config --global credential.helper cache
git push
# 💡 提示输入密码时粘贴令牌
```

### 2. ⏳ SSH 连接超时
```bash
# 🛠️ 测试连接
ssh -T git@github.com

# 🌐 解决方案：
# 1. 检查~/.ssh/config文件
Host github.com
  Hostname ssh.github.com
  Port 443
  User git
# 2. 重启ssh服务
sudo service ssh restart
```

---

## 三、🌿分支与合并问题

### 1. ↩️ 如何撤销合并？
```bash
# 📜 查看合并提交记录
git log --merges

# ⏪ 撤销特定合并
git revert -m 1 <merge-commit-hash>
```

### 2. ⚔️ 分支冲突解决流程
```bash
# 1. 🔍 查看冲突文件
git status

# 2. ✋ 手动解决冲突后标记为已解决
git add conflicted_file.txt

# 3. ✅ 继续合并
git commit
```

### 3. ♻️ 误删远程分支恢复
```bash
# 🕵️ 查看本地引用记录
git reflog

# 🔄 恢复分支
git checkout -b recovered_branch HEAD@{5}
git push origin recovered_branch
```

---

## 四、⚙️配置与优化问题

### 1. 🚀 加速GitHub访问
```bash
# 🌍 修改hosts文件（需管理员权限）
140.82.113.3 github.com
199.232.69.194 github.global.ssl.fastly.net

# 🪞 或使用镜像地址
git config --global url."https://hub.fastgit.org".insteadOf https://github.com
```

### 2. 🔌 设置代理
```bash
# 🌐 HTTP代理
git config --global http.proxy http://127.0.0.1:1080

# 🧦 SOCKS5代理
git config --global http.proxy socks5://127.0.0.1:1080
```

### 3. 🧹 清理大文件历史
```bash
# 🧰 使用BFG工具
java -jar bfg.jar --strip-blobs-bigger-than 100M repo.git
git reflog expire --expire=now --all
git gc --prune=now --aggressive
```

---

## 五、🎯特殊场景处理

### 1. 🧩 处理子模块(Submodule)
```bash
# 📦 克隆包含子模块的仓库
git clone --recurse-submodules https://github.com/username/repo.git

# 🔄 更新子模块
git submodule update --init --recursive
```

### 2. ⏮️ 恢复误删的文件
```bash
# 🔎 查看删除记录
git log --diff-filter=D -- path/to/file

# ⏪ 恢复指定版本
git checkout <commit-hash>^ -- path/to/file
```

### 3. ✂️ 拆分大仓库
```bash
# 🪚 使用filter-branch
git filter-branch --prune-empty --subdirectory-filter subfolder branch_name
```

---

## 六、✨实用技巧
### 1. 📅 查看贡献日历
```bash
git log --pretty=format:"%ad" --date=short | uniq -c
```

### 2. 🔍 搜索所有提交内容
```bash
git grep "搜索关键词" $(git rev-list --all)
```

### 3. 📊 统计代码贡献量
```bash
git log --author="用户名" --pretty=tformat: --numstat | awk '{ add += $1; subs += $2 } END { printf "📈 添加行数: %s\n📉 删除行数: %s\n", add, subs }'
```

> ⚠️ 提示：执行危险操作前建议先创建备份分支