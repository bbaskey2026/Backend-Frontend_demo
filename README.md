
# Random Users Application - Complete Documentation

A full-stack web application that fetches random user data from JSONPlaceholder API and displays them in an elegant dark-themed interface.

## Project Overview

This application consists of a Node.js/Express backend server and a modern frontend with HTML, CSS, and JavaScript. It demonstrates how to fetch data from a public API and display it in a user-friendly way.

## Tech Stack

**Backend:**
- Node.js
- Express.js
- Axios (for HTTP requests)

**Frontend:**
- HTML5
- CSS3
- JavaScript (Vanilla)
- Font Awesome Icons

**External API:**
- JSONPlaceholder (https://jsonplaceholder.typicode.com)

## Project Structure

```
project-root/
├── server.js              # Main server file
├── package.json           # Project dependencies
├── public/
│   ├── index.html         # Home page
│   ├── result.html        # Results page
│   ├── style/
│   │   └── style.css      # Global styling
│   └── script/
│       ├── script.js      # Frontend logic
│       └── dashboard.js   # Results page logic
└── README.md              # This file
```

## Setup Instructions

### Prerequisites

- Node.js (v14 or higher)
- npm (Node Package Manager)
- Modern web browser

### Installation

1. **Clone or download the project**
   ```bash
   git clone <repository-url>
   cd random-users-app
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```
   
   This installs:
   - `express` - Web framework
   - `axios` - HTTP client
   - `path` - Node.js module for file paths

3. **Start the server**
   ```bash
   node server.js
   ```
   
   Or with nodemon for development:
   ```bash
   npm install --save-dev nodemon
   npm run dev
   ```

4. **Open in browser**
   - Navigate to `http://localhost:3000`
   - The home page will load

## API Integration

### JSONPlaceholder API

**Endpoint:** `https://jsonplaceholder.typicode.com/users`

**What it provides:**
- 10 fake user objects
- Realistic user data structure
- No authentication required
- Free to use

**User Object Structure:**
```json
{
  "id": 1,
  "name": "Leanne Graham",
  "username": "Bret",
  "email": "Sincere@april.com",
  "address": {
    "street": "Kulas Light",
    "suite": "Apt. 556",
    "city": "Gwenborough",
    "zipcode": "92998-3874"
  },
  "phone": "1-770-736-8031",
  "website": "hildegard.org",
  "company": {
    "name": "Romaguera-Crona",
    "catchPhrase": "Multi-layered client-server neural-net"
  }
}
```

### Fetching Data

The frontend fetches users with this code:

```javascript
const response = await axios.get('https://jsonplaceholder.typicode.com/users');
const users = response.data;
```

**What happens:**
1. Axios makes a GET request to JSONPlaceholder
2. Returns an array of 10 user objects
3. Data is stored in sessionStorage
4. User is redirected to results page
5. Results page displays the users in cards

## Server Routes

### Route 1: Home Page

**Route:** `GET /`

**File Served:** `public/index.html`

**Purpose:** Serves the landing page

**Code:**
```javascript
app.get('/', (req, res) => {
    res.sendFile(path.join(__dirname, 'public', 'index.html'));
});
```

**What happens:**
- User visits `http://localhost:3000/`
- Server sends the index.html file
- Home page loads with "Fetch Random Users" button
- User can click button to fetch users from API

**Features on this page:**
- Dark theme design
- "Fetch Random Users" button
- Feature showcase grid
- Loading spinner during fetch
- No effects or animations

### Route 2: Results Page

**Route:** `GET /result`

**File Served:** `public/result.html`

**Purpose:** Serves the results/dashboard page

**Code:**
```javascript
app.get('/result', (req, res) => {
    res.sendFile(path.join(__dirname, 'public', 'result.html'));
});
```

**What happens:**
- After fetching users, frontend redirects to `/result`
- Server sends the result.html file
- Page displays fetched user cards
- Each card shows user information in a grid layout
- User can go back to home page

**Features on this page:**
- Displays user cards in grid
- Shows user name, email, phone, website
- Shows location and company info
- Font Awesome icons for each field
- Back button to return home
- Dark theme matching home page

## Frontend Logic

### Home Page (index.html)

**JavaScript Function:**
```javascript
async function fetchUsers() {
    const btn = document.querySelector('.fetch-btn');
    const loading = document.querySelector('.loading');
    
    btn.disabled = true;
    loading.classList.add('show');
    
    try {
        const response = await axios.get('https://jsonplaceholder.typicode.com/users');
        const users = response.data;
        
        // Store in sessionStorage
        sessionStorage.setItem('randomUsers', JSON.stringify(users));
        
        // Redirect after 1 second
        setTimeout(() => {
            window.location.href = '/result';
        }, 1000);
        
    } catch (error) {
        console.error('Error:', error);
        alert('Failed to fetch users. Please try again.');
        btn.disabled = false;
        loading.classList.remove('show');
    }
}
```

**What it does:**
1. Disables fetch button
2. Shows loading spinner
3. Makes API request via Axios
4. Stores response in sessionStorage
5. Redirects to results page
6. Handles errors gracefully

### Results Page (result.html)

**JavaScript Functions:**

**getInitials()** - Gets user initials for avatar:
```javascript
function getInitials(name) {
    return name.split(' ').map(n => n[0]).join('').toUpperCase();
}
// Example: "John Doe" → "JD"
```

**displayUsers()** - Renders user cards:
```javascript
function displayUsers(users) {
    // Creates card HTML for each user
    // Displays name, email, phone, website, location, company
    // Shows loading/no-data states
}
```

## Data Flow

```
┌─────────────────────┐
│   User opens app    │
│  (http://localhost) │
└──────────┬──────────┘
           │
           ▼
┌──────────────────────┐
│   / route serves     │
│   index.html         │
└──────────┬──────────┘
           │
           ▼
┌──────────────────────────┐
│  User clicks "Fetch"     │
│  button on home page     │
└──────────┬───────────────┘
           │
           ▼
┌──────────────────────────┐
│  axios.get() requests    │
│  JSONPlaceholder API     │
└──────────┬───────────────┘
           │
           ▼
┌──────────────────────────┐
│  API returns 10 users    │
│  (JSON array)            │
└──────────┬───────────────┘
           │
           ▼
┌──────────────────────────┐
│  Data stored in          │
│  sessionStorage          │
└──────────┬───────────────┘
           │
           ▼
┌──────────────────────────┐
│  Redirect to /result     │
└──────────┬───────────────┘
           │
           ▼
┌──────────────────────────┐
│  /result route serves    │
│  result.html             │
└──────────┬───────────────┘
           │
           ▼
┌──────────────────────────┐
│  result.html retrieves   │
│  data from sessionStorage │
└──────────┬───────────────┘
           │
           ▼
┌──────────────────────────┐
│  displayUsers() renders  │
│  user cards in grid      │
└──────────────────────────┘
```

## How It Works Step-by-Step

### Scenario: First-time user

1. User opens `http://localhost:3000` in browser
2. Server receives GET request to `/`
3. Server sends `index.html` file
4. Home page loads with dark theme
5. User sees "Fetch Random Users" button
6. User clicks the button
7. `fetchUsers()` function is called
8. Loading spinner appears
9. Axios makes HTTP GET request to JSONPlaceholder
10. JSONPlaceholder responds with 10 user objects
11. Response data is converted to JSON string
12. Stored in `sessionStorage` with key `'randomUsers'`
13. After 1 second, browser redirects to `/result`
14. Server receives GET request to `/result`
15. Server sends `result.html` file
16. Results page loads
17. `displayUsers()` function retrieves data from sessionStorage
18. Creates 10 user cards dynamically
19. Each card displays: name, username, email, phone, website, location, company
20. User can view all profiles or click back to home

## Storage Details

### sessionStorage

**Key:** `randomUsers`

**Value:** JSON string of user array

**Lifespan:** Until browser tab is closed

**Example:**
```javascript
// Storing
sessionStorage.setItem('randomUsers', JSON.stringify(users));

// Retrieving
const users = JSON.parse(sessionStorage.getItem('randomUsers'));
```

**Why sessionStorage?**
- Temporary storage (cleared when tab closes)
- Perfect for passing data between pages
- No server database needed
- Faster than making API calls again

## Styling

### Color Scheme

- **Background:** Black (#000000)
- **Primary Text:** White (#ffffff)
- **Secondary Text:** Light Gray (#cccccc)
- **Borders:** White (#ffffff)
- **Card Background:** Dark Gray (#1a1a1a)
- **Hover State:** Slightly lighter (#333333)

### Responsive Design

- Desktop: 3-column grid
- Tablet: 2-column grid
- Mobile: 1-column grid

## Error Handling

### On Frontend

**If fetch fails:**
```javascript
catch (error) {
    console.error('Error:', error);
    alert('Failed to fetch users. Please try again.');
    btn.disabled = false;
    loading.classList.remove('show');
}
```

**Common errors:**
- Network is offline
- API is down
- CORS issues (usually not a problem with JSONPlaceholder)

### On Backend

**If file not found:**
```javascript
res.sendFile() // Automatically sends 404 if file doesn't exist
```

**Ensure files exist at:**
- `public/index.html`
- `public/result.html`

## Browser Compatibility

✅ Supported:
- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)

✅ Features used:
- Fetch API / Axios
- sessionStorage
- ES6 JavaScript
- CSS Grid
- Font Awesome Icons

## Troubleshooting

### Server won't start

**Problem:** `Error: Cannot find module 'express'`

**Solution:** Run `npm install`

```bash
npm install
```

---

### Page shows blank

**Problem:** Server running but page is blank

**Solution:** Check console (F12) for errors. Verify:
- `index.html` exists in `public/` folder
- Server is running on port 3000
- No JavaScript errors in console

---

### Users not displaying

**Problem:** Results page is blank

**Solution:** 
- Check if sessionStorage has data (F12 → Application → sessionStorage)
- Verify API request completed successfully
- Check browser console for JavaScript errors

---

### API not responding

**Problem:** "Failed to fetch users" error

**Solution:**
- Check internet connection
- JSONPlaceholder API might be down (rare)
- Check CORS in browser console
- Try manually visiting: https://jsonplaceholder.typicode.com/users

---

### Port 3000 already in use

**Problem:** `Error: listen EADDRINUSE: address already in use :::3000`

**Solution:** Kill the process using port 3000

```bash
# On Windows
netstat -ano | findstr :3000
taskkill /PID <PID> /F

# On Mac/Linux
lsof -ti:3000 | xargs kill -9
```

Or change port in server.js:
```javascript
const PORT = 3001; // Change to different port
```

## Testing the App

### Test Case 1: Basic Flow
1. Start server: `node server.js`
2. Open `http://localhost:3000`
3. Click "Fetch Random Users"
4. Wait for loading
5. See user cards appear
6. Click "Back to Home"
7. Repeat process

### Test Case 2: Browser Storage
1. Open DevTools (F12)
2. Go to Application → sessionStorage
3. Click "Fetch Random Users"
4. Check sessionStorage for `randomUsers` key
5. Should contain JSON array of 10 users

### Test Case 3: Error Handling
1. Open DevTools (F12)
2. Go to Network tab
3. Turn on offline mode
4. Click "Fetch Random Users"
5. Should show error message
6. Button should be enabled again

## Performance Notes

- **First load:** ~500ms-1s (API call + redirect)
- **Subsequent loads:** Instant (data in sessionStorage)
- **Network request:** ~200-400ms (JSONPlaceholder)
- **Rendering:** <100ms (10 cards)

## Production Considerations

⚠️ **Before deploying to production:**

1. **Add error logging**
   ```javascript
   // Use services like Sentry or LogRocket
   ```

2. **Implement rate limiting**
   ```javascript
   // Prevent abuse of API calls
   ```

3. **Add environment variables**
   ```javascript
   const API_URL = process.env.API_URL || 'https://jsonplaceholder.typicode.com/users';
   ```

4. **Use a real database**
   ```javascript
   // Store user data instead of sessionStorage
   ```

5. **Add authentication**
   ```javascript
   // Protect routes with middleware
   ```

6. **Enable compression**
   ```javascript
   app.use(express.compression());
   ```

7. **Use HTTPS**
   ```javascript
   // Secure data transmission
   ```

## Future Enhancements

- Add pagination (show 5 users at a time)
- Search/filter functionality
- Sort by name, email, etc.
- Export users as CSV
- User profile detail page
- Favorite users feature
- Real backend database
- User authentication
- Comments/posts for each user (JSONPlaceholder has this too)

## API Alternatives

If you want to try different APIs:

**JSONPlaceholder Posts:**
```javascript
axios.get('https://jsonplaceholder.typicode.com/posts')
```

**JSONPlaceholder Comments:**
```javascript
axios.get('https://jsonplaceholder.typicode.com/comments')
```

**Other free APIs:**
- RandomUser.me: https://randomuser.me/api/?results=10
- GitHub Users: https://api.github.com/users
- Star Wars: https://swapi.dev/api/people/

## Useful Commands

```bash
# Install dependencies
npm install

# Start server
node server.js

# Start with auto-reload (if nodemon installed)
npm run dev

# Install nodemon
npm install --save-dev nodemon

# View installed packages
npm list

# Update packages
npm update
```

## File Checklist

Before running the app, ensure these files exist:

- ✅ `server.js` - Main server file
- ✅ `package.json` - Dependencies file
- ✅ `public/index.html` - Home page
- ✅ `public/result.html` - Results page
- ✅ `public/style/style.css` - Styling (if separate)
- ✅ `public/script/script.js` - Frontend logic (if separate)

## License

This is a free demo project for educational purposes.

## Support

For issues:
1. Check browser console (F12)
2. Check server terminal for errors
3. Verify all files are in correct locations
4. Clear sessionStorage and try again
5. Restart the server
6. Check internet connection

## Additional Resources

- [Express.js Documentation](https://expressjs.com)
- [Axios Documentation](https://axios-http.com)
- [JSONPlaceholder Documentation](https://jsonplaceholder.typicode.com)
- [Font Awesome Icons](https://fontawesome.com)
- [JavaScript sessionStorage](https://developer.mozilla.org/en-US/docs/Web/API/sessionStorage)
- [Node.js Path Module](https://nodejs.org/api/path.html)
