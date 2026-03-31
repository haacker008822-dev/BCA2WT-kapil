# Day 14 — HTML5 Basics & Semantic Elements

📖 **Type:** Theory Session
🕐 **Duration:** 2 Hours
📚 **Unit:** 3 — HTML5

---

## Learning Objectives

By the end of this session, students will be able to:
- Explain the advantages of HTML5 over HTML4
- Use semantic elements for page structure
- Differentiate between semantic and non-semantic elements
- Build a well-structured page using HTML5 semantic tags

---

## 1. What is HTML5?

HTML5 is the **fifth and current version** of HTML, finalized in 2014 as a "Living Standard" (continuously updated). It introduces new elements, APIs, and capabilities.

### HTML5 vs HTML4

| Feature | HTML4 | HTML5 |
|---------|-------|-------|
| Doctype | Complex: `<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN"...>` | Simple: `<!DOCTYPE html>` |
| Multimedia | Needs Flash/plugins | Native `<audio>` & `<video>` |
| Graphics | Not built-in | `<canvas>` & `<svg>` |
| Structure | `<div id="header">` | `<header>`, `<nav>`, `<main>` |
| Forms | Basic inputs | Date, email, range, color pickers |
| Storage | Cookies only | localStorage, sessionStorage |
| Offline | Not supported | Service Workers, App Cache |

---

## 2. Semantic Elements

### What is Semantic HTML?

> **Analogy:** Imagine reading a newspaper. You can tell the **headline**, **article**, **sidebar**, and **advertisement** apart just by looking — because they each have a distinct visual layout with clear meaning. **Semantic HTML** gives web page sections the same kind of built-in meaning.

**Semantic elements** clearly describe their meaning to both the browser and the developer.

| Non-Semantic (meaningless) | Semantic (meaningful) |
|---------------------------|----------------------|
| `<div id="header">` | `<header>` |
| `<div id="nav">` | `<nav>` |
| `<div class="article">` | `<article>` |
| `<div id="footer">` | `<footer>` |

### HTML5 Semantic Elements

```
┌─────────────────────────────────────────────┐
│  <header>                                   │
│    Logo, site title, search bar             │
├─────────────────────────────────────────────┤
│  <nav>                                      │
│    Home | About | Courses | Contact         │
├────────────────────────────┬────────────────┤
│  <main>                    │  <aside>       │
│  ┌──────────────────────┐  │  Sidebar       │
│  │ <article>            │  │  - Links       │
│  │   <h2>Title</h2>     │  │  - Ads         │
│  │   <p>Content...</p>  │  │  - Related     │
│  │   <section>          │  │                │
│  │     Sub-section      │  │                │
│  │   </section>         │  │                │
│  │ </article>           │  │                │
│  └──────────────────────┘  │                │
├────────────────────────────┴────────────────┤
│  <footer>                                   │
│    Copyright, contact, social links         │
└─────────────────────────────────────────────┘
```

### Tag Reference

| Tag | Purpose | Analogy |
|-----|---------|---------|
| `<header>` | Page or section header | Letterhead on stationery |
| `<nav>` | Navigation links | Table of contents |
| `<main>` | Primary page content (only one per page) | The main article |
| `<article>` | Self-contained content (blog post, news story) | A newspaper article |
| `<section>` | Thematic grouping of content | A chapter in a book |
| `<aside>` | Side content (ads, related links) | Sidebar in a newspaper |
| `<footer>` | Page or section footer | Fine print at the bottom |
| `<figure>` | Image/diagram with caption | Photo with caption |
| `<figcaption>` | Caption for `<figure>` | The caption text |
| `<details>` | Expandable/collapsible content | FAQ accordion |
| `<summary>` | Heading for `<details>` | FAQ question |
| `<mark>` | Highlighted text | Highlighter pen |
| `<time>` | Date/time markup | Calendar entry |

### `<section>` vs `<article>` — The Common Confusion

Students often mix up `<section>` and `<article>`. Here is a simple way to remember:

