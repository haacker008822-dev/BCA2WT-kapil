# Day 15 — HTML5 Forms & New Input Types

🔬 **Type:** Theory + Practical
🕐 **Duration:** 2 Hours
📚 **Unit:** 3 — HTML5
🧪 **Lab Experiments:** 12, 13

---

## Learning Objectives

By the end of this session, students will be able to:
- Create HTML forms with various input types
- Use HTML5-specific input types (date, email, range, color, etc.)
- Add form elements like radio buttons, checkboxes, dropdowns
- Apply basic HTML5 form validation attributes

---

## 1. HTML Forms Basics

> **Analogy:** An HTML form is like a **paper application form** at a bank. It has fields for name, address, date of birth, checkboxes for services, and a submit button. The form collects information and sends it somewhere for processing.

### Basic Form Structure

```html
<!-- action: URL where form data is sent when submitted -->
<!-- method: How the data is sent (GET or POST) -->
<form action="/submit" method="POST">
    <!-- for="name" links this label to the input with id="name" -->
    <label for="name">Name:</label>
    <!-- type="text" creates a single-line text input -->
    <input type="text" id="name" name="name">
    
    <!-- type="submit" sends the form data to the server -->
    <button type="submit">Submit</button>
</form>
```

> **Code Explanation:**
> - `<form>` — The container that groups all form elements together. Without it, inputs won't be submitted.
> - `action="/submit"` — The URL (server address) where form data will be sent. Think of it as the postal address on an envelope.
> - `method="POST"` — Sends data hidden in the request body (not visible in the URL). Safer for sensitive data.
> - `<label for="name">` — The `for` attribute links this label to the input with `id="name"`. Clicking the label focuses the input.
> - `<input type="text" id="name" name="name">` — A text input field. The `name` attribute is the **key** used when data is sent (like a column name in a form).
> - `<button type="submit">` — Triggers form submission when clicked.

| Attribute | Purpose |
|-----------|---------|
| `action` | URL where form data is sent |
| `method` | `GET` (in URL) or `POST` (in body) |

### POST vs GET — When to Use Which?

> **Analogy:** Sending data via **GET** is like writing a message on a **postcard** — everyone can read it. Sending via **POST** is like putting the message inside a sealed **envelope** — it's hidden from casual view.

| Feature | GET | POST |
|---------|-----|------|
| **Data location** | Appended to URL: `?name=Rahul&age=20` | Hidden in request body |
| **Visible in URL bar** | ✅ Yes | ❌ No |
| **Bookmarkable** | ✅ Yes (URL contains data) | ❌ No |
| **URL length limit** | ~2,048 characters (browser limit) | No practical limit |
| **Security** | ❌ Less secure (visible in URL, browser history, server logs) | ✅ More secure (not in URL) |
| **Cached by browser** | ✅ Yes | ❌ No |
| **Best for** | Search forms, filters, navigation | Login forms, registration, file uploads |

**When to use GET:**
- Search forms (e.g., Google search — `?q=mandsaur+university`)
- Filtering products (e.g., `?category=electronics&price=under-500`)
- Any form where you want the result to be bookmarkable

**When to use POST:**
- Login and registration forms (passwords should never appear in URL!)
- File uploads
- Any form that modifies data on the server (create account, place order)
- Forms with large amounts of data

> ⚠️ **Important:** POST is **not encrypted** by itself — it just hides data from the URL. For true security, always use **HTTPS** (which encrypts the entire request).

### What Happens When a Form is Submitted?

1. User fills in the form and clicks "Submit"
2. Browser collects all input values using their `name` attributes
3. Data is formatted as **key=value** pairs (e.g., `fullname=Rahul+Sharma&age=20`)
4. If `method="GET"`: Data is appended to the URL after a `?` symbol
5. If `method="POST"`: Data is placed in the request body (hidden)
6. Browser sends the request to the URL specified in `action`
7. Server processes the data and sends back a response

**What does `action="#"` mean?**

In our lab examples, you'll see `action="#"` — this means "submit the form to the current page." Since we don't have a server running, this prevents errors. The `#` is a placeholder. In a real application, you would use a server URL like `action="https://api.example.com/register"`.

### The Importance of `<label>` — Accessibility & Usability

The `<label>` tag is not just decorative text — it serves two critical purposes:

