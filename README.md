# CSS-Only Tooltips with Pseudo-Elements

This example demonstrates a new method to create animated tooltips using **only CSS** with no JavaScript required.

The tooltip text is pulled from a custom HTML attribute and displayed using `::before` and `::after` pseudo-elements.

---

## What This Example Demonstrates

- Positioning context with `position: relative`
- Absolute positioning
- Pseudo-elements (`::before` and `::after`)
- Using `attr()` to read custom data attributes
- CSS transforms (`translate`, `scale`)
- `transform-origin`
- CSS transitions
- Layering with `z-index`

---

## Project Files

- `index.html` — Example page with tooltip links
- `tooltips.css` — Tooltip styling (pseudo-elements + animation)

---

## How It Works

### 1) Add Tooltip Text in HTML

Each tooltip link looks like this:

```html
<a href="#" class="tooltip" data-name="I'm a tooltip!">link text</a>
```

Two key pieces:

- `class="tooltip"` applies the tooltip styling.
- `data-name="..."` stores the tooltip text.

The tooltip text is pulled into CSS with:

```css
content: attr(data-name);
```

---

### 2) Create a Positioning Context

```css
a.tooltip {
  position: relative;
}
```

This is required because the tooltip pieces use `position: absolute;`.
`position: relative;` makes the link the reference box for the tooltip.

---

### 3) Tooltip Bubble with `::before`

The tooltip bubble is created using `a::before`.

Key ideas:

- `bottom: 100%` places the bubble above the link.
- `left: 50%` + `translateX(-50%)` centers it horizontally.
- `scale(0)` + `opacity: 0` hides it at first.
- On hover, it scales to `1` and fades in.

Example:

```css
a::before {
  content: attr(data-name);
  position: absolute;
  left: 50%;
  bottom: 100%;
  transform: translateX(-50%) translateY(-0.5rem) scale(0);
  transform-origin: center bottom;
  opacity: 0;
  transition: transform 0.3s ease, opacity 0.3s ease;
}

a:hover::before {
  transform: translateX(-50%) translateY(-0.5rem) scale(1);
  opacity: 1;
}
```

---

### 4) Tooltip Arrow with `::after`

The arrow is created using `a::after` and a CSS triangle technique:

```css
border-top: 0.7rem solid black;
border-left: 0.5rem solid transparent;
border-right: 0.5rem solid transparent;
```

---

### 5) Animation Notes

The tooltip grows from the center because of:

```css
transform-origin: center bottom;
```

Without `transform-origin`, the tooltip would scale from the top-left corner.

---

## How to Use This in Your Own Project

1. Add the `tooltip` class to a link.
2. Add a `data-name` attribute with your tooltip text.
3. Copy the CSS into your stylesheet.
4. Adjust colors, border radius, or timing as desired.

Example:

```html
<a href="#" class="tooltip" data-name="Helpful info here">Hover me</a>
```

---

## Suggested Experiments

- Make the tooltip slide upward while fading in.
- Add a drop shadow.
- Move the tooltip below the link.
- Trigger it with `:focus` instead of `:hover`.
- Create multiple tooltip color variations with extra classes.

---

## Key Concept

CSS can generate content and animate it without JavaScript.
