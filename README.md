# Arthur — UX/UI Designer Portfolio

A production-ready personal portfolio template crafted with precision using **vanilla HTML5 and CSS3 only**. This project focuses on high-performance, accessibility, and maintainable architecture, delivering a seamless experience without the need for heavy frameworks or external dependencies.

🔗 **Live Demo:** [Add your Vercel URL here]

---

## Overview

This portfolio template is designed for designers and developers who value clean, lightweight code. By leveraging BEM methodology and CSS design tokens, it offers a scalable structure that is easy to customize and deploy.

Built with zero JavaScript dependencies and optimized for modern web standards, it ensures lightning-fast load times and full cross-browser compatibility.

---

## Tech Stack

| Layer      | Technology                            |
| ---------- | ------------------------------------- |
| Markup     | HTML5 (semantic elements)             |
| Styling    | CSS3 (Custom Properties, Flexbox)     |
| Icons      | Font Awesome 6 (self-hosted)          |
| Fonts      | Google Fonts — Oswald + Space Grotesk |
| Deployment | Vercel + GitHub                       |

---

## Project Structure

```

Arthur/
├── assets/               # All images (WebP format)
│   ├── pic-1.webp
│   ├── portfolio-*.webp
│   └── ...
├── css/
│   ├── normalize.css     # CSS reset
│   ├── all.min.css       # Font Awesome (local)
│   └── arthur.css        # Main stylesheet
├── webfonts/         # FA icon fonts
└── index.html
```

---

## CSS Architecture

### 1. Design Tokens — Single Source of Truth

All colors, typography, spacing, and transitions are defined once in `:root` and referenced everywhere via CSS Custom Properties. No hardcoded values anywhere in the stylesheet.

```css
:root {
  /* Colors */
  --color-primary: #000000;
  --color-accent: #8a8a8a;
  --color-bg-light: #f5f5f5;
  --color-text-muted: #666666;

  /* Typography */
  --font-primary: "Oswald", sans-serif;
  --font-secondary: "Space Grotesk", sans-serif;
  --text-sm: 0.9375rem; /* 15px */
  --text-3xl: 3.125rem; /* 50px */

  /* Spacing */
  --section-padding: 5.625rem; /* 90px */
  --footer-height: 16rem;

  /* Transitions */
  --transition-fast: 0.3s ease;
  --transition-mid: 0.5s ease;
}
```

### 2. Stylesheet Structure

The CSS file follows a strict top-to-bottom order:

```

1.  Custom Properties (Design Tokens)
2.  CSS Reset & Base
3.  Scrollbar
4.  Layout — .container
5.  Accessibility Utilities — .sr-only, :focus-visible
6.  Reusable Components — .section-header, .btn
7.  Header + Sidebar + Menu
8.  Hero Section
9.  About Section
10. Statistics Section
11. Services Section
12. Skills Section
13. Portfolio Section
14. Testimonials Section
15. Pricing Section
16. Contact CTA Section
17. Instagram Feed Section
18. Footer
19. Keyframe Animations (consolidated)
```

### 3. Naming Convention — Modified BEM

Classes follow a `block__element--modifier` pattern, scoped per section to prevent collisions:

```css
/* Block */
.services {
}

/* Element */
.services__grid {
}
.services__card {
}
.services__card-body {
}

/* Modifier */
.pricing__card--featured {
}
.testimonials__arrow--prev {
}
.pricing__feature--unavailable {
}
```

### 4. Reusable Components

Two global components are defined once and reused across all sections:

**`.section-header`** — used in Services, Portfolio, Pricing, Skills, Chat:

```html
<div class="section-header">
  <div class="section-header__title">
    <p>Subtitle</p>
    <h2 id="section-id">Section Title</h2>
  </div>
</div>
```

**`.btn`** — replaces the invalid `<button><a>` pattern used throughout the original:

```html
<a href="#" class="btn" data-label="Button Text">
  <span class="btn__label">Button Text</span>
</a>
```

The `data-label` attribute feeds the CSS `::after` flip animation, keeping the 3D hover effect DRY across all button instances without repeating CSS per section.

### 5. Responsive Breakpoints — Standardized

