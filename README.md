# beautiful-moonlight

A small design system on top of [Pico CSS](https://picocss.com): brand
tokens, typography and a few components, themed for zoltansimon.me and
timu.io.

Plain CSS. No build step, no framework. Works with Pico's classless and
class-based builds. Grown out of `pure-typography-i`.

**Styleguide:** https://zsim0n.github.io/beautiful-moonlight

## Use

```bash
npm install @picocss/pico beautiful-moonlight
```

```css
@import "@picocss/pico/css/pico.classless.min.css";
@import "beautiful-moonlight";
```

Or straight from a CDN:

```html
<link rel="stylesheet" href="https://unpkg.com/@picocss/pico@2/css/pico.classless.min.css">
<link rel="stylesheet" href="https://unpkg.com/beautiful-moonlight/src/beautiful-moonlight.css">
```

Pick a brand and theme on `<html>`:

```html
<html data-brand="timu" data-theme="dark">
```

- `data-brand`: none (zoltansimon.me, the default) or `timu`
- `data-theme`: `light`, `dark`, or leave it off to follow the OS (same as Pico)

## What's in it

| File | What |
| --- | --- |
| `tokens.css` | Brand palette (`--bm-*`) mapped onto Pico's `--pico-*` variables |
| `typography.css` | Link style, `.lead`, text utilities, subdued links, SVGs in dark mode |
| `components.css` | `bm-header`, `bm-card` (linked `<article>`), `bm-alert`, `bm-badge` |

Everything else (buttons, forms, nav, cards, tables, accordions) is Pico.
Each file can be imported on its own, e.g. `beautiful-moonlight/tokens.css`.

A brand only sets its accent; everything else is shared. To add one:

```css
[data-brand="new"] {
  --bm-accent-light: #0a7;
  --bm-accent-dark: #4c9;
}
```

## Develop

`npm run dev` serves the styleguide (`index.html`) on :8080 and reloads on save.
GitHub Pages serves it from the repo root (Settings → Pages → Deploy from branch `main`).

## License

MIT
