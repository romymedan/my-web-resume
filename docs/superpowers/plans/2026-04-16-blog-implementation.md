# Blog Feature Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add a static HTML blog to romymedan.com with a first post, a listing page, and a homepage teaser section.

**Architecture:** Three new/modified HTML files with no build tools. Each page embeds its own CSS/JS matching the existing design system. Blog posts live in `blog/posts/`, the listing page at `blog/index.html`, and the homepage (`index.html`) gets a nav link + teaser section.

**Tech Stack:** HTML, CSS, vanilla JavaScript, GitHub Pages

---

## File Structure

```
my-web-resume/
├── index.html                                              # MODIFY: add "Blog" nav link + teaser section
├── blog/
│   ├── index.html                                          # CREATE: blog listing page
│   └── posts/
│       └── week-1-why-i-started-building-agenticqa.html    # CREATE: first blog post
```

---

### Task 1: Create the First Blog Post Page

**Files:**
- Create: `blog/posts/week-1-why-i-started-building-agenticqa.html`

This is the core deliverable — a standalone HTML page with the full design system embedded.

- [ ] **Step 1: Create the directory structure**

```bash
mkdir -p blog/posts
```

- [ ] **Step 2: Create the blog post HTML file**

Create `blog/posts/week-1-why-i-started-building-agenticqa.html` with the complete content below. This is a standalone page with all CSS embedded (same pattern as `index.html`).

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Why I Started Building AgenticQA - Romy Medan</title>
  <meta name="description" content="Week 1: I've been in QA for more than a decade. Everything else is automated, but QA is still stuck in 2010. So I started building AgenticQA." />
  <link rel="icon" type="image/svg+xml" href="../../assets/favicon.svg" />
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,300;1,400&family=Nunito:wght@300;400;500;600;700&display=swap" rel="stylesheet" />
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    :root {
      --cream: #FAF7F2;
      --cream-dark: #F0EBE1;
      --rose: #C8857A;
      --rose-light: #F0D5D0;
      --rose-deep: #A85F55;
      --sage: #7A9E8A;
      --sage-light: #C8DDD0;
      --sage-dark: #4E7260;
      --plum: #7B5EA7;
      --plum-light: #E4DAF5;
      --amber: #D4923A;
      --amber-light: #F5E0C0;
      --warm-brown: #7A5C4E;
      --text-dark: #3A2E28;
      --text-mid: #6B5248;
      --text-light: #9E8278;
      --font-display: 'Cormorant Garamond', Georgia, serif;
      --font-body: 'Nunito', sans-serif;
    }

    html { scroll-behavior: smooth; }

    body {
      background: var(--cream);
      color: var(--text-dark);
      font-family: var(--font-body);
      font-size: 16px;
      line-height: 1.7;
      overflow-x: hidden;
    }

    /* ——— NAV ——— */
    nav {
      position: fixed;
      top: 0; left: 0; right: 0;
      z-index: 100;
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 1.1rem 3rem;
      background: rgba(250, 247, 242, 0.88);
      backdrop-filter: blur(18px);
      -webkit-backdrop-filter: blur(18px);
      border-bottom: 1px solid rgba(200,133,122,0.12);
      transition: box-shadow 0.4s, background 0.4s;
    }
    nav.scrolled {
      box-shadow: 0 4px 32px rgba(122,94,78,0.10);
      background: rgba(250, 247, 242, 0.95);
    }
    .nav-logo {
      font-family: var(--font-display);
      font-size: 1.35rem;
      font-weight: 400;
      color: var(--text-dark);
      text-decoration: none;
      letter-spacing: 0.02em;
    }
    .nav-logo span { color: var(--rose); font-style: italic; }
    .nav-links { display: flex; gap: 2rem; list-style: none; }
    .nav-links a {
      font-size: 0.78rem;
      font-weight: 600;
      letter-spacing: 0.13em;
      text-transform: uppercase;
      color: var(--text-mid);
      text-decoration: none;
      transition: color 0.25s;
      position: relative;
    }
    .nav-links a::after {
      content: '';
      position: absolute;
      bottom: -3px; left: 0; right: 0;
      height: 1.5px;
      background: var(--rose);
      transform: scaleX(0);
      transform-origin: right;
      transition: transform 0.3s;
    }
    .nav-links a:hover { color: var(--rose); }
    .nav-links a:hover::after { transform: scaleX(1); transform-origin: left; }
    .nav-links a.active { color: var(--rose); }
    .nav-links a.active::after { transform: scaleX(1); transform-origin: left; }
    .nav-toggle {
      display: none;
      background: none; border: none; cursor: pointer;
      width: 28px; height: 20px;
      position: relative; z-index: 101;
    }
    .nav-toggle span {
      display: block;
      width: 100%; height: 2px;
      background: var(--text-dark);
      position: absolute; left: 0;
      transition: all 0.35s;
    }
    .nav-toggle span:nth-child(1) { top: 0; }
    .nav-toggle span:nth-child(2) { top: 9px; }
    .nav-toggle span:nth-child(3) { top: 18px; }
    .nav-toggle.active span:nth-child(1) { top: 9px; transform: rotate(45deg); }
    .nav-toggle.active span:nth-child(2) { opacity: 0; }
    .nav-toggle.active span:nth-child(3) { top: 9px; transform: rotate(-45deg); }

    /* ——— POST ——— */
    .post-container {
      max-width: 720px;
      margin: 0 auto;
      padding: 6rem 1.5rem 4rem;
    }
    .back-link {
      display: inline-flex;
      align-items: center;
      gap: 6px;
      font-size: 0.85rem;
      font-weight: 600;
      color: var(--sage-dark);
      text-decoration: none;
      margin-bottom: 2.5rem;
      transition: color 0.2s;
    }
    .back-link:hover { color: var(--sage); }
    .post-meta {
      font-size: 0.72rem;
      font-weight: 700;
      letter-spacing: 0.14em;
      text-transform: uppercase;
      color: var(--sage);
      margin-bottom: 0.75rem;
    }
    .post-title {
      font-family: var(--font-display);
      font-size: clamp(2rem, 5vw, 2.8rem);
      font-weight: 400;
      line-height: 1.15;
      color: var(--text-dark);
      margin-bottom: 1.2rem;
    }
    .post-tags {
      display: flex;
      gap: 0.5rem;
      flex-wrap: wrap;
      margin-bottom: 2rem;
    }
    .tag {
      font-size: 0.68rem;
      font-weight: 600;
      letter-spacing: 0.04em;
      padding: 0.25rem 0.75rem;
      border-radius: 20px;
      background: var(--plum-light);
      color: var(--plum);
    }
    .tag.sage { background: var(--sage-light); color: var(--sage-dark); }
    .tag.rose { background: var(--rose-light); color: var(--rose-deep); }
    .tag.amber { background: var(--amber-light); color: var(--amber); }
    .post-divider {
      height: 2px;
      background: linear-gradient(90deg, var(--rose-light), var(--sage-light), var(--plum-light));
      margin-bottom: 2.5rem;
      border: none;
    }

    /* ——— POST BODY ——— */
    .post-body p {
      font-size: 1.05rem;
      line-height: 1.8;
      color: var(--text-dark);
      margin-bottom: 1.5rem;
    }
    .post-body h2 {
      font-family: var(--font-display);
      font-size: 1.8rem;
      font-weight: 400;
      color: var(--text-dark);
      margin: 2.5rem 0 1rem;
    }
    .post-body ol {
      margin: 1rem 0 1.5rem 0;
      padding: 0;
      list-style: none;
      counter-reset: steps;
    }
    .post-body ol li {
      counter-increment: steps;
      position: relative;
      padding: 0.75rem 1rem 0.75rem 3.5rem;
      margin-bottom: 0.5rem;
      background: rgba(122, 158, 138, 0.06);
      border-radius: 8px;
      font-size: 0.95rem;
      line-height: 1.6;
      color: var(--text-mid);
    }
    .post-body ol li::before {
      content: counter(steps);
      position: absolute;
      left: 1rem;
      top: 0.75rem;
      width: 1.6rem;
      height: 1.6rem;
      background: var(--sage);
      color: white;
      border-radius: 50%;
      font-size: 0.75rem;
      font-weight: 700;
      display: flex;
      align-items: center;
      justify-content: center;
    }
    .post-body .tech-stack {
      display: flex;
      flex-wrap: wrap;
      gap: 0.4rem;
      margin: 1rem 0 1.5rem;
    }
    .post-body .tech-stack span {
      font-size: 0.72rem;
      font-weight: 600;
      padding: 0.3rem 0.7rem;
      border-radius: 16px;
      background: var(--cream-dark);
      color: var(--text-mid);
      border: 1px solid rgba(200,133,122,0.15);
    }
    .post-body em { color: var(--text-mid); font-style: italic; }
    .post-body strong { font-weight: 700; color: var(--text-dark); }

    /* ——— POST FOOTER ——— */
    .post-footer {
      margin-top: 3rem;
      padding-top: 2rem;
      border-top: 1px solid var(--cream-dark);
    }
    .post-footer-actions {
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
      gap: 1rem;
    }
    .share-link {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      font-size: 0.85rem;
      font-weight: 600;
      color: var(--plum);
      text-decoration: none;
      padding: 0.5rem 1.2rem;
      border: 1.5px solid var(--plum-light);
      border-radius: 24px;
      transition: all 0.2s;
    }
    .share-link:hover { background: var(--plum-light); }
    .follow-cta {
      font-size: 0.85rem;
      color: var(--text-light);
    }
    .follow-cta a {
      color: var(--rose);
      text-decoration: none;
      font-weight: 600;
    }
    .follow-cta a:hover { text-decoration: underline; }

    /* ——— FOOTER ——— */
    footer {
      text-align: center; padding: 2rem 5%;
      font-size: 0.75rem; color: var(--text-light);
      border-top: 1px solid var(--rose-light);
    }

    /* ——— RESPONSIVE ——— */
    @media (max-width: 750px) {
      nav { padding: 1rem 1.5rem; }
      .nav-toggle { display: block; }
      .nav-links {
        position: fixed;
        top: 0; right: 0;
        width: min(320px, 85vw);
        height: 100vh;
        background: var(--cream);
        flex-direction: column;
        padding: 5rem 2rem 2rem;
        gap: 1.6rem;
        box-shadow: -8px 0 40px rgba(122,94,78,0.12);
        transform: translateX(100%);
        transition: transform 0.4s cubic-bezier(0.23, 1, 0.32, 1);
      }
      .nav-links.open { transform: translateX(0); }
      .nav-links a { font-size: 0.9rem; }
      .mobile-overlay {
        position: fixed; inset: 0; z-index: 99;
        background: rgba(58,46,40,0.3);
        backdrop-filter: blur(4px);
        -webkit-backdrop-filter: blur(4px);
        opacity: 0; pointer-events: none;
        transition: opacity 0.3s;
      }
      .mobile-overlay.visible { opacity: 1; pointer-events: auto; }
      .post-container { padding: 5rem 1.2rem 3rem; }
      .post-title { font-size: clamp(1.6rem, 7vw, 2.2rem); }
      .post-body ol li { padding-left: 3rem; }
      .post-body ol li::before { left: 0.75rem; }
      .post-footer-actions { flex-direction: column; align-items: flex-start; }
    }

    /* Focus styles */
    a:focus-visible, button:focus-visible {
      outline: 2px solid var(--rose);
      outline-offset: 3px;
      border-radius: 4px;
    }

    /* Reduced motion */
    @media (prefers-reduced-motion: reduce) {
      *, *::before, *::after {
        animation-duration: 0.01ms !important;
        animation-iteration-count: 1 !important;
        transition-duration: 0.01ms !important;
      }
    }
  </style>
