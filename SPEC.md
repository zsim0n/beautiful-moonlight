# Spec: beautiful-moonlight

Agent instructions that produce this repo. Hand this file to a coding agent
in an empty folder and it should rebuild the same thing.

## Goal

A tiny design system for my side projects, on top of **Pico CSS v2**
(classless build). Two brands: **zoltansimon.me** (default) and **timu.io**.
Light and dark themes. Published to npm, styleguide on GitHub Pages.

## Principles

- **Plain CSS.** No Sass, no PostCSS, no build step, no JS framework.
- **Pico does the work.** Only add what Pico lacks. Never restyle what Pico
  already does well (buttons, forms, nav, cards, tables, accordions).
- **Theme through Pico's variables.** Map the brand onto `--pico-*`, don't
  fight Pico with overrides.
- **Prefer deletion.** No dependencies in the repo. If a tool is heavier than
  what it shows, drop it. (Storybook was tried and removed: too much of its
  own UI, too little of ours.)

## Files

```
src/beautiful-moonlight.css   entry: @imports the three files below
src/tokens.css                brand palette → Pico variables
src/typography.css            the few type helpers Pico doesn't have
src/components.css            header, linked card, alert, badge
index.html                    the styleguide, one page
package.json, README.md, LICENSE (MIT), .gitignore, .nvmrc (22)
```

## Tokens (`src/tokens.css`)

- Palette as `--bm-*`: laser `#ff3b14`, ember `#ff6a2c`, amber `#e0a45c`,
  paper `#f1ece4`, ink `#2b2b2e`, charcoal `#16161a`, slate `#1e1e24`.
- A brand sets only two vars: `--bm-accent-light` and `--bm-accent-dark`.
  - zoltansimon.me (default, on `:root`): laser / ember.
  - timu.io (`[data-brand="timu"]`): `#663399` / `#a77fd8`.
- Status colours: `--bm-info`, `--bm-success`, `--bm-warning` (amber),
  `--bm-danger`, with lighter variants in dark mode.
- Map accents onto all of Pico's `--pico-primary*` vars, deriving hover,
  focus and underline with `color-mix()`.
- **Use Pico's exact selectors** or Pico wins the cascade:
  - light: `[data-theme="light"], :root:not([data-theme="dark"])`
  - dark: `[data-theme="dark"]` and
    `@media (prefers-color-scheme: dark) { :root:not([data-theme]) }`
- Dark mode backgrounds: charcoal page, slate cards.
- `--bm-header-bg/fg`: paper/ink in light, charcoal/paper in dark.
- `--pico-font-size: 80%`, no link underlines.

## Typography (`src/typography.css`)

- Links: accent colour, no underline.
- `.lead`, `.text-left/right/center`, `.text-muted`, `.text-accent`.
- `a.subdued`: muted links for a row of tags or footer links.
- `u.dotted`, `u.dashed`.
- SVG images get a white backing in dark mode (diagrams with dark text).

## Components (`src/components.css`)

All prefixed `bm-`.

- `.bm-header`: header bar using `--bm-header-bg/fg`; text and links inside
  keep the header colour, not the accent.
- `a.bm-card > article`: the whole card is a link. Pico colours text inside
  `<a>` with the accent, so reset `--pico-color` to inherit; on hover, ring the
  card in the accent and colour only the heading.
- `.bm-alert` + `-success/-warning/-danger`: left border in the status colour,
  10% tinted background.
- `.bm-badge` + `.bm-badge-accent`: small pill.

## Styleguide (`index.html`)

- One static page. Loads Pico classless from jsDelivr (pinned `2.1.1`) and
  `src/beautiful-moonlight.css`.
- `.bm-header` nav with two `<select>`s: brand and theme. They set
  `data-brand` / `data-theme` on `<html>`; also readable from
  `?brand=&theme=` in the URL.
- Sections: Colors (swatches of the vars), Typography, Components,
  Pico (buttons, form, card, table, accordion).
- GitHub corner top-right: accent triangle with the GitHub mark, linking to
  the repo.
- Page-only styles stay in a `<style>` block in the page, not in `src/`.

## Package

- `name: beautiful-moonlight`, MIT, `files: ["src"]`.
- `main`/`style`/`exports["."]` → `src/beautiful-moonlight.css`;
  `exports["./*"]` → `src/*` so single files can be imported.
- `peerDependencies: { "@picocss/pico": "^2.0.0" }`. No other dependencies.
- `scripts.dev`: `npx -y live-server@1.2.2 --port=8080` (nothing installed).
- GitHub Pages: deploy from branch `main`, root. No workflow.

## Done when

- `npm run dev` shows the styleguide and every section reads well in all four
  combinations: zoltansimon/timu × light/dark.
- `npm pack` contains only `src/`, `README.md`, `LICENSE`, `package.json`.
