# Day 16 — Multimedia: Audio, Video, Canvas & SVG

🔬 **Type:** Theory + Practical
🕐 **Duration:** 2 Hours
📚 **Unit:** 3 — HTML5
🧪 **Lab Experiment:** 9 (extended with HTML5 features)

---

## Learning Objectives

By the end of this session, students will be able to:
- Embed audio and video using HTML5 tags (review + advanced features)
- Draw graphics using the `<canvas>` element with JavaScript
- Create scalable vector graphics using `<svg>`
- Understand when to use Canvas vs SVG

---

## 1. HTML5 Audio & Video (Recap + Advanced)

### Advanced Video Features

```html
<video id="myVideo" width="640" height="360" controls preload="metadata"
       poster="https://via.placeholder.com/640x360?text=Click+Play">
    <source src="lecture.mp4" type="video/mp4">
    <source src="lecture.webm" type="video/webm">
    <track src="subtitles_en.vtt" kind="subtitles" srclang="en" label="English">
    Your browser does not support HTML5 video.
</video>
```

> **Code Explanation:**
> - `<video>` — Embeds a video player in the page. The `id="myVideo"` lets JavaScript control it.
> - `width="640" height="360"` — Sets the video display size in pixels.
> - `controls` — Shows play/pause, volume, progress bar, and fullscreen buttons.
> - `preload="metadata"` — Loads only video metadata (duration, dimensions) — not the full video. Saves bandwidth.
> - `poster="..."` — The thumbnail image shown before the video plays. Like a movie poster.
> - `<source src="lecture.mp4" type="video/mp4">` — The primary video file. The `type` helps the browser choose the right format.
> - `<source src="lecture.webm" type="video/webm">` — Fallback format. If the browser can't play MP4, it tries WebM.
> - `<track>` — Adds subtitles/captions from a `.vtt` file (explained below).
> - The text "Your browser does not support HTML5 video." — Fallback message for very old browsers.

### The `<track>` Element (Subtitles)

```html
<track src="captions.vtt" kind="subtitles" srclang="en" label="English" default>
```

> **Code Explanation:**
> - `src="captions.vtt"` — Path to the subtitle file in **WebVTT** format.
> - `kind="subtitles"` — Type of text track (subtitles, captions, descriptions, or chapters).
> - `srclang="en"` — Language of the subtitles.
> - `label="English"` — The name shown to users in the subtitle menu.
> - `default` — This track is active by default when the video loads.

| Attribute | Purpose |
|-----------|---------|
| `kind` | `subtitles`, `captions`, `descriptions`, `chapters` |
| `srclang` | Language of the track |
| `label` | User-visible label |
| `default` | Use this track by default |

### WebVTT Subtitle Format Basics

The `.vtt` (Web Video Text Tracks) file is a simple text file that contains timed subtitles. Here is the basic format:

```
WEBVTT

00:00:01.000 --> 00:00:04.000
Namaste! Welcome to the Web Technology course.

00:00:05.000 --> 00:00:08.000
Today we will learn about HTML5 multimedia.

00:00:09.000 --> 00:00:13.000
Let's start with the <b>audio</b> and <b>video</b> elements.
```

> **Code Explanation:**
> - `WEBVTT` — The first line must be exactly this text. It identifies the file format.
> - `00:00:01.000 --> 00:00:04.000` — Time range in `HH:MM:SS.mmm` format. This subtitle shows from 1 second to 4 seconds.
> - The text below the time range is the actual subtitle displayed on screen.
> - You can use basic HTML tags like `<b>` (bold) and `<i>` (italic) inside subtitles.
> - Each subtitle block is separated by a blank line.

**How to create a VTT file:**
1. Open Notepad
2. Type the content in the format shown above
3. Save as `subtitles.vtt` (choose "All Files" in the Save dialog, not ".txt")

---

## 2. The `<canvas>` Element

> **Analogy:** `<canvas>` is a **blank whiteboard** in your classroom. By itself, it's empty. You need **JavaScript** (the marker) to draw shapes, text, and images on it.

