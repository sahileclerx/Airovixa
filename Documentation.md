
# Airovixa Full System Architecture

## 1. High Level Architecture

```
                Users (Web + Mobile PWA)
                         │
                         │
                  Next.js Frontend
                         │
                 REST API Requests
                         │
                PHP API Backend Layer
                         │
                   MySQL Database
                         │
               Admin Panel (PHP)

```

## 2. Applications in the System

You will build **3 separate applications**.

### 1️⃣ User App (Frontend) -> Next.js (PWA)

Users can:
-   Register
-   Login
-   Search Aircraft Parts
-   Scan QR / Barcode (Future)
-   View Part Details
-   Save Parts
-   Manage Profile

----------

### 2️⃣ Admin Panel -> PHP + MySQL

Admin can:
-   Manage Users
-   Approve registrations
-   Add/Edit/Delete Parts
-   Upload images
-   Embed videos
-   Manage tags
-   View analytics

----------

### 3️⃣ API Server -> PHP REST API

Acts as bridge between **Next.js App & Admin Panel** => **MySQL**

----------

## 3. Infrastructure Architecture

```
                Cloudflare CDN
                      │
        ┌─────────────┴─────────────┐
        │                           │
   Next.js App                Admin Panel
  (Vercel / VPS)               (VPS)
        │                           │
        └─────────────┬─────────────┘
                      │
                   PHP API
                      │
                  MySQL DB
                      │
                File Storage
              (S3 / Local Disk)

```

----------

## 4. Database Architecture

### Tables Overview

- users
- parts
- part_images
- saved_parts
- user_sessions
- admin_users
- logs

----------

### USERS TABLE
|Field|Type|
|--|--|
|id|bigint|
|name|varchar|
|email|varchar|
|employee_id|text(image_url)|
|password_hash|varchar|
|status|enum(pending,approved,blocked)|
|created_at|timestamp|
|updated_at|timestamp|

----------

### PARTS TABLE

|Field|Type|
|--|--|
|id|bigint|
|name|varchar|
|part_number|varchar|
|manufacturer|varchar|
|aircraft_compatibility|varchar|
|description|longtext|
|qr_code|varchar|
|barcode|varchar|
|images|text(JSON of URLs)|
|created_at|timestamp|
|updated_at|timestamp|

----------

### PART IMAGES

|Field|Type|
|--|--|
|id|bigint|
|part_id|bigint|
|image_url|text|

----------

### SAVED PARTS

|Field|Type|
|--|--|
|user_id|bigint|
|part_id|bigint|

----------

### ADMIN USERS
|Field|Type|
|--|--|
|id|int|
|name|varchar|
|email|varchar|
|password|varchar|
----------

## 5. API Architecture ( api.airovixa.com )

### AUTH APIs

#### Register

```
POST /auth/register
name
email
company_name
employee_id
password
status → `pending`

```
----------

#### Login

```
POST /auth/login
JWT Token
```
----------

#### Forgot Password

```
POST /auth/forgot-password
```
----------

#### Reset Password

```
POST /auth/reset-password
```

----------

### PART SEARCH APIs

#### Search Parts

```
GET /parts/search?q=engine
```

----------

#### Scan QR

```
GET /parts/scan/{code}
```

----------

#### Part Details

```
GET /parts/{id}
```

----------

#### Save Part

```
POST /parts/save
```

----------

#### Saved Parts

```
GET /user/saved
```

----------

### USER APIs

#### Profile

```
GET /user/profile
```

----------

#### Update Profile

```
PUT /user/profile
```

----------

#### Change Password

```
POST /user/change-password
```

----------

### ADMIN APIs

#### Users

```
GET /admin/users
POST /admin/user/approve
POST /admin/user/block
```
----------

### Parts

```
GET /admin/parts
POST /admin/parts
PUT /admin/parts/{id}
DELETE /admin/parts/{id}
```

----------

## 6. Next.js Frontend Architecture

```
/app
   /login
   /register
   /forgot-password
   /reset-password

   /home
   /search
   /part/[id]
   /saved
   /settings

/components
   Header
   SearchBar
   PartCard
   Pagination
   Footer
   Loader
   QRScanner

/lib
   api.ts
   auth.ts
   utils.ts

/store
   authStore
   partStore

```
----------

## 7. Admin Panel Architecture

```
/admin
   /dashboard
   /users
   /parts
   /parts/add
   /parts/edit
   /settings

```
----------

Admin Components
```
Sidebar
Topbar
DataTable
FormBuilder
ImageUploader
RichEditor
VideoEmbed

```

----------

## 8. Search System
Initial:

```
MySQL FULLTEXT SEARCH

```

Query example

```
SELECT *
FROM parts
WHERE MATCH(name,description)
AGAINST('engine')

```

----------

Future Upgrade

```
Algolia
OR
ElasticSearch

```

----------

## 9. QR / Barcode Scan

Frontend uses:

```
html5-qrcode

```

Flow

```
Scan QR
   ↓
Get Code
   ↓
Call API

GET /parts/scan/{code}

```

----------

## 10. Security
 **Password** -> bcrypt hashing
 **Auth** -> JWT tokens
 **Rate limit** -> attempts
**Admin** -> IP restriction

----------

## 11. PWA Setup (next-pwa)

#### Features
- Installable app
- Offline support
- Mobile experience
- Push notifications

----------

## 12. Hosting Architecture

**Recommended Setup** : VPS 8GB RAM
Example:
- VPS 8GB RAM
- DigitalOcean
- AWS Lightsail
- Hetzner



Domains
- airovixa.com        → Next.js
- admin.airovixa.com  → Admin Panel
- api.airovixa.com    → PHP API

----------

## 14. Development Timeline
**Week 1** -> Design + Database
**Week 2** -> Admin panel base
**Week 3** -> Parts CRUD
**Week 4** -> Auth system
**Week 5** -> Next.js frontend
**Week 6** -> Search + Scan
**Week 7** -> Testing
**Week 8** -> Deployment

----------
