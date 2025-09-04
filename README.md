# WordPress + MySQL + phpMyAdmin Docker Setup

A complete Docker Compose configuration for running WordPress with MySQL database and phpMyAdmin interface.

Read util end for Cleanup proocess. Once the Project is done make sure you stop the running containers and Delete the Containers and Images as well.

## 🚀 Quick Start

```bash
# Clone and start
git clone https://github.com/31RahulPatel/docker-wordpress-mysql-phpmyadmin.git
cd wordpress
docker compose up -d

# Access services
# WordPress: http://localhost:8080
# phpMyAdmin: http://localhost:8081
```

## 📋 Prerequisites

For Windows :
- [Docker Desktop](https://www.docker.com/products/docker-desktop/) installed


## 🔧 Services

| Service | Image | Port | Purpose |
|---------|-------|------|---------|
| WordPress | `wordpress:6.5-php8.3-apache` | 8080 | CMS Frontend |
| MySQL | `mysql:8.0` | 3306 | Database |
| phpMyAdmin | `phpmyadmin:latest` | 8081 | DB Management |

## 🔑 Default Credentials

**MySQL:**
- Root Password: `password`
- Database: `wordpress`
- User: `wordpress`
- Password: `wordpress`

**phpMyAdmin:**
- Username: `root`
- Password: `RootPass123!`

## 📁 Project Structure

```
wordpress/
├── docker-compose.yaml    # Main configuration
├── README.md             # This file
└── volumes/              # Created automatically
    ├── db_data/          # MySQL data
    └── wordpress_data/   # WordPress files
```

## 🛠️ Commands

```bash
# Start services
docker compose up -d

# View logs
docker compose logs -f

# Stop services
docker compose down

# Stop and remove data (⚠️ destructive)
docker compose down -v

# Restart specific service
docker compose restart wordpress
```

## 🌐 Access URLs

- **WordPress Site:** http://localhost:8080
- **WordPress Admin:** http://localhost:8080/wp-admin
- **phpMyAdmin:** http://localhost:8081

## 🔄 Development Workflow

1. **Initial Setup:**
   ```bash
   docker compose up -d
   ```

2. **WordPress Installation:**
   - Visit http://localhost:8080
   - Follow WordPress setup wizard
   - Use database credentials above

3. **Database Management:**
   - Access phpMyAdmin at http://localhost:8081
   - Login with root credentials

## 📊 Monitoring

Check service status:
```bash
docker compose ps
docker compose logs wordpress
docker compose logs db
```

## 🔧 Customization (Extras):

### Change Ports
Edit `docker-compose.yaml`:
```yaml
ports:
  - "8080:80"  # Change 8080 to your preferred port
```

### Update Passwords
Modify environment variables in `docker-compose.yaml`:
```yaml
environment:
  MYSQL_ROOT_PASSWORD: YourNewPassword
```

### Add SSL/HTTPS
Mount certificates and update WordPress configuration:
```yaml
volumes:
  - ./certs:/etc/ssl/certs
```

## 🚨 Troubleshooting

**WordPress can't connect to database:**
```bash
docker compose logs db
docker compose restart wordpress
```

**Port already in use:**
```bash
# Check what's using the port
lsof -i :8080
# Change port in docker-compose.yaml
```

**Permission issues:**
```bash
docker compose exec wordpress chown -R www-data:www-data /var/www/html
```

## 🧹 Cleanup

Remove everything (including data):
```bash
docker compose down -v --remove-orphans
docker system prune -a
```
CONFIRM :
```bash
docker ps 
docker ps -a
docker images
```

## 📚 Resources

- [WordPress Documentation](https://wordpress.org/support/)
- [Docker Compose Reference](https://docs.docker.com/compose/)
- [MySQL Docker Hub](https://hub.docker.com/_/mysql)
- [phpMyAdmin Documentation](https://docs.phpmyadmin.net/)

## 🤝 Contributing

1. Fork the repository
2. Create feature branch
3. Make changes
4. Test locally
5. Submit pull request

---

**Note:** This setup is optimized for development. For production, consider adding SSL certificates, security hardening, and backup strategies.