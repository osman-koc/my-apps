<p align="center">
  <img src="logo.svg" width="128" height="128" alt="kocdev">
</p>

<h1 align="center">kocdev store</h1>

<p align="center">
  <em>Apps & tools crafted by Osman Koç.</em><br>
  A personal app catalog powered by <a href="https://github.com/f/appetit">Appétit</a> — the App Store-inspired catalog by <a href="https://github.com/f">Fatih Kadir Akın (FKA)</a>.
</p>

<p align="center">
  <a href="https://apps.osmankoc.dev">Live</a> ·
  <a href="https://osmankoc.dev/projects">osmankoc.dev/projects</a> ·
  <a href="https://github.com/f/appetit">Upstream: Appétit</a>
</p>

---

> **This is a fork of [Appétit](https://github.com/f/appetit)** by [Fatih Kadir Akın (FKA)](https://github.com/f), customised as a personal catalog for [Osman Koç](https://osmankoc.dev)'s apps and projects.
> All credit for the framework, UI, and architecture goes to FKA. This fork changes only the store data, branding, and category configuration.

Appétit is a beautiful, browsable app catalog that looks and feels like the Apple App Store. It's built entirely with vanilla HTML, CSS, and JS — no frameworks, no build step, no dependencies. Just edit `apps.json` and deploy.

## What's different from upstream

- **Store:** rebranded as `kocdev` — Osman Koç's personal app catalog
- **Apps:** projects from [osmankoc.dev/projects](https://osmankoc.dev/projects) (mobile, web, VS Code extensions, Telegram bots, games)
- **Categories:** Web Apps, Developer Tools, Utilities, Productivity, Lifestyle, Health & Fitness, Entertainment, Games
- **Logo:** custom `OK` monogram
- **Domain:** `apps.osmankoc.dev`

## Features (upstream)

- **App Store UI** — Sidebar navigation, featured carousel, app cards, detail pages with screenshots
- **Dark & Light themes** — System preference detection with manual toggle, persisted in localStorage
- **JSON-driven** — All apps, categories, and featured items defined in a single `apps.json`
- **Install modals** — `brew install` and `npx` commands with one-click copy to clipboard
- **Search** — Instant client-side filtering across names, descriptions, and features
- **GitHub stats** — Live star and fork counts, updatable with the included `update-stats.sh` script
- **Responsive** — Desktop sidebar collapses on mobile
- **Zero dependencies** — Pure HTML/CSS/JS, deploys anywhere as static files

## Quick Start

```bash
git clone https://github.com/osman-koc/my-apps.git
cd my-apps
python3 -m http.server 8080
```

Open [localhost:8080](http://localhost:8080) and you're running.

## Adding or editing apps

Edit `apps.json`. Each app entry supports:

```jsonc
{
  "id": "my-app",
  "name": "My App",
  "subtitle": "A short tagline",
  "description": "One-liner for list views.",
  "longDescription": "Full description for the detail page.",
  "icon": "https://example.com/icon.png",   // or use iconEmoji: "🚀"
  "iconStyle": { "scale": 1.3, "objectFit": "cover", "borderRadius": "22%" },
  "category": ["mobile", "web"],
  "platform": "iOS & Android",
  "price": "Free",
  "github": "https://github.com/osman-koc/my-app",  // null if private
  "homepage": "https://my-app.dev",
  "language": "Flutter",
  "downloadUrl": "https://play.google.com/store/apps/details?id=com.example.app",
  "requirements": "iOS 13+ or Android 6+",
  "features": ["Feature one", "Feature two"],
  "screenshots": ["https://example.com/screenshot.png"]
}
```

### Categories used in this fork

```json
"categories": [
  { "id": "web", "name": "Web Apps" },
  { "id": "developer-tools", "name": "Developer Tools" },
  { "id": "utilities", "name": "Utilities" },
  { "id": "productivity", "name": "Productivity" },
  { "id": "lifestyle", "name": "Lifestyle" },
  { "id": "health-fitness", "name": "Health & Fitness" },
  { "id": "entertainment", "name": "Entertainment" },
  { "id": "games", "name": "Games" }
]
```

### Featured banner

```json
"featured": [
  {
    "id": "my-app",
    "headline": "NEW",
    "title": "A catchy headline.",
    "subtitle": "A longer description for the featured banner."
  }
]
```

## Update GitHub Stats

Fetch live star and fork counts from the GitHub API:

```bash
./update-stats.sh
```

For higher rate limits:

```bash
GITHUB_TOKEN=ghp_xxx ./update-stats.sh
```

## File Structure

```
├── index.html          Main HTML shell
├── style.css           All styles (dark + light themes)
├── app.js              Routing, rendering, carousel, modals
├── apps.json           All app data — edit this file
├── logo.svg            App icon / favicon
├── update-stats.sh     Fetches GitHub stars/forks into apps.json
├── CNAME               Custom domain for GitHub Pages
└── .nojekyll           Prevents Jekyll processing
```

## Deploy to GitHub Pages

1. Push to a GitHub repo
2. Settings → Pages → Source: branch `master`, folder `/`
3. Add a `CNAME` file with your custom domain (`apps.osmankoc.dev`)

## Credits

- **[Appétit](https://github.com/f/appetit)** — original framework by [Fatih Kadir Akın (FKA)](https://github.com/f) · MIT License
- **kocdev store** — fork & customisation by [Osman Koç](https://osmankoc.dev)

## License

MIT