**1. Clickable area:** When `<label for="email">` is linked to `<input id="email">`, clicking the label text focuses the input. This is especially helpful on mobile phones where input fields are small.

**2. Screen reader support:** Screen readers announce the label when the input is focused — "Email, text field" — so visually impaired users know what to type.

```html
<!-- ✅ CORRECT: Label linked to input using for/id -->
<label for="email">Email Address:</label>
<input type="email" id="email" name="email">

<!-- ❌ WRONG: No link between label and input -->
<label>Email Address:</label>
<input type="email" name="email">

<!-- ✅ ALSO CORRECT: Wrapping input inside label (no for/id needed) -->
<label>
    Email Address:
    <input type="email" name="email">
</label>
```

> **Code Explanation:**
> - `for="email"` on the label must match `id="email"` on the input — this creates the link.
> - The `name` attribute is separate — it's used for form data submission, not for label linking.
> - Wrapping the input inside `<label>` also works and doesn't require `for`/`id` matching.

---

## 2. Input Types

### Classic Input Types

```html
<input type="text" placeholder="Enter name">         <!-- Single-line text -->
<input type="password" placeholder="Enter password">  <!-- Hidden characters -->
<input type="email" placeholder="email@example.com">  <!-- Email validation -->
<input type="number" min="1" max="150">               <!-- Numbers only -->
<input type="tel" placeholder="Phone number">         <!-- Phone number -->
<input type="url" placeholder="https://...">          <!-- URL validation -->
```

> **Code Explanation:**
> - `type="text"` — A basic single-line text field. The `placeholder` shows hint text that disappears when the user starts typing.
> - `type="password"` — Same as text, but characters are hidden (shown as dots ●●●).
> - `type="email"` — Browser automatically validates that the input contains an `@` symbol and a domain.
> - `type="number"` — Only allows numeric input. `min` and `max` set the allowed range.
> - `type="tel"` — For telephone numbers. Does **not** validate format (phone formats vary by country).
> - `type="url"` — Validates that the input starts with `http://` or `https://`.

### Mobile Keyboard Types — How Input Types Change the Keyboard

On mobile phones, **different input types trigger different keyboards**. This makes form filling much easier:

| Input Type | Mobile Keyboard Shows | Example |
|-----------|----------------------|---------|
| `type="text"` | Standard QWERTY keyboard | Full keyboard |
| `type="email"` | Keyboard with `@` and `.com` buttons | Easy to type `rahul@gmail.com` |
| `type="tel"` | Numeric keypad (phone dialer style) | Easy to type `+91 98765 43210` |
| `type="url"` | Keyboard with `/`, `.com`, and `:` buttons | Easy to type `https://mu.ac.in` |
| `type="number"` | Numeric keypad | Easy to type `12345` |
| `type="search"` | Keyboard with "Search" button instead of "Enter" | Quick search submission |

> **Try it:** Open any form on your mobile phone and notice how the keyboard changes when you tap on email vs phone number fields. This is why choosing the correct `type` matters — it improves user experience (UX) on mobile devices.

### HTML5 New Input Types

```html
<input type="date">          <!-- Date picker -->
<input type="time">          <!-- Time picker -->
<input type="datetime-local"> <!-- Date + Time -->
<input type="month">         <!-- Month picker -->
<input type="week">          <!-- Week picker -->
<input type="color">         <!-- Color picker -->
<input type="range" min="0" max="100"> <!-- Slider -->
<input type="search">        <!-- Search box -->
<input type="file">          <!-- File upload -->
<input type="hidden">        <!-- Hidden field -->
```

> **Code Explanation:**
> - `type="date"` — Shows a date picker calendar. The value is stored in `YYYY-MM-DD` format (e.g., `2026-03-15`).
> - `type="time"` — Shows a time picker with hours and minutes.
> - `type="datetime-local"` — Combines date and time in one picker.
> - `type="month"` — Lets user pick a month and year (e.g., "March 2026").
> - `type="week"` — Lets user pick a specific week of the year.
> - `type="color"` — Opens a color picker dialog. The value is a hex code like `#FF5733`.
> - `type="range"` — Shows a slider between `min` and `max` values.
> - `type="search"` — Similar to text, but may show a clear (✕) button in some browsers.
> - `type="file"` — Opens a file browser dialog to upload files.
> - `type="hidden"` — Invisible to the user but sends data with the form (used for tracking IDs, tokens, etc.).

