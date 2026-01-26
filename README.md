## 👋 Welcome to gitlab 🚀

Complete DevOps platform with Git repository management

## 📋 Description

Complete DevOps platform with Git repository management

## 🚀 Services

- **app**: gitlab/gitlab-ce:latest

## 📦 Installation

### Option 1: Quick Install
```bash
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/gitlab/main/docker-compose.yaml" -o compose.yml
```

### Option 2: Git Clone
```bash
git clone "https://github.com/composemgr/gitlab" ~/.local/srv/docker/gitlab
cd ~/.local/srv/docker/gitlab
docker compose up -d
```

### Option 3: Using composemgr
```bash
composemgr install gitlab
```

## 🔧 Configuration

### Environment Variables

```shell
TZ=America/New_York
TZ=America/New_York
APP_ADMIN_USER=root
APP_ADMIN_PASS=changeme_admin_password
EMAIL_SERVER_PORT=587
EMAIL_SERVER_HOST=172.17.0.1
EMAIL_SERVER_MAIL_FROM=no-reply@${BASE_DOMAIN_NAME:-${BASE_HOST_NAME
```

See `docker-compose.yaml` for complete list of configurable options.

## 🌐 Access

- **Web Interface**: http://172.17.0.1:59129

## 📂 Volumes

- `./rootfs/config/gitlab` - Data storage
- `./rootfs/data/log/gitlab` - Data storage
- `./rootfs/data/gitlab` - Data storage

## 🔐 Security

- Change all default passwords before deploying to production
- Use strong secrets for all authentication tokens
- Configure HTTPS using a reverse proxy (nginx, traefik, caddy)
- Regularly update Docker images for security patches
- Backup your data regularly

## 🔍 Logging

```shell
docker compose logs -f app
```

## 🛠️ Management

```bash
# Start services
docker compose up -d

# Stop services
docker compose down

# Update to latest images
docker compose pull && docker compose up -d

# View logs
docker compose logs -f

# Restart services
docker compose restart
```

## 📋 Requirements

- Docker Engine 20.10+
- Docker Compose V2+

## 🤝 Author

🤖 casjay: [Github](https://github.com/casjay) 🤖  
🦄 composemgr: [Github](https://github.com/composemgr) 🦄
