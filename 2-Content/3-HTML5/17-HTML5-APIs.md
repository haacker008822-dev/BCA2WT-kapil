# Day 17 — HTML5 APIs: Geolocation, Storage & Drag-and-Drop

📖 **Type:** Theory Session
🕐 **Duration:** 2 Hours
📚 **Unit:** 3 — HTML5

---

## Learning Objectives

By the end of this session, students will be able to:
- Use the Geolocation API to get user location
- Store and retrieve data using localStorage and sessionStorage
- Implement basic Drag and Drop functionality
- Understand the difference between cookies and Web Storage

---

## 1. Geolocation API

> **Analogy:** When you open Google Maps on your phone and it shows your location, that's the Geolocation API at work. It asks the device "Where am I?" and the browser asks the user for permission before sharing.

### Getting User Location

```html
<button onclick="getLocation()">📍 Get My Location</button>
<p id="location"></p>

<script>
function getLocation() {
    if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(showPosition, showError);
    } else {
        document.getElementById('location').textContent = 
            "Geolocation is not supported by this browser.";
    }
}

function showPosition(position) {
    const lat = position.coords.latitude;
    const lon = position.coords.longitude;
    document.getElementById('location').innerHTML = 
        `Latitude: ${lat}<br>Longitude: ${lon}<br>
         <a href="https://www.google.com/maps?q=${lat},${lon}" target="_blank">
             View on Google Maps
         </a>`;
}

function showError(error) {
    const messages = {
        1: "User denied the request for Geolocation.",
        2: "Location information is unavailable.",
        3: "The request to get location timed out."
    };
    document.getElementById('location').textContent = 
        messages[error.code] || "An unknown error occurred.";
}
</script>
```

> **Code Explanation:**
> - `navigator.geolocation` — Checks if the browser supports the Geolocation API. Most modern browsers do.
> - `getCurrentPosition(successCallback, errorCallback)` — Asks the browser for the user's location. Takes two functions: one for success, one for error.
> - `position.coords.latitude` and `position.coords.longitude` — The actual location coordinates (decimal degrees, e.g., 24.0667 for Mandsaur).
> - The Google Maps link is constructed dynamically using template literals — `${lat},${lon}` inserts the coordinates into the URL.
> - `error.code` — Returns 1 (permission denied), 2 (unavailable), or 3 (timeout). The `messages` object maps these to user-friendly messages.

### HTTPS Requirement for Geolocation

> ⚠️ **Important:** Modern browsers **require HTTPS** (secure connection) for the Geolocation API to work. If your website uses `http://` instead of `https://`, the browser will block location access.

| Scenario | Geolocation Works? |
|----------|-------------------|
| `https://yoursite.com` | ✅ Yes |
| `http://yoursite.com` | ❌ No (blocked by browser) |
| `file:///C:/mypage.html` (local file) | ✅ Yes (for testing) |
| `http://localhost` (local development) | ✅ Yes (exception for localhost) |

> **For lab practice:** Opening HTML files directly from your computer (`file:///...`) will work. But when you deploy a website online, it **must** use HTTPS.

### Position Object Properties

| Property | Description |
|----------|-------------|
| `coords.latitude` | Latitude (decimal degrees) |
| `coords.longitude` | Longitude (decimal degrees) |
| `coords.accuracy` | Accuracy in meters |
| `coords.altitude` | Altitude (if available) |
| `coords.speed` | Speed (if moving) |
| `timestamp` | When the position was determined |

---

## 2. Web Storage API

> **Analogy:** Think of **cookies** as sticky notes on a envelope — small, visible to everyone handling the envelope, and sent back and forth with every request. **Web Storage** is like a **desk drawer** — larger, private, and stays in the browser without being sent with requests.

### localStorage vs sessionStorage vs Cookies

| Feature | localStorage | sessionStorage | Cookies |
|---------|-------------|---------------|---------|
| **Capacity** | ~5-10 MB | ~5-10 MB | ~4 KB |
| **Lifetime** | Until manually deleted | Until tab closes | Configurable expiry |
| **Sent to server** | No | No | Yes (every request) |
| **Scope** | Same origin | Same tab + origin | Same origin |

