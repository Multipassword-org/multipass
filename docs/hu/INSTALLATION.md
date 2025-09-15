# Telepítési Útmutató

## Gyors Indítás

### Docker Telepítés (Ajánlott)

1. **Repository klónozása**
```bash
git clone <repository-url>
cd multipass
```

2. **Környezeti fájl létrehozása**
```bash
cp .env.example .env
```

3. **Docker Compose indítása**
```bash
docker-compose up -d
```

4. **Adatbázis migrációk futtatása**
```bash
docker-compose exec app php artisan migrate --seed
```

5. **Alkalmazás elérése**
```
http://localhost:8000
```

### Manuális Telepítés

#### Előfeltételek
- PHP 8.3+
- Node.js 18+
- MariaDB 10.4+ vagy MySQL 8.0+
- Composer
- NPM

#### Telepítési Lépések

1. **Klónozás és beállítás**
```bash
git clone <repository-url>
cd multipass
composer install
npm install
```

2. **Környezeti konfiguráció**
```bash
cp .env.example .env
php artisan key:generate
```

3. **Adatbázis beállítása**
```bash
# Adatbázis konfigurálása .env fájlban
php artisan migrate --seed
```

4. **Eszközök építése**
```bash
npm run build
```

5. **Fejlesztői szerver indítása**
```bash
php artisan serve
```

## Alapértelmezett Bejelentkezési Adatok

- **Admin**: `admin@multipass.local` / `admin`
- **Felhasználó**: `user@multipass.local` / `user`

⚠️ **Változtassa meg ezeket a jelszavakat az első bejelentkezés után!**

## Éles Környezeti Telepítés

### Webszerver Konfiguráció

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

### Éles Környezeti Optimalizálás

```bash
# Éles függőségek telepítése
composer install --optimize-autoloader --no-dev

# Éles eszközök építése
npm run build

# Konfiguráció cache-elése
php artisan config:cache
php artisan route:cache
php artisan view:cache

# Jogosultságok beállítása
chown -R www-data:www-data storage bootstrap/cache
chmod -R 775 storage bootstrap/cache
```

## Hibaelhárítás

### Gyakori Problémák

**Composer problémák**: Composer frissítése és cache törlése
```bash
composer self-update
composer clear-cache
```

**Node.js problémák**: npm cache törlése
```bash
npm cache clean --force
rm -rf node_modules package-lock.json
npm install
```

**Adatbázis problémák**: Konfiguráció és jogosultságok ellenőrzése
```bash
php artisan config:clear
php artisan cache:clear
```

**Jogosultság problémák**: Helyes tulajdonjog beállítása
```bash
chown -R www-data:www-data storage bootstrap/cache
chmod -R 775 storage bootstrap/cache
```