### Understanding the Canvas Coordinate System

Before drawing on canvas, you must understand how coordinates work:

```
(0,0) ────────────────────────── X-axis (increases →)
  │
  │    ★ Point (50, 30) means:
  │       50 pixels from left edge
  │       30 pixels from top edge
  │
  │    ┌─────────────┐
  │    │ fillRect     │  fillRect(100, 80, 150, 60) means:
  │    │ (100,80,     │    Start at x=100, y=80
  │    │  150, 60)    │    Width = 150px, Height = 60px
  │    └─────────────┘
  │
  Y-axis (increases ↓)
```

> **Key Points:**
> - **(0, 0) is the TOP-LEFT corner** — not the bottom-left like in mathematics!
> - **X increases to the RIGHT** (just like math)
> - **Y increases DOWNWARD** (opposite of math — this confuses many students!)
> - All measurements are in **pixels**
> - Think of it like reading a page — you start from the top-left and go right and down.

### Basic Canvas Setup

```html
<canvas id="myCanvas" width="400" height="300" style="border: 1px solid #000;">
    Your browser does not support canvas.
</canvas>

<script>
    const canvas = document.getElementById('myCanvas');
    const ctx = canvas.getContext('2d');
    
    // Draw a rectangle
    ctx.fillStyle = '#1565C0';
    ctx.fillRect(50, 50, 150, 100);
    
    // Draw a circle
    ctx.beginPath();
    ctx.arc(300, 100, 50, 0, Math.PI * 2);
    ctx.fillStyle = '#E91E63';
    ctx.fill();
    
    // Draw text
    ctx.font = '20px Arial';
    ctx.fillStyle = '#333';
    ctx.fillText('Hello Canvas!', 100, 250);
    
    // Draw a line
    ctx.beginPath();
    ctx.moveTo(50, 200);
    ctx.lineTo(350, 200);
    ctx.strokeStyle = '#4CAF50';
    ctx.lineWidth = 3;
    ctx.stroke();
</script>
```

> **Code Explanation:**
> - `document.getElementById('myCanvas')` — Gets the canvas element from the HTML.
> - `canvas.getContext('2d')` — Gets the 2D drawing context (the "pen" object). All drawing methods are called on this `ctx` object.
> - **Rectangle:** `ctx.fillStyle = '#1565C0'` sets the fill color (blue). `ctx.fillRect(50, 50, 150, 100)` draws a filled rectangle starting at position (50, 50), 150px wide and 100px tall.
> - **Circle:** `ctx.beginPath()` starts a new drawing path (like lifting the pen). `ctx.arc(300, 100, 50, 0, Math.PI * 2)` draws a full circle at center (300, 100) with radius 50. `0` to `Math.PI * 2` means 0° to 360° (full circle). `ctx.fill()` fills the circle with the current `fillStyle`.
> - **Text:** `ctx.font = '20px Arial'` sets the font. `ctx.fillText('Hello Canvas!', 100, 250)` draws text at position (100, 250).
> - **Line:** `ctx.moveTo(50, 200)` moves the pen to the starting point without drawing. `ctx.lineTo(350, 200)` draws a line to the endpoint. `ctx.strokeStyle` sets line color, `ctx.lineWidth` sets thickness, and `ctx.stroke()` actually draws the line.

### Canvas Drawing Methods

| Method | Purpose |
|--------|---------|
| `fillRect(x, y, w, h)` | Filled rectangle |
| `strokeRect(x, y, w, h)` | Rectangle outline |
| `clearRect(x, y, w, h)` | Clear an area |
| `beginPath()` | Start a new path |
| `moveTo(x, y)` | Move pen without drawing |
| `lineTo(x, y)` | Draw line to point |
| `arc(x, y, r, start, end)` | Draw arc/circle |
| `fill()` | Fill the path |
| `stroke()` | Draw the outline |
| `fillText(text, x, y)` | Draw filled text |
| `drawImage(img, x, y)` | Draw an image |

