1) **Selector**: `.hero-cta`  
**Problem**: The CTA button lacks a visible focus state for keyboard navigation, failing WCAG 2.2 SC 2.4.7.  
**Fix**:  
```css
.hero-cta:focus-visible {
  outline: 2px solid var(--gold);
  outline-offset: 4px;
}
```

2) **Selector**: `.nav-cta`  
**Problem**: The gold-on-transparent button has an insufficient contrast ratio (Γëê3.1:1) against the dark espresso background when the nav is scrolled.  
**Fix**:  
```css
.nav.scrolled .nav-cta {
  border-color: var(--gold-light);
  color: var(--gold-light) !important;
}
```

3) **Selector**: `.box-card-number`  
**Problem**: The large ΓÇ£01/02/03ΓÇ¥ numbers are pure decorative text; screen-readers will read them as ΓÇ£zero-oneΓÇ¥, which is meaningless.  
**Fix**:  
```html
<span class="box-card-number" aria-hidden="true">01</span>
```

4) **Selector**: `.reveal`  
**Problem**: When the `.visible` class is added, the element snaps to opacity 1 instantly for users who have `prefers-reduced-motion: reduce`, but no alternative is supplied.  
**Fix**:  
```css
@media (prefers-reduced-motion: reduce) {
  .reveal {
    transition: none;
    opacity: 1;
    transform: none;
  }
}
```

5) **Selector**: `.hero-scroll-line`  
**Problem**: The pulsing scroll-indicator is a pure decoration that loops forever and may trigger motion sensitivity.  
**Fix**:  
```css
@media (prefers-reduced-motion: reduce) {
  .hero-scroll-line { animation: none; }
}
```

6) **Selector**: `.nav-links a`  
**Problem**: Links in the nav have only an opacity change on hover; the hit-area is too small on touch devices and the hover style is not obvious.  
**Fix**:  
```css
.nav-links a {
  padding: 0.5rem 0.75rem;
  border-radius: 4px;
}
.nav-links a:hover,
.nav-links a:focus-visible {
  background: rgba(201,168,76,0.15);
  opacity: 1;
}
```

7) **Selector**: `.box-card`  
**Problem**: The card hover lift effect uses `transform: translateY(-4px)` but has no `will-change`, causing a subtle repaint stutter on lower-end devices.  
**Fix**:  
```css
.box-card {
  will-change: transform;
}
```

8) **Selector**: `.section-label::before`  
**Problem**: The 2 px gold line is created with a pseudo-element that is not announced to screen-readers; it should be hidden.  
**Fix**:  
```css
.section-label::before {
  content: '';
  speak: none;
  aria-hidden: true;
}
```

9) **Selector**: `.producer-card::before` (top border)  
**Problem**: The 3 px gold bar that scales in on hover has no `will-change`, leading to a visible jag on first hover.  
**Fix**:  
```css
.producer-card::before {
  will-change: transform;
}
```

10) **Selector**: `.hero-title`  
**Problem**: The clamped font-size can drop below 3 rem on very small viewports, but the letter-spacing of 0.08 em (Γëê2.4 px) is too tight, hurting legibility.  
**Fix**:  
```css
@media (max-width: 400px) {
  .hero-title {
    letter-spacing: 0.04em;
  }
}
```

11) **Selector**: `.exp-step-num`  
**Problem**: The step numbers are not inside an ordered list, so screen-readers lose the semantic ΓÇ£step 1, step 2ΓÇ¥ context.  
**Fix**:  
```html
<ol class="exp-steps">
  <li class="exp-step">
    <span class="exp-step-num">1</span>
    ΓÇª
  </li>
</ol>
```

12) **Selector**: `.pull-quote::before`  
**Problem**: The decorative quotation mark is created with CSS generated content; it should be hidden from assistive tech.  
**Fix**:  
```css
.pull-quote::before {
  aria-hidden: true;
  speak: none;
}
```

13) **Selector**: `.hero-bg::after` (gold line)  
**Problem**: The single-pixel gradient line is absolutely positioned but lacks `aria-hidden`, so some screen-readers may try to announce it.  
**Fix**:  
```css
.hero-bg::after {
  aria-hidden: true;
}
```

14) **Selector**: `.box-card-list li::before`  
**Problem**: The mid-dot bullet is rendered via CSS generated content; it needs an `aria-hidden` equivalent so screen-readers donΓÇÖt read ΓÇ£middle dotΓÇ¥.  
**Fix**:  
```css
.box-card-list li::before {
  content: '┬╖';
  aria-hidden: true;
}
```

15) **Selector**: `.nav-toggle`  
**Problem**: The hamburger button has no accessible name or state for screen-readers.  
**Fix**:  
```html
<button class="nav-toggle" aria-label="Open navigation" aria-expanded="false">
  <span></span><span></span><span></span>
</button>
```
```js
// in the mobile-menu toggle JS
btn.setAttribute('aria-expanded', isOpen);
```

16) **Selector**: `.hero-cta`  
**Problem**: The button text is set in uppercase via CSS; true screen-reader pronunciation is preserved, but the visual word-shape is lost for dyslexic users.  
**Fix**:  
```css
.hero-cta {
  text-transform: uppercase;
  font-variant-ligatures: none;
  letter-spacing: 0.18em;
}
```

17) **Selector**: `.reveal-delay-*`  
**Problem**: The staggered delays are hard-coded; on very large pages the last item (0.6 s) may still be animating while the user has already scrolled past.  
**Fix**:  
```css
.reveal-delay-4 { transition-delay: 0.3s; }
```

18) **Selector**: `.exp-visual-pattern svg`  
**Problem**: The inline SVG pattern is purely decorative and must be hidden from assistive tech.  
**Fix**:  
```html
<svg aria-hidden="true" focusable="false"> ΓÇª </svg>
```

19) **Selector**: `.section-intro`  
**Problem**: The italic serif intro text has a line-height of 1.7 but no `max-width` in ch units, leading to 90-character lines on large screens.  
**Fix**:  
```css
.section-intro {
  max-width: 60ch;
}
```

20) **Selector**: `.producer-card`  
**Problem**: The card has no `:focus-visible` style when a keyboard user tabs to the link inside.  
**Fix**:  
```css
.producer-card a:focus-visible {
  outline: 2px solid var(--gold);
  outline-offset: 2px;
}
```
