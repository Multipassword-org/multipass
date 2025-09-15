# Funkciók Áttekintése

## Alapvető Funkciók

### 🔐 Biztonsági Funkciók
- **End-to-End Titkosítás**: Minden jelszó AES-256 titkosítással
- **Kétfaktoros Autentikáció**: TOTP-alapú 2FA támogatás
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

## Részletes Funkció Leírások

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

### Rendszer Beállítások

#### Általános Beállítások
- Cégnév és branding
- Alapértelmezett nyelvi beállítások
- Időzóna konfiguráció

#### Biztonsági Beállítások
- Jelszó szabályzat konfiguráció
- Munkamenet timeout beállítások
- 2FA kényszerítési szabályzatok

#### Email Beállítások
- SMTP konfiguráció
- Email sablonok testreszabása
- Értesítési beállítások

#### LDAP Beállítások
- LDAP szerver konfiguráció
- Felhasználó szinkronizációs beállítások
- Csoport hozzárendelési konfiguráció

## Felhasználói Szerepkörök és Jogosultságok

### Admin Felhasználók
- Teljes rendszer hozzáférés és konfiguráció
- Felhasználó és csoport kezelés
- Rendszer beállítások és karbantartás
- Aktivitás monitorozás és naplók
- LDAP konfiguráció és kezelés

### Rendszer Felhasználók
- Személyes jelszó kezelés
- Hozzáférés megosztott mappákhoz és csoportokhoz
- Profil kezelés
- Korlátozott rendszer hozzáférés

## Fejlett Funkciók

### Jelszó Megosztás
- Biztonságos jelszó megosztás lejárattal
- Hozzáférési jelszó védelem
- Megtekintési szám korlátozások
- Email értesítések

### Aktivitás Naplózás
- Átfogó audit nyomvonal
- Felhasználói művelet követés
- Rendszer esemény naplózás
- Biztonsági monitorozás

### Karbantartási Mód
- Rendszer karbantartás csak admin hozzáféréssel
- Automatikus email kezelés
- Felhasználói értesítési rendszer
- Valós idejű dashboard frissítések

### Licenc Kezelés
- Licenc validáció és kezelés
- Funkció aktiválás licenc alapján
- Licenc lejárat kezelés
- Támogatás és frissítések

## Mobil Támogatás

### Reszponzív Design
- Mobilbarát felület
- Érintésre optimalizált vezérlők
- Adaptív elrendezések
- Eszközök közötti szinkronizáció

### Progresszív Web Alkalmazás
- Offline funkcionalitás
- Alkalmazás-szerű élmény
- Push értesítések
- Kezdőképernyő telepítés

## Integrációs Képességek

### API Hozzáférés
- RESTful API végpontok
- Autentikációs tokenek
- Sebesség korlátozás
- Átfogó dokumentáció

### Harmadik Fél Integrációk
- Böngésző bővítmények
- Mobil alkalmazások
- Vállalati rendszerek
- Egyedi integrációk

## Biztonsági Funkciók

### Adatvédelem
- End-to-end titkosítás
- Biztonságos kulcs kezelés
- Adatbázis biztonsági másolat titkosítás
- Biztonságos törlés

### Hozzáférés-vezérlés
- Multi-faktoros autentikáció
- Szerepkör-alapú jogosultságok
- Munkamenet kezelés
- IP korlátozások

### Megfelelőség
- GDPR megfelelőség
- SOC 2 megfelelőség
- Audit naplózás
- Adatmegőrzési szabályzatok