### localStorage Example

```html
<h2>My Notes App</h2>
<textarea id="notepad" rows="5" cols="50" placeholder="Type your notes..."></textarea>
<br>
<button onclick="saveNote()">💾 Save</button>
<button onclick="loadNote()">📂 Load</button>
<button onclick="clearNote()">🗑️ Clear</button>

<script>
function saveNote() {
    const note = document.getElementById('notepad').value;
    localStorage.setItem('myNote', note);
    alert('Note saved!');
}

function loadNote() {
    const note = localStorage.getItem('myNote');
    if (note) {
        document.getElementById('notepad').value = note;
    } else {
        alert('No saved note found.');
    }
}

function clearNote() {
    localStorage.removeItem('myNote');
    document.getElementById('notepad').value = '';
    alert('Note cleared!');
}
</script>
```

> **Code Explanation:**
> - `document.getElementById('notepad').value` — Gets the text typed in the textarea.
> - `localStorage.setItem('myNote', note)` — Stores the note with key `'myNote'`. Think of it like putting a labeled file in a drawer.
> - `localStorage.getItem('myNote')` — Retrieves the note using the same key. Returns `null` if the key doesn't exist.
> - `localStorage.removeItem('myNote')` — Deletes only the `'myNote'` item from storage.
> - `alert('Note saved!')` — Shows a browser popup to confirm the action.
> - **Key point:** Close the browser, reopen it, and click "Load" — your note is still there! localStorage persists until manually deleted.

### Web Storage Methods

| Method | Purpose |
|--------|---------|
| `setItem(key, value)` | Store a key-value pair |
| `getItem(key)` | Retrieve value by key |
| `removeItem(key)` | Remove a specific item |
| `clear()` | Remove ALL stored items |
| `key(index)` | Get key name by index |
| `length` | Number of stored items |

### Storing Objects with JSON.stringify and JSON.parse

localStorage can only store **strings**. If you try to store an object or array directly, it gets converted to `"[object Object]"` — which is useless. You must **convert objects to JSON strings** before storing them.

```html
<script>
// Creating a student object
var student = {
    name: "Priya Sharma",
    rollNo: "BCA2024-042",
    city: "Mandsaur",
    subjects: ["Web Technology", "Data Structures", "Mathematics"]
};

// ❌ WRONG: Storing object directly — saves as "[object Object]"
// localStorage.setItem('student', student);

// ✅ CORRECT: Convert object to JSON string first
localStorage.setItem('student', JSON.stringify(student));

// Retrieving: Parse the JSON string back to an object
var savedStudent = JSON.parse(localStorage.getItem('student'));

// Now you can access properties normally
document.write("Name: " + savedStudent.name + "<br>");       // Priya Sharma
document.write("City: " + savedStudent.city + "<br>");        // Mandsaur
document.write("Subjects: " + savedStudent.subjects.join(", ")); // Web Technology, Data Structures, Mathematics
</script>
```

> **Code Explanation:**
> - `JSON.stringify(student)` — Converts the JavaScript object to a JSON string: `'{"name":"Priya Sharma","rollNo":"BCA2024-042",...}'`
> - `localStorage.setItem('student', ...)` — Stores the JSON string with key `'student'`.
> - `JSON.parse(localStorage.getItem('student'))` — Reads the JSON string from storage and converts it back into a JavaScript object.
> - After parsing, you can access `savedStudent.name`, `savedStudent.city`, etc., just like a normal object.
> - **Tip:** Always wrap `JSON.parse()` in a `try-catch` block in production code to handle corrupted data.

### Storage Quota — How Much Can You Store?

| Storage Type | Typical Limit | Notes |
|-------------|--------------|-------|
| localStorage | **5 MB** per origin | Some browsers allow up to 10 MB |
| sessionStorage | **5 MB** per origin | Same limit as localStorage |
| Cookies | **4 KB** per cookie | Much smaller! |