</head>
<body>

  <!-- NAV -->
  <nav id="navbar">
    <a class="nav-logo" href="../../">Romy <span>Medan</span></a>
    <button class="nav-toggle" id="navToggle" aria-label="Toggle navigation menu" aria-expanded="false">
      <span></span><span></span><span></span>
    </button>
    <ul class="nav-links" id="navLinks">
      <li><a href="../../#experience-bg">Experience</a></li>
      <li><a href="../../#projects-bg">Projects</a></li>
      <li><a href="../" class="active">Blog</a></li>
      <li><a href="../../#skills-bg">Skills</a></li>
      <li><a href="../../#interests-bg">Interests</a></li>
      <li><a href="../../#contact-bg">Contact</a></li>
    </ul>
  </nav>
  <div class="mobile-overlay" id="mobileOverlay"></div>

  <article class="post-container">
    <a class="back-link" href="../">&larr; All posts</a>

    <div class="post-meta">Week 1 &middot; April 16, 2026</div>
    <h1 class="post-title">Why I Started Building AgenticQA</h1>
    <div class="post-tags">
      <span class="tag sage">QA</span>
      <span class="tag">AI Agents</span>
      <span class="tag rose">Playwright</span>
      <span class="tag amber">Side Project</span>
    </div>
    <hr class="post-divider" />

    <div class="post-body">
      <p>I've been in QA for more than a decade. Amazon, Honeywell, NCR. Led teams, built frameworks, caught bugs nobody else would have found.</p>

      <p>And honestly&hellip; it's crazy how innovation has been hard to adopt for QA teams.</p>

      <p>We're still doing the same thing we did in 2010: read a Jira ticket, write test cases, run them, file bugs with screenshots and steps to reproduce. Retest, reopen, all over again. Every sprint. Every ticket.</p>

      <p>Everything else is now automated: from coding, deployments, infrastructure, and even code reviews. But QA? We're still copy-pasting into Jira.</p>

      <h2>Going Deep on AI Agents</h2>

      <p>Around the same time, I started testing agentic systems and chatbots, and decided to go deep on learning how AI agents work. What they can actually do. How they fail. How you orchestrate them into something useful. And I thought: why not point that at the problem I know best?</p>

      <p>So I started building. On my own time. No sprint, no ticket, no one asking for it.</p>

      <h2>The Pipeline</h2>

      <p>I'm calling it <strong>AgenticQA</strong>. It's an 8-step AI pipeline where each step is its own agent, running sequentially like a real QA workflow:</p>

      <ol>
        <li>Reads the Jira ticket and acceptance criteria</li>
        <li>Explores the target URL with a real browser, navigates pages, takes snapshots, reads content</li>
        <li>Enriches the criteria using the ticket, Figma designs, and the explorer's findings</li>
        <li>Generates test cases, including happy paths and edge cases</li>
        <li>Executes them in a real browser using Playwright and captures failure screenshots</li>
        <li>Writes bug reports in Jira format, including steps to reproduce, severity, and environment</li>
        <li>Runs WCAG 2.1 accessibility checks with axe-core</li>
        <li>Outputs a reusable Playwright test script</li>
      </ol>

      <p>Built with:</p>
      <div class="tech-stack">
        <span>TypeScript</span>
        <span>React</span>
        <span>Express</span>
        <span>Playwright</span>
        <span>Claude API</span>
        <span>axe-core</span>
        <span>Railway</span>
      </div>

      <p>Real-time updates stream to a dashboard so you can watch each agent work. Deployed on Railway as a single service.</p>

      <h2>What's Next</h2>

      <p>It's not done. I'm still building, still breaking things, still learning how agentic systems fail in ways I didn't expect. But it already reads real tickets, explores real pages, runs a real browser, and files real bugs.</p>

      <p>I'm not trying to replace QA engineers. I'm trying to stop wasting their time on work that a machine should've been doing years ago.</p>

      <p><em>This is post one of a series. I'll share what I'm building as I go, what's working, what's not, and what I'm still figuring out along the way.</em></p>
    </div>

    <div class="post-footer">
      <div class="post-footer-actions">
        <a class="share-link" href="https://www.linkedin.com/in/romymedan" target="_blank" rel="noopener">
          <svg width="14" height="14" viewBox="0 0 24 24" fill="currentColor"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 0 1-2.063-2.065 2.064 2.064 0 1 1 2.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>
          Share on LinkedIn
        </a>
        <span class="follow-cta">Follow the journey on <a href="https://www.linkedin.com/in/romymedan" target="_blank" rel="noopener">LinkedIn</a></span>
      </div>
    </div>
  </article>

  <footer>
    <p>Crafted with care &middot; Romy Medan &middot; Atlanta Metro Area</p>
  </footer>

  <script>
    // Nav scroll shadow
    const navbar = document.getElementById('navbar');
    window.addEventListener('scroll', () => {
      navbar.classList.toggle('scrolled', window.scrollY > 30);
    }, { passive: true });

    // Mobile nav toggle
    const navToggle = document.getElementById('navToggle');
    const navLinks = document.getElementById('navLinks');
    const overlay = document.getElementById('mobileOverlay');

    function closeMenu() {
      navToggle.classList.remove('active');
      navToggle.setAttribute('aria-expanded', 'false');
      navLinks.classList.remove('open');
      overlay.classList.remove('visible');
      document.body.style.overflow = '';
    }

    navToggle.addEventListener('click', () => {
      const isOpen = navLinks.classList.contains('open');
      if (isOpen) {
        closeMenu();
      } else {
        navToggle.classList.add('active');
        navToggle.setAttribute('aria-expanded', 'true');
        navLinks.classList.add('open');
        overlay.classList.add('visible');
        document.body.style.overflow = 'hidden';
      }
    });

    overlay.addEventListener('click', closeMenu);
    navLinks.querySelectorAll('a').forEach(link => {
      link.addEventListener('click', closeMenu);
    });
  </script>
