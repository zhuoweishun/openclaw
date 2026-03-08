# 部署指南 (Deployment Guide)

## 服务器信息

| 项目 | 值 |
|------|-----|
| 公网 IP | 106.54.51.133 |
| 内网 IP | 10.0.0.4 |
| 系统 | Ubuntu 24.04.4 LTS |
| 位置 | 腾讯轻量云服务器 |

---

## 部署场景

### 场景 1：OpenClaw Agents 部署

```bash
# 1. 启动所有 Agents
cd /root/.openclaw
pm2 start ecosystem.config.js

# 2. 查看状态
pm2 list

# 3. 查看日志
pm2 logs

# 4. 保存配置
pm2 save

# 5. 配置开机自启
pm2 startup
# 按提示运行生成的命令
```

**验证：**
```bash
# 检查 Gateway 状态
openclaw gateway status

# 测试飞书机器人
# 在飞书中发送消息测试
```

---

### 场景 2：静态网站部署（HTML/CSS/JS）

#### 方案 A：GitHub Pages（推荐）
```bash
# 1. 进入项目目录
cd /root/claude-workspace/openclaw-repo

# 2. 提交代码
git add .
git commit -m "feat: 更新网站"
git push origin main

# 3. 访问
# https://zhuoweishun.github.io/openclaw/
```

#### 方案 B：服务器托管
```bash
# 1. 安装 Nginx
apt install nginx -y

# 2. 复制项目文件
cp -r /root/claude-workspace/projects/tank-battle/* /var/www/html/

# 3. 重启 Nginx
systemctl restart nginx

# 4. 访问
# http://106.54.51.133/
```

---

### 场景 3：Node.js 应用部署

```bash
# 1. 进入项目目录
cd /root/claude-workspace/projects/my-node-app

# 2. 安装依赖
npm install

# 3. PM2 启动
pm2 start app.js --name my-node-app

# 4. 查看状态
pm2 status

# 5. 查看日志
pm2 logs my-node-app
```

**配置 Nginx 反向代理：**
```bash
# 1. 安装 Nginx
apt install nginx -y

# 2. 创建配置
cat > /etc/nginx/sites-available/my-app << 'EOF'
server {
    listen 80;
    server_name your-domain.com;

    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
EOF

# 3. 启用配置
ln -s /etc/nginx/sites-available/my-app /etc/nginx/sites-enabled/
nginx -t
systemctl reload nginx
```

---

### 场景 4：Python 应用部署

```bash
# 1. 进入项目目录
cd /root/claude-workspace/projects/my-python-app

# 2. 创建虚拟环境
python3 -m venv venv
source venv/bin/activate

# 3. 安装依赖
pip install -r requirements.txt

# 4. PM2 启动
pm2 start app.py --name my-python-app --interpreter python3

# 5. 或使用 Gunicorn
pip install gunicorn
gunicorn -w 4 -b 0.0.0.0:8000 app:app
```

---

### 场景 5：Docker 容器化部署

```bash
# 1. 创建 Dockerfile
cat > Dockerfile << 'EOF'
FROM node:22-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install --production
COPY . .
EXPOSE 3000
CMD ["node", "app.js"]
EOF

# 2. 构建镜像
docker build -t my-app .

# 3. 运行容器
docker run -d -p 80:3000 --name my-app-container my-app

# 4. 查看日志
docker logs my-app-container

# 5. 停止容器
docker stop my-app-container
```

**Docker Compose 多服务部署：**
```yaml
# docker-compose.yml
version: '3'
services:
  web:
    build: .
    ports:
      - "80:3000"
    restart: always
  redis:
    image: redis:alpine
    restart: always
```

```bash
# 启动所有服务
docker-compose up -d

# 查看状态
docker-compose ps

# 停止所有服务
docker-compose down
```

---

## 域名和 SSL 配置

### 1. 域名解析

```
在域名服务商处添加 A 记录：
@ → 106.54.51.133
www → 106.54.51.133
```

### 2. SSL 证书（Let's Encrypt 免费）

```bash
# 1. 安装 Certbot
apt install certbot python3-certbot-nginx -y

# 2. 获取证书
certbot --nginx -d your-domain.com -d www.your-domain.com

# 3. 自动续期
# Certbot 会自动配置定时任务
```

---

## 监控和维护

### PM2 监控
```bash
# 查看状态
pm2 list

# 查看日志
pm2 logs

# 重启应用
pm2 restart all

# 停止应用
pm2 stop all

# 删除应用
pm2 delete all
```

### Docker 监控
```bash
# 查看容器
docker ps

# 查看日志
docker logs <container-id>

# 查看资源使用
docker stats
```

### 系统监控
```bash
# 查看资源使用
htop

# 查看磁盘使用
df -h

# 查看网络
netstat -tlnp
```

---

## 备份策略

### 代码备份
```bash
# Git 自动推送
git push origin main
```

### 数据库备份
```bash
# SQLite 备份
cp data.db data.db.backup.$(date +%Y%m%d)

# MySQL 备份
mysqldump -u root -p database > backup.sql
```

### 全量备份
```bash
# 使用备份脚本
/root/claude-workspace/scripts/backup.sh
```

---

## 部署检查清单

部署前检查：

- [ ] 代码已测试
- [ ] Git 已提交
- [ ] 依赖已安装
- [ ] 环境变量已配置
- [ ] 数据库已迁移
- [ ] 备份已完成

部署后检查：

- [ ] 服务已启动
- [ ] 日志无错误
- [ ] 功能测试通过
- [ ] 监控已配置
- [ ] 备份已设置

---

## 故障排查

### 服务无法访问
```bash
# 1. 检查服务状态
pm2 list
systemctl status nginx
docker ps

# 2. 检查端口
netstat -tlnp | grep :80

# 3. 检查防火墙
ufw status
```

### 日志查看
```bash
# PM2 日志
pm2 logs

# Nginx 日志
tail -f /var/log/nginx/error.log

# 系统日志
journalctl -xe
```

### 重启服务
```bash
# PM2
pm2 restart all

# Nginx
systemctl restart nginx

# Docker
docker restart <container-id>
```

---

*最后更新：2026-03-08*