### Multi-line Text

```html
<textarea rows="5" cols="40" placeholder="Enter your message..."></textarea>
```

> **Code Explanation:**
> - `<textarea>` — Unlike `<input>`, this creates a **multi-line** text box (like a paragraph input).
> - `rows="5"` — Sets the visible height to 5 text lines.
> - `cols="40"` — Sets the visible width to 40 characters.
> - `placeholder` — Hint text shown when the textarea is empty.
> - Users can type long text like addresses, feedback, or descriptions here.

---

## 3. Form Elements

### Radio Buttons (Choose ONE)

```html
<p>Gender:</p>
<input type="radio" id="male" name="gender" value="male">
<label for="male">Male</label>

<input type="radio" id="female" name="gender" value="female">
<label for="female">Female</label>

<input type="radio" id="other" name="gender" value="other">
<label for="other">Other</label>
```

> **Code Explanation:**
> - `type="radio"` — Creates a radio button. Radio buttons let the user choose **only one** option from a group.
> - `name="gender"` — All three radio buttons share the same `name`. This groups them together — selecting one automatically deselects the others.
> - `id="male"` and `for="male"` — Links each label to its radio button. Clicking "Male" text selects the radio button.
> - `value="male"` — The value sent to the server when this option is selected. The form data would be `gender=male`.

> **Key:** All radio buttons in a group must share the same `name` attribute.

### Checkboxes (Choose MULTIPLE)

```html
<p>Hobbies:</p>
<input type="checkbox" id="reading" name="hobbies" value="reading">
<label for="reading">Reading</label>

<input type="checkbox" id="coding" name="hobbies" value="coding">
<label for="coding">Coding</label>

<input type="checkbox" id="gaming" name="hobbies" value="gaming">
<label for="gaming">Gaming</label>
```

> **Code Explanation:**
> - `type="checkbox"` — Creates a checkbox. Unlike radio buttons, **multiple** checkboxes can be selected at once.
> - `name="hobbies"` — All checkboxes share the same `name`. When the form is submitted, all selected values are sent (e.g., `hobbies=reading&hobbies=coding`).
> - `id` and `for` link each label to its checkbox — clicking the text toggles the checkbox.
> - `value="reading"` — The value sent when this checkbox is checked.

### Dropdown (`<select>`)

```html
<label for="subject">Favorite Subject:</label>
<select id="subject" name="subject">
    <option value="" disabled selected>-- Choose --</option>
    <option value="web">Web Technology</option>
    <option value="ds">Data Structures</option>
    <option value="math">Mathematics</option>
</select>
```

> **Code Explanation:**
> - `<select>` — Creates a dropdown menu. The user clicks it to see options and picks one.
> - `<option value="">` — Each option in the dropdown. The `value` is what gets sent to the server.
> - `disabled selected` on the first option — Makes "-- Choose --" the default display but prevents it from being submitted (forces the user to pick a real option).
> - `for="subject"` on the label links to `id="subject"` on the select element.

### Datalist (Searchable Dropdown)

```html
<label for="city">City:</label>
<input list="cities" id="city" name="city">
<datalist id="cities">
    <option value="Mandsaur">
    <option value="Indore">
    <option value="Bhopal">
    <option value="Mumbai">
</datalist>
```

> **Code Explanation:**
> - `<datalist id="cities">` — Defines a list of suggestions. Unlike `<select>`, the user can also type a custom value.
> - `<input list="cities">` — The `list` attribute connects the input to the datalist with matching `id`. This is what makes the suggestions appear.
> - `<option value="Mandsaur">` — Each suggestion. As the user types "Man", the browser filters and shows "Mandsaur".
> - **Key difference from `<select>`:** Datalist allows free typing + suggestions. Select only allows choosing from fixed options.

---

## 4. HTML5 Validation Attributes

```html
<input type="text" required>                    <!-- Must fill -->
<input type="text" minlength="3" maxlength="50"> <!-- Length limits -->
<input type="number" min="1" max="150">          <!-- Number range -->
<input type="text" pattern="[A-Za-z]+" title="Letters only"> <!-- Regex -->
<input type="email" required>                    <!-- Must be valid email -->
```