</body>
</html>
```

- [ ] **Step 3: Verify the post renders correctly**

Open in a browser:
```bash
open blog/posts/week-1-why-i-started-building-agenticqa.html
```

Verify:
- Nav bar displays with "Blog" highlighted
- Post title, meta, tags, and divider render correctly
- 8-step pipeline shows as numbered circles with sage backgrounds
- Tech stack pills display
- "Share on LinkedIn" and "Follow the journey" links work
- Mobile hamburger menu works (resize browser to <750px)
- "All posts" back link points to `../`

- [ ] **Step 4: Commit**

```bash
git add blog/posts/week-1-why-i-started-building-agenticqa.html
git commit -m "feat: add first blog post - Why I Started Building AgenticQA"
```

---

### Task 2: Create the Blog Listing Page

**Files:**
- Create: `blog/index.html`

- [ ] **Step 1: Create the listing page**

Create `blog/index.html` with the complete content below:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Blog - Romy Medan</title>
  <meta name="description" content="Weekly notes on building AgenticQA — an AI-powered QA pipeline. What's working, what's breaking, and what I'm learning." />
  <link rel="icon" type="image/svg+xml" href="../assets/favicon.svg" />
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,300;1,400&family=Nunito:wght@300;400;500;600;700&display=swap" rel="stylesheet" />
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    :root {
      --cream: #FAF7F2;
      --cream-dark: #F0EBE1;
      --rose: #C8857A;
      --rose-light: #F0D5D0;
      --rose-deep: #A85F55;
      --sage: #7A9E8A;
      --sage-light: #C8DDD0;
      --sage-dark: #4E7260;
      --plum: #7B5EA7;
      --plum-light: #E4DAF5;
      --amber: #D4923A;
      --amber-light: #F5E0C0;
      --warm-brown: #7A5C4E;
      --text-dark: #3A2E28;
      --text-mid: #6B5248;
      --text-light: #9E8278;
      --font-display: 'Cormorant Garamond', Georgia, serif;
      --font-body: 'Nunito', sans-serif;
    }

    html { scroll-behavior: smooth; }

    body {
      background: var(--cream);
      color: var(--text-dark);
      font-family: var(--font-body);
      font-size: 16px;
      line-height: 1.7;
      overflow-x: hidden;
    }

    /* ——— NAV ——— */
    nav {
      position: fixed;
      top: 0; left: 0; right: 0;
      z-index: 100;
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 1.1rem 3rem;
      background: rgba(250, 247, 242, 0.88);
      backdrop-filter: blur(18px);
      -webkit-backdrop-filter: blur(18px);
      border-bottom: 1px solid rgba(200,133,122,0.12);
      transition: box-shadow 0.4s, background 0.4s;
    }
    nav.scrolled {
      box-shadow: 0 4px 32px rgba(122,94,78,0.10);
      background: rgba(250, 247, 242, 0.95);
    }
    .nav-logo {
      font-family: var(--font-display);
      font-size: 1.35rem;
      font-weight: 400;
      color: var(--text-dark);
      text-decoration: none;
      letter-spacing: 0.02em;
    }
    .nav-logo span { color: var(--rose); font-style: italic; }
    .nav-links { display: flex; gap: 2rem; list-style: none; }
    .nav-links a {
      font-size: 0.78rem;
      font-weight: 600;
      letter-spacing: 0.13em;
      text-transform: uppercase;
      color: var(--text-mid);
      text-decoration: none;
      transition: color 0.25s;
      position: relative;
    }
    .nav-links a::after {
      content: '';
      position: absolute;
      bottom: -3px; left: 0; right: 0;
      height: 1.5px;
      background: var(--rose);
      transform: scaleX(0);
      transform-origin: right;
      transition: transform 0.3s;
    }
    .nav-links a:hover { color: var(--rose); }
    .nav-links a:hover::after { transform: scaleX(1); transform-origin: left; }
    .nav-links a.active { color: var(--rose); }
    .nav-links a.active::after { transform: scaleX(1); transform-origin: left; }
    .nav-toggle {
      display: none;
      background: none; border: none; cursor: pointer;
      width: 28px; height: 20px;
      position: relative; z-index: 101;
    }
    .nav-toggle span {
      display: block;
      width: 100%; height: 2px;
      background: var(--text-dark);
      position: absolute; left: 0;
      transition: all 0.35s;
    }
    .nav-toggle span:nth-child(1) { top: 0; }
    .nav-toggle span:nth-child(2) { top: 9px; }
    .nav-toggle span:nth-child(3) { top: 18px; }
    .nav-toggle.active span:nth-child(1) { top: 9px; transform: rotate(45deg); }
    .nav-toggle.active span:nth-child(2) { opacity: 0; }
    .nav-toggle.active span:nth-child(3) { top: 9px; transform: rotate(-45deg); }

    /* ——— SCROLL REVEAL ——— */
    .reveal {
      opacity: 0;
      transform: translateY(36px);
      transition: opacity 0.7s cubic-bezier(0.23, 1, 0.32, 1), transform 0.7s cubic-bezier(0.23, 1, 0.32, 1);
    }
    .reveal.visible { opacity: 1; transform: translateY(0); }
    .reveal-delay-1 { transition-delay: 0.12s; }
    .reveal-delay-2 { transition-delay: 0.24s; }
    .reveal-delay-3 { transition-delay: 0.36s; }

    /* ——— LISTING ——— */
    .listing-container {
      max-width: 720px;
      margin: 0 auto;
      padding: 6rem 1.5rem 4rem;
    }
    .listing-header {
      text-align: center;
      margin-bottom: 3rem;
    }
    .section-label {
      font-size: 0.7rem; font-weight: 700; letter-spacing: 0.22em;
      text-transform: uppercase; color: var(--rose); margin-bottom: 0.4rem;
    }
    .section-title {
      font-family: var(--font-display);
      font-size: clamp(2rem, 4vw, 2.9rem);
      font-weight: 300; line-height: 1.15; color: var(--text-dark); margin-bottom: 0.5rem;
    }
    .section-bar {
      width: 56px; height: 3px; border-radius: 2px;
      background: linear-gradient(90deg, var(--rose), var(--plum), var(--sage));
      margin: 0.9rem auto 1.5rem;
    }
    .listing-subtitle {
      font-size: 0.95rem;
      color: var(--text-mid);
      line-height: 1.6;
      max-width: 560px;
      margin: 0 auto;
    }

    .posts-list {
      display: flex;
      flex-direction: column;
      gap: 1rem;
    }
    .post-card {
      padding: 1.5rem 1.8rem;
      background: white;
      border-radius: 10px;
      border-left: 4px solid var(--sage);
      box-shadow: 0 2px 12px rgba(122,94,78,0.05);
      text-decoration: none;
      color: inherit;
      display: block;
      transition: transform 0.2s, box-shadow 0.2s;
    }
    .post-card:hover {
      transform: translateY(-2px);
      box-shadow: 0 6px 24px rgba(122,94,78,0.1);
    }
    .post-card.rose-border { border-left-color: var(--rose); }
    .post-card.plum-border { border-left-color: var(--plum); }
    .post-card.amber-border { border-left-color: var(--amber); }
    .post-card-meta {
      font-size: 0.7rem;
      font-weight: 700;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      margin-bottom: 0.4rem;
      color: var(--sage);
    }
    .post-card-meta.rose { color: var(--rose); }
    .post-card-meta.plum { color: var(--plum); }
    .post-card-meta.amber { color: var(--amber); }
    .post-card-title {
      font-family: var(--font-display);
      font-size: 1.35rem;
      font-weight: 400;
      color: var(--text-dark);
      margin-bottom: 0.4rem;
      line-height: 1.3;
    }
    .post-card-excerpt {
      font-size: 0.88rem;
      color: var(--text-mid);
      line-height: 1.6;
      margin-bottom: 0.6rem;
    }
    .post-card-tags {
      display: flex;
      gap: 0.4rem;
      flex-wrap: wrap;
    }
    .tag {
      font-size: 0.65rem;
      font-weight: 600;
      letter-spacing: 0.04em;
      padding: 0.22rem 0.6rem;
      border-radius: 16px;
      background: var(--plum-light);
      color: var(--plum);
    }
    .tag.sage { background: var(--sage-light); color: var(--sage-dark); }
    .tag.rose { background: var(--rose-light); color: var(--rose-deep); }
    .tag.amber { background: var(--amber-light); color: var(--amber); }

    /* ——— FOOTER ——— */
    footer {
      text-align: center; padding: 2rem 5%;
      font-size: 0.75rem; color: var(--text-light);
      border-top: 1px solid var(--rose-light);
    }

    /* ——— RESPONSIVE ——— */
    @media (max-width: 750px) {
      nav { padding: 1rem 1.5rem; }
      .nav-toggle { display: block; }
      .nav-links {
        position: fixed;
        top: 0; right: 0;
        width: min(320px, 85vw);
        height: 100vh;
        background: var(--cream);
        flex-direction: column;
        padding: 5rem 2rem 2rem;
        gap: 1.6rem;
        box-shadow: -8px 0 40px rgba(122,94,78,0.12);
        transform: translateX(100%);
        transition: transform 0.4s cubic-bezier(0.23, 1, 0.32, 1);
      }
      .nav-links.open { transform: translateX(0); }
      .nav-links a { font-size: 0.9rem; }
      .mobile-overlay {
        position: fixed; inset: 0; z-index: 99;
        background: rgba(58,46,40,0.3);
        backdrop-filter: blur(4px);
        -webkit-backdrop-filter: blur(4px);
        opacity: 0; pointer-events: none;
        transition: opacity 0.3s;
      }
      .mobile-overlay.visible { opacity: 1; pointer-events: auto; }
      .listing-container { padding: 5rem 1.2rem 3rem; }
      .post-card { padding: 1.2rem 1.4rem; }
    }

    /* Focus styles */
    a:focus-visible, button:focus-visible {
      outline: 2px solid var(--rose);
      outline-offset: 3px;
      border-radius: 4px;
    }

    /* Reduced motion */
    @media (prefers-reduced-motion: reduce) {
      *, *::before, *::after {
        animation-duration: 0.01ms !important;
        animation-iteration-count: 1 !important;
        transition-duration: 0.01ms !important;
      }
      .reveal { opacity: 1; transform: none; }
    }
  </style>
</head>
<body>

  <!-- NAV -->
  <nav id="navbar">
    <a class="nav-logo" href="../">Romy <span>Medan</span></a>
    <button class="nav-toggle" id="navToggle" aria-label="Toggle navigation menu" aria-expanded="false">
      <span></span><span></span><span></span>
    </button>
    <ul class="nav-links" id="navLinks">
      <li><a href="../#experience-bg">Experience</a></li>
      <li><a href="../#projects-bg">Projects</a></li>
      <li><a href="./" class="active">Blog</a></li>
      <li><a href="../#skills-bg">Skills</a></li>
      <li><a href="../#interests-bg">Interests</a></li>
      <li><a href="../#contact-bg">Contact</a></li>
    </ul>
  </nav>
  <div class="mobile-overlay" id="mobileOverlay"></div>

  <main class="listing-container">
    <div class="listing-header">
      <p class="section-label reveal">What I'm Building</p>
      <h2 class="section-title reveal">The AgenticQA Journey</h2>
      <div class="section-bar reveal"></div>
      <p class="listing-subtitle reveal">Weekly notes on building an AI-powered QA pipeline &mdash; what's working, what's breaking, and what I'm learning along the way.</p>
    </div>

    <div class="posts-list">
      <!-- Week 1 -->
      <a class="post-card reveal" href="posts/week-1-why-i-started-building-agenticqa.html">
        <div class="post-card-meta">Week 1 &middot; April 16, 2026</div>
        <h3 class="post-card-title">Why I Started Building AgenticQA</h3>
        <p class="post-card-excerpt">I've been in QA for more than a decade. Everything else is now automated, but QA is still stuck in 2010. So I started building.</p>
        <div class="post-card-tags">
          <span class="tag sage">QA</span>
          <span class="tag">AI Agents</span>
          <span class="tag rose">Playwright</span>
          <span class="tag amber">Side Project</span>
        </div>
      </a>
    </div>
  </main>

  <footer>
    <p>Crafted with care &middot; Romy Medan &middot; Atlanta Metro Area</p>
  </footer>

  <script>
    // Nav scroll shadow
    const navbar = document.getElementById('navbar');
    window.addEventListener('scroll', () => {
      navbar.classList.toggle('scrolled', window.scrollY > 30);
    }, { passive: true });

    // Mobile nav toggle
    const navToggle = document.getElementById('navToggle');
    const navLinks = document.getElementById('navLinks');
    const overlay = document.getElementById('mobileOverlay');

    function closeMenu() {
      navToggle.classList.remove('active');
      navToggle.setAttribute('aria-expanded', 'false');
      navLinks.classList.remove('open');
      overlay.classList.remove('visible');
      document.body.style.overflow = '';
    }

    navToggle.addEventListener('click', () => {
      const isOpen = navLinks.classList.contains('open');
      if (isOpen) {
        closeMenu();
      } else {
        navToggle.classList.add('active');
        navToggle.setAttribute('aria-expanded', 'true');
        navLinks.classList.add('open');
        overlay.classList.add('visible');
        document.body.style.overflow = 'hidden';
      }
    });

    overlay.addEventListener('click', closeMenu);
    navLinks.querySelectorAll('a').forEach(link => {
      link.addEventListener('click', closeMenu);
    });

    // Scroll reveal
    const reveals = document.querySelectorAll('.reveal');
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(e => {
        if (e.isIntersecting) {
          e.target.classList.add('visible');
          observer.unobserve(e.target);
        }
      });
    }, { threshold: 0.12 });
    reveals.forEach(el => observer.observe(el));
  </script>
</body>
</html>
```

