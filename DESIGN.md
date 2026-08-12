# Mozon Broast — 3D Animated Landing Page

Scroll-driven 3D landing page for Mozon Broast (Al Nahda 2, Dubai), built with the
scroll3d scaffold: Lenis smooth scroll + Three.js r160 (UMD, CDN-pinned), zero build
step, zero generated assets. The existing corporate order form (`index-1.html`) is
untouched and linked from the Menu and Order sections.

## Plan vs build

| Section (id) | Nav label | Planned technique | Built technique | Notes |
|---|---|---|---|---|
| `hero` | HOME | 3d-scene-effect (`platter`) | 3d-scene-effect (`platter`) | Custom procedural broast platter (plate, golden pieces, garnish, steam particles); camera sweeps top-down → hero angle and dollies in with scroll |
| `story` | STORY | hybrid-2d3d (`abstract`) | hybrid-2d3d (`abstract`) | Editorial copy + count-up stats (14h open, 5km free delivery, 40+ items); inline idle-rotating torus knot in brand gold |
| `menu` | MENU | hybrid-2d3d (`reveal`) | hybrid-2d3d (`reveal`) | Six signature items with real AED prices from the order form; stage/copy columns mirrored for rhythm |
| `experience` | EXPLORE | pointer-follow-effect (`abstract`) | pointer-follow-effect (`abstract`) | Cursor-driven golden particle field; static centered pose on touch/reduced-motion, overlay copy still scroll-driven |
| `order` | ORDER | outro (no 3D) | outro (no 3D) | WhatsApp CTA, corporate order form link, tel link, address/hours |

No plan deviations. No Higgsfield credits spent (all sections are real-time WebGL —
zero-cost techniques only).

## Palette

| Token | Value | Used for |
|---|---|---|
| `--accent` | `#e53935` | Broast red — brand mark, hero glow, menu-section 3D object |
| `--accent-2` / `--gold` | `#ffc107` | Brand gold — stats, prices, nav hover, 3D accents |
| `--bg` | `#0c0605` | Warm near-black page background |
| `--ink` | `#fdf6ee` | Warm off-white text |

Fonts: Bebas Neue (display) + Inter (body), matching the existing order form's brand.

## Atmosphere layer

Motion language borrowed from the supplied MADAX / Shinobi reference builds, kept
deliberately dim so it never competes with content:

- Ambient ember field (`#embers`, canvas-2D, warm gold, 28–70 particles by viewport area)
- Cursor glow — fine-pointer devices only, hidden on touch and under reduced motion
- Sitewide scroll progress bar pinned to the top of the viewport
- Scroll-spy nav — the active section's link highlights in brand gold

## Files

- `index.html` — page shell, section markup, `*_SECTIONS` registries, library tags
- `styles.css` — scroll3d `base.css` + world/parallax/hybrid fragments + Mozon custom fragment
- `choreography.js` — shared scroll/pointer/color utilities (unmodified scaffold)
- `site.js` — Lenis driver, `.reveal`/`.stat-num` IntersectionObserver, overlay driver for pinned `.world` sections (jobs `video-scroll-effect.js` would own in a scrub build), plus the atmosphere layer above
- `3d-scene-effect.js` — scaffold engine + custom `platter` geometry/camera case
- `pointer-follow-effect.js`, `hybrid-2d3d.js` — scaffold engines
- `vendor/` — `three@0.160.0` and `lenis@1.3.21`, vendored from the npm registry so the page has no third-party runtime dependency

## Fixes made to the upstream scaffold

- **Off-centre pinned headlines.** The upstream engines write
  `el.style.transform = translateY(...)` onto `.reveal-line`, which clobbers that
  rule's own `translate(-50%, -50%)` centering — every pinned headline rendered
  pushed right by half its width (measured: box left edge at x=720 in a 1440px
  viewport). Both drivers here write
  `translate(-50%, calc(-50% + Npx))` instead.
- **Hero headline invisible at rest.** A first line with `data-in="0.00"` peaks at
  the midpoint of its window, so it is at opacity 0 at scroll progress 0. The first
  line of each pinned section now opens on a negative `data-in` so it is already
  legible before the visitor scrolls.
- **Mobile nav.** The scaffold hides `.hud-nav` entirely below 700px; this build
  keeps it as a compact horizontally-scrollable row so sections stay reachable.

## Verification

Driven in headless Chromium (Playwright) at 1440×900 and 390×844:

- All four engines initialize (1 world, 1 parallax, 2 hybrids), Lenis active, no page errors
- Scrolled through all five sections — copy, counters, progress bar and scroll-spy all track
- Reduced-motion pass: Lenis off, embers/glow hidden, headline forced visible, engines hold static poses, zero console errors

The only console error in local testing is the Google Fonts request, which the
sandbox proxy blocks; it resolves normally in production, and Bebas Neue/Inter fall
back to system fonts if it ever fails.

## Accessibility / degradation

- `prefers-reduced-motion`: sections unpin, static camera poses, first overlay line shown
- Touch devices: pointer section falls back to a static centered pose; hint hidden
- Nav collapses on <700px viewports (per scaffold default)

## Deploy

No Cloudflare credentials in this environment — the site is served by the repo's
existing GitHub Pages setup instead (`index.html` at the repo root becomes the live
landing page; the order form stays at `/index-1.html`).
