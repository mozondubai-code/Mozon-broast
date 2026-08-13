# 🍗 Mozon Broast — 3D Animated Website + Online Order Form

**Mozon Broast**, Al Nahda 2, Dubai (Near NMC Hospital).

## 🌐 Live Site
👉 https://mozondubai-code.github.io/mozon-broast

| Page | File | What it is |
|---|---|---|
| Landing page | `index.html` | Scroll-driven 3D animated site (Three.js + Lenis) |
| Order form | `index-1.html` | Corporate & office order form → WhatsApp (unchanged) |

The landing page links straight into the order form from both its Menu and Order
sections, so the ordering flow is unchanged — it just gains a front door.

## 🎬 The 3D landing page

A frame-scrub hero over real footage, plus real-time WebGL geometry built in code:

- **Home** — cinematic frame-scrub: real footage scrubbed frame-by-frame as you
  scroll, forward then back
- **Story** — editorial copy with count-up stats and an inline rotating 3D object
- **Menu** — six signature plates with live prices, linking to the full order form,
  with a procedural 3D broast platter alongside
- **Explore** — cursor-driven golden particle field
- **Order** — WhatsApp, order form and call-now actions

Plus an ambient ember field, cursor glow, scroll progress bar and scroll-spy nav.
Fully responsive, and it degrades cleanly on touch devices and under
`prefers-reduced-motion`.

Build notes, the section/technique plan and the scaffold fixes are in [`DESIGN.md`](DESIGN.md).

## 🛠 Local preview

No build step — it's static files:

```bash
python3 -m http.server 8000
# open http://127.0.0.1:8000/
```

`three@0.160.0` and `lenis@1.3.21` are vendored under `vendor/`, so the page has no
third-party runtime dependency.

## 📞 Contact
- WhatsApp / Call: +971 52 487 7701
- Location: Al Nahda 2, Near NMC Hospital, Dubai, UAE
- Delivery: Free within 5km
- Hours: Daily 12PM – 2AM
