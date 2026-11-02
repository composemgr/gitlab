## 👋 Welcome to gitlab 🚀

The DevOps platform built on a single application

## 📋 Description

The DevOps platform built on a single application

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
cp default.env .env
docker compose --env-file .env up -d
```

### Option 3: Using composemgr
```bash
composemgr install gitlab
```

## 🔧 Configuration

### Environment Variables

```shell
TZ=America/New_York
BASE_HOST_NAME=gitlab.example.com
APP_ADMIN_PASS=replace-with-a-random-password
EMAIL_SERVER_HOST=172.17.0.1
EMAIL_SERVER_PORT=587
```

See `docker-compose.yaml` for complete list of configurable options.

Further GitLab settings are made in the omnibus config mounted at
`./volumes/config/gitlab/gitlab.rb`. The compose file seeds
`GITLAB_OMNIBUS_CONFIG`; values you add to `gitlab.rb` take effect on the next
`docker compose --env-file .env up -d`.

### Environment Files

`default.env.sample` holds the full set of variables and is copied to `.env`
before starting the stack:

```bash
cp default.env .env
docker compose --env-file .env up -d
```

`app.env.sample` holds the app-specific overrides and is copied to `app.env`:

```bash
cp app.env.sample app.env
```

`composemgr up` applies `app.env` and `default.env` automatically. Raw
`docker compose` commands need `--env-file .env` to pick up the same values.

### Reverse Proxy

Three standalone compose files ship in this repo:

| File | Use |
|------|-----|
| `docker-compose.yaml` | Default, published on `172.17.0.1:64186` |
| `docker-compose.traefik.yaml` | Behind an existing external `traefik` network |
| `docker-compose.tunnel.yaml` | Behind an existing external `cloudflare` tunnel network |

```bash
docker compose -f docker-compose.traefik.yaml --env-file .env up -d
```

The proxy variants publish no ports at all, so GitLab's SSH service is not
reachable from the host in any variant.

## 🌐 Access

- **Web Interface**: http://172.17.0.1:64186

GitLab's built-in SSH service is reachable only inside the project network;
no host port is published for it. Use HTTPS remotes for host access.

Non-HTTP protocol ports are published identically in all three compose variants, because they cannot be proxied over HTTP: `2224` (Git SSH, container `22`).

## 📂 Volumes

- `./volumes/config/gitlab` - Omnibus configuration (`gitlab.rb`)
- `./volumes/logs/gitlab` - GitLab logs
- `./volumes/data/gitlab` - Repositories, database, and application data

## 🔐 Security

- Set `APP_ADMIN_PASS` to a strong random password before the first start; it
  only applies to the initial `root` account
- GitLab needs at least 4GB of RAM; `shm_size` is set to 4g for this reason
- GitLab sends transactional emails; configure a real SMTP relay
- Configure HTTPS using a reverse proxy (nginx, traefik, caddy)
- Regularly update Docker images for security patches
- Backup your data regularly

## 🔍 Logging

```shell
docker compose --env-file .env logs -f app
```

## 🛠️ Management

```bash
# Start services
docker compose --env-file .env up -d

# Stop services
docker compose --env-file .env down

# Update to latest images
docker compose --env-file .env pull && docker compose --env-file .env up -d

# View logs
docker compose --env-file .env logs -f

# Restart services
docker compose --env-file .env restart
```

## 📋 Requirements

- Docker Engine 20.10+
- Docker Compose V2+
- 4GB+ of RAM

## 🤝 Author

🤖 casjay: [Github](https://github.com/casjay) 🤖  
🦄 composemgr: [Github](https://github.com/composemgr) 🦄
