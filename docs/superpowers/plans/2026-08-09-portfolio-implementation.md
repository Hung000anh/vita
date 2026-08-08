# Portfolio Website Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a dark-mode-first multi-page personal portfolio website for `hung000anh.github.io` without external frameworks, featuring glassmorphism styling, AI cyan-purple accents, theme/language toggles, and interactive project tag filtering.

**Architecture:** Pure static multi-page architecture HTML5/CSS3/Vanilla JS. Global CSS variables handle dark/light themes, glassmorphism, and responsive layouts. Shared navbar JS manages theme/language persistence in `localStorage`, active links, and mobile navigation.

**Tech Stack:** HTML5, CSS3 (Flexbox/Grid/CSS Variables/Backdrop Filter), Vanilla JavaScript (ES6+).

## Global Constraints

- Primary Background: `#0f172a` (Deep Slate - Dark Mode Default)
- Card Background: `rgba(30, 41, 59, 0.7)` with `backdrop-filter: blur(12px)`
- Accent Gradient: `linear-gradient(135deg, #06b6d4, #8b5cf6)`
- No external frameworks (Bootstrap, Tailwind, React, jQuery, etc.)
- All sub-pages must share identical Navigation Bar order and Footer

---

### Task 1: CSS Design System & Theme Engine

**Files:**
- Create: `css/style.css`

**Interfaces:**
- Consumes: None
- Produces: CSS custom variables, global utility classes (`.card`, `.btn-gradient`, `.badge`), layout rules for navbar and grid layouts.

- [ ] **Step 1: Create `css/style.css` with Design System Variables and Base Styles**

```css
:root {
  --bg-primary: #0f172a;
  --bg-card: rgba(30, 41, 59, 0.7);
  --bg-card-hover: rgba(51, 65, 85, 0.5);
  --text-primary: #f8fafc;
  --text-secondary: #94a3b8;
  --accent-gradient: linear-gradient(135deg, #06b6d4, #8b5cf6);
  --accent-cyan: #06b6d4;
  --accent-purple: #8b5cf6;
  --border-glass: 1px solid rgba(255, 255, 255, 0.1);
  --shadow-glow: 0 0 15px rgba(6, 182, 212, 0.3);
  --radius-sm: 6px;
  --radius-md: 10px;
  --radius-lg: 16px;
  --transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
  --font-main: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
}

[data-theme="light"] {
  --bg-primary: #f8fafc;
  --bg-card: rgba(255, 255, 255, 0.8);
  --bg-card-hover: rgba(241, 245, 249, 0.9);
  --text-primary: #0f172a;
  --text-secondary: #475569;
  --border-glass: 1px solid rgba(0, 0, 0, 0.08);
  --shadow-glow: 0 4px 12px rgba(6, 182, 212, 0.15);
}

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  background-color: var(--bg-primary);
  color: var(--text-primary);
  font-family: var(--font-main);
  line-height: 1.6;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  transition: var(--transition);
}

/* Glassmorphism Panel */
.glass-panel {
  background: var(--bg-card);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  border: var(--border-glass);
  border-radius: var(--radius-md);
  padding: 1.5rem;
  transition: var(--transition);
}

.glass-panel:hover {
  background: var(--bg-card-hover);
  box-shadow: var(--shadow-glow);
}

/* Gradient Text & Buttons */
.gradient-text {
  background: var(--accent-gradient);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  font-weight: 700;
}

.btn-gradient {
  background: var(--accent-gradient);
  color: #ffffff;
  padding: 0.6rem 1.2rem;
  border-radius: var(--radius-sm);
  text-decoration: none;
  font-weight: 600;
  display: inline-block;
  border: none;
  cursor: pointer;
  transition: var(--transition);
}

.btn-gradient:hover {
  opacity: 0.9;
  box-shadow: var(--shadow-glow);
}

/* Badges */
.badge {
  background: rgba(6, 182, 212, 0.15);
  color: var(--accent-cyan);
  border: 1px solid rgba(6, 182, 212, 0.3);
  padding: 0.2rem 0.6rem;
  border-radius: var(--radius-sm);
  font-size: 0.85rem;
  font-weight: 500;
  display: inline-block;
  margin-right: 0.4rem;
  margin-bottom: 0.4rem;
}

/* Header & Navbar */
.navbar {
  position: sticky;
  top: 0;
  z-index: 100;
  background: var(--bg-card);
  backdrop-filter: blur(16px);
  border-bottom: var(--border-glass);
  padding: 1rem 2rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.nav-links {
  display: flex;
  gap: 1.2rem;
  list-style: none;
  align-items: center;
}

.nav-links a {
  color: var(--text-secondary);
  text-decoration: none;
  font-size: 0.95rem;
  font-weight: 500;
  transition: var(--transition);
}

.nav-links a:hover,
.nav-links a.active {
  color: var(--text-primary);
  border-bottom: 2px solid var(--accent-cyan);
}

.nav-controls {
  display: flex;
  gap: 0.8rem;
}

.btn-control {
  background: rgba(255, 255, 255, 0.05);
  border: var(--border-glass);
  color: var(--text-primary);
  padding: 0.4rem 0.8rem;
  border-radius: var(--radius-sm);
  cursor: pointer;
  font-size: 0.9rem;
  transition: var(--transition);
}

.btn-control:hover {
  background: var(--bg-card-hover);
}

/* Layout Container & Footer */
.container {
  max-width: 1100px;
  width: 90%;
  margin: 2rem auto;
  flex: 1;
}

footer {
  text-align: center;
  padding: 2rem;
  color: var(--text-secondary);
  border-top: var(--border-glass);
  font-size: 0.9rem;
}
```

