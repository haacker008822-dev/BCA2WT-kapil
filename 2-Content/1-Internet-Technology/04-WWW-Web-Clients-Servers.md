# Day 4 — World Wide Web, Web Clients & Web Servers

📖 **Type:** Theory Session
🕐 **Duration:** 2 Hours
📚 **Unit:** 1 — Internet Technology

---

## Learning Objectives

By the end of this session, students will be able to:
- Differentiate between the Internet and the World Wide Web
- Explain the client-server architecture of the web
- Describe how web browsers and web servers work
- Understand URLs and how web resources are located

---

## 1. Internet ≠ World Wide Web

> **Common Misconception:** Most people use "internet" and "web" interchangeably. They are NOT the same thing.

| Feature | Internet | World Wide Web (WWW) |
|---------|----------|---------------------|
| **What** | Global network of connected computers | A service that runs ON the internet |
| **When** | 1969 (ARPANET) | 1989 (Tim Berners-Lee) |
| **Analogy** | The road system | The trucks and shops using the roads |
| **Includes** | Email, FTP, VoIP, IoT, WWW | Websites, web apps, hyperlinks |
| **Protocol** | TCP/IP | HTTP/HTTPS |

> **Analogy:** The internet is the **highway system** — the physical infrastructure of roads, bridges, and traffic signals. The WWW is just one type of **vehicle** (websites) that travels on those highways. Other vehicles include email (SMTP), file transfers (FTP), and video calls (VoIP).

---

## 2. The World Wide Web (WWW)

### What is the WWW?

The **World Wide Web** is a system of interlinked **hypertext documents** and resources, accessed via the internet using **web browsers**. It was invented by **Tim Berners-Lee** at CERN in **1989**.

### Three Pillars of the WWW

| Pillar | What It Is | Purpose |
|--------|-----------|---------|
| **HTML** | HyperText Markup Language | Structure of web pages |
| **HTTP** | HyperText Transfer Protocol | Rules for transferring web pages |
| **URL** | Uniform Resource Locator | Address of web resources |

### How the Web Works — Simplified

```
┌──────────────┐         HTTP Request          ┌──────────────┐
│              │ ──────────────────────────────▶│              │
│  Web Client  │    "GET /index.html"           │  Web Server  │
│  (Browser)   │                                │  (Apache/    │
│              │ ◀──────────────────────────────│   Nginx)     │
│              │         HTTP Response           │              │
└──────────────┘    HTML + CSS + Images          └──────────────┘
```

---

## 3. Web Clients (Browsers)

### What is a Web Client?

A **web client** is any software that requests and displays web content. The most common web clients are **web browsers**.

### How a Browser Works

```
User types URL
      │
      ▼
┌─────────────────┐
│  1. URL Parser   │ → Breaks down the URL
├─────────────────┤
│  2. DNS Resolver │ → Converts domain to IP
├─────────────────┤
│  3. HTTP Client  │ → Sends request to server
├─────────────────┤
│  4. HTML Parser  │ → Reads the HTML structure
├─────────────────┤
│  5. CSS Engine   │ → Applies styling
├─────────────────┤
│  6. JS Engine    │ → Runs JavaScript code
├─────────────────┤
│  7. Rendering    │ → Paints pixels on screen
│     Engine       │
└─────────────────┘
      │
      ▼
  Webpage displayed!
```

### Popular Web Browsers

| Browser | Engine | Developer | Market Share (approx.) |
|---------|--------|-----------|----------------------|
| Google Chrome | Blink/V8 | Google | ~65% |
| Safari | WebKit | Apple | ~18% |
| Firefox | Gecko | Mozilla | ~3% |
| Edge | Blink/V8 | Microsoft | ~5% |
| Opera | Blink/V8 | Opera Software | ~2% |

### Browser Developer Tools

Every modern browser includes **Developer Tools** (press `F12`) that let you:
- Inspect HTML elements
- View and edit CSS styles
- Debug JavaScript
- Monitor network requests
- Check performance

> 💡 **Pro Tip:** We'll use browser Developer Tools extensively throughout this course for debugging our web pages.

---

## 4. Web Servers

### What is a Web Server?

> **Analogy:** A web server is like a **librarian**. When you ask for a book (request a URL), the librarian (server) finds the book in the library (file system) and hands it to you (sends the response). If the book doesn't exist, the librarian tells you "Not Found" (404 error).

A **web server** is a computer that:
1. Stores web files (HTML, CSS, images, etc.)
2. Runs server software to handle HTTP requests
3. Sends responses back to clients

