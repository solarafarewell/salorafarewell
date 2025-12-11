# Dual User + Admin Authentication System - Test Guide

## ✅ What's Been Completed

Your website now has a full dual-role authentication system with separate views for users and admins.

### Features Implemented:
1. **User Login System** - Any username, password: `user123`
   - Users see a read-only calendar showing availability
   - Shows booked dates in red 🔴 and available dates in green 🟢
   - Can view availability for different rooms (Basic, Premium, Deluxe)
   - Can navigate between months to see future availability

2. **Admin Login System** - Password: `admin123`
   - Admins can edit the calendar directly
   - Click any date to toggle between booked/available
   - Full control over all bookings for all rooms
   - Can navigate months and manage the entire calendar

3. **Navigation Authentication UI**
   - When logged out: Shows "⚙️ Admin" and "👤 User Login" buttons
   - When logged in: Shows logged-in user label and "Logout" button
   - Dynamic buttons update based on authentication state

4. **Session Management**
   - Tokens stored in browser localStorage
   - Sessions persist across page reloads
   - Logout clears all tokens and returns to login screen

## 🧪 How to Test

### Test 1: User Login & Calendar View
1. Open the website
2. Look for the nav buttons at the top right
3. Click **"👤 User Login"**
4. Enter:
   - **Username**: `john` (or any name)
   - **Password**: `user123`
5. Click "Login"
6. **Expected Result**: You should see the "📅 Room Availability" calendar
   - Select different rooms from the dropdown
   - See dates in red (booked) and green (available)
   - Use Prev/Next buttons to navigate months
   - Cannot click dates (read-only view)

### Test 2: Admin Login & Calendar Edit
1. Open the website
2. Click **"⚙️ Admin"**
3. Enter:
   - **Password**: `admin123`
4. Click "Login"
5. **Expected Result**: You should see the admin calendar editor
   - Can click any date to toggle booked/available
   - Clicking a date shows a confirm dialog
   - Changes appear immediately
   - Changes are synced to localStorage

### Test 3: Logout & Re-login
1. While logged in, click the **"Logout"** button (top right)
2. **Expected Result**: 
   - Page reloads
   - Login buttons reappear
   - Previous session is cleared
3. Log back in with either user or admin credentials
4. **Expected Result**: You should see the appropriate panel for that role

### Test 4: Session Persistence
1. Log in as a user
2. Refresh the page (F5 or Ctrl+R)
3. **Expected Result**: 
   - You stay logged in
   - Calendar view remains open
   - User label still shows in nav

### Test 5: Admin Makes Changes, User Sees Updates
1. **In one browser tab:**
   - Log in as admin
   - Click a date to book it (turns red)
   - Note which date you booked

2. **In another browser tab (or logout and re-login as user):**
   - Log in as a user
   - Look at the same room
   - **Expected Result**: The date you booked as admin shows as red (booked)

### Test 6: Multiple Rooms
1. Log in as user
2. In the "Select Room" dropdown, choose different rooms
3. **Expected Result**: Calendar updates to show each room's availability independently

## 📋 Demo Credentials

**User Login:**
- Username: Any name (e.g., `john`, `alice`, `user`)
- Password: `user123`

**Admin Login:**
- Password: `admin123`

## 🎨 Visual Indicators

### User Calendar:
- **🟢 Green cells**: Available dates
- **🔴 Red cells**: Booked dates

### Admin Calendar:
- **🔵 Blue cells**: Available dates
- **🔴 Red cells**: Booked dates
- Click any cell to toggle

### Navigation:
- **When logged out**: Red "Admin" button + Blue "User Login" button
- **When logged in**: User/Admin label + Red "Logout" button

## 🔧 Technical Details

### Authentication Model:
- **User**: `username` + `password: 'user123'` (any username works)
- **Admin**: `password: 'admin123'` only
- Tokens stored in `localStorage` as:
  - `_userToken` (for user sessions)
  - `_adminToken` (for admin sessions)
  - `_userName` (to display user's name)

### Data Storage:
- Bookings stored in localStorage under keys like:
  - `bookings_room-basic`
  - `bookings_room-premium`
  - `bookings_room-deluxe`
- Each booking is stored as a date string: `YYYY-MM-DD`

### Firestore Sync (if configured):
- Changes automatically sync to Firestore (if database is configured)
- Bookings include ownership information (userId)
- Users can only modify their own bookings in Firestore

## 🐛 Troubleshooting

| Issue | Solution |
|-------|----------|
| Login buttons not showing | Clear browser cache and reload (Ctrl+Shift+Del) |
| Calendar not updating after booking | Check browser console for errors |
| Logout button not working | Make sure you're clicking the red "Logout" button in nav |
| Dates resetting after refresh | Check if localStorage is enabled in browser |
| Can't see admin panel | Make sure password is exactly `admin123` |

## 📝 Next Steps (Optional Enhancements)

If you want to extend this system further:

1. **Add booking request form for users** - Let users submit booking requests (name, email, dates, notes)
2. **Add order/payment system** - Integrate with payment providers
3. **Email notifications** - Send confirmation emails when bookings change
4. **Admin dashboard** - Show booking statistics, revenue, upcoming reservations
5. **Backend authentication** - Replace localStorage with real server-side auth
6. **Database integration** - Use Firebase Auth instead of password-only system

## ✨ You're All Set!

Your dual authentication system is ready to use. Users can see availability, and admins can manage the calendar. Happy testing! 🎉