- [ ] **Step 2: Commit CSS Design System**

```bash
git add css/style.css
git commit -m "feat: add CSS design system with glassmorphism and theme variables"
```

---

### Task 2: Shared JavaScript (Navbar, Theme, Language)

**Files:**
- Create: `js/main.js`

**Interfaces:**
- Consumes: CSS custom variables (`[data-theme]`)
- Produces: Theme toggle (`toggleTheme()`), Language state (`toggleLanguage()`), Navigation active state updater.

- [ ] **Step 1: Write `js/main.js`**

```javascript
document.addEventListener('DOMContentLoaded', () => {
  // 1. Theme Management
  const savedTheme = localStorage.getItem('theme') || 'dark';
  document.documentElement.setAttribute('data-theme', savedTheme);

  const themeBtn = document.getElementById('theme-toggle');
  if (themeBtn) {
    themeBtn.textContent = savedTheme === 'dark' ? '☀️' : '🌙';
    themeBtn.addEventListener('click', () => {
      const currentTheme = document.documentElement.getAttribute('data-theme');
      const newTheme = currentTheme === 'dark' ? 'light' : 'dark';
      document.documentElement.setAttribute('data-theme', newTheme);
      localStorage.setItem('theme', newTheme);
      themeBtn.textContent = newTheme === 'dark' ? '☀️' : '🌙';
    });
  }

  // 2. Language State Toggle
  const savedLang = localStorage.getItem('lang') || 'en';
  const langBtn = document.getElementById('lang-toggle');
  if (langBtn) {
    langBtn.textContent = savedLang.toUpperCase();
    langBtn.addEventListener('click', () => {
      const currentLang = localStorage.getItem('lang') || 'en';
      const newLang = currentLang === 'en' ? 'vi' : 'en';
      localStorage.setItem('lang', newLang);
      langBtn.textContent = newLang.toUpperCase();
      // Future hook for translation loading
    });
  }

  // 3. Navbar Active Link Highlight
  const currentPath = window.location.pathname.split('/').pop() || 'index.html';
  const navLinks = document.querySelectorAll('.nav-links a');
  navLinks.forEach(link => {
    const href = link.getAttribute('href');
    if (href === currentPath || (currentPath === '' && href === 'index.html')) {
      link.classList.add('active');
    }
  });
});
```

- [ ] **Step 2: Commit `js/main.js`**

```bash
git add js/main.js
git commit -m "feat: add main JS script for theme toggle, language state, and navbar active link"
```

---

### Task 3: Home Page (`index.html`)

**Files:**
- Create: `index.html`

**Interfaces:**
- Consumes: `css/style.css`, `js/main.js`
- Produces: Hero section, quick overview section

- [ ] **Step 1: Create `index.html`**

