# API Dokumentáció

## Autentikáció

### Bejelentkezés
```http
POST /api/login
Content-Type: application/json

{
    "email": "user@example.com",
    "password": "password"
}
```

**Válasz:**
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

### Kijelentkezés
```http
POST /api/logout
Authorization: Bearer {token}
```

**Válasz:**
```json
{
    "success": true,
    "message": "Sikeresen kijelentkezett"
}
```

## Jelszó Kezelés

### Jelszavak Lekérése
```http
GET /api/passwords
Authorization: Bearer {token}
```

**Válasz:**
```json
{
    "success": true,
    "passwords": [
        {
            "id": 1,
            "name": "My Password",
            "username": "user@example.com",
            "url": "https://example.com",
            "folder_id": 1,
            "created_at": "2024-01-01T00:00:00Z",
            "updated_at": "2024-01-01T00:00:00Z"
        }
    ]
}
```

### Jelszó Létrehozása
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

**Válasz:**
```json
{
    "success": true,
    "password": {
        "id": 1,
        "name": "My Password",
        "username": "user@example.com",
        "url": "https://example.com",
        "folder_id": 1,
        "created_at": "2024-01-01T00:00:00Z",
        "updated_at": "2024-01-01T00:00:00Z"
    }
}
```

### Jelszó Frissítése
```http
PUT /api/passwords/{id}
Authorization: Bearer {token}
Content-Type: application/json

{
    "name": "Updated Name",
    "password": "new-password"
}
```

**Válasz:**
```json
{
    "success": true,
    "password": {
        "id": 1,
        "name": "Updated Name",
        "username": "user@example.com",
        "url": "https://example.com",
        "folder_id": 1,
        "updated_at": "2024-01-01T00:00:00Z"
    }
}
```

### Jelszó Törlése
```http
DELETE /api/passwords/{id}
Authorization: Bearer {token}
```

**Válasz:**
```json
{
    "success": true,
    "message": "Jelszó sikeresen törölve"
}
```

## Mappa Kezelés

### Mappák Lekérése
```http
GET /api/folders
Authorization: Bearer {token}
```

**Válasz:**
```json
{
    "success": true,
    "folders": [
        {
            "id": 1,
            "name": "Work",
            "description": "Work-related passwords",
            "parent_id": null,
            "private": false,
            "created_at": "2024-01-01T00:00:00Z",
            "updated_at": "2024-01-01T00:00:00Z"
        }
    ]
}
```

### Mappa Létrehozása
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

**Válasz:**
```json
{
    "success": true,
    "folder": {
        "id": 1,
        "name": "New Folder",
        "description": "Folder description",
        "parent_id": null,
        "private": false,
        "created_at": "2024-01-01T00:00:00Z",
        "updated_at": "2024-01-01T00:00:00Z"
    }
}
```

### Mappa Frissítése
```http
PUT /api/folders/{id}
Authorization: Bearer {token}
Content-Type: application/json

{
    "name": "Updated Folder Name",
    "description": "Updated description"
}
```

### Mappa Törlése
```http
DELETE /api/folders/{id}
Authorization: Bearer {token}
```

## Felhasználókezelés (Csak Admin)

### Felhasználók Lekérése
```http
GET /api/users
Authorization: Bearer {token}
```

**Válasz:**
```json
{
    "success": true,
    "users": [
        {
            "id": 1,
            "name": "John Doe",
            "email": "john@example.com",
            "is_admin": false,
            "created_at": "2024-01-01T00:00:00Z",
            "updated_at": "2024-01-01T00:00:00Z"
        }
    ]
}
```

### Felhasználó Létrehozása
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

**Válasz:**
```json
{
    "success": true,
    "user": {
        "id": 1,
        "name": "New User",
        "email": "newuser@example.com",
        "is_admin": false,
        "created_at": "2024-01-01T00:00:00Z",
        "updated_at": "2024-01-01T00:00:00Z"
    }
}
```

### Felhasználó Frissítése
```http
PUT /api/users/{id}
Authorization: Bearer {token}
Content-Type: application/json

{
    "name": "Updated Name",
    "email": "updated@example.com"
}
```

### Felhasználó Törlése
```http
DELETE /api/users/{id}
Authorization: Bearer {token}
```

## Csoport Kezelés

### Csoportok Lekérése
```http
GET /api/groups
Authorization: Bearer {token}
```

### Csoport Létrehozása
```http
POST /api/groups
Authorization: Bearer {token}
Content-Type: application/json

{
    "name": "New Group",
    "description": "Group description"
}
```

