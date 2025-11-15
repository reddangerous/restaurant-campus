# System Architecture Diagram

## High-Level Architecture

```

BROWSER 
http://localhost:3000 


HTTP Requests (with JWT token)


REACT FRONTEND 


Pages Components Context 

- Login - Protected - Auth 
- Home Route Context 
- Menu 
- Checkout 
- Orders 
- Vendor 
Dashboard Services 

- API calls 
- fetch() 



REST API Calls


EXPRESS BACKEND 
http://localhost:5000 


Routes Controllers Middleware 

- Auth - Auth - JWT Auth 
- Restaurant - Restaurant - Role Check 
- Menu - Menu 
- Orders - Orders 



Database Layer 
(better-sqlite3 library) 



SQL Queries


SQLITE DATABASE 
database.db 


users restaurants menu_items 



orders order_items 


```

## Authentication Flow

```

1. Login 2. Validate 
User Backend Database 
email/password credentials 


3. Generate JWT


4. Return Token JWT 
Token 
+ User Info 

5. Store in localStorage


Browser 
Storage 


For subsequent requests:

Request with 
User Backend 
Bearer Token 


Verify JWT


Allow 
or 
Deny 

```

## Student Order Flow

```
1. Browse Restaurants

Home GET /api/restaurants


2. View Menu

Menu GET /api/restaurants/:id


3. Add to Cart

Cart (State in React)


4. Checkout

Checkout POST /api/orders
{restaurant_id, items, address}

5. Track Orders

Orders GET /api/orders/my-orders

```

## Vendor Order Management Flow

```
1. View Dashboard

Dashboard GET /api/orders/vendor/orders


2. Filter Orders

Filter (Client-side filtering)


3. Update Status

Update PUT /api/orders/:id/status
{status: "confirmed"}

Order Status Progression:
pending → confirmed → preparing → ready → delivered
```

## Database Relationships

```

users 
id 
email 
password Foreign Key
role 




vendor_id student_id

restaurants orders 
id id 
name total_amt 
category status 


restaurant_id order_id 


menu_items order_items 
id id 
name quantity 
price price 


menu_item_id

(references menu_items.id)
```

## File Structure Visual

```
481-project-main/

backend/ # Node.js Backend
src/
config/
database.js [DB Connection]
initDatabase.js [Table Creation]

controllers/ [Business Logic]
authController.js
restaurantController.js
menuController.js
orderController.js

middleware/ [Auth & Validation]
auth.js

routes/ [API Endpoints]
authRoutes.js
restaurantRoutes.js
menuRoutes.js
orderRoutes.js

server.js [Entry Point]

package.json
.env
database.db [SQLite File]

frontend/ # React Frontend
src/
components/
ProtectedRoute.js [Route Guard]

context/
AuthContext.js [Global Auth State]

pages/ [Page Components]
Login.js
Register.js
Home.js
RestaurantMenu.js
Checkout.js
StudentOrders.js
VendorDashboard.js

services/
api.js [API Calls]

App.js [Main Component]
index.js [Entry Point]

package.json
```

## API Request/Response Flow

```
Example: Create Order

1. User Action
Click "Place Order" button

2. Frontend (React)

Checkout.js 
- Collect form data 
- Call orderAPI.create() 


3. API Service

api.js 
- Add Authorization header 
- fetch(POST, /api/orders) 


HTTP POST
Headers: {Authorization: "Bearer token"}
Body: {restaurant_id, items, address}

4. Backend 

Routes (orderRoutes.js) 
- Check authentication 
- Check role (student) 


5. Controller 

orderController.js 
- Validate data 
- Calculate total 
- Create order in DB 
- Create order items 


6. Database 

SQLite 
- INSERT into orders 
- INSERT into order_items 
- Return new IDs 


7. Response 

{ 
message: "Order created", 
order: {id: 5, total: 42} 
} 


8. Frontend 

- Show success message 
- Navigate to orders page 

```

## Security Layers

```

Request from Browser 




Layer 1: CORS 
- Check origin 
- Allow/Deny 




Layer 2: JWT Verification 
- Check if token exists 
- Verify token signature 
- Check expiration 




Layer 3: Role Authorization 
- Check user role 
- Match required role 
- Allow/Deny 




Layer 4: Database Queries 
- Prepared statements 
- Foreign key constraints 
- Data validation 




Process Request 

```

---

**This visual guide shows how all the pieces fit together!**