```html
<!DOCTYPE html>
<html lang="en" data-theme="dark">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Hung Anh Nguyen | Portfolio</title>
  <link rel="stylesheet" href="css/style.css">
</head>
<body>
  <header class="navbar">
    <a href="index.html" class="gradient-text" style="text-decoration:none; font-size:1.4rem;">Hung Anh Nguyen</a>
    <nav>
      <ul class="nav-links">
        <li><a href="education.html">Education</a></li>
        <li><a href="experience.html">Experience</a></li>
        <li><a href="projects.html">Projects</a></li>
        <li><a href="publications.html">Publications</a></li>
        <li><a href="skills.html">Skills</a></li>
        <li><a href="honors.html">Honors & Awards</a></li>
        <li><a href="certifications.html">Certifications</a></li>
        <li><a href="links.html">Links</a></li>
      </ul>
    </nav>
    <div class="nav-controls">
      <button id="lang-toggle" class="btn-control">EN</button>
      <button id="theme-toggle" class="btn-control">☀️</button>
    </div>
  </header>

  <main class="container">
    <section class="glass-panel" style="text-align:center; padding:3rem 1.5rem; margin-bottom:2rem;">
      <h1 style="font-size: 2.5rem; margin-bottom: 0.5rem;">Hung Anh Nguyen</h1>
      <p class="gradient-text" style="font-size: 1.3rem; margin-bottom: 1rem;">AI Engineer & Backend Developer</p>
      <p style="max-width: 700px; margin: 0 auto 1.5rem auto; color: var(--text-secondary);">
        Specializing in LLM integration, data extraction pipelines, financial news sentiment classification, and high-performance backend automation systems.
      </p>
      <div style="display:flex; gap:1rem; justify-content:center;">
        <a href="projects.html" class="btn-gradient">View Projects</a>
        <a href="links.html" class="btn-control" style="text-decoration:none;">Contact / Links</a>
      </div>
    </section>

    <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 1.5rem;">
      <div class="glass-panel">
        <h3>⚡ Experience</h3>
        <p style="color: var(--text-secondary); margin-top:0.5rem;">AI Engineer at Digitech Solution & QA Tester at Stopest Co., Ltd.</p>
        <a href="experience.html" class="gradient-text" style="display:inline-block; margin-top:1rem; text-decoration:none;">Read more &rarr;</a>
      </div>
      <div class="glass-panel">
        <h3>🚀 Top Projects</h3>
        <p style="color: var(--text-secondary); margin-top:0.5rem;">Hach Thach Thon, Smart News AI, Cudo Market, and Excerpo.</p>
        <a href="projects.html" class="gradient-text" style="display:inline-block; margin-top:1rem; text-decoration:none;">Explore projects &rarr;</a>
      </div>
      <div class="glass-panel">
        <h3>🎓 Education</h3>
        <p style="color: var(--text-secondary); margin-top:0.5rem;">BS in Computer Science at Industrial University of Ho Chi Minh City (GPA: 3.31/4.00).</p>
        <a href="education.html" class="gradient-text" style="display:inline-block; margin-top:1rem; text-decoration:none;">View details &rarr;</a>
      </div>
    </div>
  </main>

  <footer>
    <p>&copy; 2026 Hung Anh Nguyen. All rights reserved.</p>
  </footer>

  <script src="js/main.js"></script>
</body>
</html>
```

- [ ] **Step 2: Commit `index.html`**

```bash
git add index.html
git commit -m "feat: add Home page index.html with hero section and overview cards"
```

---

### Task 4: Education, Experience & Publications Pages

**Files:**
- Create: `education.html`
- Create: `experience.html`
- Create: `publications.html`

**Interfaces:**
- Consumes: `css/style.css`, `js/main.js`

- [ ] **Step 1: Create `education.html`**

```html
<!DOCTYPE html>
<html lang="en" data-theme="dark">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Education | Hung Anh Nguyen</title>
  <link rel="stylesheet" href="css/style.css">
</head>
<body>
  <header class="navbar">
    <a href="index.html" class="gradient-text" style="text-decoration:none; font-size:1.4rem;">Hung Anh Nguyen</a>
    <nav>
      <ul class="nav-links">
        <li><a href="education.html">Education</a></li>
        <li><a href="experience.html">Experience</a></li>
        <li><a href="projects.html">Projects</a></li>
        <li><a href="publications.html">Publications</a></li>
        <li><a href="skills.html">Skills</a></li>
        <li><a href="honors.html">Honors & Awards</a></li>
        <li><a href="certifications.html">Certifications</a></li>
        <li><a href="links.html">Links</a></li>
      </ul>
    </nav>
    <div class="nav-controls">
      <button id="lang-toggle" class="btn-control">EN</button>
      <button id="theme-toggle" class="btn-control">☀️</button>
    </div>
  </header>

  <main class="container">
    <h2 style="margin-bottom: 1.5rem;">Education</h2>
    <div class="glass-panel">
      <div style="display: flex; justify-content: space-between; align-items: flex-start; flex-wrap: wrap;">
        <div>
          <h3>Industrial University of Ho Chi Minh City</h3>
          <p class="gradient-text">Bachelor of Science in Computer Science</p>
        </div>
        <span class="badge">2026 | Ho Chi Minh City, Vietnam</span>
      </div>
      <ul style="margin-top: 1rem; padding-left: 1.2rem; color: var(--text-secondary);">
        <li><strong>Cumulative GPA:</strong> 3.31 / 4.00 (Classification: Very Good)</li>
        <li><strong>Completed Credits:</strong> 156 Credits</li>
      </ul>
    </div>
  </main>

  <footer>
    <p>&copy; 2026 Hung Anh Nguyen. All rights reserved.</p>
  </footer>
  <script src="js/main.js"></script>
</body>
</html>
```