> **Code Explanation:**
> - `required` — The form cannot be submitted if this field is empty. The browser shows an error message automatically.
> - `minlength="3" maxlength="50"` — The text must be between 3 and 50 characters long.
> - `min="1" max="150"` — For number inputs, the value must be within this range.
> - `pattern="[A-Za-z]+"` — A regular expression (regex) that the input must match. `[A-Za-z]+` means "only letters, at least one." The `title` attribute shows a custom error hint.
> - `type="email" required` — Combines type validation (must be a valid email format) with required validation (cannot be empty).

| Attribute | Purpose |
|-----------|---------|
| `required` | Field must be filled |
| `minlength` / `maxlength` | Text length constraints |
| `min` / `max` | Number range constraints |
| `pattern` | Regex pattern to match |
| `placeholder` | Hint text in empty field |
| `autofocus` | Auto-focus on page load |
| `readonly` | Can see but not edit |
| `disabled` | Grayed out, can't interact |

---

## Practical Session

### 🧪 Lab Experiment 12: User Information Form

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>User Information Form</title>
</head>
<body style="font-family: Arial; max-width: 600px; margin: 30px auto;">

    <h1>Student Registration Form</h1>
    <hr>

    <form action="#" method="POST">
        
        <p>
            <label for="fullname"><strong>Full Name:</strong></label><br>
            <input type="text" id="fullname" name="fullname" 
                   placeholder="Enter your full name" required 
                   style="width: 100%; padding: 8px; margin-top: 5px;">
        </p>

        <p>
            <label for="age"><strong>Age:</strong></label><br>
            <input type="number" id="age" name="age" 
                   min="16" max="60" placeholder="e.g., 20" required
                   style="width: 100%; padding: 8px; margin-top: 5px;">
        </p>

        <p>
            <label for="address"><strong>Address:</strong></label><br>
            <textarea id="address" name="address" rows="3" 
                      placeholder="Enter your address" required
                      style="width: 100%; padding: 8px; margin-top: 5px;"></textarea>
        </p>

        <p>
            <label for="subject"><strong>Favorite Subject:</strong></label><br>
            <select id="subject" name="subject" required
                    style="width: 100%; padding: 8px; margin-top: 5px;">
                <option value="" disabled selected>-- Select Subject --</option>
                <option value="Web Technology">Web Technology</option>
                <option value="Data Structures">Data Structures</option>
                <option value="Mathematics">Mathematics</option>
                <option value="English">English</option>
            </select>
        </p>

        <p>
            <label for="movie"><strong>Favorite Movie:</strong></label><br>
            <input type="text" id="movie" name="movie" 
                   placeholder="e.g., 3 Idiots"
                   style="width: 100%; padding: 8px; margin-top: 5px;">
        </p>

        <p>
            <label for="singer"><strong>Favorite Singer:</strong></label><br>
            <input type="text" id="singer" name="singer" 
                   placeholder="e.g., Arijit Singh"
                   style="width: 100%; padding: 8px; margin-top: 5px;">
        </p>

        <p>
            <button type="submit" 
                    style="padding: 10px 30px; background: #1565C0; color: white; border: none; cursor: pointer;">
                Submit
            </button>
            <button type="reset" style="padding: 10px 30px;">Reset</button>
        </p>

    </form>

</body>
</html>
```

> **Code Explanation:**
> - `<form action="#" method="POST">` — The form submits to the same page (`#` is a placeholder since we don't have a server). Data is sent via POST (hidden from URL).
> - `<label for="fullname">` linked to `<input id="fullname">` — Clicking "Full Name:" focuses the input field.
> - `placeholder="Enter your full name"` — Hint text that disappears when the user starts typing.
> - `required` — Browser prevents submission if this field is empty.
> - `type="number" min="16" max="60"` — Only accepts numbers between 16 and 60 (valid age range for students/staff).
> - `<textarea rows="3">` — Multi-line input for the address.
> - `<select>` with `disabled selected` on the first option — Forces the user to choose a subject; the placeholder option cannot be submitted.
> - `type="submit"` — The submit button sends all form data. `type="reset"` clears all fields back to their default values.
> - Inline `style` attributes — Used for quick styling (in real projects, use external CSS).

---

