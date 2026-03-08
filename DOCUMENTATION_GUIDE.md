# 文档编写指南

## 文档类型

| 类型 | 用途 | 模板位置 |
|------|------|---------|
| README.md | 项目说明 | PROJECT_TEMPLATE/ |
| DEVELOPMENT_LOG.md | 开发日志 | PROJECT_TEMPLATE/ |
| API_DOCS.md | API 文档 | PROJECT_TEMPLATE/ |
| ADR_TEMPLATE.md | 架构决策 | PROJECT_TEMPLATE/ |
| ISSUE_TRACKER.md | 问题追踪 | PROJECT_TEMPLATE/ |
| CHANGELOG.md | 变更日志 | 根目录 |

---

## 文档规范

### 1. README.md（必须有）

每个项目必须有的说明文档：
- 项目简介
- 技术栈
- 快速开始
- 文件结构

### 2. 开发日志（推荐）

每天记录：
- 完成的工作
- 遇到的问题
- 解决方案
- 明日计划

### 3. API 文档（有 API 时）

包含：
- 基础信息
- 认证方式
- 接口列表
- 错误码

### 4. 架构决策（重要项目）

记录重大技术决策：
- 背景
- 决策内容
- 备选方案
- 影响分析

### 5. 问题追踪（团队协作）

记录 Bug 和功能请求：
- 问题描述
- 复现步骤
- 解决方案
- 状态跟踪

---

## 文档更新流程

```
1. 创建/修改文档
2. 自审内容准确性
3. Git 提交
4. 更新 CHANGELOG.md
```

---

## 文档检查清单

项目发布前检查：

- [ ] README.md 完整
- [ ] 代码有注释
- [ ] API 文档更新
- [ ] CHANGELOG.md 更新
- [ ] 敏感信息已移除

---

*最后更新：2026-03-08*