> **What is "origin"?** An origin is the combination of protocol + domain + port. For example, `https://mu.ac.in` is one origin. All pages on `https://mu.ac.in` share the same 5 MB localStorage.

**What happens if you exceed the limit?**
The browser throws a `QuotaExceededError`. You should handle this:

```javascript
try {
    localStorage.setItem('bigData', veryLargeString);
} catch (e) {
    if (e.name === 'QuotaExceededError') {
        alert('Storage is full! Please clear some saved data.');
    }
}
```

### Security Implications — What NOT to Store

> ⚠️ **NEVER store sensitive data in localStorage!**

localStorage is vulnerable to **XSS (Cross-Site Scripting)** attacks. If an attacker injects malicious JavaScript into your page, they can read everything in localStorage.

| Data Type | Safe to Store in localStorage? | Why? |
|-----------|-------------------------------|------|
| User preferences (theme, language) | ✅ Yes | Not sensitive |
| Shopping cart items | ✅ Yes | Not sensitive |
| Passwords | ❌ **NEVER** | XSS can steal them |
| Authentication tokens (JWT) | ❌ **NEVER** | XSS can steal them for account takeover |
| Aadhaar number / PAN card | ❌ **NEVER** | Sensitive personal data |
| Credit/debit card details | ❌ **NEVER** | Financial data — extremely dangerous |

> **Rule of Thumb:** Only store data in localStorage that you would be comfortable writing on a sticky note and leaving on your desk. If it's sensitive, use **secure HTTP-only cookies** or **server-side sessions** instead.

### Storage Event — Cross-Tab Communication

When one browser tab changes localStorage, **other tabs of the same website** can detect the change using the `storage` event. This is useful for syncing data across tabs.

```html
<script>
// This runs in Tab 2 when Tab 1 changes localStorage
window.addEventListener('storage', function(event) {
    document.write("Key changed: " + event.key + "<br>");
    document.write("Old value: " + event.oldValue + "<br>");
    document.write("New value: " + event.newValue + "<br>");
    document.write("Changed by page: " + event.url + "<br>");
});
</script>
```

> **Code Explanation:**
> - `window.addEventListener('storage', ...)` — Listens for changes to localStorage made by **other tabs** (not the current tab).
> - `event.key` — The key that was changed (e.g., `'myNote'`).
> - `event.oldValue` — The previous value before the change.
> - `event.newValue` — The new value after the change.
> - `event.url` — The URL of the page that made the change.
> - **Use case:** If a student has your website open in two tabs and saves a note in Tab 1, Tab 2 can automatically update to show the new note.

### sessionStorage Example

```html
<script>
// Count page views in current session
let views = sessionStorage.getItem('pageViews') || 0;
views = parseInt(views) + 1;
sessionStorage.setItem('pageViews', views);

document.write(`<p>Page views this session: <strong>${views}</strong></p>`);
document.write(`<p><em>Close the tab and reopen — count resets!</em></p>`);
</script>
```

> **Code Explanation:**
> - `sessionStorage.getItem('pageViews') || 0` — Gets the current page view count. If it doesn't exist (first visit), defaults to `0`.
> - `parseInt(views) + 1` — Converts the string to a number and adds 1. Remember, localStorage/sessionStorage stores **strings only**.
> - `sessionStorage.setItem('pageViews', views)` — Saves the updated count.
> - `document.write(...)` — Displays the count on the page. Template literals (backticks) allow embedding variables with `${views}`.
> - **Key difference from localStorage:** This count resets when the tab is closed. Try it: refresh the page (count increases), then close and reopen the tab (count resets to 1).

---

## 3. Drag and Drop API

> **Analogy:** Drag and drop on a webpage works just like **moving files on your desktop** — click, hold, drag to a new location, and release.

