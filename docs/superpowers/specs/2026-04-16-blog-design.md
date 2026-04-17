# Blog Feature Design — romymedan.com

## Overview

Add a static HTML blog to romymedan.com for weekly journal entries documenting the AgenticQA project. No build tools, no dependencies — pure HTML/CSS/JS matching the existing site's design system.

## Content Strategy

- Weekly posts cross-posted from LinkedIn (same content, formatted for the web)
- Tone: honest, personal, technically deep — dev journal style
- First post: "Why I Started Building AgenticQA" (LinkedIn post from April 16, 2026)

## File Structure

```
my-web-resume/
├── index.html                                              # Modified: add nav link + teaser section
├── blog/
│   ├── index.html                                          # Blog listing page
│   └── posts/
│       └── week-1-why-i-started-building-agenticqa.html    # First post
```

Each new weekly post is a single HTML file in `blog/posts/`. The listing page and homepage teaser are updated manually to include the new entry.

## Changes to index.html (Homepage)

### 1. Navigation Link

Add "Blog" to the nav bar between "Projects" and "Skills":

```
Experience | Projects | Blog | Skills | Interests | Contact
```

Links to `blog/` (relative path, compatible with GitHub Pages custom domain).

### 2. "From the Blog" Teaser Section

Placed between the Projects and Skills sections. Contains:

- Section label: "What I'm Building"
- Section title: "From the Blog"
- Gradient section bar (same as other sections)
- One card showing the latest post: week number, date, title, 1-2 line excerpt, tags, "Read more" link
- "View all posts" link below the card
- Card has white background, sage left border, hover lift effect

When a new post is published, update this teaser's content (~5 lines of HTML).

## Blog Listing Page (`blog/index.html`)

Standalone HTML page with the full design system embedded (same approach as `index.html`).

### Structure

- Same nav bar as homepage, with "Blog" link visually active
- Page header:
  - Section label: "What I'm Building"
  - Section title: "The AgenticQA Journey"
  - Gradient section bar
  - Subtitle: "Weekly notes on building an AI-powered QA pipeline — what's working, what's breaking, and what I'm learning along the way."
- Post list: stacked cards, newest first
- Same footer as homepage
- Scroll reveal animations via IntersectionObserver

### Post Card Design

Each card in the listing:

- White background, rounded corners, subtle shadow
- Colored left border cycling through: sage → rose → plum → amber (repeating)
- Week number + date (small, uppercase, colored to match border)
- Post title (Cormorant Garamond, ~1.35rem)
- 1-2 line excerpt (Nunito, text-mid color)
- Tag pills (same style as skill tags on homepage)
- Entire card is a clickable link to the full post
- Hover: slight lift + deeper shadow

## Individual Blog Post Page (`blog/posts/*.html`)

Standalone HTML page, same design system.

### Layout

Single centered column, max-width 720px. Clean and minimal, no sidebar.

### Post Header

- "← All posts" back link (sage color, top of page)
- Week number + date (small, uppercase, sage)
- Post title (Cormorant Garamond, ~2.8rem)
- Tag pills row
- Gradient divider line (rose → sage → plum)

### Post Body

Styled content area supporting:

- **Paragraphs**: 1.05rem, 1.8 line-height, generous bottom margin
- **Headings** (h2): Cormorant Garamond, 1.8rem, extra top margin
- **Ordered lists**: Custom-styled with numbered circles (sage background, white text), each item has a subtle sage-tinted background row
- **Tech stack pills**: Small rounded pills with cream-dark background and subtle border
- **Bold and italic**: Standard styling
- **Code blocks**: If needed in future posts (monospace, subtle background)

### Post Footer

- Thin top border separator
- Two items side by side:
  - "Share on LinkedIn" button (plum outline, LinkedIn icon)
  - "Follow the journey on LinkedIn" text with link (rose color)
- Previous/Next post navigation (added when more posts exist)

### Site Footer

Same as homepage: "Crafted with care · Romy Medan · Atlanta Metro Area"

## Design System (Inherited)

All pages use the existing design tokens:

- **Colors**: cream, rose, sage, plum, amber (with light/dark variants)
- **Typography**: Cormorant Garamond (display), Nunito (body)
- **Animations**: Scroll reveal via IntersectionObserver, hover transitions
- **Responsive**: Breakpoints at 960px, 750px, 400px
- **Accessibility**: Reduced motion support, semantic HTML, aria attributes

## Responsive Behavior

- Post body max-width shrinks with padding on smaller screens
- Blog listing cards stack full-width on mobile
- Homepage teaser card goes full-width on mobile
- Nav hamburger menu includes "Blog" link on mobile
- All touch targets meet minimum size requirements

## Weekly Workflow (Adding a New Post)

1. Create `blog/posts/week-N-title-slug.html` using the post template
2. Update `blog/index.html` — add a new card at the top of the list
3. Update `index.html` — swap the teaser card content to the new post
4. Commit and push to deploy via GitHub Pages