- [ ] **Step 2: Verify the listing page renders correctly**

Open in a browser:
```bash
open blog/index.html
```

Verify:
- Page header shows "The AgenticQA Journey" with subtitle
- Week 1 post card displays with sage left border
- Card is clickable and navigates to the post page
- Tags display correctly
- Mobile hamburger menu works
- Scroll reveal animations trigger

- [ ] **Step 3: Commit**

```bash
git add blog/index.html
git commit -m "feat: add blog listing page"
```

---

### Task 3: Add Blog Nav Link and Teaser Section to Homepage

**Files:**
- Modify: `index.html:764-769` (nav links)
- Modify: `index.html:1018-1020` (insert teaser section between Projects and Skills)
- Modify: `index.html:475` (add CSS for teaser section)

- [ ] **Step 1: Add "Blog" to the navigation links**

In `index.html`, find the nav links (line 764-769) and add the Blog link between Projects and Skills:

Replace:
```html
    <ul class="nav-links" id="navLinks">
      <li><a href="#experience-bg">Experience</a></li>
      <li><a href="#projects-bg">Projects</a></li>
      <li><a href="#skills-bg">Skills</a></li>
      <li><a href="#interests-bg">Interests</a></li>
      <li><a href="#contact-bg">Contact</a></li>
    </ul>
```