> **Think of it like a newspaper.** An `<article>` is a **complete news story** that makes sense on its own — you could cut it out and give it to a friend. A `<section>` is a **chapter or part** within a story — it only makes sense as part of something bigger.

| Question to Ask | If **Yes** → Use | If **No** → Use |
|----------------|-------------------|-----------------|
| Can this content stand alone (e.g., shared on WhatsApp, posted on another site)? | `<article>` | `<section>` |
| Does it have its own heading and makes complete sense independently? | `<article>` | `<section>` |
| Is it just grouping related paragraphs under one topic? | `<section>` | Maybe `<div>` |

**Real-world examples:**

| Content | Correct Tag | Why? |
|---------|------------|------|
| A blog post on "Top 10 places in Mandsaur" | `<article>` | Self-contained, shareable |
| The "History" section within that blog post | `<section>` | Part of the article, not independent |
| A product review on Flipkart | `<article>` | Independent, complete content |
| "Specifications" tab within that review | `<section>` | Grouped content within the review |
| A student's profile card on the university website | `<article>` | Each card is self-contained |
| The "Achievements" part within the profile | `<section>` | Part of the profile |

### Nesting Rules — What Can Go Inside What?

Semantic elements can be **nested** inside each other, but there are rules:

```
✅ VALID NESTING:

<article>                      ← A blog post
  <section>                    ← A chapter within the post
    <p>Content here...</p>
  </section>
  <section>                    ← Another chapter
    <p>More content...</p>
  </section>
</article>

<section>                      ← A "Latest News" section
  <article>                    ← Individual news story
    <h3>News Title</h3>
    <p>Story details...</p>
  </article>
  <article>                    ← Another news story
    <h3>Another Title</h3>
    <p>More details...</p>
  </article>
</section>

❌ INVALID / BAD PRACTICE:

<header>
  <header>                     ← ❌ Cannot nest header inside header
  </header>
</header>

<footer>
  <header>                     ← ❌ Avoid header inside footer
  </header>
</footer>
```

**Quick nesting reference:**

| Parent Element | Can Contain | Cannot Contain |
|---------------|-------------|---------------|
| `<article>` | `<section>`, `<header>`, `<footer>`, `<aside>`, other `<article>` | `<main>` |
| `<section>` | `<article>`, `<header>`, `<footer>`, `<aside>` | `<main>` |
| `<main>` | `<article>`, `<section>`, `<aside>` | Another `<main>` |
| `<header>` | `<nav>`, most flow content | `<header>`, `<footer>`, `<main>` |
| `<footer>` | `<nav>`, most flow content | `<header>`, `<footer>`, `<main>` |
| `<aside>` | `<article>`, `<section>`, `<header>`, `<footer>` | `<main>` |

> **Rule of Thumb:** There should be **only one `<main>`** per page, and `<main>` should not appear inside `<article>`, `<aside>`, `<header>`, or `<footer>`.

### SEO Benefits — How Semantic HTML Improves Search Rankings

> **Analogy:** Imagine Google's search bot as a **new student visiting Mandsaur University** for the first time. If the campus has clear signboards ("Library", "BCA Department", "Canteen"), the student finds everything quickly. If there are no signs — just numbered buildings — the student is lost. **Semantic HTML is like putting signboards on your website** for search engine bots.

**How search engines use semantic elements:**

| Semantic Element | What Google Understands |
|-----------------|------------------------|
| `<header>` | "This is the site's branding and top-level info" |
| `<nav>` | "These are the main navigation links — important pages" |
| `<main>` | "This is the primary content I should index and rank" |
| `<article>` | "This is a complete, independent piece of content" |
| `<h1>` inside `<article>` | "This is the main topic of this content" |
| `<aside>` | "This is supplementary — not the main content" |
| `<footer>` | "Contact info, copyright, less important links" |
| `<time datetime="...">` | "This is a specific date — useful for news, events" |

**Non-semantic vs Semantic — SEO comparison:**

