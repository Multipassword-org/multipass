# Multipass Password Manager - Complete Documentation

## Table of Contents

1. [Overview](#overview)
2. [Features](#features)
3. [Technology Stack](#technology-stack)
4. [Installation](#installation)
   - [System Requirements](#system-requirements)
   - [Docker Installation](#docker-installation)
   - [Manual Installation](#manual-installation)
5. [Configuration](#configuration)
6. [Usage Guide](#usage-guide)
7. [API Documentation](#api-documentation)
8. [Security](#security)
9. [Troubleshooting](#troubleshooting)
10. [Development](#development)

## Overview

**Multipass** is a modern, secure password manager built with Laravel 12 backend and React 19 frontend. It provides enterprise-grade security with user-friendly interface, supporting both individual and team usage scenarios.

### Key Objectives
- **Security**: End-to-end encryption for all stored data
- **User Experience**: Modern, intuitive interface with dark mode support
- **Scalability**: Multi-user support with role-based access control
- **Accessibility**: Multi-language support (English/Hungarian) and responsive design

## Features

### 🔐 Core Security Features
- **End-to-End Encryption**: All passwords encrypted with AES-256
- **Two-Factor Authentication (2FA)**: TOTP-based 2FA support
- **Role-Based Access Control**: Admin and user roles with granular permissions
- **Session Management**: Secure session handling with automatic logout
- **Activity Logging**: Comprehensive audit trail for all actions

### 👥 User Management
- **Multi-User Support**: Family and team usage scenarios
- **LDAP/Active Directory Integration**: Enterprise authentication
- **User Groups**: Organize users into groups with shared permissions
- **Private Folders**: Automatic private folder creation for each user
- **User Profiles**: Comprehensive user profile management

### 📁 Organization & Management
- **Hierarchical Folders**: Tree and list view with drag-and-drop support
- **Custom Fields**: Define custom fields for password entries
- **Password Generation**: Built-in strong password generator
- **Import/Export**: Support for various password manager formats
- **Search & Filter**: Advanced search and filtering capabilities

### 🌐 Enterprise Features
- **LDAP Integration**: Full LDAP/AD synchronization
- **Email System**: SMTP configuration with custom templates
- **Maintenance Mode**: System maintenance with admin-only access
- **System Settings**: Comprehensive system configuration
- **License Management**: License validation and management
- **Activity Monitoring**: Real-time activity logs and monitoring

### 🎨 User Interface
- **Responsive Design**: Mobile-friendly interface
- **Dark Mode**: Automatic and manual theme switching
- **Multi-Language**: English and Hungarian support
- **Modern UI**: Built with Tailwind CSS and Radix UI components
- **Accessibility**: WCAG compliant interface

## Technology Stack

### Backend
- **Laravel 12**: Modern PHP framework with MVC architecture
- **PHP 8.3**: Latest PHP version with modern features
- **MariaDB**: Primary database with JSON optimization
- **Redis**: Caching and session storage
- **Queue System**: Background job processing

### Frontend
- **React 19**: Modern JavaScript library with hooks
- **TypeScript**: Type-safe JavaScript development
- **Inertia.js**: Full-stack framework for seamless SPA experience
- **Tailwind CSS 4**: Utility-first CSS framework
- **Radix UI**: Accessible component primitives

### Development Tools
- **Vite**: Fast build tool and development server
- **Pest**: Modern PHP testing framework
- **Laravel Pint**: Code formatting
- **ESLint & Prettier**: Code quality and formatting

## Installation

### System Requirements

#### Minimum Requirements
- **PHP**: 8.3 or higher
- **Node.js**: 18 or higher
- **Database**: MariaDB 10.4+ or MySQL 8.0+
- **Web Server**: Apache 2.4+ or Nginx 1.18+
- **Memory**: 2GB RAM minimum
- **Storage**: 1GB free space

#### Recommended Requirements
- **PHP**: 8.3 with OPcache enabled
- **Node.js**: 20 LTS
- **Database**: MariaDB 10.11+ with InnoDB
- **Web Server**: Nginx 1.24+ with PHP-FPM
- **Memory**: 4GB RAM or higher
- **Storage**: 10GB+ SSD storage

### Docker Installation

#### Prerequisites
- Docker 20.10+
- Docker Compose 2.0+

#### Quick Start with Docker

1. **Clone the repository**
```bash
git clone <repository-url>
cd multipass
```

2. **Create Docker Compose file**
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

3. **Create Dockerfile**
```dockerfile
# Dockerfile
FROM php:8.3-fpm

# Install system dependencies
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

# Install PHP extensions
RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd

# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Set working directory
WORKDIR /var/www/html

# Copy application files
COPY . .

# Install dependencies
RUN composer install --optimize-autoloader --no-dev
RUN npm install && npm run build

# Set permissions
RUN chown -R www-data:www-data /var/www/html
RUN chmod -R 755 /var/www/html

# Expose port
EXPOSE 8000

# Start PHP-FPM
CMD ["php-fpm"]
```

4. **Build and start containers**
```bash
docker-compose up -d --build
```

5. **Run database migrations**
```bash
docker-compose exec app php artisan migrate --seed
```

6. **Access the application**
```
http://localhost:8000
```

### Manual Installation

#### Step 1: Clone Repository
```bash
git clone <repository-url>
cd multipass
```

#### Step 2: Install PHP Dependencies
```bash
composer install --optimize-autoloader
```

#### Step 3: Install Node.js Dependencies
```bash
npm install
```

#### Step 4: Environment Configuration
```bash
cp .env.example .env
php artisan key:generate
```

#### Step 5: Database Setup
```bash
# Configure database in .env file
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=multipass
DB_USERNAME=your_username
DB_PASSWORD=your_password

# Run migrations
php artisan migrate --seed
```

#### Step 6: Build Frontend Assets
```bash
npm run build
```

#### Step 7: Configure Web Server

##### Nginx Configuration
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

##### Apache Configuration
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

#### Step 8: Set Permissions
```bash
chown -R www-data:www-data storage bootstrap/cache
chmod -R 775 storage bootstrap/cache
```

#### Step 9: Start Services
```bash
# Start Laravel development server
php artisan serve

# Or configure as systemd service for production
```

## Configuration

### Environment Variables

#### Application Settings
```env
APP_NAME="Multipass Password Manager"
APP_ENV=production
APP_KEY=base64:your-app-key
APP_DEBUG=false
APP_URL=https://your-domain.com
```

#### Database Configuration
```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=multipass
DB_USERNAME=your_username
DB_PASSWORD=your_password
```

#### Cache Configuration
```env
CACHE_DRIVER=redis
QUEUE_CONNECTION=redis
SESSION_DRIVER=redis
```

#### Mail Configuration
```env
MAIL_MAILER=smtp
MAIL_HOST=your-smtp-host
MAIL_PORT=587
MAIL_USERNAME=your-email
MAIL_PASSWORD=your-password
MAIL_ENCRYPTION=tls
MAIL_FROM_ADDRESS=noreply@your-domain.com
MAIL_FROM_NAME="Multipass Password Manager"
```

#### LDAP Configuration
```env
LDAP_ENABLED=true
LDAP_HOST=ldap.your-domain.com
LDAP_PORT=389
LDAP_BASE_DN=dc=your-domain,dc=com
LDAP_USER_DN=cn=admin,dc=your-domain,dc=com
LDAP_PASSWORD=your-ldap-password
```

### System Settings

Access system settings through the admin dashboard:

1. **General Settings**
   - Company name and branding
   - Default language settings
   - Timezone configuration

2. **Security Settings**
   - Password policy configuration
   - Session timeout settings
   - 2FA enforcement policies

3. **Email Settings**
   - SMTP configuration
   - Email templates customization
   - Notification preferences

4. **LDAP Settings**
   - LDAP server configuration
   - User synchronization settings
   - Group mapping configuration

## Usage Guide

### Getting Started

#### Default Login Credentials
- **Admin User**: `admin@multipass.local` / `admin`
- **Regular User**: `user@multipass.local` / `user`

⚠️ **Important**: Change these passwords immediately after first login!

### User Roles

#### Admin Users
- Full system access and configuration
- User and group management
- System settings and maintenance
- Activity monitoring and logs
- LDAP configuration and management

#### Regular Users
- Personal password management
- Access to shared folders and groups
- Profile management
- Limited system access

### Password Management

#### Creating Password Entries
1. Navigate to the desired folder
2. Click "Add Password" button
3. Fill in the required information:
   - Name/Title
   - Username
   - Password (or generate one)
   - URL (optional)
   - Notes (optional)
   - Custom fields (if configured)

#### Password Generation
- Click the "Generate Password" button
- Configure password options:
  - Length (8-128 characters)
  - Include uppercase letters
  - Include lowercase letters
  - Include numbers
  - Include special characters
  - Exclude similar characters

#### Organizing Passwords
- Create folders for different categories
- Use custom fields for additional information
- Tag passwords for easy searching
- Set expiration dates for temporary passwords

### Folder Management

#### Creating Folders
1. Click "Create Folder" in the dashboard
2. Enter folder name and description
3. Choose parent folder (optional)
4. Set visibility (private/public)
5. Configure permissions

#### Folder Permissions
- **Owner**: Full access to folder and contents
- **Read**: View folder contents
- **Write**: Modify folder contents
- **Admin**: Manage folder permissions

### User Management (Admin Only)

#### Creating Users
1. Access User Management from admin dashboard
2. Click "Add User"
3. Fill in user details:
   - Name and email
   - Password
   - Role (Admin/User)
   - Groups (optional)

#### Managing Groups
1. Access Group Management
2. Create groups for organizing users
3. Assign permissions to groups
4. Add users to appropriate groups

### LDAP Integration

#### Enabling LDAP
1. Configure LDAP settings in System Settings
2. Test LDAP connection
3. Enable LDAP authentication
4. Configure user synchronization

#### LDAP User Management
- LDAP users are automatically synchronized
- Local password changes are restricted for LDAP users
- Group memberships are synchronized from LDAP
- User attributes are updated automatically

### Two-Factor Authentication

#### Enabling 2FA
1. Go to Profile Settings
2. Click "Enable Two-Factor Authentication"
3. Scan QR code with authenticator app
4. Enter verification code
5. Save backup codes securely

#### 2FA Apps
- Google Authenticator
- Microsoft Authenticator
- Authy
- Any TOTP-compatible app

### Email System

#### Configuring Email
1. Access System Settings
2. Navigate to Email Configuration
3. Enter SMTP settings
4. Test email delivery
5. Configure email templates

#### Email Templates
- Welcome emails for new users
- Password reset emails
- Security notifications
- System maintenance notifications

## API Documentation

### Authentication

#### Login
```http
POST /api/login
Content-Type: application/json

{
    "email": "user@example.com",
    "password": "password"
}
```

#### Response
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

### Password Management

#### Get Passwords
```http
GET /api/passwords
Authorization: Bearer {token}
```

#### Create Password
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

#### Update Password
```http
PUT /api/passwords/{id}
Authorization: Bearer {token}
Content-Type: application/json

{
    "name": "Updated Name",
    "password": "new-password"
}
```

#### Delete Password
```http
DELETE /api/passwords/{id}
Authorization: Bearer {token}
```

### Folder Management

#### Get Folders
```http
GET /api/folders
Authorization: Bearer {token}
```

#### Create Folder
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

### User Management (Admin Only)

#### Get Users
```http
GET /api/users
Authorization: Bearer {token}
```

#### Create User
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

## Security

### Encryption

#### Data Encryption
- All passwords encrypted with AES-256
- Encryption keys stored separately from data
- Client-side encryption for sensitive operations
- Secure key derivation using PBKDF2

#### Transmission Security
- HTTPS enforced for all communications
- TLS 1.3 for secure data transmission
- Secure session management
- CSRF protection on all forms

### Access Control

#### Authentication
- Strong password requirements
- Account lockout after failed attempts
- Session timeout configuration
- Two-factor authentication support

#### Authorization
- Role-based access control (RBAC)
- Granular permissions system
- Resource-level access control
- Audit logging for all actions

### Data Protection

#### Privacy
- No plaintext password storage
- Encrypted database backups
- Secure data deletion
- GDPR compliance features

#### Backup Security
- Encrypted backup files
- Secure backup storage
- Regular backup verification
- Disaster recovery procedures

## Troubleshooting

### Common Issues

#### Installation Problems

**Issue**: Composer dependencies fail to install
```bash
# Solution: Update Composer and clear cache
composer self-update
composer clear-cache
composer install --no-cache
```

**Issue**: Node.js build fails
```bash
# Solution: Clear npm cache and reinstall
npm cache clean --force
rm -rf node_modules package-lock.json
npm install
```

**Issue**: Database connection fails
```bash
# Check database configuration
php artisan config:clear
php artisan cache:clear
# Verify database credentials in .env file
```

#### Runtime Issues

**Issue**: 500 Internal Server Error
```bash
# Check Laravel logs
tail -f storage/logs/laravel.log

# Common solutions:
php artisan config:clear
php artisan cache:clear
php artisan view:clear
chmod -R 775 storage bootstrap/cache
```

**Issue**: Assets not loading
```bash
# Rebuild frontend assets
npm run build
# Or for development:
npm run dev
```

**Issue**: Email not sending
```bash
# Test email configuration
php artisan tinker
# Then run:
Mail::raw('Test email', function($message) {
    $message->to('test@example.com')->subject('Test');
});
```

### Performance Optimization

#### Database Optimization
```sql
-- Add indexes for better performance
CREATE INDEX idx_items_owner_id ON items(owner_id);
CREATE INDEX idx_folders_owner_id ON folders(owner_id);
CREATE INDEX idx_activity_logs_user_id ON activity_logs(user_id);
```

#### Caching Configuration
```env
# Use Redis for better performance
CACHE_DRIVER=redis
SESSION_DRIVER=redis
QUEUE_CONNECTION=redis
```

#### PHP Optimization
```ini
; php.ini optimizations
opcache.enable=1
opcache.memory_consumption=256
opcache.max_accelerated_files=20000
opcache.validate_timestamps=0
```

### Log Analysis

#### Laravel Logs
```bash
# View recent errors
tail -f storage/logs/laravel.log

# Search for specific errors
grep "ERROR" storage/logs/laravel.log
```

#### Web Server Logs
```bash
# Nginx error logs
tail -f /var/log/nginx/error.log

# Apache error logs
tail -f /var/log/apache2/error.log
```

## Development

### Development Environment Setup

#### Prerequisites
- PHP 8.3 with extensions: pdo_mysql, mbstring, xml, ctype, json, bcmath
- Node.js 18+ and npm
- MariaDB 10.4+ or MySQL 8.0+
- Git

#### Setup Steps
```bash
# Clone repository
git clone <repository-url>
cd multipass

# Install dependencies
composer install
npm install

# Setup environment
cp .env.example .env
php artisan key:generate

# Configure database
# Edit .env file with your database settings

# Run migrations
php artisan migrate --seed

# Start development servers
composer run dev
```

#### Development Commands
```bash
# Start all development services
composer run dev

# Run tests
php artisan test

# Code formatting
vendor/bin/pint

# Frontend development
npm run dev

# Build for production
npm run build
```

### Code Structure

#### Backend Structure
```
app/
├── Console/Commands/          # Artisan commands
├── Http/
│   ├── Controllers/          # Application controllers
│   ├── Middleware/           # Custom middleware
│   └── Requests/             # Form request validation
├── Models/                   # Eloquent models
├── Services/                 # Business logic services
├── Traits/                   # Reusable traits
└── Providers/                # Service providers
```

#### Frontend Structure
```
resources/js/
├── components/               # Reusable React components
├── pages/                    # Page components
├── lib/                      # Utility libraries
├── types/                    # TypeScript type definitions
└── css/                      # Stylesheets
```

### Testing

#### Running Tests
```bash
# Run all tests
php artisan test

# Run specific test file
php artisan test tests/Feature/UserTest.php

# Run with coverage
php artisan test --coverage
```

#### Writing Tests
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

### Contributing

#### Code Standards
- Follow PSR-12 coding standards
- Use Laravel Pint for code formatting
- Write tests for new features
- Document public APIs
- Follow semantic versioning

#### Pull Request Process
1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Write tests
5. Run the test suite
6. Submit a pull request

### Deployment

#### Production Deployment
```bash
# Install production dependencies
composer install --optimize-autoloader --no-dev

# Build frontend assets
npm run build

# Run migrations
php artisan migrate --force

# Clear caches
php artisan config:cache
php artisan route:cache
php artisan view:cache

# Set permissions
chown -R www-data:www-data storage bootstrap/cache
chmod -R 775 storage bootstrap/cache
```

#### Environment Configuration
```env
APP_ENV=production
APP_DEBUG=false
APP_URL=https://your-domain.com

# Use Redis for production
CACHE_DRIVER=redis
SESSION_DRIVER=redis
QUEUE_CONNECTION=redis

# Database optimization
DB_CONNECTION=mysql
DB_STRICT_MODE=false
```

---

## Support

For additional support and documentation:
- Check the troubleshooting section above
- Review the GitHub issues page
- Contact the development team

## License

This project is licensed under the MIT License - see the LICENSE file for details.