- [ ] **Step 2: Create `experience.html`**

```html
<!DOCTYPE html>
<html lang="en" data-theme="dark">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Experience | Hung Anh Nguyen</title>
  <link rel="stylesheet" href="css/style.css">
</head>
<body>
  <header class="navbar">
    <a href="index.html" class="gradient-text" style="text-decoration:none; font-size:1.4rem;">Hung Anh Nguyen</a>
    <nav>
      <ul class="nav-links">
        <li><a href="education.html">Education</a></li>
        <li><a href="experience.html">Experience</a></li>
        <li><a href="projects.html">Projects</a></li>
        <li><a href="publications.html">Publications</a></li>
        <li><a href="skills.html">Skills</a></li>
        <li><a href="honors.html">Honors & Awards</a></li>
        <li><a href="certifications.html">Certifications</a></li>
        <li><a href="links.html">Links</a></li>
      </ul>
    </nav>
    <div class="nav-controls">
      <button id="lang-toggle" class="btn-control">EN</button>
      <button id="theme-toggle" class="btn-control">☀️</button>
    </div>
  </header>

  <main class="container">
    <h2 style="margin-bottom: 1.5rem;">Work Experience</h2>
    <div style="display:flex; flex-direction:column; gap:1.5rem;">
      <div class="glass-panel">
        <div style="display:flex; justify-content:space-between; flex-wrap:wrap;">
          <div>
            <h3>Digitech Solution</h3>
            <p class="gradient-text">AI Engineer</p>
          </div>
          <span class="badge">Sep 2025 – Nov 2025 | Ho Chi Minh City</span>
        </div>
        <ul style="margin-top: 1rem; padding-left: 1.2rem; color: var(--text-secondary);">
          <li>Built data extraction pipelines to compile B2B profiles from YellowPages into the DigiOmniAI database for targeted multi-channel marketing.</li>
          <li>Engineered DigiZaloAI, a Gemini-powered Zalo chatbot automating 24/7 customer service with context-aware responses and personalized care, optimizing HR costs and boosting conversions.</li>
        </ul>
      </div>

      <div class="glass-panel">
        <div style="display:flex; justify-content:space-between; flex-wrap:wrap;">
          <div>
            <h3>Stopest Co., Ltd.</h3>
            <p class="gradient-text">Quality Assurance Tester</p>
          </div>
          <span class="badge">Mar 2023 – Jun 2023 | Ho Chi Minh City</span>
        </div>
        <ul style="margin-top: 1rem; padding-left: 1.2rem; color: var(--text-secondary);">
          <li>Conducted manual testing on web and mobile applications to ensure UI/UX consistency and functional integrity.</li>
          <li>Identified and reported software defects using detailed visual bug reports to accelerate developer resolution.</li>
        </ul>
      </div>
    </div>
  </main>

  <footer>
    <p>&copy; 2026 Hung Anh Nguyen. All rights reserved.</p>
  </footer>
  <script src="js/main.js"></script>
</body>
</html>
```

- [ ] **Step 3: Create `publications.html`**

```html
<!DOCTYPE html>
<html lang="en" data-theme="dark">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Publications | Hung Anh Nguyen</title>
  <link rel="stylesheet" href="css/style.css">
</head>
<body>
  <header class="navbar">
    <a href="index.html" class="gradient-text" style="text-decoration:none; font-size:1.4rem;">Hung Anh Nguyen</a>
    <nav>
      <ul class="nav-links">
        <li><a href="education.html">Education</a></li>
        <li><a href="experience.html">Experience</a></li>
        <li><a href="projects.html">Projects</a></li>
        <li><a href="publications.html">Publications</a></li>
        <li><a href="skills.html">Skills</a></li>
        <li><a href="honors.html">Honors & Awards</a></li>
        <li><a href="certifications.html">Certifications</a></li>
        <li><a href="links.html">Links</a></li>
      </ul>
    </nav>
    <div class="nav-controls">
      <button id="lang-toggle" class="btn-control">EN</button>
      <button id="theme-toggle" class="btn-control">☀️</button>
    </div>
  </header>

  <main class="container">
    <h2 style="margin-bottom: 1.5rem;">Publications</h2>
    <div class="glass-panel">
      <span class="badge">2025</span>
      <h3 style="margin-top: 0.5rem;">News Website Sentiment Analysis System and User Support Chatbot</h3>
      <p style="color: var(--text-secondary); margin-top: 0.3rem;"><strong>Authors:</strong> Anh Nguyen, Thiet Pham, Thang Truong</p>
      <p style="color: var(--text-secondary); margin-top: 0.3rem;"><strong>Journal:</strong> Student Scientific Research Communication (SSRC), Vol. 1, No. 2</p>
    </div>
  </main>

  <footer>
    <p>&copy; 2026 Hung Anh Nguyen. All rights reserved.</p>
  </footer>
  <script src="js/main.js"></script>
</body>
</html>
```

