# API Documentation

## Authentication

### Login
```http
POST /api/login
Content-Type: application/json

{
    "email": "user@example.com",
    "password": "password"
}
```

**Response:**
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

### Logout
```http
POST /api/logout
Authorization: Bearer {token}
```

**Response:**
```json
{
    "success": true,
    "message": "Logged out successfully"
}
```

## Password Management

### Get Passwords
```http
GET /api/passwords
Authorization: Bearer {token}
```

**Response:**
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

### Create Password
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

**Response:**
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

### Update Password
```http
PUT /api/passwords/{id}
Authorization: Bearer {token}
Content-Type: application/json

{
    "name": "Updated Name",
    "password": "new-password"
}
```

**Response:**
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

### Delete Password
```http
DELETE /api/passwords/{id}
Authorization: Bearer {token}
```

**Response:**
```json
{
    "success": true,
    "message": "Password deleted successfully"
}
```

## Folder Management

### Get Folders
```http
GET /api/folders
Authorization: Bearer {token}
```

**Response:**
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

### Create Folder
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

**Response:**
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

### Update Folder
```http
PUT /api/folders/{id}
Authorization: Bearer {token}
Content-Type: application/json

{
    "name": "Updated Folder Name",
    "description": "Updated description"
}
```

### Delete Folder
```http
DELETE /api/folders/{id}
Authorization: Bearer {token}
```

## User Management (Admin Only)

### Get Users
```http
GET /api/users
Authorization: Bearer {token}
```

**Response:**
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

### Create User
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

**Response:**
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

### Update User
```http
PUT /api/users/{id}
Authorization: Bearer {token}
Content-Type: application/json

{
    "name": "Updated Name",
    "email": "updated@example.com"
}
```

### Delete User
```http
DELETE /api/users/{id}
Authorization: Bearer {token}
```

## Group Management

### Get Groups
```http
GET /api/groups
Authorization: Bearer {token}
```

### Create Group
```http
POST /api/groups
Authorization: Bearer {token}
Content-Type: application/json

{
    "name": "New Group",
    "description": "Group description"
}
```

### Update Group
```http
PUT /api/groups/{id}
Authorization: Bearer {token}
Content-Type: application/json

{
    "name": "Updated Group Name"
}
```

### Delete Group
```http
DELETE /api/groups/{id}
Authorization: Bearer {token}
```

## Password Sharing

### Create Share
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

**Response:**
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

### View Shared Password
```http
GET /api/password-share/{token}
```

**Response:**
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

### Get User Shares
```http
GET /api/password-share/my-shares
Authorization: Bearer {token}
```

### Revoke Share
```http
DELETE /api/password-share/{shareId}/revoke
Authorization: Bearer {token}
```

## System Settings (Admin Only)

### Get System Settings
```http
GET /api/system/settings
Authorization: Bearer {token}
```

### Update System Settings
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

## Activity Logs

### Get Activity Logs
```http
GET /api/activity-logs
Authorization: Bearer {token}
```

**Response:**
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

## Error Responses

### Validation Error
```json
{
    "success": false,
    "message": "Validation failed",
    "errors": {
        "email": ["The email field is required."],
        "password": ["The password field is required."]
    }
}
```

### Authentication Error
```json
{
    "success": false,
    "message": "Unauthorized"
}
```

### Not Found Error
```json
{
    "success": false,
    "message": "Resource not found"
}
```

### Server Error
```json
{
    "success": false,
    "message": "Internal server error"
}
```

## Rate Limiting

The API implements rate limiting to prevent abuse:

- **Authentication endpoints**: 5 requests per minute
- **General API endpoints**: 60 requests per minute
- **Password operations**: 30 requests per minute

Rate limit headers are included in responses:
```
X-RateLimit-Limit: 60
X-RateLimit-Remaining: 59
X-RateLimit-Reset: 1640995200
```

## Pagination

List endpoints support pagination:

```http
GET /api/passwords?page=1&per_page=20
```

**Response:**
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

## Filtering and Sorting

### Filtering
```http
GET /api/passwords?folder_id=1&search=work
```

### Sorting
```http
GET /api/passwords?sort=name&order=asc
```

## Webhooks

### Webhook Events
- `password.created`
- `password.updated`
- `password.deleted`
- `user.created`
- `user.updated`
- `user.deleted`

### Webhook Payload
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