> **Detailed Method Explanations:**
> - `beginPath()` — **Always call this before drawing a new shape.** It resets the current path. Without it, new shapes would connect to old ones.
> - `arc(x, y, r, startAngle, endAngle)` — Draws a curve. For a **full circle**, use `0` to `Math.PI * 2` (0° to 360°). For a **semicircle**, use `0` to `Math.PI` (0° to 180°). Angles are in **radians**, not degrees.
> - `moveTo(x, y)` — Like lifting your pen and placing it somewhere else. No line is drawn.
> - `lineTo(x, y)` — Draws a line from the current position to (x, y). Must call `stroke()` afterward to make the line visible.
> - `fill()` — Fills the current path with the color set by `fillStyle`.
> - `stroke()` — Draws the outline of the current path using `strokeStyle` and `lineWidth`.
> - `clearRect(x, y, w, h)` — Erases a rectangular area. Useful for animations (clear → redraw).

### Indian Flag Example

```html
<canvas id="flag" width="300" height="200" style="border: 1px solid #ccc;"></canvas>
<script>
    const c = document.getElementById('flag');
    const ctx = c.getContext('2d');
    
    // Saffron stripe
    ctx.fillStyle = '#FF9933';
    ctx.fillRect(0, 0, 300, 67);
    
    // White stripe (default background)
    ctx.fillStyle = '#FFFFFF';
    ctx.fillRect(0, 67, 300, 67);
    
    // Green stripe
    ctx.fillStyle = '#138808';
    ctx.fillRect(0, 134, 300, 67);
    
    // Ashoka Chakra (simplified circle)
    ctx.beginPath();
    ctx.arc(150, 100, 25, 0, Math.PI * 2);
    ctx.strokeStyle = '#000080';
    ctx.lineWidth = 2;
    ctx.stroke();
</script>
```

> **Code Explanation:**
> - The Indian flag is 300×200 pixels, divided into 3 equal horizontal stripes of ~67px each.
> - **Saffron stripe:** `ctx.fillStyle = '#FF9933'` sets the official saffron color. `ctx.fillRect(0, 0, 300, 67)` fills from top-left corner, full width, 67px tall.
> - **White stripe:** `ctx.fillRect(0, 67, 300, 67)` starts at y=67 (below saffron), same width and height.
> - **Green stripe:** `ctx.fillRect(0, 134, 300, 67)` starts at y=134 (below white). `#138808` is the official India green.
> - **Ashoka Chakra (simplified):** `ctx.arc(150, 100, 25, 0, Math.PI * 2)` draws a circle at the center of the flag (150, 100) with radius 25. `#000080` (navy blue) matches the Chakra color. `ctx.stroke()` draws only the outline (not filled).
> - **Note:** The actual Ashoka Chakra has 24 spokes — drawing those requires more advanced trigonometry with `Math.sin()` and `Math.cos()`.

---

## 3. SVG (Scalable Vector Graphics)

> **Analogy:** If Canvas is a **painting** (raster — fixed pixels), SVG is like **paper cutting art** (vector — mathematical shapes). SVG looks sharp at ANY size — zoom in 1000% and it's still crisp.

### Basic SVG

```html
<svg width="400" height="200" style="border: 1px solid #ccc;">
    <!-- Rectangle -->
    <rect x="10" y="10" width="150" height="80" 
          fill="#1565C0" stroke="#0D47A1" stroke-width="2" rx="10"/>
    
    <!-- Circle -->
    <circle cx="300" cy="60" r="50" fill="#E91E63" opacity="0.8"/>
    
    <!-- Line -->
    <line x1="10" y1="150" x2="390" y2="150" 
          stroke="#4CAF50" stroke-width="2"/>
    
    <!-- Text -->
    <text x="100" y="190" font-size="18" fill="#333">Hello SVG!</text>
    
    <!-- Ellipse -->
    <ellipse cx="200" cy="100" rx="60" ry="30" 
             fill="none" stroke="#FF9800" stroke-width="2"/>
</svg>
```