With:
```html
    <ul class="nav-links" id="navLinks">
      <li><a href="#experience-bg">Experience</a></li>
      <li><a href="#projects-bg">Projects</a></li>
      <li><a href="blog/">Blog</a></li>
      <li><a href="#skills-bg">Skills</a></li>
      <li><a href="#interests-bg">Interests</a></li>
      <li><a href="#contact-bg">Contact</a></li>
    </ul>
```

- [ ] **Step 2: Add CSS for the blog teaser section**

In `index.html`, find the Projects CSS section (`#projects-bg` around line 475) and add the blog teaser CSS after the projects CSS block (before `#skills-bg`). Find this line:

```css
    #skills-bg { background: var(--cream); }
```

And insert before it:

```css
    /* ——— BLOG TEASER ——— */
    #blog-teaser { background: var(--cream); padding: 5rem 0; }
    .blog-teaser-card {
      max-width: 640px;
      margin: 0 auto;
      text-align: left;
      padding: 1.8rem 2rem;
      background: white;
      border-radius: 12px;
      border-left: 4px solid var(--sage);
      box-shadow: 0 2px 16px rgba(122,94,78,0.06);
      transition: transform 0.2s, box-shadow 0.2s;
      text-decoration: none;
      display: block;
      color: inherit;
    }
    .blog-teaser-card:hover {
      transform: translateY(-2px);
      box-shadow: 0 6px 24px rgba(122,94,78,0.1);
    }
    .blog-teaser-meta {
      font-size: 0.72rem;
      font-weight: 700;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      color: var(--sage);
      margin-bottom: 0.5rem;
    }
    .blog-teaser-title {
      font-family: var(--font-display);
      font-size: 1.6rem;
      font-weight: 400;
      color: var(--text-dark);
      margin-bottom: 0.5rem;
      line-height: 1.3;
    }
    .blog-teaser-excerpt {
      font-size: 0.92rem;
      color: var(--text-mid);
      line-height: 1.6;
      margin-bottom: 0.8rem;
    }
    .blog-teaser-tags {
      display: flex;
      gap: 0.4rem;
      flex-wrap: wrap;
      margin-bottom: 0.8rem;
    }
    .blog-teaser-readmore {
      font-size: 0.8rem;
      font-weight: 600;
      color: var(--sage-dark);
    }
    .blog-teaser-viewall {
      display: inline-block;
      margin-top: 1.5rem;
      font-size: 0.85rem;
      font-weight: 600;
      color: var(--rose);
      text-decoration: none;
      transition: color 0.2s;
    }
    .blog-teaser-viewall:hover { color: var(--rose-deep); }

```

