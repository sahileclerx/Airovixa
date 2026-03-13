
## 1. High Level Architecture
|Component|Technology|
|--|--|
|User Web App|Next.js (PWA)|
|Admin Panel|React|
|Authentication|Firebase Auth|
|Database|Firestore|
|File Storage|Firebase Storage|
|Backend Logic|Firebase Cloud Functions|
|Search|Algolia Search|
|QR / Barcode Scan|react-qr-barcode-scanner|
|Email|Sendgrid|
----------

## 2. Core Features - User Side (PWA)

1️⃣ Registration  
2️⃣ Admin approval required  
3️⃣ Login  
4️⃣ Aircraft part search  
5️⃣ Scan QR / Barcode  
6️⃣ View part details  
7️⃣ PWA install on phone    

----------

## 3. Admin Panel Features

### User Management

Admin can:
-   Approve user
-   Reject user
-   Deactivate user
-   View user list
-   Search user

User states:
- pending  
- approved  
- rejected  
- deactivated

### Parts Management (CRUD)

Admin can:
-   Add part
-   Edit part
-   Delete part
-   Upload image
-   Generate QR code
-   Upload documents

----------

## 4. Database Design (Firestore)

- users  
  -  userId: primary 
  -  name: text 
   - email: text  
   - company: text
   - employeeid: text
   - profilepicture: link
   - role: user  | admin
   - status: "pending | approved | rejected"  
  -  createdAt: date

- parts  
   - partId  
   - partName  
   - partNumber  
   - aircraftModel  
   - manufacturer  
   - description  
   - category  
   - barcode  
   - qrCode  
   - image  
   - documents  
   - video
   - createdAt
----------

## 5. Search methods

User can search by: Part Name | Part Number | QR Code | Barcode | Category | Aircraft Model

----------

## 6. QR / Barcode Scan

### Workflow:
Scan code  > extract partNumber  > fetch part details  > show result

----------

## 7. Image & File Storage
### Firebase Storage
Structure:
/parts /partId/image.jpg  | document.pdf
/users_profile_images/userId/image.jpg

----------


# 8. PWA Setup

Next.js can become installable app.

### Features:
-   Offline caching
-   Add to home screen
-   Mobile friendly
-   Push notifications (optional)
    
### Tools:
next-pwa

----------

# 9. Admin Panel Architecture

### Tools:
React  | Tailwind CSS |  Firebase SDK

### Admin features:
-   Dashboard
-   Users
-   Parts
-   Analytics
----------

# 14. Folder Structure

### User App (Next.js)
/app  
/components  
/lib  
/hooks  
/pages  
/utils  
/services

### Admin Panel

/src  
/components  
/pages  
/services  
/hooks  
/utils

----------

# 15. Performance Planning

For 10k users + 10k parts Firestore is fine.
Optimize by:
-   Pagination
-   Indexing
-   Caching
-   CDN for images

----------

# 16. Deployment

- Frontend > Vercel
- Admin > Firebase Hosting
 - Backend > Firebase
----------

# 17. Estimated Development Phases

**Phase 1** : Authentication + User approval
**Phase 2** :  Parts CRUD
**Phase 3**: Search engine
**Phase 4**: QR / Barcode scanner
**Phase 5**: PWA + polish

----------

# 18. Approx Timeline

|Component|Time Required|
|--|--|
|Planning|3 days|
|Designing|3 Days|
|Auth system (Admin + User with Approval)|5 days|
|Admin panel (Dashboard)| 3 Days |
|Parts system|5 days|
|Search system|5 days|
|Scanner|3 days|
|PWA|2 days|
|Testing|5 days|
|QA Fixes|10 Days|
|Total|44 Days|

----------

# 20. Future Features
-   AI part search
-   Image recognition search 
-   Aircraft maintenance logs
-   Supplier integration
-   Inventory tracking
----------
