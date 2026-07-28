# Goshtoso Getting Started

A small, complete Go app for learning Goshtoso with templ, HTMX, Alpine.js, and
server-rendered UI components.

The app renders a filterable, sortable, paginated dog-breeds table with embedded
dog images. There is no JavaScript build step and no CDN dependency.

## Run It

```bash
git clone https://github.com/araihu/goshtoso-getting-started dog-breeds
cd dog-breeds
go run .
```

Open [http://localhost:3000](http://localhost:3000).

## Files

- `main.go`: HTTP server, dog data, filtering, sorting, pagination, asset routes,
  and HTMX fragment endpoint.
- `page.templ`: the page template rendered by the server.
- `page_templ.go`: generated templ output so the app can run immediately.
- `assets/dogs/*.webp`: starter app images embedded into the binary.

## Asset Model

The app uses two asset sources:

- Goshtoso runtime assets are served from `/assets/` by
  `github.com/araihu/goshtoso/assets.Handler()`. This includes compiled CSS,
  themes, Alpine.js, HTMX, fonts, and library artwork.
- Starter app assets are served from `/dog-images/` by this app. The dog images
  live in `assets/dogs` and are embedded with Go's `embed` package.
- Arai Hû's organization theme is vendored as `araihu.css`, served at
  `/araihu.css`, and selected by default. Other Goshtoso themes remain
  available through the normal `data-theme` contract.

That split keeps Goshtoso reusable while keeping your application images under
your application's control.

## Regenerate Templ

If you edit `page.templ`, regenerate the Go output:

```bash
templ generate
go run .
```

## Dependency Note

This starter currently pins Goshtoso to the latest main-branch pseudo-version so
it can use the newest `table.ImageCell` helper before the next tagged release.
After the next Goshtoso tag, you can update with:

```bash
go get github.com/araihu/goshtoso@latest
go mod tidy
```