```html
<!-- ❌ Non-semantic: Google sees a wall of <div> tags — no meaning -->
<div id="header">
  <div class="title">Raj's Sweet Shop - Mandsaur</div>
</div>
<div id="content">
  <div class="post">Best Mawa Bati in Mandsaur...</div>
</div>

<!-- ✅ Semantic: Google clearly understands the page structure -->
<header>
  <h1>Raj's Sweet Shop - Mandsaur</h1>
</header>
<main>
  <article>
    <h2>Best Mawa Bati in Mandsaur</h2>
    <p>Our shop has been serving authentic Mawa Bati since 1985...</p>
    <time datetime="2026-01-15">January 15, 2026</time>
  </article>
</main>
```

> **Key Point:** Google has confirmed that using semantic HTML helps its bots understand your content better, which can lead to **rich snippets** (enhanced search results with dates, ratings, etc.) and better rankings.

### Accessibility Benefits — How Screen Readers Use Semantic Elements

> **Analogy:** A visually impaired student using a **screen reader** (like JAWS or NVDA software) cannot see the webpage. The screen reader reads aloud the content. **Semantic elements act like a map** — they tell the screen reader "this is navigation," "this is the main content," "this is a sidebar," so the user can **jump directly** to the section they want.

**How screen readers use semantic elements:**

| Element | Screen Reader Behavior |
|---------|----------------------|
| `<nav>` | Announces "Navigation region" — user can skip to it or skip past it |
| `<main>` | Announces "Main content" — user can jump directly to main content |
| `<header>` | Announces "Banner" — user knows this is the page header |
| `<footer>` | Announces "Content info" — user knows this is the footer |
| `<article>` | Announces "Article" — user knows this is a self-contained piece |
| `<aside>` | Announces "Complementary" — user can skip sidebar content |
| `<h1>` to `<h6>` | User can navigate by headings — like a table of contents |

**Without semantic HTML**, a screen reader sees:
```
"div... div... div... div... link... div... text..."
— No structure, no way to navigate!
```

**With semantic HTML**, a screen reader sees:
```
"Navigation region: 4 links — Home, About, Courses, Contact"
"Main content: Article — About the Department"
"Complementary: Quick Links — 3 links"
"Content info: Copyright 2026 Mandsaur University"
```

> **Important:** In India, the **Rights of Persons with Disabilities Act, 2016** encourages accessible digital content. Using semantic HTML is a step toward making your websites accessible to all users.

---

## 3. Building a Page with Semantic HTML5

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BCA Department - Mandsaur University</title>
</head>
<body>

    <header>
        <h1>Mandsaur University</h1>
        <p>Department of Computer Applications (BCA)</p>
    </header>

    <nav>
        <a href="#about">About</a> |
        <a href="#courses">Courses</a> |
        <a href="#faculty">Faculty</a> |
        <a href="#contact">Contact</a>
    </nav>

    <main>
        <article>
            <h2 id="about">About the Department</h2>
            <p>The BCA department was established in <time datetime="2015">2015</time> 
               with a vision to produce skilled IT professionals.</p>
            
            <section>
                <h3>Our Vision</h3>
                <p>To be a center of excellence in computer education.</p>
            </section>
            
            <section>
                <h3>Our Mission</h3>
                <p>To provide quality education through theoretical and practical learning.</p>
            </section>
        </article>

        <article id="courses">
            <h2>Courses</h2>
            
            <details>
                <summary><strong>Semester I</strong></summary>
                <ul>
                    <li>Programming in C</li>
                    <li>Computer Fundamentals</li>
                    <li>Mathematics I</li>
                </ul>
            </details>

            <details open>
                <summary><strong>Semester II (Current)</strong></summary>
                <ul>
                    <li>Web Technology</li>
                    <li>Data Structures</li>
                    <li>Discrete Mathematics</li>
                </ul>
            </details>
        </article>

        <article id="faculty">
            <h2>Faculty</h2>
            <figure>
                <img src="https://via.placeholder.com/200x200?text=HOD" alt="HOD Photo" width="200">
                <figcaption><strong>Dr. Faculty Name</strong> — Head of Department</figcaption>
            </figure>
        </article>
    </main>

    <aside>
        <h3>Quick Links</h3>
        <ul>
            <li><a href="#">University Website</a></li>
            <li><a href="#">Online Results</a></li>
            <li><a href="#">Library Portal</a></li>
        </ul>
        
        <h3>Upcoming Events</h3>
        <p>Tech Fest: <time datetime="2026-04-20">April 20, 2026</time></p>
    </aside>

    <footer>
        <p>&copy; <time datetime="2026">2026</time> Mandsaur University. All Rights Reserved.</p>
        <address>
            Rewas Dewda Road, Mandsaur, MP 458001<br>
            Email: <a href="mailto:bca@mandsauruniversity.edu.in">bca@mandsauruniversity.edu.in</a>
        </address>
    </footer>

