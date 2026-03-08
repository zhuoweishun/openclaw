# 自动化脚本手册

## 项目生命周期

### 1. 初始化项目
```bash
./scripts/init-project.sh my-project
```

### 2. 开发
```bash
# 编辑代码...
# 使用代码片段库
# 遵循代码规范
```

### 3. 提交
```bash
./scripts/auto-commit.sh "feat: 功能描述"
```

### 4. 部署
```bash
./scripts/deploy.sh
```

### 5. 备份
```bash
./scripts/backup.sh
```

### 6. 清理
```bash
./scripts/clean.sh --dry-run  # 预览
./scripts/clean.sh            # 执行
```

---

## 脚本列表

| 脚本 | 用途 | 命令 |
|------|------|------|
| init-project.sh | 初始化新项目 | `./init-project.sh 项目名` |
| auto-commit.sh | 自动提交 | `./auto-commit.sh "提交信息"` |
| deploy.sh | 部署到 GitHub | `./deploy.sh` |
| backup.sh | 备份工作区 | `./backup.sh` |
| clean.sh | 清理临时文件 | `./clean.sh [--dry-run]` |
| generate-report.sh | 生成报告 | `./generate-report.sh [项目名]` |
| status.sh | 查看状态 | `./status.sh` |
| scan-secrets.sh | 敏感信息扫描 | `./scan-secrets.sh` |
| check-permissions.sh | 权限检查 | `./check-permissions.sh` |
| config-helper.sh | 配置助手 | `./config-helper.sh 项目名` |

---

## 监控和维护

### 查看状态
```bash
./scripts/status.sh
```

### 生成报告
```bash
./scripts/generate-report.sh
```

### 安全检查
```bash
./scripts/scan-secrets.sh
./scripts/check-permissions.sh
```

---

*最后更新：2026-03-08*
