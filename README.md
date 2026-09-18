# Overcoming Average

Podcast and personal brand site for Chad Keith. Live on GitHub Pages from `main` at `/`.

**Preview:** https://chadakeith.github.io/overcoming-average/

**Later domain:** `overcomingaverage.net` (DNS cutover is a later task. Do not flip registrar or Cloudflare DNS from this repo yet.)

## Pages

- Home
- Episodes
- About

No FAQ, team, privacy, or terms stubs. No invented Apple / Spotify / feed URLs. Listen links stay as "Listen links coming" until real URLs exist.

## Local preview

```bash
python3 -m http.server 8080
```

Open http://127.0.0.1:8080/

## GitHub Pages

Source: branch `main`, folder `/`. A `.nojekyll` file is in the root so Pages serves the files as-is.

`CNAME.example` is a reminder only. There is no live `CNAME` file, so github.io stays the preview host until the domain cutover.

## DNS cutover later (Cloudflare, apex + www)

Do this only when you are ready to move `overcomingaverage.net` off the current host. Do not change DNS in this task.

1. In this repo, add a root file named `CNAME` with a single line:
   ```
   overcomingaverage.net
   ```
   Commit it to `main`. GitHub Pages will then expect the custom domain.
2. In the GitHub repo: **Settings → Pages → Custom domain** → `overcomingaverage.net`. Check **Enforce HTTPS** after certificates issue.
3. In Cloudflare DNS for `overcomingaverage.net`:
   - Apex (`overcomingaverage.net`): CNAME flattened to `chadakeith.github.io`, or A records to the current GitHub Pages IPs from [GitHub Pages custom domain docs](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site).
   - `www`: CNAME to `chadakeith.github.io`.
   - Proxy status: start on DNS only (grey cloud) until the GitHub SSL cert issues, then you can orange-cloud if you want.
4. After the domain resolves, update these files from the github.io URLs to `https://overcomingaverage.net/`:
   - canonical and `og:url` on each page
   - `sitemap.xml`
   - `robots.txt`
   - `site.webmanifest` start/scope/icon paths
   - 404 absolute asset paths
5. Set the GitHub repo homepage to `https://overcomingaverage.net`.

Until that cutover, keep canonical, sitemap, and robots pointed at the github.io preview.