- [ ] **Step 3: Add the blog teaser HTML section**

In `index.html`, find the gap between the Projects section closing and the Skills section opening (between lines 1018 and 1020). Find:

```html
  </div>

  <!-- SKILLS -->
```

(This is the end of the projects `</div>` and start of skills.) Insert the teaser section between them:

```html
  </div>

  <!-- BLOG TEASER -->
  <div id="blog-teaser">
    <div class="section-wrap" style="text-align: center;">
      <p class="section-label reveal">What I'm Building</p>
      <h2 class="section-title reveal">From the Blog</h2>
      <div class="section-bar reveal" style="margin-left: auto; margin-right: auto;"></div>

      <a class="blog-teaser-card reveal" href="blog/posts/week-1-why-i-started-building-agenticqa.html">
        <div class="blog-teaser-meta">Week 1 &middot; April 16, 2026</div>
        <h3 class="blog-teaser-title">Why I Started Building AgenticQA</h3>
        <p class="blog-teaser-excerpt">I've been in QA for more than a decade. Everything else is now automated &mdash; from coding, deployments, infrastructure, and even code reviews. But QA? We're still copy-pasting into Jira.</p>
        <div class="blog-teaser-tags">
          <span class="tag sage">QA</span>
          <span class="tag plum">AI Agents</span>
          <span class="tag rose">Playwright</span>
          <span class="tag amber">Side Project</span>
        </div>
        <span class="blog-teaser-readmore">Read more &rarr;</span>
      </a>

      <a class="blog-teaser-viewall reveal" href="blog/">View all posts &rarr;</a>
    </div>
  </div>

  <!-- SKILLS -->
```

