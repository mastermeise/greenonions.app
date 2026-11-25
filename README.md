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
| `support.html` | Support page. **Required by App Store Connect** — the listing's support URL. Long-form FAQ; the landing page's Questions section is the short form of the same answers. |
| `robots.txt` | Allows every crawler, AI assistants included, and points at the sitemap. Added 2026-09-06 after chatgpt.com appeared as a referrer. |
| `sitemap.xml` | The three pages. Add a row when a page is added. |

## Search and assistants

`index.html` carries JSON-LD (`SoftwareApplication` + `FAQPage`) in its head. The FAQ entries
mirror the Questions section word for word: change one, regenerate the other. No `llms.txt`,
deliberately; revisit if assistant referrals become a steady share of visits.

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

## podcasts/rows.json

The app (2.0 and later) reads this file once a launch for the rows on Library →
Podcasts: a name and the Apple podcast categories that fill it. No file, or a file that
doesn't read, and the app keeps the rows built into it. Nothing links to it, so it isn't
in the sitemap.

Build and check it with `marketing-2.0/rows.py` in the app repo (`wip/talks`). January
2027's row, "First runs of the year", comes out again on 1 Feb:

    python3 -c "import json;p='podcasts/rows.json';d=json.load(open(p));d['rows']=[r for r in d['rows'] if r['id']!='firstruns2027'];json.dump(d,open(p,'w'),ensure_ascii=False,indent=1)"
