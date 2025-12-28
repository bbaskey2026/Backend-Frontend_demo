# Random Users App - Beginner's Guide

A simple web app that shows random people from the internet!

## What This App Does

Click a button → Get random people → See their info on the screen

That's it! 🎉

## What You Need

1. **Node.js** - Download from https://nodejs.org/
2. A **code editor** - Like VS Code
3. A **web browser** - Chrome, Firefox, Safari, etc.

## How to Run (Super Easy!)

### Step 1: Open Terminal/Command Prompt
- Windows: Press `Windows + R`, type `cmd`, press Enter
- Mac: Press `Command + Space`, type `terminal`, press Enter

### Step 2: Go to Your Project Folder
```bash
cd path-to-your-project
```

### Step 3: Install Required Packages
Copy and paste this:
```bash
npm install
```

Wait for it to finish...

### Step 4: Start the Server
```bash
node server.js
```

You should see:
```
Server running on http://localhost:3000
```

### Step 5: Open Your Browser
Go to: `http://localhost:3000`

Done! You're running the app! 🚀

## What Happens When You Use the App

### Home Page (`/`)
1. You see a button that says "Fetch Random Users"
2. Click it
3. A loading spinner appears
4. Wait a moment...

### Getting Data
The app asks the internet for 10 random people using this API:
```
https://jsonplaceholder.typicode.com/users
```

(Don't worry about what an API is - just think of it as a service that gives you data)

### Results Page (`/result`)
After the app gets the data, you see:
- **Name** - Person's full name
- **Email** - Their email address
- **Phone** - Their phone number
- **Website** - Their website
- **Location** - City and zip code
- **Company** - Where they work

### Want to See More?
Click "Back to Home" and fetch more users!

## File Locations

Your project should look like this:

```
📁 Backend-Frontend_demo
  ├── 📁 node_modules (auto-created, don't touch)
  ├── 📁 public
  │   ├── 📄 index.html (home page)
  │   ├── 📄 result.html (results page)
  ├── 📄 server.js (the main file)
  ├── 📄 package.json (list of things to install)
  ├── 📄 package-lock.json (auto-created, don't touch)
  └── 📄 README.md (this file)
```

**Important files you need:**
- ✅ `server.js` - Main server file
- ✅ `package.json` - List of packages to install
- ✅ `public/index.html` - Home page
- ✅ `public/result.html` - Results page

**Auto-created (ignore these):**
- `node_modules/` - Created when you run `npm install`
- `package-lock.json` - Created automatically

## The Two Pages

### Page 1: Home (`localhost:3000/`)

Shows:
- Title: "Random Users"
- Description: "Discover random user profiles..."
- A big button: "Fetch Random Users"
- 3 feature boxes (Users, Design, Speed)

**What the button does:**
- Gets 10 random people from the internet
- Saves them temporarily
- Takes you to the results page

### Page 2: Results (`localhost:3000/result`)

Shows:
- Back button (to go home)
- Title: "Your Random Users"
- Cards with each person's info
- Click "Back to Home" to go fetch more

## Where Does the Data Come From?

We use something called **JSONPlaceholder** - it's a fake API that gives us fake people data for testing.

**The API Link:**
```
https://jsonplaceholder.typicode.com/users
```

This gives us 10 fake people like:
- Name: Leanne Graham
- Email: sincere@april.com
- Phone: 1-770-736-8031
- And more...

## How Data Moves Around

```
1. You click button
   ↓
2. App asks JSONPlaceholder API for data
   ↓
3. API sends back 10 people
   ↓
4. App saves the data (temporarily)
   ↓
5. You see the results page with all the people
```

## What is `sessionStorage`?

Think of it like a sticky note on your browser.

When we get the data from the API, we write it on this sticky note:
```javascript
sessionStorage.setItem('randomUsers', data);
```

Then on the results page, we read it:
```javascript
const data = sessionStorage.getItem('randomUsers');
```

**Important:** The sticky note disappears when you close the browser tab!

## Server Routes (The Two Pages)

### Route 1: Home Page
```
URL: http://localhost:3000/
Shows: index.html
Button: Fetches users
```

### Route 2: Results Page
```
URL: http://localhost:3000/result
Shows: result.html
Content: User cards
```

## What Each File Does

| File | Purpose |
|------|---------|
| `server.js` | Runs the server & handles routes |
| `index.html` | Home page (button to fetch) |
| `result.html` | Results page (shows people) |

## Dark Theme Explained

The app uses a dark design:
- **Black background** - Easy on the eyes
- **White text** - Easy to read
- **White borders** - Makes cards stand out
- **Icons** - From Font Awesome library

## Common Problems & Fixes

### Problem: "Cannot find module 'express'"
**Fix:** Run this:
```bash
npm install
```

### Problem: "Port 3000 already in use"
**Fix:** Another app is using port 3000. Try a different port or close the other app.

### Problem: Blank page
**Fix:** 
- Make sure you ran `node server.js`
- Make sure you went to `http://localhost:3000`
- Press Ctrl+F5 to refresh (hard refresh)

### Problem: "Failed to fetch users"
**Fix:**
- Check if your internet is working
- The API might be down (rare)
- Check browser console for errors (Press F12)

### Problem: Users not showing on results page
**Fix:**
- Make sure you clicked the button on home page
- Wait for loading to finish
- Check browser console (F12) for errors

## How to Stop the Server

Press `Ctrl + C` in your terminal

You'll see something like:
```
^C
```

That means it stopped. To start again, run `node server.js` again.

## Useful Keyboard Shortcuts

| Shortcut | What It Does |
|----------|------------|
| F12 | Open Developer Tools |
| Ctrl + R | Refresh page |
| Ctrl + Shift + R | Hard refresh (clear cache) |
| Ctrl + C | Stop server (in terminal) |

## What is an API?

**Simple explanation:** An API is like a restaurant menu.
- You ask for something (like a pizza)
- The kitchen gives you what you asked for
- You don't need to know how they made it

Our API is JSONPlaceholder - we ask for users, it gives us users!

## What is Axios?

It's a tool that helps us ask the API for data. Like using a phone to call someone instead of visiting in person.

```javascript
// Ask for users
const response = await axios.get('https://jsonplaceholder.typicode.com/users');
// Get the answer
const users = response.data;
```

## What is Express?

It's a tool that helps us run a server on your computer so people can visit `http://localhost:3000`

## Next Steps (After It Works)

1. **Understand the code** - Read through `script.js` and understand what each line does
2. **Change the style** - Edit `style.css` to use different colors
3. **Try a different API** - Use a different data source
4. **Add more pages** - Create new HTML pages and routes
5. **Store data differently** - Try localStorage instead of sessionStorage

## Getting Help

1. **Google the error** - Copy the error message and search it
2. **Check the console** - Press F12, click Console, read error messages
3. **Restart everything** - Stop server, close terminal, start again
4. **Ask a friend** - Show them the error message

## Quick Checklist

Before asking for help, check:
- ✅ Did you run `npm install`?
- ✅ Did you run `node server.js`?
- ✅ Did you go to `http://localhost:3000`?
- ✅ Is the server still running in terminal?
- ✅ Did you wait for loading to finish?
- ✅ Do you have internet connection?

## You Did It!

If you can see the home page and click the button to see user cards, **you successfully built and ran a web app!** 🎉

Congratulations! This is how real websites work!

## Want to Learn More?

- JavaScript tutorials on YouTube
- Express.js documentation online
- JSONPlaceholder API examples
- CSS tutorials for styling

Have fun! 🚀
