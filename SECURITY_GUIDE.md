# 安全配置指南

## 🔒 密钥管理

### 基本原则

```
✅ 敏感信息放入 .env 文件
✅ .env 文件加入 .gitignore
✅ 使用 .env.example 作为模板
✅ 生产环境使用独立配置
```

### 什么是敏感信息？

```
❌ 不要提交：
- API Key / API Secret
- 数据库密码
- 第三方服务密钥
- 私钥文件 (.pem, .key)
- 个人身份信息

✅ 可以提交：
- 代码文件
- 配置文件模板
- 公开的资源文件
```

---

## 📁 .env 使用规范

### 创建 .env 文件

```bash
# 1. 复制模板
cp .env.example .env

# 2. 编辑 .env（填入真实值）
nano .env

# 3. 确认 .env 在 .gitignore 中
cat .gitignore | grep .env
```

### .env 示例

```bash
# .env
API_KEY=sk-xxx-真实密钥
DB_PASSWORD=真实密码

# .env.example（可以提交）
API_KEY=your_api_key_here
DB_PASSWORD=your_db_password
```

---

## 🔍 敏感信息扫描

### 检查是否泄露

```bash
# 检查 Git 历史中是否有敏感文件
git log --all --full-history -- "**/.env"

# 检查当前文件
grep -r "API_KEY\|SECRET\|PASSWORD" --exclude="*.example" .
```

### 如果已经泄露

```bash
# 1. 立即撤销密钥
# 2. 从 Git 历史中删除
git filter-branch --force --index-filter \
  "git rm --cached --ignore-unmatch path/to/secret" \
  --prune-empty --tag-name-filter cat -- --all

# 3. 强制推送
git push origin --force --all
```

---

## 🛡️ 最佳实践

### 1. 环境变量

```javascript
// ✅ 正确：从环境变量读取
const apiKey = process.env.API_KEY;

// ❌ 错误：硬编码
const apiKey = "sk-xxx-真实密钥";
```

### 2. 配置文件

```javascript
// ✅ config.js
const config = {
  apiKey: process.env.API_KEY,
  env: process.env.NODE_ENV || 'development'
};

module.exports = config;
```

### 3. 部署时

```bash
# ✅ 在服务器上设置环境变量
export API_KEY="真实密钥"
npm start

# 或使用 .env 文件
# 确保 .env 不被上传
```

---

## 📋 检查清单

部署前检查：

- [ ] .env 文件未提交
- [ ] .gitignore 包含敏感文件
- [ ] 代码中无硬编码密钥
- [ ] 使用环境变量
- [ ] API 密钥有访问限制

---

*最后更新：2026-03-08*