- [ ] **Step 4: Verify the homepage changes**

Open in a browser:
```bash
open index.html
```

Verify:
- "Blog" appears in the nav bar between "Projects" and "Skills"
- Clicking "Blog" navigates to `blog/index.html`
- The teaser section appears between Projects and Skills
- Teaser card shows the Week 1 post with correct styling
- Card hover effect works (slight lift + deeper shadow)
- "View all posts" link navigates to `blog/index.html`
- Mobile nav includes "Blog" link
- Scroll reveal animation works on the teaser section
- Overall flow feels natural (Projects → Blog Teaser → Skills)

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: add Blog nav link and teaser section to homepage"
```

---

### Task 4: End-to-End Verification

- [ ] **Step 1: Test the full navigation flow**

Open the homepage and verify this complete flow:

1. Homepage loads → scroll to blog teaser → click the post card → arrives at Week 1 post
2. On the post page → click "← All posts" → arrives at blog listing
3. On the listing page → click Week 1 card → arrives at Week 1 post
4. On any blog page → click "Romy Medan" logo → returns to homepage
5. On any blog page → click nav links (Experience, Projects, Skills, etc.) → navigates to homepage sections

- [ ] **Step 2: Test responsive behavior**

Resize browser to mobile width (<750px) and verify:
- Hamburger menu appears on all three pages
- Blog link is in the mobile menu
- Post content is readable and properly padded
- Teaser card is full-width on mobile
- Ordered list items don't overflow

- [ ] **Step 3: Final commit (if any fixes needed)**

If any fixes were made during verification:
```bash
git add -A
git commit -m "fix: blog responsive and navigation fixes"
```
