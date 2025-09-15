# Features Overview

## Core Features

### 🔐 Security Features
- **End-to-End Encryption**: All passwords encrypted with AES-256
- **Two-Factor Authentication**: TOTP-based 2FA support
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

## Detailed Feature Descriptions

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

### System Settings

#### General Settings
- Company name and branding
- Default language settings
- Timezone configuration

#### Security Settings
- Password policy configuration
- Session timeout settings
- 2FA enforcement policies

#### Email Settings
- SMTP configuration
- Email templates customization
- Notification preferences

#### LDAP Settings
- LDAP server configuration
- User synchronization settings
- Group mapping configuration

## User Roles and Permissions

### Admin Users
- Full system access and configuration
- User and group management
- System settings and maintenance
- Activity monitoring and logs
- LDAP configuration and management

### Regular Users
- Personal password management
- Access to shared folders and groups
- Profile management
- Limited system access

## Advanced Features

### Password Sharing
- Secure password sharing with expiration
- Access password protection
- View count limitations
- Email notifications

### Activity Logging
- Comprehensive audit trail
- User action tracking
- System event logging
- Security monitoring

### Maintenance Mode
- System maintenance with admin-only access
- Automatic email handling
- User notification system
- Real-time dashboard updates

### License Management
- License validation and management
- Feature activation based on license
- License expiration handling
- Support and updates

## Mobile Support

### Responsive Design
- Mobile-friendly interface
- Touch-optimized controls
- Adaptive layouts
- Cross-device synchronization

### Progressive Web App
- Offline functionality
- App-like experience
- Push notifications
- Home screen installation

## Integration Capabilities

### API Access
- RESTful API endpoints
- Authentication tokens
- Rate limiting
- Comprehensive documentation

### Third-Party Integrations
- Browser extensions
- Mobile apps
- Enterprise systems
- Custom integrations

## Security Features

### Data Protection
- End-to-end encryption
- Secure key management
- Data backup encryption
- Secure deletion

### Access Control
- Multi-factor authentication
- Role-based permissions
- Session management
- IP restrictions

### Compliance
- GDPR compliance
- SOC 2 compliance
- Audit logging
- Data retention policies
