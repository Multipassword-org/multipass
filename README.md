# Multipass Password Manager Documentation

Welcome to the comprehensive documentation for Multipass Password Manager. This documentation is available in multiple languages and covers all aspects of the application.

## Available Languages / Elérhető Nyelvek

- 🇺🇸 [English Documentation](docs/en/README.md)
- 🇭🇺 [Magyar Dokumentáció](docs/hu/README.md)

## Quick Links / Gyors Linkek

### English
- [Installation Guide](docs/en/INSTALLATION.md)
- [Features Overview](docs/en/FEATURES.md)
- [API Documentation](docs/en/API.md)

### Magyar
- [Telepítési Útmutató](docs/hu/INSTALLATION.md)
- [Funkciók Áttekintése](docs/hu/FEATURES.md)
- [API Dokumentáció](docs/hu/API.md)

## What is Multipass? / Mi a Multipass?

Multipass is a modern, secure password manager built with Laravel 12 backend and React 19 frontend. It provides enterprise-grade security with user-friendly interface, supporting both individual and team usage scenarios.

A Multipass egy modern, biztonságos jelszókezelő alkalmazás, amely Laravel 12 backend és React 19 frontend technológiákra épül. Vállalati szintű biztonságot biztosít felhasználóbarát felülettel, támogatva mind az egyéni, mind a csapat használatot.

## Key Features / Főbb Funkciók

### 🔐 Security / Biztonság
- End-to-end encryption / End-to-end titkosítás
- Two-factor authentication / Kétfaktoros autentikáció
- Role-based access control / Szerepkör-alapú hozzáférés-vezérlés
- Activity logging / Aktivitás naplózás

### 👥 User Management / Felhasználókezelés
- Multi-user support / Többfelhasználós támogatás
- LDAP/Active Directory integration / LDAP/Active Directory integráció
- User groups / Felhasználói csoportok
- Private folders / Privát mappák

### 📁 Organization / Szervezés
- Hierarchical folders / Hierarchikus mappák
- Custom fields / Egyedi mezők
- Password generation / Jelszó generálás
- Import/Export / Import/Export

### 🌐 Enterprise Features / Vállalati Funkciók
- LDAP integration / LDAP integráció
- Email system / Email rendszer
- Maintenance mode / Karbantartási mód
- System settings / Rendszer beállítások

## Technology Stack / Technológiai Stack

### Backend / Backend
- **Laravel 12**: Modern PHP framework
- **PHP 8.3**: Latest PHP version
- **MariaDB**: Primary database
- **Redis**: Caching and sessions

### Frontend / Frontend
- **React 19**: Modern JavaScript library
- **TypeScript**: Type-safe development
- **Inertia.js**: Full-stack framework
- **Tailwind CSS 4**: Utility-first CSS

## Getting Started / Kezdő Lépések

### Default Credentials / Alapértelmezett Bejelentkezési Adatok

- **Admin**: `admin@multipass.local` / `admin`
- **User**: `user@multipass.local` / `user`

⚠️ **Important / Fontos**: Change these passwords immediately after first login! / Változtassa meg ezeket a jelszavakat az első bejelentkezés után!

### Quick Installation / Gyors Telepítés

#### Docker (Recommended / Ajánlott)
```bash
git clone <repository-url>
cd multipass
docker-compose up -d
docker-compose exec app php artisan migrate --seed
```

#### Manual / Manuális
```bash
git clone <repository-url>
cd multipass
composer install
npm install
cp .env.example .env
php artisan key:generate
php artisan migrate --seed
npm run build
php artisan serve
```

## Support / Támogatás

For additional support and documentation:
További támogatás és dokumentáció:

- Check the troubleshooting sections in the language-specific documentation
- Review the GitHub issues page
- Contact the development team

- Tekintse meg a hibaelhárítási részeket a nyelvspecifikus dokumentációban
- Nézze át a GitHub issues oldalt
- Lépjen kapcsolatba a fejlesztői csapattal

## License / Licenc

This project is licensed under the MIT License - see the LICENSE file for details.

Ez a projekt MIT licenc alatt áll - a részletekért lásd a LICENSE fájlt.
