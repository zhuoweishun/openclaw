# PM2 进程管理指南

## 什么是 PM2？

PM2 是 Node.js 应用的进程管理工具，支持：
- 自动重启
- 日志管理
- 内存限制
- 开机自启
- 多实例管理

---

## 基本命令

### 启动应用
```bash
# 启动单个文件
pm2 start app.js

# 指定名称
pm2 start app.js --name my-app

# 指定实例数
pm2 start app.js -i 4

# 使用配置文件
pm2 start ecosystem.config.js
```

### 查看状态
```bash
# 列表
pm2 list

# 详细信息
pm2 show <app-name>

# 监控
pm2 monit
```

### 日志管理
```bash
# 查看所有日志
pm2 logs

# 查看指定应用日志
pm2 logs <app-name>

# 清空日志
pm2 flush
```

### 控制应用
```bash
# 重启
pm2 restart <app-name>
pm2 restart all

# 停止
pm2 stop <app-name>
pm2 stop all

# 删除
pm2 delete <app-name>
pm2 delete all
```

---

## 开机自启

### 配置自启
```bash
# 生成启动命令
pm2 startup

# 按提示运行生成的命令，例如：
# sudo env PATH=$PATH:/usr/bin pm2 startup systemd -u root --hp /root

# 保存当前进程列表
pm2 save

# 恢复进程
pm2 resurrect
```

---

## 配置文件示例

### ecosystem.config.js
```javascript
module.exports = {
  apps: [
    {
      name: 'my-app',
      script: 'app.js',
      instances: 1,
      autorestart: true,
      watch: false,
      max_memory_restart: '1G',
      env: {
        NODE_ENV: 'production',
        PORT: 3000
      }
    }
  ]
};
```

### 使用配置
```bash
# 启动
pm2 start ecosystem.config.js

# 重启
pm2 restart ecosystem.config.js

# 停止
pm2 stop ecosystem.config.js
```

---

## 内存限制

```javascript
{
  max_memory_restart: '1G'  // 超过 1GB 自动重启
}
```

---

## 集群模式

```bash
# 启动 4 个实例（负载均衡）
pm2 start app.js -i 4

# 根据 CPU 核心数自动启动
pm2 start app.js -i max
```

---

## 健康检查

```bash
# 监控面板
pm2 monit

# JSON 格式状态
pm2 list --json

# 检查单个应用
pm2 show <app-name>
```

---

## 常见问题

### 应用无法启动
```bash
# 查看日志
pm2 logs <app-name>

# 查看错误
pm2 logs <app-name> --err
```

### 内存占用过高
```bash
# 重启应用
pm2 restart <app-name>

# 调整内存限制
# 修改 max_memory_restart
```

### 日志文件过大
```bash
# 清空日志
pm2 flush

# 配置日志轮转
# 在 ecosystem.config.js 中添加：
{
  max_lines: 10000,
  max_size: '10M'
}
```

---

*最后更新：2026-03-08*