- [ ] **Step 4: Commit education, experience, and publications pages**

```bash
git add education.html experience.html publications.html
git commit -m "feat: add education, experience, and publications pages"
```

---

### Task 5: Projects Page with Interactive Tag Filter

**Files:**
- Create: `projects.html`
- Create: `js/project-filter.js`

**Interfaces:**
- Consumes: `css/style.css`, `js/main.js`
- Produces: Tag-based project filtering logic (`data-tags`)

- [ ] **Step 1: Create `js/project-filter.js`**

```javascript
document.addEventListener('DOMContentLoaded', () => {
  const filterBtns = document.querySelectorAll('.filter-btn');
  const projectCards = document.querySelectorAll('.project-card');

  filterBtns.forEach(btn => {
    btn.addEventListener('click', () => {
      filterBtns.forEach(b => b.classList.remove('active'));
      btn.classList.add('active');

      const filter = btn.getAttribute('data-filter');

      projectCards.forEach(card => {
        const tags = card.getAttribute('data-tags').split(' ');
        if (filter === 'all' || tags.includes(filter)) {
          card.style.display = 'block';
        } else {
          card.style.display = 'none';
        }
      });
    });
  });
});
```

- [ ] **Step 2: Create `projects.html`**

```html
<!DOCTYPE html>
<html lang="en" data-theme="dark">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Projects | Hung Anh Nguyen</title>
  <link rel="stylesheet" href="css/style.css">
  <style>
    .filter-btn.active {
      background: var(--accent-gradient);
      color: #fff;
    }
  </style>
</head>
<body>
  <header class="navbar">
    <a href="index.html" class="gradient-text" style="text-decoration:none; font-size:1.4rem;">Hung Anh Nguyen</a>
    <nav>
      <ul class="nav-links">
        <li><a href="education.html">Education</a></li>
        <li><a href="experience.html">Experience</a></li>
        <li><a href="projects.html">Projects</a></li>
        <li><a href="publications.html">Publications</a></li>
        <li><a href="skills.html">Skills</a></li>
        <li><a href="honors.html">Honors & Awards</a></li>
        <li><a href="certifications.html">Certifications</a></li>
        <li><a href="links.html">Links</a></li>
      </ul>
    </nav>
    <div class="nav-controls">
      <button id="lang-toggle" class="btn-control">EN</button>
      <button id="theme-toggle" class="btn-control">☀️</button>
    </div>
  </header>

  <main class="container">
    <h2 style="margin-bottom: 1rem;">Projects</h2>

    <div style="display: flex; gap: 0.5rem; flex-wrap: wrap; margin-bottom: 1.5rem;">
      <button class="btn-control filter-btn active" data-filter="all">All</button>
      <button class="btn-control filter-btn" data-filter="ai">AI / LLM</button>
      <button class="btn-control filter-btn" data-filter="backend">Backend</button>
      <button class="btn-control filter-btn" data-filter="fullstack">Fullstack</button>
      <button class="btn-control filter-btn" data-filter="automation">Automation</button>
    </div>

    <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(320px, 1fr)); gap: 1.5rem;">
      
      <!-- Project 1 -->
      <div class="glass-panel project-card" data-tags="ai backend">
        <h3>Hach Thach Thon</h3>
        <p class="gradient-text" style="font-size:0.9rem; margin-bottom:0.5rem;">AI & Backend Developer</p>
        <p style="color: var(--text-secondary); margin-bottom:1rem; font-size:0.95rem;">
          Designed backend with pay-per-word billing and AI translation engine with LLM integrations, dynamic prompts, chapter splitting, glossary management, and EPUB/DOCX export.
        </p>
        <div style="margin-bottom: 1rem;">
          <span class="badge">Python</span>
          <span class="badge">FastAPI</span>
          <span class="badge">Supabase</span>
          <span class="badge">LLM</span>
        </div>
        <a href="https://hachthachthon.site" target="_blank" class="btn-gradient">Live Site</a>
      </div>

      <!-- Project 2 -->
      <div class="glass-panel project-card" data-tags="ai backend">
        <h3>Smart News AI</h3>
        <p class="gradient-text" style="font-size:0.9rem; margin-bottom:0.5rem;">AI & Backend Developer</p>
        <p style="color: var(--text-secondary); margin-bottom:1rem; font-size:0.95rem;">
          Built backend and ETL pipelines for automated financial news aggregation, real-time sentiment classification, and a context-aware chatbot (Web Zalo).
        </p>
        <div style="margin-bottom: 1rem;">
          <span class="badge">Python</span>
          <span class="badge">FastAPI</span>
          <span class="badge">n8n</span>
          <span class="badge">Deep Learning</span>
        </div>
        <a href="https://smart-new-ai-client.vercel.app" target="_blank" class="btn-gradient">Live Site</a>
      </div>

      <!-- Project 3 -->
      <div class="glass-panel project-card" data-tags="fullstack">
        <h3>Cudo Market</h3>
        <p class="gradient-text" style="font-size:0.9rem; margin-bottom:0.5rem;">Full-stack Developer</p>
        <p style="color: var(--text-secondary); margin-bottom:1rem; font-size:0.95rem;">
          Integrated currency market intelligence platform (candlestick charts, COT positioning, seasonality, community sentiment, economic calendar, and news).
        </p>
        <div style="margin-bottom: 1rem;">
          <span class="badge">Python</span>
          <span class="badge">Streamlit</span>
          <span class="badge">Supabase</span>
        </div>
        <div style="display:flex; gap:0.5rem;">
          <a href="https://cudomarket.streamlit.app" target="_blank" class="btn-gradient">Live Site</a>
          <a href="https://github.com/Hung000anh/cudo-market" target="_blank" class="btn-control" style="text-decoration:none;">GitHub</a>
        </div>
      </div>

      <!-- Project 4 -->
      <div class="glass-panel project-card" data-tags="automation backend">
        <h3>Excerpo</h3>
        <p class="gradient-text" style="font-size:0.9rem; margin-bottom:0.5rem;">Backend / Automation Engineer</p>
        <p style="color: var(--text-secondary); margin-bottom:1rem; font-size:0.95rem;">
          A multi-source extractor that automates bulk downloading of chapters/text from platforms (Qidian, 17k, Biquge, etc.), supporting background batch scraping and export.
        </p>
        <div style="margin-bottom: 1rem;">
          <span class="badge">JavaScript</span>
          <span class="badge">HTML</span>
          <span class="badge">Automation</span>
        </div>
        <a href="https://github.com/Hung000anh/excerpo" target="_blank" class="btn-control" style="text-decoration:none;">GitHub</a>
      </div>

    </div>
  </main>

  <footer>
    <p>&copy; 2026 Hung Anh Nguyen. All rights reserved.</p>
  </footer>
  <script src="js/main.js"></script>
  <script src="js/project-filter.js"></script>
</body>
</html>
```