### 🧪 Lab Experiment 13: Advanced Form Elements

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Advanced Form</title>
</head>
<body style="font-family: Arial; max-width: 600px; margin: 30px auto;">

    <h1>Complete Registration Form</h1>
    <hr>

    <form action="#" method="POST">

        <!-- Text fields from Lab 12 -->
        <fieldset>
            <legend><strong>Personal Information</strong></legend>
            
            <p>
                <label for="name">Name:</label><br>
                <input type="text" id="name" name="name" required 
                       style="width:100%; padding:8px;">
            </p>
            <p>
                <label for="email">Email:</label><br>
                <input type="email" id="email" name="email" required 
                       placeholder="you@example.com" style="width:100%; padding:8px;">
            </p>
            <p>
                <label for="pwd">Password:</label><br>
                <input type="password" id="pwd" name="password" 
                       minlength="8" required style="width:100%; padding:8px;">
            </p>
            <p>
                <label for="dob">Date of Birth:</label><br>
                <input type="date" id="dob" name="dob" style="padding:8px;">
            </p>
        </fieldset>

        <br>

        <!-- Radio Buttons -->
        <fieldset>
            <legend><strong>Gender</strong></legend>
            <input type="radio" id="male" name="gender" value="male" required>
            <label for="male">Male</label> &nbsp;
            <input type="radio" id="female" name="gender" value="female">
            <label for="female">Female</label> &nbsp;
            <input type="radio" id="other" name="gender" value="other">
            <label for="other">Other</label>
        </fieldset>

        <br>

        <!-- Checkboxes -->
        <fieldset>
            <legend><strong>Interests</strong></legend>
            <input type="checkbox" id="web" name="interests" value="web">
            <label for="web">Web Development</label><br>
            <input type="checkbox" id="app" name="interests" value="app">
            <label for="app">App Development</label><br>
            <input type="checkbox" id="ai" name="interests" value="ai">
            <label for="ai">Artificial Intelligence</label><br>
            <input type="checkbox" id="game" name="interests" value="game">
            <label for="game">Game Development</label>
        </fieldset>

        <br>

        <!-- HTML5 Special Inputs -->
        <fieldset>
            <legend><strong>Preferences</strong></legend>
            <p>
                <label for="fcolor">Favorite Color:</label>
                <input type="color" id="fcolor" name="fcolor" value="#1565C0">
            </p>
            <p>
                <label for="skill">Skill Level (1-10):</label>
                <input type="range" id="skill" name="skill" min="1" max="10" value="5">
            </p>
            <p>
                <label for="website">Personal Website:</label><br>
                <input type="url" id="website" name="website" 
                       placeholder="https://yoursite.com" style="width:100%; padding:8px;">
            </p>
        </fieldset>

        <br>
        <p>
            <button type="submit" style="padding:12px 40px; background:#4CAF50; color:white; border:none; cursor:pointer; font-size:16px;">
                ✅ Submit
            </button>
            <button type="reset" style="padding:12px 40px; font-size:16px;">🔄 Reset</button>
        </p>
    </form>

</body>
</html>
```

> **Code Explanation:**
> - `<fieldset>` — Groups related form fields with a visible border. Like sections in a paper form.
> - `<legend>` — The title for each fieldset group (e.g., "Personal Information", "Gender").
> - `type="email" required placeholder="you@example.com"` — Email input with validation, required attribute, and placeholder hint.
> - `type="password" minlength="8"` — Password field that requires at least 8 characters for security.
> - `type="date"` — Shows a calendar date picker (no need to type the date manually).
> - Radio buttons (`type="radio"`) — All share `name="gender"`, so only one can be selected. The `required` on the first one makes the entire group required.
> - Checkboxes (`type="checkbox"`) — Share `name="interests"` but multiple can be selected simultaneously.
> - `type="color" value="#1565C0"` — Opens a color picker with a default blue color.
> - `type="range" min="1" max="10" value="5"` — A slider starting at 5, ranging from 1 to 10.
> - `type="url"` — Validates that the input is a proper URL (must include `https://`).
> - `type="submit"` sends the form; `type="reset"` clears all fields to their initial values.

---

## Summary

| Element | Purpose |
|---------|---------|
| `<form>` | Container for form elements |
| `<input type="...">` | Various input types |
| `<textarea>` | Multi-line text input |
| `<select>` + `<option>` | Dropdown menu |
| `<datalist>` | Searchable suggestions |
| `<fieldset>` + `<legend>` | Group related form fields |
| `<label>` | Accessible label for inputs |
| `required`, `pattern`, `min/max` | HTML5 validation |

---

*Day 15 of 55 | Unit 3 — HTML5 | Web Technology (25BCA060)*
