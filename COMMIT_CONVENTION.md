# Git 提交规范

## 提交格式

```
<类型>: <简短描述>

[可选：详细描述]
```

## 类型说明

| 类型 | 说明 | 示例 |
|------|------|------|
| `feat` | 新功能 | `feat: 添加坦克大战游戏` |
| `fix` | Bug 修复 | `fix: 修复游戏开始按钮` |
| `docs` | 文档更新 | `docs: 更新 README` |
| `style` | 代码格式 | `style: 格式化代码` |
| `refactor` | 重构 | `refactor: 重构游戏逻辑` |
| `perf` | 性能优化 | `perf: 优化渲染性能` |
| `test` | 测试 | `test: 添加单元测试` |
| `chore` | 构建/工具 | `chore: 更新依赖` |

## 提交示例

```bash
# 新功能
feat: 添加坦克大战 HTML 游戏

# Bug 修复
fix: 修复游戏开始按钮不响应问题

# 文档更新
docs: 添加项目开发日志

# 自动提交
./scripts/auto-commit.sh "feat: 添加新项目"
```

## 自动提交

```bash
# 使用自动提交脚本
./scripts/auto-commit.sh "feat: 新功能描述"

# 默认提交信息（时间戳）
./scripts/auto-commit.sh
```

---

*最后更新：2026-03-08*