- [ ] **Step 3: Commit `projects.html` and `js/project-filter.js`**

```bash
git add projects.html js/project-filter.js
git commit -m "feat: add projects page with interactive tag filtering"
```

---

### Task 6: Skills, Honors & Awards, Certifications, and Links Pages

**Files:**
- Create: `skills.html`
- Create: `honors.html`
- Create: `certifications.html`
- Create: `links.html`

**Interfaces:**
- Consumes: `css/style.css`, `js/main.js`

- [ ] **Step 1: Create `skills.html`**

```html
<!DOCTYPE html>
<html lang="en" data-theme="dark">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Skills | Hung Anh Nguyen</title>
  <link rel="stylesheet" href="css/style.css">
</head>
<body>
  <header class="navbar">
    <a href="index.html" class="gradient-text" style="text-decoration:none; font-size:1.4rem;">Hung Anh Nguyen</a>
    <nav>
      <ul class="nav-links">
        <li><a href="education.html">Education</a></li>
        <li><a href="experience.html">Experience</a></li>
        <li><a href="projects.html">Projects</a></li>
        <li><a href="publications.html">Publications</a></li>
        <li><a href="skills.html">Skills</a></li>
        <li><a href="honors.html">Honors & Awards</a></li>
        <li><a href="certifications.html">Certifications</a></li>
        <li><a href="links.html">Links</a></li>
      </ul>
    </nav>
    <div class="nav-controls">
      <button id="lang-toggle" class="btn-control">EN</button>
      <button id="theme-toggle" class="btn-control">☀️</button>
    </div>
  </header>

  <main class="container">
    <h2 style="margin-bottom: 1.5rem;">Skills Matrix</h2>
    <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 1.5rem;">
      
      <div class="glass-panel">
        <h3>Programming Languages</h3>
        <div style="margin-top: 1rem;">
          <span class="badge">Python</span>
          <span class="badge">JavaScript</span>
          <span class="badge">TypeScript</span>
          <span class="badge">SQL</span>
        </div>
      </div>

      <div class="glass-panel">
        <h3>Frameworks & Libraries</h3>
        <div style="margin-top: 1rem;">
          <span class="badge">PyTorch</span>
          <span class="badge">TensorFlow</span>
          <span class="badge">Keras</span>
          <span class="badge">Scikit-Learn</span>
          <span class="badge">Hugging Face</span>
          <span class="badge">OpenCV</span>
          <span class="badge">Pandas</span>
          <span class="badge">NumPy</span>
          <span class="badge">FastAPI</span>
        </div>
      </div>

      <div class="glass-panel">
        <h3>Databases</h3>
        <div style="margin-top: 1rem;">
          <span class="badge">PostgreSQL</span>
          <span class="badge">MySQL</span>
          <span class="badge">SQL Server</span>
          <span class="badge">MongoDB</span>
        </div>
      </div>

      <div class="glass-panel">
        <h3>Tools & Platforms</h3>
        <div style="margin-top: 1rem;">
          <span class="badge">N8n</span>
          <span class="badge">Docker</span>
          <span class="badge">Supabase</span>
          <span class="badge">Git</span>
          <span class="badge">GitHub</span>
          <span class="badge">GitHub Actions</span>
        </div>
      </div>

    </div>
  </main>

  <footer>
    <p>&copy; 2026 Hung Anh Nguyen. All rights reserved.</p>
  </footer>
  <script src="js/main.js"></script>
</body>
</html>
```