> **Code Explanation:**
> - `<svg width="400" height="200">` — Creates an SVG drawing area of 400×200 pixels. SVG uses the same coordinate system as canvas (0,0 at top-left).
> - `<rect x="10" y="10" width="150" height="80" fill="#1565C0" rx="10"/>` — A rectangle at position (10,10), 150×80px, blue filled, with `rx="10"` for rounded corners (10px radius).
> - `<circle cx="300" cy="60" r="50" fill="#E91E63" opacity="0.8"/>` — A circle with center at (300,60), radius 50, pink fill, 80% opacity (slightly transparent).
> - `<line x1="10" y1="150" x2="390" y2="150" stroke="#4CAF50" stroke-width="2"/>` — A line from point (10,150) to (390,150). `stroke` is the line color.
> - `<text x="100" y="190" font-size="18" fill="#333">` — Text positioned at (100,190). In SVG, `fill` colors the text (not `color` like in CSS).
> - `<ellipse cx="200" cy="100" rx="60" ry="30">` — An ellipse (oval) centered at (200,100) with horizontal radius 60 and vertical radius 30. `fill="none"` means only the outline is drawn.

### SVG Shapes Reference

| Shape | Tag | Key Attributes |
|-------|-----|----------------|
| Rectangle | `<rect>` | x, y, width, height, rx (rounded) |
| Circle | `<circle>` | cx, cy, r |
| Ellipse | `<ellipse>` | cx, cy, rx, ry |
| Line | `<line>` | x1, y1, x2, y2 |
| Polygon | `<polygon>` | points |
| Polyline | `<polyline>` | points |
| Path | `<path>` | d (path data) |
| Text | `<text>` | x, y, font-size |

---

## 4. Canvas vs SVG

| Feature | Canvas | SVG |
|---------|--------|-----|
| **Type** | Raster (pixels) | Vector (math) |
| **Drawn with** | JavaScript | HTML/XML tags |
| **Scaling** | Loses quality when zoomed | Always crisp |
| **Performance** | Better for many objects (games) | Better for few complex shapes |
| **Interactivity** | Must handle manually | Each shape is a DOM element |
| **Best for** | Games, image editing, charts | Icons, logos, diagrams, maps |
| **File size** | Depends on resolution | Depends on complexity |

### When to Use Canvas vs SVG — Detailed Comparison

**Use Canvas when:**
- Building **games** (e.g., a simple Snake or Brick Breaker game) — Canvas handles rapid pixel updates efficiently
- Creating **image editors** or **photo filters** — Canvas can manipulate individual pixels
- Drawing **data charts with thousands of data points** — Canvas performs better with many elements
- Creating **animations with many moving objects** (e.g., particle effects, rain simulation)

**Use SVG when:**
- Displaying **logos and icons** — SVG stays sharp on all screen sizes (Retina displays, 4K monitors)
- Creating **interactive diagrams** — Each SVG shape is a DOM element that can have click events, hover effects
- Building **maps** — SVG elements can be individually styled and made interactive
- Designing **infographics** — Complex shapes with text that need to scale for print and web

**Real-world Indian examples:**

| Use Case | Best Choice | Why? |
|----------|------------|------|
| IRCTC seat availability chart (many data points) | Canvas | Many elements, rapid updates |
| Swiggy restaurant logo on the app | SVG | Must look sharp on all phones |
| Paytm transaction graph | Canvas | Many data points, smooth animation |
| Indian Railway route map (interactive) | SVG | Clickable stations, zoom-friendly |
| Aadhaar QR code generator | Canvas | Pixel-level manipulation needed |
| Government website navigation icons | SVG | Scalable, accessible, small file size |

---

## Practical Session

