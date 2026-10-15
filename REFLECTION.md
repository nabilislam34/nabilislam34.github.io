# Reflection & AI Attribution

## 1. Difference between `flex-direction: row` and `flex-direction: column`

`flex-direction` controls which direction flex items are placed inside a flex container.

- **`row`** (the default): items are laid out **horizontally**, left to right. `justify-content` controls spacing along that horizontal axis and `align-items` controls vertical alignment.
- **`column`**: items are stacked **vertically**, top to bottom. Now `justify-content` controls vertical spacing and `align-items` controls horizontal alignment.

In practice on this site: the navbar uses `flex-direction: row` on desktop so the name sits on the left and links sit on the right. When the screen is 768px or narrower the media query switches it to `flex-direction: column` so the name and each link stack on top of each other into a vertical menu that fits on a phone.

---

## 2. Why relative units (`%`, `vh`, `rem`) matter instead of fixed pixels (`px`)

If you use `px` everywhere, the layout is frozen at whatever size you typed. On a phone that might be way too wide, and if a user bumps up their browser font size for accessibility, nothing scales with it.

Relative units fix both problems:

- **`%` and `vw/vh`** — sizes relative to the parent or the viewport, so the layout naturally shrinks and grows as the screen changes.
- **`rem`** — relative to the root font size. If someone sets their browser to "large text", everything sized in `rem` (padding, font-size, gap) scales up automatically. Hard-coded `px` ignores that setting completely.

On this site padding, font sizes, and gaps all use `rem` so the layout stays proportional across screen sizes, and the grid columns use `1fr` so they divide the available space evenly instead of being stuck at a fixed pixel width.

---

## 3. AI Attribution

### Prompt Used:
> "follow instructions in the pdf and do the assignment C:\Users\Zoro_\Documents local backup of HDD\0 School work\2026 fall\web dev\WD_HW2 (4).pdf"

### AI-Provided CSS Modification:
When generating the initial responsive navigation bar and grid showcase, the AI provided the following CSS rule for the navigation links:

```css
.nav-links {
  display: flex;
  justify-content: flex-end;
  gap: 1rem;
}

@media (max-width: 768px) {
  .nav-links {
    flex-direction: column;
    align-items: center;
  }
}
```

**Why it needed modification:**
While this aligned links to the right on desktop, in the mobile view (`flex-direction: column`) with `align-items: center`, each `<a>` link tag only stretched as wide as its text content. This created very small, awkward touch targets on mobile phones where tapping slightly outside the text failed to trigger the link. 

Furthermore, the parent container `.navbar` had `justify-content: space-between` with `flex-direction: row`, meaning on mobile screens the logo and navigation menu stayed horizontally pinned to opposite sides, causing severe horizontal overflow and squishing the navigation list.

**The Fix:**
I modified the mobile media query CSS so that `.navbar` switches to `flex-direction: column` with `align-items: stretch`, and gave `.nav-links li` and `.nav-links li a` a full `width: 100%` with block display and generous vertical padding (`0.7rem 1rem`):

```css
@media (max-width: 768px) {
  .navbar {
    flex-direction: column;
    align-items: stretch;
    padding: 1rem 1.25rem;
    gap: 0.75rem;
  }

  .nav-links {
    flex-direction: column;
    width: 100%;
    gap: 0.35rem;
  }

  .nav-links li {
    width: 100%;
  }

  .nav-links li a {
    display: block;
    width: 100%;
    text-align: center;
    padding: 0.7rem 1rem;
  }
}
```

This transformed the navigation into a full-width, touch-friendly mobile drawer menu that spans the viewport cleanly without overflow.
