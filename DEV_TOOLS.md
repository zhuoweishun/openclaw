# 开发工具手册

## 快速命令

### 项目创建
```bash
# 从模板创建新项目
cp -r /root/claude-workspace/scripts/PROJECT_TEMPLATE \
      /root/claude-workspace/projects/新项目名

# 初始化配置
./scripts/config-helper.sh 新项目名
```

### Git 操作
```bash
# 自动提交
./scripts/auto-commit.sh "feat: 功能描述"

# 查看状态
git status

# 查看历史
git log --oneline -10

# 推送
git push origin main
```

### 部署
```bash
# 部署到 GitHub Pages
./scripts/deploy.sh

# 备份
./scripts/backup.sh
```

### 安全检查
```bash
# 扫描敏感信息
./scripts/scan-secrets.sh

# 检查权限
./scripts/check-permissions.sh
```

---

## 代码片段

位置：`/root/claude-workspace/scripts/SNIPPETS/`

| 类型 | 文件 |
|------|------|
| HTML | `html-snippets.md` |
| CSS | `css-snippets.md` |
| JavaScript | `js-snippets.md` |

---

## 模板文件

位置：`/root/claude-workspace/scripts/PROJECT_TEMPLATE/`

| 模板 | 用途 |
|------|------|
| `README.md` | 项目说明 |
| `index.html` | HTML 模板 |
| `style.css` | CSS 模板 |
| `app.js` | JS 模板 |
| `package.json` | Node 配置 |
| `.env.example` | 环境变量模板 |

---

## 文档模板

| 文档 | 用途 |
|------|------|
| `DEVELOPMENT_LOG.md` | 开发日志 |
| `API_DOCS.md` | API 文档 |
| `ADR_TEMPLATE.md` | 架构决策 |
| `ISSUE_TRACKER.md` | 问题追踪 |

---

## 在线资源

| 资源 | URL |
|------|-----|
| GitHub | https://github.com/zhuoweishun/openclaw |
| GitHub Pages | https://zhuoweishun.github.io/openclaw/ |

---

*最后更新：2026-03-08*
