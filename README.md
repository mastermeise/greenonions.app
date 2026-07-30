# greenonions.app

Marketing site for **Green Onions** — an iPhone app that tempo-matches the music you already own
to your running cadence, in real time, with the pitch preserved.

Static site, hosted on GitHub Pages at <https://greenonions.app>.

## Structure

| File | Purpose |
| --- | --- |
| `index.html` | Landing page. Self-contained; only external request is Oswald from Google Fonts. |
| `privacy.html` | Privacy policy. **Required by App Store Connect** — this URL goes in the app listing. |
| `CNAME` | Custom domain for GitHub Pages. Must contain the bare apex domain. |

## Brand tokens

Kept in sync with `Shared/Theme.swift` in the app repo:

- grass `#00E74D` · lime `#E1F600` · asphalt `#0E0F12` — these are the app icon's
  greens (`design/icon/GO-appicon.svg`); site, app, and icon share one palette.
- Display type: Oswald (SIL OFL). Body: system font.
- The checkerboard is a beat sequencer — cells flip grass→lime on the beat. The hero grid
  animates at 160 BPM (`--beat: .375s`).

## Deploying

Push to `main`. GitHub Pages rebuilds automatically.

## DNS

Registrar and DNS are both Porkbun. Apex `A` records point at GitHub Pages:

```
A     @     185.199.108.153
A     @     185.199.109.153
A     @     185.199.110.153
A     @     185.199.111.153
CNAME www   mastermeise.github.io
```

`.app` is HSTS-preloaded, so HTTPS is mandatory — "Enforce HTTPS" must stay enabled in
repo Settings → Pages.