### How a Web Server Processes Requests

```
Client Request                        Server Processing
─────────────                        ─────────────────
GET /about.html          ┌──────────────────────────────┐
        ──────────────▶  │ 1. Receive the request        │
                         │ 2. Parse the URL path          │
                         │ 3. Find the file (/about.html) │
                         │ 4. Read the file contents       │
                         │ 5. Prepare HTTP response        │
        ◀──────────────  │ 6. Send response + file         │
HTTP 200 OK              └──────────────────────────────┘
+ about.html content
```

### Popular Web Servers

| Server | Developer | Used By |
|--------|-----------|---------|
| **Apache HTTP Server** | Apache Foundation | ~30% of websites |
| **Nginx** | Nginx Inc. | ~34% of websites |
| **IIS** | Microsoft | Windows-based servers |
| **LiteSpeed** | LiteSpeed Technologies | High-performance sites |
| **Node.js** | OpenJS Foundation | JavaScript-based servers |

### Static vs Dynamic Web Servers

| Feature | Static Server | Dynamic Server |
|---------|---------------|----------------|
| **Content** | Pre-built HTML files | Generated on-the-fly |
| **Speed** | Faster (just serve files) | Slower (processing needed) |
| **Example** | Personal portfolio | Amazon product page |
| **Changes** | Need to edit HTML files | Content changes with user/data |

---

## 5. URLs (Uniform Resource Locators)

### Anatomy of a URL

```
https://www.mandsauruniversity.edu.in:443/departments/bca?year=2026#syllabus
└─┬──┘  └─┬─────────────────────────┘└┬┘ └──────┬──────┘ └───┬───┘ └──┬───┘
Scheme          Host (Domain)        Port    Path         Query    Fragment
```

| Component | Example | Purpose |
|-----------|---------|---------|
| **Scheme** | `https://` | Protocol to use |
| **Host** | `www.mandsauruniversity.edu.in` | Which server to contact |
| **Port** | `:443` | Which "door" on the server (443 = HTTPS default) |
| **Path** | `/departments/bca` | Which resource on the server |
| **Query String** | `?year=2026` | Additional parameters |
| **Fragment** | `#syllabus` | Jump to a section on the page |

### Common URL Schemes

| Scheme | Purpose | Default Port |
|--------|---------|-------------|
| `http://` | Regular web traffic | 80 |
| `https://` | Secure web traffic | 443 |
| `ftp://` | File transfer | 21 |
| `mailto:` | Email link | — |
| `file://` | Local file | — |

---

## 6. Client-Server Architecture

### The Request-Response Cycle

```
    CLIENT                              SERVER
  ┌────────┐                         ┌────────┐
  │        │ ─── 1. Request ────────▶│        │
  │Browser │                         │Web     │
  │        │ ◀── 2. Response ────────│Server  │
  │        │                         │        │
  └────────┘                         └────────┘
  
  Request:  "Please give me the homepage"
  Response: "Here's the HTML + CSS + images"
```

### What Happens When You Visit a Website

1. **You type** `www.google.com` and press Enter
2. **DNS lookup** — domain name → IP address
3. **TCP connection** — 3-way handshake with the server
4. **HTTP request** — browser sends `GET / HTTP/1.1`
5. **Server processing** — server finds and prepares the page
6. **HTTP response** — server sends back HTML, CSS, JS, images
7. **Browser rendering** — browser builds and displays the page
8. **Connection close** — (or kept alive for more requests)

---

## Summary

| Concept | Key Takeaway |
|---------|-------------|
| WWW | A service running on the internet (not the internet itself) |
| Web Client | Software (browser) that requests and displays web content |
| Web Server | Computer that stores and serves web files |
| URL | Complete address of a web resource |
| Client-Server | Browser sends requests, server sends responses |
| Static vs Dynamic | Static = pre-built files; Dynamic = generated per request |

---

## Self-Assessment Questions

1. Explain the difference between the Internet and the World Wide Web.
2. What are the three pillars of the WWW?
3. Describe the role of a web browser in displaying a webpage.
4. Break down this URL into its components: `https://shop.example.com:8080/products?category=books#fiction`
5. What is the difference between a static and dynamic web server?
6. List any four popular web browsers and their rendering engines.

---

## Reading for Next Session

Tomorrow we cover **HTTP, HTTPS, Proxy Servers, and Firewalls** — the protocols and security mechanisms that protect web communication.

---

*Day 4 of 55 | Unit 1 — Internet Technology | Web Technology (25BCA060)*