</body>
</html>
```

> **Code Explanation:**
> - `<!DOCTYPE html>` — Declares this as an HTML5 document (the simple HTML5 doctype).
> - `<meta charset="UTF-8">` — Sets character encoding to UTF-8, supporting Hindi and other Indian language characters.
> - `<meta name="viewport" ...>` — Makes the page responsive on mobile devices.
> - `<header>` — Contains the university name and department — acts as the page banner.
> - `<nav>` — Groups navigation links (About, Courses, Faculty, Contact) — screen readers identify this as the navigation region.
> - `<main>` — Wraps the primary page content. Only one `<main>` per page.
> - `<article>` — Each self-contained content block (About, Courses, Faculty) is an article. These could be extracted and still make sense on their own.
> - `<section>` — Inside the "About" article, "Our Vision" and "Our Mission" are sections — they are thematic groupings within the article.
> - `<time datetime="2015">` — Machine-readable date. Search engines and screen readers can understand this is a year.
> - `<details>` and `<summary>` — Creates collapsible content for semester lists. The `open` attribute on Semester II means it starts expanded.
> - `<figure>` and `<figcaption>` — Groups the HOD photo with its caption, semantically linking them.
> - `<aside>` — Contains sidebar content (Quick Links, Upcoming Events) that is related but not the main content.
> - `<footer>` — Contains copyright and contact information.
> - `<address>` — Semantic tag specifically for contact information (address, email).

---

## 4. The `<details>` and `<summary>` Tags

Creates collapsible/expandable content — no JavaScript needed!

```html
<details>
    <summary>What is HTML?</summary>
    <p>HTML stands for HyperText Markup Language. It is used to structure web content.</p>
</details>

<details>
    <summary>What is CSS?</summary>
    <p>CSS stands for Cascading Style Sheets. It is used to style HTML elements.</p>
</details>
```

> **Code Explanation:**
> - `<details>` — Creates a collapsible/expandable widget. By default, the content is hidden (collapsed).
> - `<summary>` — The visible heading that the user clicks to expand/collapse. Think of it as the "question" in an FAQ.
> - The `<p>` inside `<details>` is the hidden content that appears when the user clicks the summary.
> - No JavaScript is needed — this is built-in browser functionality!
> - **Tip:** Add the `open` attribute to `<details open>` if you want the content to start in the expanded state.

---

## Practice Exercise

Convert the department page from Day 6 (which used `<div>` tags) into a fully semantic HTML5 page:
1. Replace `<div>` sections with `<header>`, `<nav>`, `<main>`, `<article>`, `<section>`, `<aside>`, `<footer>`
2. Add `<figure>` and `<figcaption>` for images
3. Use `<time>` for dates
4. Create an FAQ section using `<details>` and `<summary>`
5. Add a sidebar (`<aside>`) with quick links

---

## Summary

| Element | Purpose |
|---------|---------|
| `<header>` | Page/section header |
| `<nav>` | Navigation |
| `<main>` | Primary content (only 1) |
| `<article>` | Self-contained content |
| `<section>` | Thematic grouping |
| `<aside>` | Sidebar/tangential content |
| `<footer>` | Footer |
| `<figure>` + `<figcaption>` | Image + caption |
| `<details>` + `<summary>` | Expandable content |
| `<time>` | Machine-readable date/time |

---

*Day 14 of 55 | Unit 3 — HTML5 | Web Technology (25BCA060)*
