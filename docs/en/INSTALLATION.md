# Installation Guide

## Quick Start

### Docker Installation (Recommended)

1. **Clone the repository**
```bash
git clone <repository-url>
cd multipass
```

2. **Create environment file**
```bash
cp .env.example .env
```

3. **Start with Docker Compose**
```bash
docker-compose up -d
```

4. **Run database migrations**
```bash
docker-compose exec app php artisan migrate --seed
```

5. **Access the application**
```
http://localhost:8000
```

### Manual Installation

#### Prerequisites
- PHP 8.3+
- Node.js 18+
- MariaDB 10.4+ or MySQL 8.0+
- Composer
- NPM

#### Installation Steps

1. **Clone and setup**
```bash
git clone <repository-url>
cd multipass
composer install
npm install
```

2. **Environment configuration**
```bash
cp .env.example .env
php artisan key:generate
```

3. **Database setup**
```bash
# Configure database in .env
php artisan migrate --seed
```

4. **Build assets**
```bash
npm run build
```

5. **Start development server**
```bash
php artisan serve
```

## Default Credentials

- **Admin**: `admin@multipass.local` / `admin`
- **User**: `user@multipass.local` / `user`

⚠️ **Change these passwords immediately after first login!**

## Production Deployment

### Web Server Configuration

#### Nginx
```nginx
server {
    listen 80;
    server_name your-domain.com;
    root /path/to/multipass/public;

    index index.php;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        fastcgi_pass unix:/var/run/php/php8.3-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
        include fastcgi_params;
    }
}
```

#### Apache
```apache
<VirtualHost *:80>
    ServerName your-domain.com
    DocumentRoot /path/to/multipass/public

    <Directory /path/to/multipass/public>
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
```

### Production Optimization

```bash
# Install production dependencies
composer install --optimize-autoloader --no-dev

# Build production assets
npm run build

# Cache configuration
php artisan config:cache
php artisan route:cache
php artisan view:cache

# Set permissions
chown -R www-data:www-data storage bootstrap/cache
chmod -R 775 storage bootstrap/cache
```

## Troubleshooting

### Common Issues

**Composer issues**: Update Composer and clear cache
```bash
composer self-update
composer clear-cache
```

**Node.js issues**: Clear npm cache
```bash
npm cache clean --force
rm -rf node_modules package-lock.json
npm install
```

**Database issues**: Check configuration and permissions
```bash
php artisan config:clear
php artisan cache:clear
```

**Permission issues**: Set correct ownership
```bash
chown -R www-data:www-data storage bootstrap/cache
chmod -R 775 storage bootstrap/cache
```
