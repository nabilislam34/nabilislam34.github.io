# Reflection & AI Attribution

## 1. Difference between `flex-direction: row` and `flex-direction: column`

In CSS Flexbox, the `flex-direction` property defines the **main axis** along which flex items are laid out:

- `flex-direction: row` (the default value): Sets the main axis horizontally from left to right (in standard LTR writing modes). Flex items are arranged side-by-side in a horizontal row. Properties like `justify-content` align items horizontally along the row, while `align-items` aligns them vertically across the cross axis.
- `flex-direction: column`: Rotates the main axis 90 degrees so it runs vertically from top to bottom. Flex items are stacked on top of one another in a single vertical column. Here, `justify-content` controls vertical spacing and alignment, while `align-items` controls horizontal alignment across the cross axis.

In this project, `flex-direction: row` was used for the desktop navigation bar to keep the brand on the left and navigation links spread horizontally to the right. When the mobile media query triggers (`@media (max-width: 768px)`), switching to `flex-direction: column` allows the navigation bar and link list to stack neatly into a touch-friendly vertical menu.

---

## 2. Why relative units (like `%`, `vh`, `rem`) are important instead of fixed pixels (`px`) for responsive design

Fixed pixel units (`px`) declare rigid, static measurements that do not adapt to different screen dimensions, resolutions, or user preferences. Using relative units is essential for responsive and accessible web design for several reasons:

1. **Fluid Adaptability Across Diverse Screen Sizes:**
   Relative units such as percentages (`%`) and viewport units (`vw`, `vh`) scale dynamically relative to their containing block or the browser viewport. For example, a card container styled with `max-width: 1240px; width: 100%` or layout columns set with relative fraction units (`1fr`) smoothly resize between ultrawide monitors, laptops, and mobile screens without causing horizontal overflow or clipping.

2. **Accessibility and User Text Scaling (`rem` vs `px`):**
   The `rem` unit (root em) is relative to the root `<html>` element's font size (which defaults to 16px in most browsers). When visually impaired users or users who prefer larger text adjust their browser's default font size or zoom level in accessibility settings, elements sized with `rem` scale proportionally across the entire interface. In contrast, hardcoded `px` font sizes or container paddings override or ignore user font settings, breaking accessibility and layout proportions.

3. **Maintainability and Proportional Scaling:**
   Using `rem` for typography, paddings, and margins makes it easy to scale an entire design system consistently. Updating the base font size or tweaking relative scales automatically preserves the visual rhythm and balance between headings, paragraphs, and cards across viewports.

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
