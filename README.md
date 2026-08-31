# QR Code Generator

A small, dependency-free browser tool for generating styled QR codes —
custom dot and corner shapes, gradients, an embedded logo with a backing
plate, and five frame styles — exported as PNG, SVG, JPEG, or WebP.

**Live:** https://shhosting.net/qr-code-generator

## Why

I wanted a QR generator that didn't require an account and didn't phone
home with whatever I was encoding. Most "free QR generator" sites either
upload your data to a server or make you sign up. Nothing here does — the
code is built and rendered entirely client-side using
[qr-code-styling](https://github.com/kozakdenys/qr-code-styling) for the
base QR rendering, with the frame, caption, and logo compositing done in
plain JS/SVG on top. Open DevTools → Network tab and confirm nothing
leaves the browser.

## Features

- 6 dot styles, 7 corner-square/corner-dot styles
- Gradient or solid color per element (dots, corners, background)
- Logo upload with a backing plate (shape, color, padding)
- 5 frame styles: None, Card, Bottom bar, Ticket, and Asset tag (a
  homelab-themed signature frame with corner rivets and an accent band)
- Adaptive caption font-sizing so long captions never overflow the frame
- 4 built-in presets: Amber, Mono, Terminal, Blueprint
- Exports to PNG, SVG, JPEG, or WebP at your chosen size
- No build step, no analytics — a single static HTML file with
  qr-code-styling embedded, no CDN calls

## Running locally

There's nothing to build. The page links `/assets/css/style.css`,
`/assets/js/nav.js`, and `/assets/img/*` from the shhosting.net site root
for header/nav/footer styling, so serve it from something that also
exposes those paths (e.g. a checkout of
[shhosting.github.io](https://github.com/shhosting/shhosting.github.io),
or a proxy pointed at the same origin) rather than opening `index.html`
directly:

```bash
python3 -m http.server 8000
```

## Contributing / review

This was written using several different AI agents and hasn't had
independent review — that's exactly what I'm looking for. If you spot
anything questionable in the SVG compositing, the export pipeline, or
general code quality, please open an issue or PR. Particularly interested
in:

- Correctness of the canvas rasterization for PNG/JPEG/WebP exports
- Edge cases in the frame/caption layout (very long captions, extreme
  logo sizes, unusual aspect ratios)
- Anything that looks like it could leak data despite the "nothing
  uploaded" claim above

## License

MIT — see [LICENSE](./LICENSE). Use it, fork it, embed it, whatever.
qr-code-styling itself is also MIT licensed; see its
[repository](https://github.com/kozakdenys/qr-code-styling) for details.
