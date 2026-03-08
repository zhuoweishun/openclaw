# 访问控制规范

## 权限管理

### 文件权限

```bash
# 脚本文件（可执行）
chmod +x script.sh

# 配置文件（仅所有者可读写）
chmod 600 .env
chmod 600 *.key

# 普通文件（所有者读写，其他人只读）
chmod 644 README.md

# 目录（所有者完全控制，其他人可读可执行）
chmod 755 projects/
```

### 推荐权限设置

| 文件类型 | 权限 | 命令 |
|---------|------|------|
| 脚本文件 | 755 | `chmod +x` |
| .env 文件 | 600 | `chmod 600 .env` |
| 私钥文件 | 600 | `chmod 600 *.key` |
| 普通文件 | 644 | `chmod 644 file` |
| 目录 | 755 | `chmod 755 dir` |

---

## Git 权限

### 提交权限

```
✅ 只有授权用户可以推送到 main 分支
✅ 重要项目启用分支保护
✅ 启用 Pull Request 审查
```

### 分支保护

```bash
# GitHub 设置 → Branches → Add rule
# 分支模式：main
# 选项：
# - Require pull request reviews
# - Require status checks to pass
# - Include administrators
```

---

## 服务器访问

### SSH 密钥

```bash
# 生成密钥
ssh-keygen -t ed25519 -C "your_email@example.com"

# 设置权限
chmod 600 ~/.ssh/id_ed25519
chmod 644 ~/.ssh/id_ed25519.pub

# 添加到 GitHub
cat ~/.ssh/id_ed25519.pub
# 复制输出到 GitHub → Settings → SSH Keys
```

### SSH 配置

```bash
# ~/.ssh/config
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519
  AddKeysToAgent yes
```

---

## 敏感操作清单

以下操作需要特别注意：

- [ ] 部署到生产环境
- [ ] 修改 API 密钥
- [ ] 访问用户数据
- [ ] 修改数据库
- [ ] 更改服务器配置
- [ ] 推送代码到 main 分支

---

## 安全检查清单

每周检查：

- [ ] 审查 Git 提交历史
- [ ] 检查 .env 文件权限
- [ ] 扫描敏感信息泄露
- [ ] 审查访问日志
- [ ] 更新依赖包

---

*最后更新：2026-03-08*
