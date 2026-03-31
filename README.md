# Quantity Measurement App - Complete Setup Guide

## Project Structure
```
frontend-qma/
├── index.html           → Redirects to auth.html
├── auth.html            → Login & Register page
├── dashboard.html       → Main dashboard (protected, requires login)
├── dashboard.js         → Dashboard logic & unit conversion
├── script.js            → Old file (no longer used)
├── styles.css           → Shared styles for all pages
└── README.md            → This file
```

## How to Run

### Option 1: VS Code Live Server (Easiest)
1. Install "Live Server" extension in VS Code
2. Right-click on `index.html` → **Open with Live Server**
3. Browser opens automatically at `http://127.0.0.1:5500`
4. You'll be redirected to the login page

### Option 2: Python
```bash
cd "d:\harshita\Harshita Agrawal\OneDrive\Documents\frontend-qma"
python -m http.server 5500
```
Then open: `http://localhost:5500`

### Option 3: Node.js
```bash
npm install -g serve
serve -p 5500
```
Then open: `http://localhost:5500`

---

## Authentication System

### Email/Password Login (No Setup Needed)
- **Login Page**: Email + Password form
- **Register Page**: Full Name + Email + Password + Confirm Password
- Credentials are stored in **localStorage** (demo purposes)
- No backend required to test

### Google Sign-In (Requires Setup)

#### Why "Access Blocked" Error Occurs:
The error happens when Google OAuth Client ID doesn't have your app's origin in the **authorized JavaScript origins** list.

#### Step-by-Step Fix:

1. **Go to Google Cloud Console:**
   - [https://console.cloud.google.com](https://console.cloud.google.com)

2. **Create a New Project:**
   - If you don't have one already

3. **Enable Google Identity Services:**
   - Search: "Identity and Access Management" → Enable OAuth 2.0

4. **Create OAuth 2.0 Client ID:**
   - Go to **Credentials** → **Create Credentials** → **OAuth Client ID**
   - Choose **Web application**

5. **Add Authorized Origins (CRITICAL):**
   Under "Authorized JavaScript origins" add:
   ```
   http://localhost:5500
   http://127.0.0.1:5500
   ```

6. **Copy Your Client ID:**
   - It looks like: `615365280199-1s4fht7q8kqldoic283m860obnjvaep6.apps.googleusercontent.com`

7. **Paste Client ID in Code:**
   - Open `auth.html`
   - Find line: `const GOOGLE_CLIENT_ID = "..."`
   - Replace with your actual Client ID

8. **Save and Reload:**
   - Refresh the browser at `http://localhost:5500`
   - Google button should now work!

#### Deployment (Later):
When deploying to production, add these origins too:
```
https://yourdomain.com
https://www.yourdomain.com
```

---

## File Descriptions

### `index.html`
- Simple redirect page to `auth.html`
- Users land here first, instantly redirected to login

### `auth.html`
- **Login Form**: Email + Password
- **Register Form**: Full Name + Email + Password
- **Toggle**: Switch between Login & Register
- **Google Button**: Integrated Google Sign-In
- Uses localStorage to store user data
- Redirects to dashboard on successful auth

### `dashboard.html`
- Protected dashboard (redirects to login if not authenticated)
- 4 measurement types: Length, Weight, Temperature, Volume
- 3 action modes: Comparison, Conversion, Arithmetic
- Shows logged-in user's name
- Logout button in header

### `dashboard.js`
- Handles auth check (redirects to login if needed)
- Displays user information
- Unit conversion logic for all measurement types
- Event listeners for type selection, action tabs, and input changes
- Logout functionality with localStorage cleanup

### `styles.css`
- Responsive design (mobile-first)
- Beautiful gradient backgrounds
- Blue & teal color scheme
- Flexbox & Grid layouts
- Variable-based CSS for easy customization

---

## Testing Without Google Auth

1. Start the app normally
2. Click **Create Account**
3. Fill in:
   - Full Name: `John Doe`
   - Email: `john@example.com`
   - Password: `test123`
   - Confirm: `test123`
4. Click **Create Account**
5. You're now logged in with localStorage (persists on refresh)
6. Logout by clicking **Logout** button in dashboard header

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| "Access Blocked" on Google button | Add `http://localhost:5500` to Authorized Origins in Google Cloud Console |
| Page blank after login | Check browser console for errors (F12 → Console tab) |
| Logout doesn't work | Clear localStorage: Open DevTools → Application → LocalStorage → Clear All |
| Can't see Google button | Ensure Google SDK script loaded (`https://accounts.google.com/gsi/client`) |
| Wrong origin error | Make sure origin matches exactly (no trailing slash, port number must match) |

---

## Features

✅ Email/Password Login & Register  
✅ Google OAuth Sign-In  
✅ Protected Dashboard (requires login)  
✅ Unit Conversion (Length, Weight, Temperature, Volume)  
✅ Comparison Mode (compare two units)  
✅ Conversion Mode (convert single value)  
✅ Arithmetic Mode (add/subtract across units)  
✅ Responsive Design (works on mobile & desktop)  
✅ Modern UI with gradients & smooth animations  
✅ LocalStorage persistence  

---

## Next Steps (Optional Enhancements)

1. **Backend Integration**: Connect to Node.js/Express API for real auth
2. **Database**: Store user credentials securely (bcrypt hashing)
3. **JWT Tokens**: Implement token-based authentication
4. **Separate Login Page**: Create dedicated auth routes
5. **PWA**: Add service worker for offline functionality

---

## License
Free to use & modify for learning purposes.
