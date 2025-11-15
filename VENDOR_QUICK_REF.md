# Quick Reference - Vendor Side

## Login
1. Go to http://localhost:3000
2. Login with your vendor account
3. Redirects to `/vendor/dashboard`

## First Time Setup
1. See "Create Your Restaurant" page
2. Fill: Name, Description, Category
3. Click "Create Restaurant"
4. Add menu items

## Daily Operations

### Manage Restaurant (`/vendor/restaurant`)
**Add Menu Item:**
- Click "Add Menu Item"
- Fill: Name, Description, Price, Category
- Submit

**Edit Item:**
- Click "Edit" on item card
- Modify fields
- Click "Update Item"

**Toggle Availability:**
- Click "Mark Unavailable" (when out of stock)
- Click "Mark Available" (when back in stock)

**Delete Item:**
- Click "Delete"
- Confirm

### Manage Orders (`/vendor/dashboard`)
**View Orders:**
- See all orders from students
- Filter: All, Pending, Confirmed, Preparing, Ready

**Process Order Workflow:**
1. Pending → Click "Confirm Order"
2. Confirmed → Click "Start Preparing"
3. Preparing → Click "Mark as Ready"
4. Ready → Click "Mark as Delivered"

Or reject: Pending → Click "Cancel Order"

## Navigation
- Dashboard: Click "Manage Restaurant" button
- Restaurant: Click "View Orders" button
- Logout: Click "Logout" (top right)

## Test Credentials (Already in Database)
**Vendor:** pizza@vendor.com / password123

## Key Files (Your Part)
```
frontend/src/pages/
  VendorDashboard.js      - Orders page
  VendorRestaurant.js     - Restaurant/menu page

backend/src/controllers/
  restaurantController.js - Restaurant logic
  menuController.js       - Menu logic
  orderController.js      - Order logic
```

## Common Commands
```bash
# Start backend
cd backend
npm start

# Start frontend (new terminal)
cd frontend
npm start

# Reset database (if needed)
cd backend
npm run init-db
```

## Order Status Colors
- Yellow: Pending
- Blue: Confirmed
- Orange: Preparing
- Green: Ready
- Gray: Delivered
- Red: Cancelled

## Quick Troubleshooting
**Can't see restaurant?** 
→ Did you create it after registration?

**No menu items showing?**
→ Add at least one menu item

**Orders not appearing?**
→ Check backend is running on port 5000

**Can't update status?**
→ Check token is valid (re-login)

## Demo Flow
1. Login as vendor
2. Show restaurant details
3. Add new menu item live
4. Toggle availability
5. Switch to dashboard
6. Show order filters
7. Update an order status
8. Show completed order