Three breakpoints only, consistent throughout the entire stylesheet:

| Name    | Value           | Layout         |
| ------- | --------------- | -------------- |
| Mobile  | `< 768px`       | Single column  |
| Tablet  | `768px – 991px` | 2-column grids |
| Desktop | `≥ 992px`       | Full layout    |

---

## Semantic HTML Structure

Every section uses the correct HTML5 landmark element and is labeled for assistive technologies:

```html
<header>
  <!-- site header -->
  <nav aria-label="Primary navigation">
    <!-- main nav -->

    <main id="main-content">
      <section aria-labelledby="hero-title">
        <!-- hero -->
        <section aria-labelledby="about-title">
          <!-- about -->
          <section aria-label="Statistics">
            <!-- statistics -->
            <section aria-labelledby="services-title">
              <!-- services -->
              <section aria-labelledby="skills-title">
                <!-- skills -->
                <section aria-labelledby="portfolio-title">
                  <!-- portfolio -->
                  <section aria-labelledby="testimonials-title">
                    <!-- testimonials -->
                    <section aria-labelledby="pricing-title">
                      <!-- pricing -->
                      <section aria-labelledby="contact-title">
                        <!-- contact CTA -->
                        <section aria-label="Instagram Feed">
                          <!-- instagram -->

                          <footer>
                            <!-- site footer -->
                            <address><!-- contact info --></address>
                          </footer>
                        </section>
                      </section>
                    </section>
                  </section>
                </section>
              </section>
            </section>
          </section>
        </section>
      </section>
    </main>
  </nav>
</header>
```

Notable semantic choices:

- `<article>` for service cards — self-contained, reusable content
- `<blockquote>` for testimonial quotes
- `<address>` for footer contact information
- `<aside>` for the sidebar panel
- `<nav>` for the portfolio filter — it navigates between content categories
- `<form role="search">` with a visually-hidden `<label>` for the header search

---

## Accessibility (WCAG 2.1 AA)

- `aria-labelledby` on every `<section>` pointing to its `<h2>` ID
- `aria-label` on all interactive icon-only controls (sidebar toggle, menu toggle, arrow buttons)
- `aria-hidden="true"` on all decorative Font Awesome icons
- `aria-live="polite"` on the testimonials auto-scroll region
- `aria-expanded` + `aria-controls` on sidebar and menu toggles
- `.sr-only` utility class for visually-hidden but screen-reader-accessible text
- `:focus-visible` ring defined globally — keyboard navigation fully styled
- `fetchpriority="high"` on hero LCP images, `loading="lazy"` on all others
- No `<button><a>` nesting anywhere — all CTAs use `<a class="btn">`

---

## Notable Techniques

**Sticky Footer Reveal**
The footer sits `position: fixed` at the bottom of the viewport. The `<main>` element has `position: relative; z-index: 1`, causing it to slide up over the footer on scroll — revealing it from beneath like a curtain.

```css
footer {
  position: fixed;
  bottom: 0;
  z-index: 0;
}
main {
  position: relative;
  z-index: 1;
  padding-bottom: var(--footer-height);
}
```

**3D Button Flip**
Buttons use a CSS 3D transform — a grey face rotates away on hover and a black face rotates in. Achieved with `rotateX` on `::after` (grey face) and an inner `<span>` (black face). The label text is fed via `data-label` attribute to keep it DRY.

**Testimonials Auto-Scroll**
Two synchronized `@keyframes` animations — `testimonial-scroll` (moves the slides track) and `counter-slide` (animates the counter number) — both run on the same `9s` duration to stay perfectly in sync. The original was hover-triggered and used mismatched durations (8s vs 10s).

**Photo Fan Effect**
The hero section features two overlapping portrait photos rotated at different angles. On hover, they fan out further using `rotate()` and `translate()` transforms for a tactile, interactive feel.

---

## Running Locally

No build step required.

```bash
git clone https://github.com/your-username/arthur-portfolio.git
cd arthur-portfolio
```

Open `index.html` directly in your browser, or use a local server:

```bash
# VS Code — Live Server extension (recommended)
# or
npx serve .
```