- [ ] **Step 2: Create `honors.html`**

```html
<!DOCTYPE html>
<html lang="en" data-theme="dark">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Honors & Awards | Hung Anh Nguyen</title>
  <link rel="stylesheet" href="css/style.css">
</head>
<body>
  <header class="navbar">
    <a href="index.html" class="gradient-text" style="text-decoration:none; font-size:1.4rem;">Hung Anh Nguyen</a>
    <nav>
      <ul class="nav-links">
        <li><a href="education.html">Education</a></li>
        <li><a href="experience.html">Experience</a></li>
        <li><a href="projects.html">Projects</a></li>
        <li><a href="publications.html">Publications</a></li>
        <li><a href="skills.html">Skills</a></li>
        <li><a href="honors.html">Honors & Awards</a></li>
        <li><a href="certifications.html">Certifications</a></li>
        <li><a href="links.html">Links</a></li>
      </ul>
    </nav>
    <div class="nav-controls">
      <button id="lang-toggle" class="btn-control">EN</button>
      <button id="theme-toggle" class="btn-control">☀️</button>
    </div>
  </header>

  <main class="container">
    <h2 style="margin-bottom: 1.5rem;">Honors & Awards</h2>
    <div class="glass-panel">
      <h3>Academic Excellence Scholarship</h3>
      <p style="color: var(--text-secondary); margin-top: 0.5rem;">
        Awarded for achieving <strong>’Excellent’</strong> classification across 3 academic semesters (Highest GPA: <strong>3.60 / 4.00</strong>).
      </p>
    </div>
  </main>

  <footer>
    <p>&copy; 2026 Hung Anh Nguyen. All rights reserved.</p>
  </footer>
  <script src="js/main.js"></script>
</body>
</html>
```

- [ ] **Step 3: Create `certifications.html`**