### Csoport Frissítése
```http
PUT /api/groups/{id}
Authorization: Bearer {token}
Content-Type: application/json

{
    "name": "Updated Group Name"
}
```

### Csoport Törlése
```http
DELETE /api/groups/{id}
Authorization: Bearer {token}
```

## Jelszó Megosztás

### Megosztás Létrehozása
```http
POST /api/password-share/create
Authorization: Bearer {token}
Content-Type: application/json

{
    "item_id": 1,
    "recipient_email": "recipient@example.com",
    "recipient_name": "Recipient Name",
    "message": "Optional message",
    "access_password": "optional-access-password",
    "max_views": 1,
    "expiration_hours": 24
}
```

**Válasz:**
```json
{
    "success": true,
    "share": {
        "id": 1,
        "share_url": "https://your-domain.com/password-share/token",
        "expires_at": "2024-01-02T00:00:00Z",
        "max_views": 1
    }
}
```

### Megosztott Jelszó Megtekintése
```http
GET /api/password-share/{token}
```

**Válasz:**
```json
{
    "success": true,
    "passwordData": {
        "item": {
            "id": 1,
            "properties": {
                "name": "Shared Password",
                "username": "user@example.com",
                "password": "password",
                "url": "https://example.com"
            }
        },
        "share": {
            "id": 1,
            "created_by": {
                "name": "John Doe"
            },
            "expires_at": "2024-01-02T00:00:00Z",
            "view_count": 0,
            "max_views": 1
        }
    }
}
```

### Felhasználó Megosztásai Lekérése
```http
GET /api/password-share/my-shares
Authorization: Bearer {token}
```

### Megosztás Visszavonása
```http
DELETE /api/password-share/{shareId}/revoke
Authorization: Bearer {token}
```

## Rendszer Beállítások (Csak Admin)

### Rendszer Beállítások Lekérése
```http
GET /api/system/settings
Authorization: Bearer {token}
```

### Rendszer Beállítások Frissítése
```http
PUT /api/system/settings
Authorization: Bearer {token}
Content-Type: application/json

{
    "company_name": "My Company",
    "default_language": "en",
    "timezone": "UTC"
}
```

## Aktivitás Naplók

### Aktivitás Naplók Lekérése
```http
GET /api/activity-logs
Authorization: Bearer {token}
```

**Válasz:**
```json
{
    "success": true,
    "logs": [
        {
            "id": 1,
            "action": "password_created",
            "description": "Password 'My Password' created",
            "user_id": 1,
            "created_at": "2024-01-01T00:00:00Z"
        }
    ]
}
```

## Hiba Válaszok

### Validációs Hiba
```json
{
    "success": false,
    "message": "Validáció sikertelen",
    "errors": {
        "email": ["Az email mező kötelező."],
        "password": ["A jelszó mező kötelező."]
    }
}
```

### Autentikációs Hiba
```json
{
    "success": false,
    "message": "Nem engedélyezett"
}
```

### Nem Található Hiba
```json
{
    "success": false,
    "message": "Erőforrás nem található"
}
```

### Szerver Hiba
```json
{
    "success": false,
    "message": "Belső szerver hiba"
}
```

## Sebesség Korlátozás

Az API sebesség korlátozást implementál a visszaélések megelőzésére:

- **Autentikációs végpontok**: 5 kérés percenként
- **Általános API végpontok**: 60 kérés percenként
- **Jelszó műveletek**: 30 kérés percenként

Sebesség korlátozás fejlécek szerepelnek a válaszokban:
```
X-RateLimit-Limit: 60
X-RateLimit-Remaining: 59
X-RateLimit-Reset: 1640995200
```

## Lapozás

Lista végpontok támogatják a lapozást:

```http
GET /api/passwords?page=1&per_page=20
```

**Válasz:**
```json
{
    "success": true,
    "data": [...],
    "pagination": {
        "current_page": 1,
        "per_page": 20,
        "total": 100,
        "last_page": 5,
        "from": 1,
        "to": 20
    }
}
```

## Szűrés és Rendezés

### Szűrés
```http
GET /api/passwords?folder_id=1&search=work
```

### Rendezés
```http
GET /api/passwords?sort=name&order=asc
```

## Webhook-ok

### Webhook Események
- `password.created`
- `password.updated`
- `password.deleted`
- `user.created`
- `user.updated`
- `user.deleted`

### Webhook Adattartalom
```json
{
    "event": "password.created",
    "data": {
        "id": 1,
        "name": "My Password",
        "user_id": 1
    },
    "timestamp": "2024-01-01T00:00:00Z"
}
```