### Interactive Canvas Drawing

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Canvas & SVG Gallery</title>
</head>
<body style="font-family: Arial; max-width: 800px; margin: 20px auto;">

    <h1>HTML5 Graphics Gallery</h1>

    <!-- Canvas Section -->
    <h2>Canvas Drawing</h2>
    <canvas id="demo" width="500" height="200" style="border:2px solid #333; display:block;"></canvas>
    <script>
        const c = document.getElementById('demo');
        const ctx = c.getContext('2d');
        
        // Gradient background
        const gradient = ctx.createLinearGradient(0, 0, 500, 0);
        gradient.addColorStop(0, '#667eea');
        gradient.addColorStop(1, '#764ba2');
        ctx.fillStyle = gradient;
        ctx.fillRect(0, 0, 500, 200);
        
        // White text
        ctx.font = 'bold 28px Arial';
        ctx.fillStyle = 'white';
        ctx.textAlign = 'center';
        ctx.fillText('Welcome to HTML5 Canvas!', 250, 80);
        
        ctx.font = '16px Arial';
        ctx.fillText('Mandsaur University - BCA Dept.', 250, 120);
        
        // Decorative circles
        ctx.beginPath();
        ctx.arc(50, 170, 20, 0, Math.PI * 2);
        ctx.fillStyle = 'rgba(255,255,255,0.3)';
        ctx.fill();
        
        ctx.beginPath();
        ctx.arc(450, 170, 20, 0, Math.PI * 2);
        ctx.fill();
    </script>

    <br>

    <!-- SVG Section -->
    <h2>SVG Drawing</h2>
    <svg width="500" height="200" style="border:2px solid #333; display:block;">
        <!-- Define a gradient that goes from teal to green -->
        <defs>
            <linearGradient id="grad1" x1="0%" y1="0%" x2="100%" y2="0%">
                <stop offset="0%" style="stop-color:#11998e;stop-opacity:1" />
                <stop offset="100%" style="stop-color:#38ef7d;stop-opacity:1" />
            </linearGradient>
        </defs>
        <!-- Background rectangle filled with the gradient -->
        <rect width="500" height="200" fill="url(#grad1)"/>
        <!-- Centered title text -->
        <text x="250" y="80" text-anchor="middle" fill="white" font-size="28" font-weight="bold">
            Welcome to SVG!
        </text>
        <!-- Centered subtitle text -->
        <text x="250" y="120" text-anchor="middle" fill="white" font-size="16">
            Scalable Vector Graphics
        </text>
        <!-- Decorative semi-transparent circles -->
        <circle cx="50" cy="170" r="20" fill="rgba(255,255,255,0.3)"/>
        <circle cx="450" cy="170" r="20" fill="rgba(255,255,255,0.3)"/>
    </svg>

</body>
</html>
```

> **Code Explanation:**
> - **Canvas Section:**
>   - `ctx.createLinearGradient(0, 0, 500, 0)` — Creates a horizontal gradient from left (0) to right (500). `addColorStop()` defines colors at positions 0 (start) and 1 (end).
>   - `ctx.fillStyle = gradient` — Uses the gradient as the fill color instead of a solid color.
>   - `ctx.fillRect(0, 0, 500, 200)` — Fills the entire canvas with the gradient background.
>   - `ctx.textAlign = 'center'` — Centers text horizontally at the x position. So `fillText('...', 250, 80)` places text centered at x=250.
>   - `'rgba(255,255,255,0.3)'` — White color with 30% opacity (semi-transparent) for decorative circles.
> - **SVG Section:**
>   - `<defs>` — Defines reusable elements (like gradients) that aren't rendered directly.
>   - `<linearGradient id="grad1">` — A gradient from teal (`#11998e`) to green (`#38ef7d`).
>   - `fill="url(#grad1)"` — References the gradient by its `id` to fill the rectangle.
>   - `text-anchor="middle"` — Centers SVG text at the x position (equivalent to `textAlign: center` in Canvas).
>   - Both Canvas and SVG produce similar visual results — notice how Canvas uses JavaScript commands while SVG uses HTML-like tags.

---

## Summary

| Element | Purpose | Best For |
|---------|---------|----------|
| `<audio>` | Embed audio | Music, podcasts |
| `<video>` | Embed video | Tutorials, demos |
| `<canvas>` | Pixel-based drawing (JS) | Games, charts |
| `<svg>` | Vector-based graphics (XML) | Logos, icons, diagrams |
| `<track>` | Subtitles for video | Accessibility |

---

*Day 16 of 55 | Unit 3 — HTML5 | Web Technology (25BCA060)*