```html
<!DOCTYPE html>
<html lang="en" data-theme="dark">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Certifications | Hung Anh Nguyen</title>
  <link rel="stylesheet" href="css/style.css">
</head>
<body>
  <header class="navbar">
    <a href="index.html" class="gradient-text" style="text-decoration:none; font-size:1.4rem;">Hung Anh Nguyen</a>
    <nav>
      <ul class="nav-links">
        <li><a href="education.html">Education</a></li>
        <li><a href="experience.html">Experience</a></li>
        <li><a href="projects.html">Projects</a></li>
        <li><a href="publications.html">Publications</a></li>
        <li><a href="skills.html">Skills</a></li>
        <li><a href="honors.html">Honors & Awards</a></li>
        <li><a href="certifications.html">Certifications</a></li>
        <li><a href="links.html">Links</a></li>
      </ul>
    </nav>
    <div class="nav-controls">
      <button id="lang-toggle" class="btn-control">EN</button>
      <button id="theme-toggle" class="btn-control">☀️</button>
    </div>
  </header>

  <main class="container">
    <h2 style="margin-bottom: 1.5rem;">Certifications</h2>
    <div style="display: flex; flex-direction: column; gap: 1rem;">
      <div class="glass-panel" style="display:flex; justify-content:space-between; align-items:center;">
        <span>TOEIC Listening & Reading</span>
        <span class="badge">2026</span>
      </div>
      <div class="glass-panel" style="display:flex; justify-content:space-between; align-items:center;">
        <span>CertNexus Certified Ethical Emerging Technologist</span>
        <span class="badge">2025</span>
      </div>
      <div class="glass-panel" style="display:flex; justify-content:space-between; align-items:center;">
        <span>Academic English: Writing</span>
        <span class="badge">2025</span>
      </div>
      <div class="glass-panel" style="display:flex; justify-content:space-between; align-items:center;">
        <span>Java FullStack Developer</span>
        <span class="badge">2024</span>
      </div>
      <div class="glass-panel" style="display:flex; justify-content:space-between; align-items:center;">
        <span>Software Development Lifecycle</span>
        <span class="badge">2024</span>
      </div>
      <div class="glass-panel" style="display:flex; justify-content:space-between; align-items:center;">
        <span>Web Design for Everybody: Basics of Web Development & Coding</span>
        <span class="badge">2024</span>
      </div>
      <div class="glass-panel" style="display:flex; justify-content:space-between; align-items:center;">
        <span>Java Testing</span>
        <span class="badge">2024</span>
      </div>
      <div class="glass-panel" style="display:flex; justify-content:space-between; align-items:center;">
        <span>Academic Skills for University Success</span>
        <span class="badge">2023</span>
      </div>
    </div>
  </main>

  <footer>
    <p>&copy; 2026 Hung Anh Nguyen. All rights reserved.</p>
  </footer>
  <script src="js/main.js"></script>
</body>
</html>
```

- [ ] **Step 4: Create `links.html`**

```html
<!DOCTYPE html>
<html lang="en" data-theme="dark">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Links & Contact | Hung Anh Nguyen</title>
  <link rel="stylesheet" href="css/style.css">
</head>
<body>
  <header class="navbar">
    <a href="index.html" class="gradient-text" style="text-decoration:none; font-size:1.4rem;">Hung Anh Nguyen</a>
    <nav>
      <ul class="nav-links">
        <li><a href="education.html">Education</a></li>
        <li><a href="experience.html">Experience</a></li>
        <li><a href="projects.html">Projects</a></li>
        <li><a href="publications.html">Publications</a></li>
        <li><a href="skills.html">Skills</a></li>
        <li><a href="honors.html">Honors & Awards</a></li>
        <li><a href="certifications.html">Certifications</a></li>
        <li><a href="links.html">Links</a></li>
      </ul>
    </nav>
    <div class="nav-controls">
      <button id="lang-toggle" class="btn-control">EN</button>
      <button id="theme-toggle" class="btn-control">☀️</button>
    </div>
  </header>

  <main class="container">
    <h2 style="margin-bottom: 1.5rem;">Links & Connect</h2>
    <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 1.5rem;">
      
      <a href="https://linkedin.com" target="_blank" class="glass-panel" style="text-decoration:none; display:block;">
        <h3>🔗 LinkedIn</h3>
        <p class="gradient-text" style="margin-top:0.5rem;">Hung Anh Nguyen</p>
      </a>

      <a href="https://github.com/Hung000anh" target="_blank" class="glass-panel" style="text-decoration:none; display:block;">
        <h3>💻 GitHub</h3>
        <p class="gradient-text" style="margin-top:0.5rem;">Hung000anh</p>
      </a>

    </div>
  </main>

  <footer>
    <p>&copy; 2026 Hung Anh Nguyen. All rights reserved.</p>
  </footer>
  <script src="js/main.js"></script>
</body>
</html>
```

- [ ] **Step 5: Commit skills, honors, certifications, and links pages**

```bash
git add skills.html honors.html certifications.html links.html
git commit -m "feat: add skills, honors, certifications, and links pages"
```

---

## Plan Review Checklist
1. All pages specified in spec are covered.
2. Styling aligns with dark mode first, `#0f172a` primary background, glassmorphic cards, and cyan-purple accent gradients.
3. Fully compatible with GitHub Pages static hosting.
