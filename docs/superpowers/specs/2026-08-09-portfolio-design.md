# Design Spec: Portfolio Website (hung000anh.github.io)

**Date:** 2026-08-09  
**Target Host:** GitHub Pages (`hung000anh.github.io`)  
**Stack:** Pure HTML5, CSS3 (Custom Variables, Glassmorphism, Flex/Grid), Vanilla JavaScript. No external frameworks.

---

## 1. Overview & Architecture

Multi-page portfolio site built with standard Web technologies. Dark mode first with glassmorphic cards and cyan-purple AI accent gradients. Includes theme switcher (Dark/Light) and language switcher toggle (EN default / VI support ready) in the global Navigation Bar.

### File Structure
```text
.
├── index.html            # Home page / Overview
├── education.html        # Education section
├── experience.html       # Experience section
├── projects.html         # Projects section with tag filtering
├── publications.html     # Publications section
├── skills.html           # Skills matrix
├── honors.html           # Honors & Awards
├── certifications.html   # Certifications
├── links.html            # External links & contact
├── css/
│   └── style.css         # Design system, glassmorphism, animations, theme vars
└── js/
    ├── main.js           # Navbar, theme toggle, lang toggle, active state
    └── project-filter.js # Interactive project tag filter
```

---

## 2. Design System & Styling Rules

### CSS Variables (`:root` - Dark Mode Default)
- **Primary Background:** `#0f172a` (Deep Slate)
- **Card / Panel Background:** `rgba(30, 41, 59, 0.7)`
- **Hover Background:** `rgba(51, 65, 85, 0.5)`
- **Main Accent Gradient:** `linear-gradient(135deg, #06b6d4, #8b5cf6)` (Cyan `#06b6d4` to Violet `#8b5cf6`)
- **Text Primary:** `#f8fafc`
- **Text Secondary:** `#94a3b8`
- **Border Glass:** `1px solid rgba(255, 255, 255, 0.1)`
- **Glow Shadow:** `0 0 15px rgba(6, 182, 212, 0.3)`
- **Border Radius:** `--radius-sm: 6px`, `--radius-md: 10px`, `--radius-lg: 16px`
- **Transition:** `all 0.2s cubic-bezier(0.4, 0, 0.2, 1)`

### Light Theme Variables (`[data-theme="light"]`)
- **Primary Background:** `#f8fafc`
- **Card / Panel Background:** `rgba(255, 255, 255, 0.8)`
- **Hover Background:** `rgba(241, 245, 249, 0.9)`
- **Text Primary:** `#0f172a`
- **Text Secondary:** `#475569`
- **Border Glass:** `1px solid rgba(0, 0, 0, 0.08)`

---

## 3. Component Details & Navigation

### Global Header / Navigation Bar (`nav.navbar`)
- **Logo:** `Hung Anh Nguyen` with gradient fill text.
- **Nav Links (Exact Order):**
  1. Education (`education.html`)
  2. Experience (`experience.html`)
  3. Projects (`projects.html`)
  4. Publications (`publications.html`)
  5. Skills (`skills.html`)
  6. Honors & Awards (`honors.html`)
  7. Certifications (`certifications.html`)
  8. Links (`links.html`)
- **Controls Right:**
  - `[EN | VI]` Language Switcher button (stores preference in `localStorage`).
  - `[☀️ / 🌙]` Theme Toggle button (stores preference in `localStorage`).

---

## 4. Page Contents & Features

1. **`index.html` (Home):**
   - Hero section with title "AI & Backend Developer", summary statement, quick action buttons to Projects and Links.
   - Quick overview cards linking to major sections.

2. **`education.html` (Education):**
   - Industrial University of Ho Chi Minh City (BS in Computer Science, 2026).
   - Cumulative GPA: `3.31/4.00` (Classification: Very Good).
   - Completed Credits: `156`.

3. **`experience.html` (Experience):**
   - **Digitech Solution** | AI Engineer (Sep 2025 – Nov 2025): B2B YellowPages ETL pipelines, DigiZaloAI customer service chatbot.
   - **Stopest Co., Ltd.** | QA Tester (Mar 2023 – Jun 2023): Manual web/mobile UI/UX testing, visual bug reporting.

4. **`projects.html` (Projects):**
   - Interactive Filter Tags: `[All]`, `[AI & Backend]`, `[Fullstack]`, `[Automation]`.
   - Projects List:
     - **Hach Thach Thon:** Pay-per-word billing, AI translation engine, LLM integration, EPUB/DOCX export. Live: `hachthachthon.site`.
     - **Smart News AI:** Financial news ETL, real-time sentiment classification, Web Zalo chatbot. Live: `smart-new-ai-client.vercel.app`.
     - **Cudo Market:** Currency market intelligence platform (candlestick, COT, seasonality). GitHub: `github.com/Hung000anh/cudo-market`, Live: `cudomarket.streamlit.app`.
     - **Excerpo:** Bulk text/chapter extractor for web novels. GitHub: `github.com/Hung000anh/excerpo`.

5. **`publications.html` (Publications):**
   - *News Website Sentiment Analysis System and User Support Chatbot* (2025).
   - Authors: Anh Nguyen, Thiet Pham, Thang Truong.
   - Journal: Student Scientific Research Communication (SSRC), Vol. 1, No. 2.

6. **`skills.html` (Skills Matrix):**
   - Grid cards grouped by: Languages, Frameworks/Libraries, Databases, Tools & Platforms.

7. **`honors.html` (Honors & Awards):**
   - Academic Excellence Scholarship (Highest GPA: 3.60/4.00 across 3 semesters).

8. **`certifications.html` (Certifications):**
   - TOEIC Listening & Reading (2026), CertNexus Ethical Emerging Technologist (2025), Academic English Writing (2025), Java FullStack Developer (2024), SDLC (2024), Web Design for Everybody (2024), Java Testing (2024), Academic Skills for University Success (2023).

9. **`links.html` (Links & Contact):**
   - Large interactive cards with neon glow for LinkedIn (`Hung Anh Nguyen`), GitHub (`Hung000anh`), and Email.
