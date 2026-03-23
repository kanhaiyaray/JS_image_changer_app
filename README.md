# 🖼️ Image Changer App

> A lightweight, interactive hover-based image switcher built with pure HTML, CSS & JavaScript.
> Hover over a city photo to instantly swap it to a new city — move away to restore the original.

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=for-the-badge)
![No Dependencies](https://img.shields.io/badge/Dependencies-Zero-blue?style=for-the-badge)
![Single File](https://img.shields.io/badge/Single-File-orange?style=for-the-badge)

---

## 📸 Preview
```
╔══════════════════════════════════════════╗
║       Image Changer Application          ║
║                                          ║
║   ┌──────────────────────────────────┐   ║
║   │                                  │   ║
║   │      🏙️  London / NYC Photo      │   ║
║   │                                  │   ║
║   └──────────────────────────────────┘   ║
║                                          ║
║         ┌─────────────────┐             ║
║         │     London      │             ║
║         └─────────────────┘             ║
║                                          ║
║   [ Hover image → switches to NYC  ]     ║
║   [ Mouse leave → restores London  ]     ║
╚══════════════════════════════════════════╝
```

---

## 📋 Table of Contents

- [Overview](#-overview)
- [How It Works](#-how-it-works)
- [Features](#-features)
- [Getting Started](#-getting-started)
- [File Structure](#-file-structure)
- [Technical Breakdown](#️-technical-breakdown)
- [Event Flow](#-event-flow-diagram)
- [JavaScript Concepts](#-javascript-concepts-used)
- [Design Decisions](#-design-decisions)
- [Real World Applications](#-real-world-applications)
- [Known Limitations](#️-known-limitations)
- [Roadmap](#-roadmap)
- [License](#-license)

---

## 🧭 Overview

**Image Changer App** is a lightweight, interactive **hover-based image switcher**
built with pure **HTML, CSS, and vanilla JavaScript**. It displays a city photograph
that dynamically swaps to a different image and updates its label when the user
hovers over it — then smoothly reverts back when the mouse leaves.

The entire application lives in a **single `.html` file** with:
- ✅ Zero dependencies
- ✅ Zero npm packages
- ✅ Zero build tools
- ✅ Zero external libraries

---

## 🧠 How It Works — In Plain English
```
Page loads → London photo displayed → "London" yellow badge → Blue border
      │
      ▼
User hovers over image  [mouseover fires]
      │
      ▼
NYC sunset photo loads → "New York City" label → Yellow border
      │
      ▼
User moves mouse away  [mouseleave fires]
      │
      ▼
London photo restored → "London" label → Blue border
      │
      ▼
State fully reset — ready for next hover ✅
```

Two JavaScript variables act as **memory**, saving the original values
before any hover changes them so they can be perfectly restored:
```js
let prev_src  = img.src;      // Saves London image URL
let prev_text = h2.innerText; // Saves "London" text
```

---

## ⚙️ Features

| # | Feature | Details |
|---|---------|---------|
| 1 | 🖱️ Hover Image Swap | Image changes instantly on `mouseover` |
| 2 | 🏷️ Dynamic Label Update | City name updates with the image |
| 3 | 🎨 Border Color Change | Blue → Yellow border on hover |
| 4 | 🔄 State Restoration | Everything reverts perfectly on `mouseleave` |
| 5 | 💾 Variable State Storage | `prev_src` & `prev_text` store original values |
| 6 | 🌑 Dark Theme | Black background with white text |
| 7 | 📦 Single File App | Complete app in one `.html` file |
| 8 | 🌐 CDN Images | External Pixabay URLs — no local files needed |

---

## 🚀 Getting Started

No installation. No setup. Just open and run.

### ▶️ Option 1 — Direct Open
```bash
open index.html
# or just double-click the file in your file explorer
```

### ▶️ Option 2 — VS Code Live Server
```
1. Open folder in VS Code
2. Right-click index.html → "Open with Live Server"
3. App opens at http://127.0.0.1:5500
```

### ▶️ Option 3 — Clone & Run
```bash
git clone https://github.com/your-username/image-changer-app.git
cd image-changer-app
open index.html
```

---

## 📁 File Structure
```
image-changer-app/
│
├── index.html     ← Complete app (HTML + CSS + JS in one file)
└── README.md      ← Project documentation
```

> 💡 Everything — structure, styles, and logic — lives inside
> a single self-contained `index.html` file. No separate folders needed.

---

## 🛠️ Technical Breakdown

### 🌐 HTML Structure
```html
<h1>Image Changer Application</h1>
<div class="image_container">
  <img src="LONDON_URL" alt="" />
  <h2>London</h2>
</div>
```
Minimal and purposeful — just a heading, a container, an image, and a label.

---

### 🎨 CSS Breakdown

| Selector | Property | Value | Effect |
|----------|----------|-------|--------|
| `body` | `background-color` | `black` | Dark page background |
| `body` | `color` | `white` | White heading text |
| `.image_container` | `display` | `flex` | Flexbox layout |
| `.image_container` | `flex-direction` | `column` | Stacks image + label |
| `.image_container` | `justify-content` | `center` | Horizontal center |
| `img` | `height` | `300px` | Fixed height prevents layout shift |
| `img` | `border` | `2px solid blue` | Default calm border |
| `img` | `border-radius` | `10px` | Rounded corners |
| `img` | `cursor` | `pointer` | Hand cursor = interactive |
| `h2` | `background-color` | `yellow` | Bright city name badge |
| `h2` | `color` | `black` | High contrast text |
| `h2` | `border-radius` | `10px` | Rounded badge corners |

---

### ⚡ JavaScript Logic

**State Storage — saves original values before hover:**
```js
let prev_src  = img.src;       // Remembers London URL
let prev_text = h2.innerText;  // Remembers "London"
```

**mouseover — fires when cursor enters image:**
```js
img.addEventListener('mouseover', () => {
  img.src          = 'NYC_PHOTO_URL';      // Swap to NYC image
  h2.innerText     = "New York City";      // Update city label
  img.style.border = '2px solid yellow';  // Change border color
});
```

**mouseleave — fires when cursor exits image:**
```js
img.addEventListener('mouseleave', () => {
  img.src          = prev_src;            // Restore London image
  h2.innerText     = prev_text;           // Restore "London"
  img.style.border = '2px solid blue';   // Restore blue border
});
```

---

### 🖼️ Images Used

| 🌍 City | Platform | Resolution |
|---------|----------|------------|
| 🇬🇧 London | Pixabay CDN | 1280px wide |
| 🇺🇸 New York City | Pixabay CDN | 1280px wide |

---

## 🧩 JavaScript Concepts Used

| Concept | Implementation |
|---------|---------------|
| `document.querySelector()` | Selects `img` and `h2` from the DOM |
| `addEventListener()` | Attaches `mouseover` and `mouseleave` handlers |
| `element.src` | Dynamically changes the image source URL |
| `element.innerText` | Dynamically updates the city name label |
| `element.style.border` | Dynamically changes inline CSS border |
| Variable state | `prev_src` + `prev_text` store original values |
| Arrow functions | `() => {}` used as event handler callbacks |
| `let` declarations | Block-scoped mutable variable declarations |
| Mouse events | `mouseover` (enter) + `mouseleave` (exit) |

---

## 🎨 Design Decisions

| Decision | Reason |
|----------|--------|
| ⚫ Black background | Modern dark aesthetic — makes images pop visually |
| 🟡 Yellow `<h2>` badge | High contrast, easy to read city name label |
| 🔵 Blue default border | Calm neutral state for the default image |
| 🟡 Yellow hover border | Matches NYC label — signals active/changed state |
| 👆 `cursor: pointer` | Communicates interactivity to the user visually |
| 📐 Flex column layout | Clean vertical stacking of image above label |
| 📏 Fixed `300px` height | Prevents layout shift during image swap |

---

## 🌍 Real-World Applications

The hover image swap technique used here powers real features in production apps:

| Industry | Use Case |
|----------|---------|
| 🛒 E-commerce | Hover product card to see alternate color or angle |
| 🗺️ Travel sites | Hover region on a map to preview destination photo |
| 👤 Team pages | Hover headshot to reveal a fun alternate photo |
| 🎮 Gaming UIs | Hover item slot to preview item details/image |
| 🏠 Real Estate | Hover thumbnail to preview interior shots |
| 📰 News/Media | Hover card to swap thumbnail with related image |

---

## ⚠️ Known Limitations

| # | Limitation | Impact |
|---|-----------|--------|
| 1 | 🌐 External CDN images | Breaks if Pixabay is unavailable |
| 2 | ⏳ No image preloading | NYC image may flicker on first hover |
| 3 | 📱 No touch support | `mouseover` doesn't fire on mobile/tablet |
| 4 | 🔢 Only 2 hardcoded images | Not scalable to more cities |
| 5 | 🎞️ No CSS transition | Image swap is instant — no fade effect |
| 6 | 📏 Fixed 300px height | May look small on large/4K screens |

---

## 🗺️ Roadmap

- [ ] ⚡ Preload hover image on page load to eliminate first-hover flicker
- [ ] 📱 Add `touchstart` / `touchend` support for mobile devices
- [ ] 🌍 Expand to 6–10 world cities using a JavaScript array
- [ ] 🎞️ Add CSS `opacity` fade transition for smooth image crossfade
- [ ] 🖱️ Add `click` event to permanently lock a selected city
- [ ] 🔢 Build auto-slideshow mode cycling cities every few seconds
- [ ] ♿ Add `alt` text and `aria-label` for accessibility

### 💡 Future Scalable Architecture
```js
// Replace hardcoded values with a city array
const cities = [
  { name: "London",   src: "london.jpg",   border: "blue"   },
  { name: "New York", src: "newyork.jpg",  border: "yellow" },
  { name: "Tokyo",    src: "tokyo.jpg",    border: "red"    },
  { name: "Paris",    src: "paris.jpg",    border: "pink"   },
];
```

---

## 🤝 Contributing
```bash
# 1. Fork the repo
# 2. Create your branch
git checkout -b feature/add-city-tokyo

# 3. Commit your changes
git commit -m "feat: add Tokyo hover image"

# 4. Push and open a Pull Request
git push origin feature/add-city-tokyo
```

---

## 👨‍💻 Author

[![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/kanhaiyaray)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/raykanhaiya/)

---

## 📜 License
```
MIT License — free to use, modify, and distribute.
```

---

<p align="center">
  🖼️ Built with HTML · CSS · JavaScript · Pixabay CDN
  <br/>
  ⭐ Star this repo if you found it helpful!
</p>