### Basic Drag and Drop

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Drag and Drop Demo</title>
    <style>
        .drop-zone {
            width: 300px;
            height: 200px;
            border: 3px dashed #aaa;
            margin: 20px;
            padding: 20px;
            text-align: center;
            display: inline-block;
            vertical-align: top;
        }
        .drop-zone.over {
            border-color: #4CAF50;
            background: #E8F5E9;
        }
        .drag-item {
            width: 100px;
            padding: 15px;
            margin: 10px;
            background: #1565C0;
            color: white;
            cursor: grab;
            display: inline-block;
            text-align: center;
        }
    </style>
</head>
<body style="font-family: Arial;">

    <h1>Drag and Drop Demo</h1>

    <div class="drag-item" draggable="true" ondragstart="drag(event)" id="item1">HTML</div>
    <div class="drag-item" draggable="true" ondragstart="drag(event)" id="item2">CSS</div>
    <div class="drag-item" draggable="true" ondragstart="drag(event)" id="item3">JS</div>

    <br>

    <div class="drop-zone" ondrop="drop(event)" ondragover="allowDrop(event)"
         ondragenter="this.classList.add('over')" ondragleave="this.classList.remove('over')">
        <p><strong>Drop Zone 1</strong></p>
        <p>Drop items here</p>
    </div>

    <div class="drop-zone" ondrop="drop(event)" ondragover="allowDrop(event)"
         ondragenter="this.classList.add('over')" ondragleave="this.classList.remove('over')">
        <p><strong>Drop Zone 2</strong></p>
        <p>Drop items here</p>
    </div>

    <script>
    function allowDrop(event) {
        event.preventDefault();
    }

    function drag(event) {
        event.dataTransfer.setData("text", event.target.id);
    }

    function drop(event) {
        event.preventDefault();
        event.target.classList.remove('over');
        const data = event.dataTransfer.getData("text");
        const element = document.getElementById(data);
        if (element) {
            event.currentTarget.appendChild(element);
        }
    }
    </script>

</body>
</html>
```

> **Code Explanation:**
> - `draggable="true"` — Makes an element draggable. By default, only images and links are draggable.
> - `ondragstart="drag(event)"` — When dragging starts, the `drag()` function stores the dragged element's ID using `event.dataTransfer.setData("text", event.target.id)`.
> - `ondragover="allowDrop(event)"` — By default, elements **cannot** receive drops. `event.preventDefault()` in `allowDrop()` overrides this and allows dropping.
> - `ondragenter` / `ondragleave` — Used to add/remove the `.over` CSS class, which changes the border color to green when an item hovers over the drop zone.
> - `ondrop="drop(event)"` — When the item is dropped: `event.dataTransfer.getData("text")` retrieves the stored element ID. `document.getElementById(data)` finds the element. `event.currentTarget.appendChild(element)` moves the element into the drop zone.
> - **CSS:** `.drag-item` uses `cursor: grab` to show a grab cursor. `.drop-zone` uses `dashed` border to indicate where items can be dropped. `.over` class provides visual feedback during drag.

### Drag and Drop Events

| Event | Fires When |
|-------|-----------|
| `dragstart` | User starts dragging |
| `drag` | During dragging |
| `dragend` | Dragging ends |
| `dragenter` | Dragged item enters drop zone |
| `dragover` | Dragged item is over drop zone |
| `dragleave` | Dragged item leaves drop zone |
| `drop` | Item is dropped |

---

## Practice Exercise

Build a **"Favorite Colors" app** that:
1. Uses Geolocation to show the user's city (approximate)
2. Has a color picker (`<input type="color">`)
3. Saves favorite colors to localStorage
4. Displays saved colors as colored boxes
5. Has a "Clear All" button

---

## Summary

| API | Purpose | Key Methods/Events |
|-----|---------|-------------------|
| **Geolocation** | Get user's location | `getCurrentPosition()` |
| **localStorage** | Persistent browser storage | `setItem()`, `getItem()`, `removeItem()` |
| **sessionStorage** | Tab-scoped storage | Same methods, clears on tab close |
| **Drag and Drop** | Interactive move elements | `dragstart`, `dragover`, `drop` |

---

*Day 17 of 55 | Unit 3 — HTML5 | Web Technology (25BCA060)*
