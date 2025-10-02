# Hugo Tailwind example

This shows a mostly minimal install of Hugo with Tailwind v4.

## Usage

### Basic

The `assets/css/main-minimal.css` file shows the absolute minimum needed to get the entire Tailwind library available. For small sites with few contributors this is fine.

### Adding constraints

The downside of making the entire Tailwind available is that, because there are so many options, it can be difficult to use the ["themed variable namespaces"](https://tailwindcss.com/docs/theme#theme-variable-namespaces) consistently. This includes design choices for type, color, spacing, and sizing.

In `assets/css/main.css` I've provided examples of disabling categories you don't need, how to override a namespace to limit the available options, and how to create custom classes. You can mix and match these techniques depending on your needs. I generally like to turn everything off and only open them as I need them, but I'm a bit of a control freak.

#### Disable namespace

Here we're removing all "blur" classes from Tailwind.

```css
@theme {
  --blur-*: initial;
}
```

#### Disable and redefine namespace

Here we have turned off all of the default "spacing" values, which powers the default padding, margin, and width/height classes, and defining our own values. This means classes like `p-1 m-3` will no longer work, but `p-md m-x-lg` will.

```css
@theme {
  --spacing-*: initial;

  --spacing-xxx-sm: 0.125rem;
  --spacing-xx-sm: 0.25rem;
  --spacing-x-sm: 0.5rem;
  --spacing-sm: 0.75rem;
  --spacing-md: 1rem;
  --spacing-lg: 1.25rem;
  --spacing-x-lg: 1.5rem;
  --spacing-xx-lg: 2rem;
  --spacing-xxx-lg: 2.5rem;
}
```

#### Custom classes

Here we're turning off all Tailwind classes completely and defining a custom foreground class (used for text and icons) completely outside of the Tailwind system. Creating a small set of classes for foregrounds, backgrounds, and borders is often all you need to build your UI.

```css
@theme {
  --color-*: initial;
}

:root {
  --tcg-fg-base: #000000;
}

.fg-base {
  color: var(--tcg-fg-base);
}
```

#### Suggested custom classes

- `fg-base` (black)
- `fg-muted` (dark gray)
- `fg-inverted` (white)
- `bg-base` (white)
- `bg-faint` (very light gray)
- `bg-muted` (slightly darker gray)
- `bg-inverted` (black)
- `border-base` (default border, light gray)
- `border-emphasis` (darker gray)

Then I would add group of color concepts as needed like "alert" (reds), "positive" (greens), "accent" or "brand" (branded color), and any lighter or darker variants.

- `alert-fg-base` (red)
- `alert-bg-base` (red)
- `alert-border-base` (red)

#### Semantic weights

The following colors are relative to the color palette and can run in both directions.

- `base`: the default color of the palette and can be dropped into any position
- `inverted`: optional

1. faint
2. dim
3. muted
4. moderate
5. emphasis
6. strong
7. heavy
8. deep
