# Raspberry Pi Zero 2 W Docker Stack

A complete Docker stack for Raspberry Pi Zero 2 W including web server, database, and various management tools.

🔍 [Live Preview](https://mineraleyt.github.io/pi2w-docker/) - See the stack in action before installing!

## Services

- **NGINX**: Web server
- **MariaDB**: Database server
- **phpMyAdmin**: Database management interface
- **Pi-hole**: Network-wide ad blocking
- **Portainer**: Docker container management
- **Watchtower**: Automatic container updates

## Prerequisites

- Raspberry Pi Zero 2 W with Raspberry Pi OS installed
- Git installed (`sudo apt-get install git`)
- Internet connection
- SSH access to your Raspberry Pi (recommended)

## Quick Start

1. Clone this repository:
```bash
git clone https://github.com/mineraleyt/pi2w-docker.git
cd pi2w-docker
```

2. Create environment file:
```bash
cp .env.example .env
```

3. Edit the environment file with your settings:
```bash
nano .env
```

4. Make the installation script executable:
```bash
chmod +x install.sh
```

5. Run the installation script:
```bash
./install.sh
```

6. Start the services:
```bash
docker compose up -d
```

## Default Ports

- NGINX: 80
- MariaDB: 3306
- phpMyAdmin: 8080
- Pi-hole: 8081 (admin interface), 53 (DNS)
- Portainer: 9000

All ports can be customized in the `.env` file.

## Configuration

### Environment Variables

Copy `.env.example` to `.env` and configure:

- `MYSQL_ROOT_PASSWORD`: MariaDB root password
- `MYSQL_DATABASE`: Default database name
- `MYSQL_USER`: Database user
- `MYSQL_PASSWORD`: Database user password
- `PIHOLE_WEBPASSWORD`: Pi-hole admin password
- `PIHOLE_TZ`: Your timezone
- Various port configurations

### Service Directories

- `nginx/html`: Web files
- `nginx/conf.d`: NGINX configuration
- `mariadb`: MariaDB data (auto-created)
- `pihole`: Pi-hole configuration (auto-created)

## Usage

### Starting Services
```bash
docker compose up -d
```

### Stopping Services
```bash
docker compose down
```

### Viewing Logs
```bash
docker compose logs -f
```

### Updating Containers
Watchtower automatically updates containers daily at 4 AM.

For manual updates:
```bash
docker compose pull
docker compose up -d
```

## Web Interfaces

- Main Page: `http://[YOUR-PI-IP]`
- Portainer: `http://[YOUR-PI-IP]:9000`
- phpMyAdmin: `http://[YOUR-PI-IP]:8080`
- Pi-hole: `http://[YOUR-PI-IP]:8081/admin`

## Security Considerations

1. Change all default passwords in `.env`
2. Use strong passwords
3. Consider enabling HTTPS
4. Regularly update your system and containers
5. Consider using Docker secrets for sensitive data

## Backup

### Database Backup
```bash
docker compose exec mariadb mysqldump -u root -p[YOUR-PASSWORD] [DATABASE] > backup.sql
```

### Restore Database
```bash
cat backup.sql | docker compose exec -i mariadb mysql -u root -p[YOUR-PASSWORD] [DATABASE]
```

## Troubleshooting

1. Check service status:
```bash
docker compose ps
```

2. View service logs:
```bash
docker compose logs [SERVICE_NAME]
```

3. Restart a service:
```bash
docker compose restart [SERVICE_NAME]
```

## Contributing

1. Fork the repository
2. Create your feature branch
3. Commit your changes
4. Push to the branch
5. Create a new Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
