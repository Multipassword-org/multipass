# Multipass Jelszókezelő - Teljes Dokumentáció

## Tartalomjegyzék

1. [Áttekintés](#áttekintés)
2. [Funkciók](#funkciók)
3. [Technológiai Stack](#technológiai-stack)
4. [Telepítés](#telepítés)
   - [Rendszerkövetelmények](#rendszerkövetelmények)
   - [Docker Telepítés](#docker-telepítés)
   - [Manuális Telepítés](#manuális-telepítés)
5. [Konfiguráció](#konfiguráció)
6. [Használati Útmutató](#használati-útmutató)
7. [API Dokumentáció](#api-dokumentáció)
8. [Biztonság](#biztonság)
9. [Hibaelhárítás](#hibaelhárítás)
10. [Fejlesztés](#fejlesztés)

## Áttekintés

**Multipass** egy modern, biztonságos jelszókezelő alkalmazás, amely Laravel 12 backend és React 19 frontend technológiákra épül. Vállalati szintű biztonságot biztosít felhasználóbarát felülettel, támogatva mind az egyéni, mind a csapat használatot.

### Fő Célkitűzések
- **Biztonság**: End-to-end titkosítás minden tárolt adathoz
- **Felhasználói Élmény**: Modern, intuitív felület sötét mód támogatással
- **Skálázhatóság**: Többfelhasználós támogatás szerepkör-alapú hozzáférés-vezérléssel
- **Hozzáférhetőség**: Többnyelvű támogatás (angol/magyar) és reszponzív design

## Funkciók

### 🔐 Alapvető Biztonsági Funkciók
- **End-to-End Titkosítás**: Minden jelszó AES-256 titkosítással
- **Kétfaktoros Autentikáció (2FA)**: TOTP-alapú 2FA támogatás
- **Szerepkör-alapú Hozzáférés-vezérlés**: Admin és felhasználói szerepkörök részletes jogosultságokkal
- **Munkamenet Kezelés**: Biztonságos munkamenet kezelés automatikus kijelentkezéssel
- **Aktivitás Naplózás**: Átfogó audit nyomvonal minden művelethez

### 👥 Felhasználókezelés
- **Többfelhasználós Támogatás**: Családi és csapat használati forgatókönyvek
- **LDAP/Active Directory Integráció**: Vállalati autentikáció
- **Felhasználói Csoportok**: Felhasználók szervezése csoportokba megosztott jogosultságokkal
- **Privát Mappák**: Automatikus privát mappa létrehozás minden felhasználóhoz
- **Felhasználói Profilok**: Átfogó felhasználói profil kezelés

### 📁 Szervezés és Kezelés
- **Hierarchikus Mappák**: Fa és lista nézet drag-and-drop támogatással
- **Egyedi Mezők**: Egyedi mezők definiálása jelszó bejegyzésekhez
- **Jelszó Generálás**: Beépített erős jelszó generátor
- **Import/Export**: Különböző jelszókezelő formátumok támogatása
- **Keresés és Szűrés**: Fejlett keresési és szűrési lehetőségek

### 🌐 Vállalati Funkciók
- **LDAP Integráció**: Teljes LDAP/AD szinkronizáció
- **Email Rendszer**: SMTP konfiguráció egyedi sablonokkal
- **Karbantartási Mód**: Rendszer karbantartás csak admin hozzáféréssel
- **Rendszer Beállítások**: Átfogó rendszer konfiguráció
- **Licenc Kezelés**: Licenc validáció és kezelés
- **Aktivitás Monitorozás**: Valós idejű aktivitás naplók és monitorozás

### 🎨 Felhasználói Felület
- **Reszponzív Design**: Mobilbarát felület
- **Sötét Mód**: Automatikus és manuális téma váltás
- **Többnyelvű**: Angol és magyar támogatás
- **Modern UI**: Tailwind CSS és Radix UI komponensekre építve
- **Hozzáférhetőség**: WCAG megfelelő felület

## Technológiai Stack

### Backend
- **Laravel 12**: Modern PHP framework MVC architektúrával
- **PHP 8.3**: Legújabb PHP verzió modern funkciókkal
- **MariaDB**: Elsődleges adatbázis JSON optimalizációval
- **Redis**: Cache és munkamenet tárolás
- **Queue Rendszer**: Háttér feladat feldolgozás

### Frontend
- **React 19**: Modern JavaScript könyvtár hookokkal
- **TypeScript**: Típusbiztos JavaScript fejlesztés
- **Inertia.js**: Full-stack framework zökkenőmentes SPA élményért
- **Tailwind CSS 4**: Utility-first CSS framework
- **Radix UI**: Hozzáférhető komponens primitívek

### Fejlesztői Eszközök
- **Vite**: Gyors build eszköz és fejlesztői szerver
- **Pest**: Modern PHP tesztelési framework
- **Laravel Pint**: Kód formázás
- **ESLint & Prettier**: Kód minőség és formázás

## Telepítés

### Rendszerkövetelmények

#### Minimális Követelmények
- **PHP**: 8.3 vagy újabb
- **Node.js**: 18 vagy újabb
- **Adatbázis**: MariaDB 10.4+ vagy MySQL 8.0+
- **Webszerver**: Apache 2.4+ vagy Nginx 1.18+
- **Memória**: 2GB RAM minimum
- **Tárhely**: 1GB szabad hely

#### Ajánlott Követelmények
- **PHP**: 8.3 OPcache engedélyezéssel
- **Node.js**: 20 LTS
- **Adatbázis**: MariaDB 10.11+ InnoDB-vel
- **Webszerver**: Nginx 1.24+ PHP-FPM-mel
- **Memória**: 4GB RAM vagy több
- **Tárhely**: 10GB+ SSD tárhely

### Docker Telepítés

#### Előfeltételek
- Docker 20.10+
- Docker Compose 2.0+

#### Gyors Indítás Docker-rel

1. **Repository klónozása**
```bash
git clone <repository-url>
cd multipass
```

2. **Docker Compose fájl létrehozása**
```yaml
# docker-compose.yml
version: '3.8'

services:
  app:
    build:
      context: .
      dockerfile: Dockerfile
    ports:
      - "8000:8000"
    volumes:
      - .:/var/www/html
    environment:
      - APP_ENV=production
      - APP_DEBUG=false
      - DB_CONNECTION=mysql
      - DB_HOST=db
      - DB_PORT=3306
      - DB_DATABASE=multipass
      - DB_USERNAME=multipass
      - DB_PASSWORD=password
    depends_on:
      - db
      - redis

  db:
    image: mariadb:10.11
    environment:
      - MYSQL_ROOT_PASSWORD=rootpassword
      - MYSQL_DATABASE=multipass
      - MYSQL_USER=multipass
      - MYSQL_PASSWORD=password
    volumes:
      - db_data:/var/lib/mysql
    ports:
      - "3306:3306"

  redis:
    image: redis:7-alpine
    ports:
      - "6379:6379"

  nginx:
    image: nginx:alpine
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - .:/var/www/html
      - ./docker/nginx.conf:/etc/nginx/nginx.conf
    depends_on:
      - app

volumes:
  db_data:
```

3. **Dockerfile létrehozása**
```dockerfile
# Dockerfile
FROM php:8.3-fpm

# Rendszer függőségek telepítése
RUN apt-get update && apt-get install -y \
    git \
    curl \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip \
    nodejs \
    npm

# PHP bővítmények telepítése
RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd

# Composer telepítése
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Munkakönyvtár beállítása
WORKDIR /var/www/html

# Alkalmazás fájlok másolása
COPY . .

# Függőségek telepítése
RUN composer install --optimize-autoloader --no-dev
RUN npm install && npm run build

# Jogosultságok beállítása
RUN chown -R www-data:www-data /var/www/html
RUN chmod -R 755 /var/www/html

# Port megnyitása
EXPOSE 8000

# PHP-FPM indítása
CMD ["php-fpm"]
```

4. **Konténerek építése és indítása**
```bash
docker-compose up -d --build
```

5. **Adatbázis migrációk futtatása**
```bash
docker-compose exec app php artisan migrate --seed
```

6. **Alkalmazás elérése**
```
http://localhost:8000
```

### Manuális Telepítés

#### 1. Lépés: Repository Klónozása
```bash
git clone <repository-url>
cd multipass
```

#### 2. Lépés: PHP Függőségek Telepítése
```bash
composer install --optimize-autoloader
```

#### 3. Lépés: Node.js Függőségek Telepítése
```bash
npm install
```

#### 4. Lépés: Környezeti Konfiguráció
```bash
cp .env.example .env
php artisan key:generate
```

#### 5. Lépés: Adatbázis Beállítása
```bash
# Adatbázis konfigurálása .env fájlban
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=multipass
DB_USERNAME=your_username
DB_PASSWORD=your_password

# Migrációk futtatása
php artisan migrate --seed
```

#### 6. Lépés: Frontend Eszközök Építése
```bash
npm run build
```

#### 7. Lépés: Webszerver Konfigurálása

##### Nginx Konfiguráció
```nginx
server {
    listen 80;
    server_name your-domain.com;
    root /path/to/multipass/public;

    add_header X-Frame-Options "SAMEORIGIN";
    add_header X-Content-Type-Options "nosniff";

    index index.php;

    charset utf-8;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location = /favicon.ico { access_log off; log_not_found off; }
    location = /robots.txt  { access_log off; log_not_found off; }

    error_page 404 /index.php;

    location ~ \.php$ {
        fastcgi_pass unix:/var/run/php/php8.3-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
        include fastcgi_params;
    }

    location ~ /\.(?!well-known).* {
        deny all;
    }
}
```

##### Apache Konfiguráció
```apache
<VirtualHost *:80>
    ServerName your-domain.com
    DocumentRoot /path/to/multipass/public

    <Directory /path/to/multipass/public>
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/multipass_error.log
    CustomLog ${APACHE_LOG_DIR}/multipass_access.log combined
</VirtualHost>
```

#### 8. Lépés: Jogosultságok Beállítása
```bash
chown -R www-data:www-data storage bootstrap/cache
chmod -R 775 storage bootstrap/cache
```

#### 9. Lépés: Szolgáltatások Indítása
```bash
# Laravel fejlesztői szerver indítása
php artisan serve

# Vagy systemd szolgáltatásként konfigurálás éles környezethez
```

## Konfiguráció

### Környezeti Változók

#### Alkalmazás Beállítások
```env
APP_NAME="Multipass Jelszókezelő"
APP_ENV=production
APP_KEY=base64:your-app-key
APP_DEBUG=false
APP_URL=https://your-domain.com
```

#### Adatbázis Konfiguráció
```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=multipass
DB_USERNAME=your_username
DB_PASSWORD=your_password
```

#### Cache Konfiguráció
```env
CACHE_DRIVER=redis
QUEUE_CONNECTION=redis
SESSION_DRIVER=redis
```

#### Email Konfiguráció
```env
MAIL_MAILER=smtp
MAIL_HOST=your-smtp-host
MAIL_PORT=587
MAIL_USERNAME=your-email
MAIL_PASSWORD=your-password
MAIL_ENCRYPTION=tls
MAIL_FROM_ADDRESS=noreply@your-domain.com
MAIL_FROM_NAME="Multipass Jelszókezelő"
```

#### LDAP Konfiguráció
```env
LDAP_ENABLED=true
LDAP_HOST=ldap.your-domain.com
LDAP_PORT=389
LDAP_BASE_DN=dc=your-domain,dc=com
LDAP_USER_DN=cn=admin,dc=your-domain,dc=com
LDAP_PASSWORD=your-ldap-password
```

### Rendszer Beállítások

A rendszer beállításokhoz az admin dashboard-on keresztül férhetünk hozzá:

1. **Általános Beállítások**
   - Cégnév és branding
   - Alapértelmezett nyelvi beállítások
   - Időzóna konfiguráció

2. **Biztonsági Beállítások**
   - Jelszó szabályzat konfiguráció
   - Munkamenet timeout beállítások
   - 2FA kényszerítési szabályzatok

3. **Email Beállítások**
   - SMTP konfiguráció
   - Email sablonok testreszabása
   - Értesítési beállítások

4. **LDAP Beállítások**
   - LDAP szerver konfiguráció
   - Felhasználó szinkronizációs beállítások
   - Csoport hozzárendelési konfiguráció

## Használati Útmutató

### Kezdő Lépések

#### Alapértelmezett Bejelentkezési Adatok
- **Admin Felhasználó**: `admin@multipass.local` / `admin`
- **Rendszer Felhasználó**: `user@multipass.local` / `user`

⚠️ **Fontos**: Változtassa meg ezeket a jelszavakat az első bejelentkezés után!

### Felhasználói Szerepkörök

#### Admin Felhasználók
- Teljes rendszer hozzáférés és konfiguráció
- Felhasználó és csoport kezelés
- Rendszer beállítások és karbantartás
- Aktivitás monitorozás és naplók
- LDAP konfiguráció és kezelés

#### Rendszer Felhasználók
- Személyes jelszó kezelés
- Hozzáférés megosztott mappákhoz és csoportokhoz
- Profil kezelés
- Korlátozott rendszer hozzáférés

### Jelszó Kezelés

#### Jelszó Bejegyzések Létrehozása
1. Navigáljon a kívánt mappához
2. Kattintson a "Jelszó Hozzáadása" gombra
3. Töltse ki a szükséges információkat:
   - Név/Cím
   - Felhasználónév
   - Jelszó (vagy generáljon egyet)
   - URL (opcionális)
   - Megjegyzések (opcionális)
   - Egyedi mezők (ha konfigurálva)

#### Jelszó Generálás
- Kattintson a "Jelszó Generálása" gombra
- Konfigurálja a jelszó opciókat:
  - Hossz (8-128 karakter)
  - Nagybetűk tartalmazása
  - Kisbetűk tartalmazása
  - Számok tartalmazása
  - Speciális karakterek tartalmazása
  - Hasonló karakterek kizárása

#### Jelszavak Szervezése
- Hozzon létre mappákat különböző kategóriákhoz
- Használjon egyedi mezőket további információkhoz
- Címkézze a jelszavakat a könnyű kereséshez
- Állítson be lejárati dátumokat ideiglenes jelszavakhoz

### Mappa Kezelés

#### Mappák Létrehozása
1. Kattintson a "Mappa Létrehozása" gombra a dashboard-on
2. Adja meg a mappa nevét és leírását
3. Válasszon szülő mappát (opcionális)
4. Állítsa be a láthatóságot (privát/nyilvános)
5. Konfigurálja a jogosultságokat

#### Mappa Jogosultságok
- **Tulajdonos**: Teljes hozzáférés a mappához és tartalmához
- **Olvasás**: Mappa tartalmának megtekintése
- **Írás**: Mappa tartalmának módosítása
- **Admin**: Mappa jogosultságok kezelése

### Felhasználókezelés (Csak Admin)

#### Felhasználók Létrehozása
1. Nyissa meg a Felhasználókezelést az admin dashboard-ból
2. Kattintson a "Felhasználó Hozzáadása" gombra
3. Töltse ki a felhasználói adatokat:
   - Név és email
   - Jelszó
   - Szerepkör (Admin/Felhasználó)
   - Csoportok (opcionális)

#### Csoportok Kezelése
1. Nyissa meg a Csoportkezelést
2. Hozzon létre csoportokat a felhasználók szervezéséhez
3. Rendeljen jogosultságokat a csoportokhoz
4. Adja hozzá a felhasználókat a megfelelő csoportokhoz

### LDAP Integráció

#### LDAP Engedélyezése
1. Konfigurálja a LDAP beállításokat a Rendszer Beállításokban
2. Tesztelje a LDAP kapcsolatot
3. Engedélyezze a LDAP autentikációt
4. Konfigurálja a felhasználó szinkronizációt

#### LDAP Felhasználókezelés
- LDAP felhasználók automatikusan szinkronizálódnak
- Helyi jelszó változtatások korlátozottak LDAP felhasználók számára
- Csoport tagságok LDAP-ból szinkronizálódnak
- Felhasználói attribútumok automatikusan frissülnek

### Kétfaktoros Autentikáció

#### 2FA Engedélyezése
1. Menjen a Profil Beállításokhoz
2. Kattintson a "Kétfaktoros Autentikáció Engedélyezése" gombra
3. Olvassa be a QR kódot egy autentikátor alkalmazással
4. Adja meg az ellenőrző kódot
5. Mentse el a biztonsági kódokat biztonságosan

#### 2FA Alkalmazások
- Google Authenticator
- Microsoft Authenticator
- Authy
- Bármely TOTP-kompatibilis alkalmazás

### Email Rendszer

#### Email Konfigurálása
1. Nyissa meg a Rendszer Beállításokat
2. Navigáljon az Email Konfigurációhoz
3. Adja meg az SMTP beállításokat
4. Tesztelje az email kézbesítést
5. Konfigurálja az email sablonokat

#### Email Sablonok
- Üdvözlő emailek új felhasználóknak
- Jelszó visszaállító emailek
- Biztonsági értesítések
- Rendszer karbantartási értesítések

## API Dokumentáció

### Autentikáció

#### Bejelentkezés
```http
POST /api/login
Content-Type: application/json

{
    "email": "user@example.com",
    "password": "password"
}
```

#### Válasz
```json
{
    "success": true,
    "user": {
        "id": 1,
        "name": "John Doe",
        "email": "user@example.com",
        "is_admin": false
    },
    "token": "api-token-here"
}
```

### Jelszó Kezelés

#### Jelszavak Lekérése
```http
GET /api/passwords
Authorization: Bearer {token}
```

#### Jelszó Létrehozása
```http
POST /api/passwords
Authorization: Bearer {token}
Content-Type: application/json

{
    "name": "My Password",
    "username": "user@example.com",
    "password": "secure-password",
    "url": "https://example.com",
    "folder_id": 1,
    "notes": "Additional notes"
}
```

#### Jelszó Frissítése
```http
PUT /api/passwords/{id}
Authorization: Bearer {token}
Content-Type: application/json

{
    "name": "Updated Name",
    "password": "new-password"
}
```

#### Jelszó Törlése
```http
DELETE /api/passwords/{id}
Authorization: Bearer {token}
```

### Mappa Kezelés

#### Mappák Lekérése
```http
GET /api/folders
Authorization: Bearer {token}
```

#### Mappa Létrehozása
```http
POST /api/folders
Authorization: Bearer {token}
Content-Type: application/json

{
    "name": "New Folder",
    "parent_id": null,
    "description": "Folder description",
    "private": false
}
```

### Felhasználókezelés (Csak Admin)

#### Felhasználók Lekérése
```http
GET /api/users
Authorization: Bearer {token}
```

#### Felhasználó Létrehozása
```http
POST /api/users
Authorization: Bearer {token}
Content-Type: application/json

{
    "name": "New User",
    "email": "newuser@example.com",
    "password": "password",
    "is_admin": false
}
```

## Biztonság

### Titkosítás

#### Adat Titkosítás
- Minden jelszó AES-256 titkosítással
- Titkosítási kulcsok külön tárolva az adatoktól
- Kliens oldali titkosítás érzékeny műveletekhez
- Biztonságos kulcs származtatás PBKDF2 használatával

#### Átviteli Biztonság
- HTTPS kényszerítés minden kommunikációhoz
- TLS 1.3 biztonságos adatátvitelhez
- Biztonságos munkamenet kezelés
- CSRF védelem minden formon

### Hozzáférés-vezérlés

#### Autentikáció
- Erős jelszó követelmények
- Fiók zárolás sikertelen kísérletek után
- Munkamenet timeout konfiguráció
- Kétfaktoros autentikáció támogatás

#### Engedélyezés
- Szerepkör-alapú hozzáférés-vezérlés (RBAC)
- Részletes jogosultság rendszer
- Erőforrás szintű hozzáférés-vezérlés
- Audit naplózás minden művelethez

### Adatvédelem

#### Adatvédelem
- Nincs nyílt szöveges jelszó tárolás
- Titkosított adatbázis biztonsági másolatok
- Biztonságos adattörlés
- GDPR megfelelőségi funkciók

#### Biztonsági Másolat Biztonság
- Titkosított biztonsági másolat fájlok
- Biztonságos biztonsági másolat tárolás
- Rendszeres biztonsági másolat ellenőrzés
- Katasztrófa helyreállítási eljárások

## Hibaelhárítás

### Gyakori Problémák

#### Telepítési Problémák

**Probléma**: Composer függőségek telepítése sikertelen
```bash
# Megoldás: Composer frissítése és cache törlése
composer self-update
composer clear-cache
composer install --no-cache
```

**Probléma**: Node.js build sikertelen
```bash
# Megoldás: npm cache törlése és újratelepítés
npm cache clean --force
rm -rf node_modules package-lock.json
npm install
```

**Probléma**: Adatbázis kapcsolat sikertelen
```bash
# Adatbázis konfiguráció ellenőrzése
php artisan config:clear
php artisan cache:clear
# Adatbázis hitelesítő adatok ellenőrzése .env fájlban
```

#### Futási Problémák

**Probléma**: 500 Belső Szerver Hiba
```bash
# Laravel naplók ellenőrzése
tail -f storage/logs/laravel.log

# Gyakori megoldások:
php artisan config:clear
php artisan cache:clear
php artisan view:clear
chmod -R 775 storage bootstrap/cache
```

**Probléma**: Eszközök nem töltődnek be
```bash
# Frontend eszközök újraépítése
npm run build
# Vagy fejlesztéshez:
npm run dev
```

**Probléma**: Email nem küldődik
```bash
# Email konfiguráció tesztelése
php artisan tinker
# Majd futtassa:
Mail::raw('Test email', function($message) {
    $message->to('test@example.com')->subject('Test');
});
```

### Teljesítmény Optimalizálás

#### Adatbázis Optimalizálás
```sql
-- Indexek hozzáadása jobb teljesítményért
CREATE INDEX idx_items_owner_id ON items(owner_id);
CREATE INDEX idx_folders_owner_id ON folders(owner_id);
CREATE INDEX idx_activity_logs_user_id ON activity_logs(user_id);
```

#### Cache Konfiguráció
```env
# Redis használata jobb teljesítményért
CACHE_DRIVER=redis
SESSION_DRIVER=redis
QUEUE_CONNECTION=redis
```

#### PHP Optimalizálás
```ini
; php.ini optimalizációk
opcache.enable=1
opcache.memory_consumption=256
opcache.max_accelerated_files=20000
opcache.validate_timestamps=0
```

### Napló Elemzés

#### Laravel Naplók
```bash
# Legutóbbi hibák megtekintése
tail -f storage/logs/laravel.log

# Specifikus hibák keresése
grep "ERROR" storage/logs/laravel.log
```

#### Webszerver Naplók
```bash
# Nginx hiba naplók
tail -f /var/log/nginx/error.log

# Apache hiba naplók
tail -f /var/log/apache2/error.log
```

## Fejlesztés

### Fejlesztői Környezet Beállítása

#### Előfeltételek
- PHP 8.3 bővítményekkel: pdo_mysql, mbstring, xml, ctype, json, bcmath
- Node.js 18+ és npm
- MariaDB 10.4+ vagy MySQL 8.0+
- Git

#### Beállítási Lépések
```bash
# Repository klónozása
git clone <repository-url>
cd multipass

# Függőségek telepítése
composer install
npm install

# Környezet beállítása
cp .env.example .env
php artisan key:generate

# Adatbázis konfigurálása
# Szerkessze a .env fájlt az adatbázis beállításokkal

# Migrációk futtatása
php artisan migrate --seed

# Fejlesztői szerverek indítása
composer run dev
```

#### Fejlesztői Parancsok
```bash
# Összes fejlesztői szolgáltatás indítása
composer run dev

# Tesztek futtatása
php artisan test

# Kód formázás
vendor/bin/pint

# Frontend fejlesztés
npm run dev

# Éles környezethez építés
npm run build
```

### Kód Struktúra

#### Backend Struktúra
```
app/
├── Console/Commands/          # Artisan parancsok
├── Http/
│   ├── Controllers/          # Alkalmazás kontrollerek
│   ├── Middleware/           # Egyedi middleware
│   └── Requests/             # Form kérés validáció
├── Models/                   # Eloquent modellek
├── Services/                 # Üzleti logika szolgáltatások
├── Traits/                   # Újrafelhasználható trait-ek
└── Providers/                # Szolgáltatás szolgáltatók
```

#### Frontend Struktúra
```
resources/js/
├── components/               # Újrafelhasználható React komponensek
├── pages/                    # Oldal komponensek
├── lib/                      # Segédkönyvtárak
├── types/                    # TypeScript típus definíciók
└── css/                      # Stíluslapok
```

### Tesztelés

#### Tesztek Futtatása
```bash
# Összes teszt futtatása
php artisan test

# Specifikus teszt fájl futtatása
php artisan test tests/Feature/UserTest.php

# Lefedettséggel futtatás
php artisan test --coverage
```

#### Tesztek Írása
```php
<?php

use App\Models\User;
use Tests\TestCase;

class UserTest extends TestCase
{
    public function test_user_can_be_created()
    {
        $user = User::factory()->create([
            'name' => 'John Doe',
            'email' => 'john@example.com'
        ]);

        $this->assertDatabaseHas('users', [
            'email' => 'john@example.com'
        ]);
    }
}
```

### Közreműködés

#### Kód Szabványok
- PSR-12 kódolási szabványok követése
- Laravel Pint használata kód formázáshoz
- Tesztek írása új funkciókhoz
- Nyilvános API-k dokumentálása
- Szelektív verziószámozás követése

#### Pull Request Folyamat
1. Fork-olja a repository-t
2. Hozzon létre egy feature ágat
3. Tegye meg a változtatásokat
4. Írjon teszteket
5. Futtassa a teszt készletet
6. Küldjön be egy pull request-et

### Telepítés

#### Éles Környezeti Telepítés
```bash
# Éles függőségek telepítése
composer install --optimize-autoloader --no-dev

# Frontend eszközök építése
npm run build

# Migrációk futtatása
php artisan migrate --force

# Cache-ek törlése
php artisan config:cache
php artisan route:cache
php artisan view:cache

# Jogosultságok beállítása
chown -R www-data:www-data storage bootstrap/cache
chmod -R 775 storage bootstrap/cache
```

#### Környezeti Konfiguráció
```env
APP_ENV=production
APP_DEBUG=false
APP_URL=https://your-domain.com

# Redis használata éles környezethez
CACHE_DRIVER=redis
SESSION_DRIVER=redis
QUEUE_CONNECTION=redis

# Adatbázis optimalizáció
DB_CONNECTION=mysql
DB_STRICT_MODE=false
```

---

## Támogatás

További támogatás és dokumentáció:
- Tekintse meg a hibaelhárítási részt fent
- Nézze át a GitHub issues oldalt
- Lépjen kapcsolatba a fejlesztői csapattal

## Licenc

Ez a projekt MIT licenc alatt áll - a részletekért lásd a LICENSE fájlt.
