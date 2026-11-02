# Shiro Games — Cloudflare Pages deployment

## Authoritative source

- Repository: `Abd-Alrahman-Shaqour/Abd-Alrahman-Shaqour.github.io`
- Production branch: `main`
- Site: plain static HTML/CSS/assets, with no build framework.
- Cloudflare Pages settings: **Connect to Git** (not Direct Upload), repository above, production branch `main`, no build command, output directory `.` (repository root), project name `shiro-games` if available.
- GitHub Cloudflare app: authorize **Only select repositories** and select only the authoritative repository.
- After Git integration is enabled, every push to `main` should automatically deploy to `shiro-games.pages.dev` (actual assigned name may differ).

## Paths to preserve

- `/`: studio homepage
- `/the-comfy-gambit/`: The Comfy Gambit
- `/the-comfy-gambit/privacy.html`: The Comfy Gambit policy
- `/neon-chambers-site/`: Neon Chambers
- `/neon-chambers-site/privacy.html`: Neon Chambers policy
- `/privacy.html`: studio privacy index
- `/support.html`: support
- `/assets/`: images, fonts and intro videos
- `/app-ads.txt`: exact current authorized sellers list, **do not edit or redirect** during migration

## Preserved source

The Neon Chambers HTML, privacy and legacy CSS were copied without modification from `Abd-Alrahman-Shaqour/neon-chambers-site`, which remains intact. The pages use shared root assets and shared root stylesheet in the authoritative repo. After consolidation, edit only the authoritative repo for the live Cloudflare website.

## Cutover / privacy safeguards

1. Buy/register `shirogames.site` in the owner's registrar account. Confirm ownership and renewals.
2. Verify Cloudflare Pages `pages.dev` deployment from Git integration, then make a test push to `main` and verify deployment source SHA changed.
3. Test both game pages, both policies, support, images, intro MP4s and exact bytes of `/app-ads.txt` against the root repository.
4. Inspect all DNS records before changing nameservers; preserve MX, SPF, DKIM, DMARC, verification TXT, and other needed records.
5. Attach `shirogames.site` as Pages custom domain; issue HTTPS certificate; redirect `www.shirogames.site` to the apex after testing.
6. Change the generic website-policy hosting paragraph from GitHub Pages to Cloudflare Pages when the cutover happens, without disturbing game-policy terms.
7. Update Google Play Store URLs for both games, AdMob publisher developer website and app-ads root, Google OAuth homepage and policy settings, plus in-game URL configs only when verified. Treat app binaries as requiring a separately authorized build/release.
8. Do not make either website repository private until old GitHub Pages URLs are audited. Private repositories can disable or break old public GitHub Pages hosting, including policy URLs embedded in released games.
9. Once old links no longer matter or durable redirects are established, verify Cloudflare site in signed-out browsing and only then consider privacy changes. Public assets/policies necessarily remain readable to players even when GitHub source is private.

DO NOT create a Direct Upload Pages project for production; this migration needs GitHub integration.

## Live cutover record — 2 November 2026

**Verified as complete**
- Domain `shirogames.site` is registered at Spaceship, with authoritative DNS moved to Cloudflare: `conrad.ns.cloudflare.com` and `nola.ns.cloudflare.com`. Spaceship auto-renew was observed off; review before renewal.
- Cloudflare zone is active; Pages project `shiro-games` is connected to the consolidated GitHub repository on `main`; `https://shirogames.site/` has an active SSL certificate and serves HTTP 200.
- `www.shirogames.site` uses a Cloudflare 301 redirect to the apex, preserving paths and query strings.
- The canonical game pages, both privacy policies, support page, artwork and intro videos were verified reachable. `https://shirogames.site/app-ads.txt` serves HTTP 200 as `text/plain`, with the required `google.com, pub-3894701665757140, DIRECT, f08c47fec0942fa0` line intact. Assets were compared against the Pages preview.
- Cloudflare Email Address Obfuscation was disabled so its injected script does not change the static policy/support HTML. The studio privacy page was updated to describe Cloudflare hosting, then verified live, establishing functioning Git-to-Pages deployment.
- The public Neon Chambers Google Play listing shows developer website `https://shirogames.site/` and privacy policy `https://shirogames.site/neon-chambers-site/privacy.html`. The Play privacy-policy metadata change was submitted for review.
- The Comfy Gambit **draft** Play entry has support contact and developer website saved, and its privacy-policy URL saved as `https://shirogames.site/the-comfy-gambit/privacy.html`; the app remains a draft.
- The Neon Chambers Google Cloud OAuth branding has homepage/policy URLs on the new domain and `shirogames.site` added as an authorized domain, while the prior domain remains authorized. Google Search Console domain property `shirogames.site` was verified using a Cloudflare DNS TXT record.

**Pending / safeguards**
- AdMob still shows Neon Chambers **Requires review / Limited ad serving**, with an app-ads.txt mismatch message despite the correct public file and new developer website. Its `Check for updates` action was retried; wait for Google's new Play website crawl and recheck. Comfy Gambit AdMob requires a published store listing later.
- Google's OAuth Branding Verification Center still shows the prior ownership rejection, originally referring to the old GitHub Pages homepage. Google's message advised waiting **24 hours after ownership verification** before submitting another branding verification request. Do not confuse saved branding with approved branding.
- AppLovin MAX signup reached a completed signup page, but the MAX dashboard requires account sign-in; app/network account integration has not been verified.
- The local `D:\Work\Casual-Puzzle-Games\Assets\PuzzleTemplate\NeonResources~\PuzzleTemplateMonetization.json` was updated to the new Neon privacy URL on the currently checked-out Chess branch. This is **not a published app update**; no Unity build was run.
- Both website repositories are still **public**. Do not privatize them until shipped apps, OAuth, AdMob and any external systems no longer rely on the old `abd-alrahman-shaqour.github.io` routes, or a proven public compatibility redirect exists. Converting the user.github.io repository to private can break those URLs.
- No AAB/APK build, Unity Player build or store binary release was performed. The Comfy Gambit draft was not submitted for release.



## SEO / Google Search setup — 2 November 2026

- Deployed a real `sitemap.xml` at `https://shirogames.site/sitemap.xml` listing 8 canonical URLs: studio homepage, both game pages, Comfy Daily leaderboard, support, privacy landing, and both game policies. The earlier sitemap URL incorrectly served homepage HTML due to Pages' SPA fallback.
- Added Cloudflare Pages `_headers` to set `Content-Type: application/xml; charset=utf-8` on `/sitemap.xml` and to add `X-Robots-Tag: noindex` only on the duplicate `https://shiro-games.pages.dev/*` host. Confirmed live XML parses with 8 URLs, Googlebot-style request returns HTTP 200 and correct type; public main domain's page headers are not marked noindex.
- All 8 HTML pages now emit their preferred **absolute canonical** links, page-specific `<title>`, unique meta descriptions, Open Graph previews and Twitter cards. The studio homepage gained `Organization` and `WebSite` JSON-LD; both game pages gained game-appropriate `VideoGame` JSON-LD. Gameplay, Privacy, AdMob app-ads, legacy URLs, script and existing layout were not intentionally changed. Rechecked canonical/OG on all 8 production routes.
- Improved on-page text on homepage to describe Neon Chambers' 500 Android sliding-block puzzles and Comfy Gambit's in-development 3D chess puzzler, without claiming that Comfy is published. Dedicated Neon and Comfy page titles/descriptions now target their **actual game names** plus meaningful puzzle/chess terms instead of generic 'Shiro Games' only.
- Google Search Console property `sc-domain:shirogames.site` is **verified**. Submitted `https://shirogames.site/sitemap.xml` through Sitemaps UI; it confirmed **'Sitemap submitted successfully'**. Its initial status reported **'Couldn't fetch'** with no discovered pages. Despite a correct public XML response, **this must be monitored** and cannot be counted as Google having accepted or indexed those 8 URLs yet. Do not continuously re-submit an unchanged sitemap; recheck after Google retries.
- Google URL Inspection reported **home URL unknown to Google**, and both Neon Chambers and The Comfy Gambit as **discovered — currently not indexed**. Submitted individual indexing requests for the homepage and both game landing pages. Search Console confirmed **'Indexing requested'**. Requests do not guarantee indexing or first-position rankings. Expect days/weeks; review page-level status and Search Performance over time.
- SEO caution: `https://shirogames.com/` is an established and unrelated French game studio branded **Shiro Games** (Northgard/Wartales/Dune: Spice Wars). Ranking first for the ambiguous term 'Shiro Games' will be particularly hard and can create naming confusion. Prioritize unique names **Neon Chambers**, **The Comfy Gambit** and precise long-tail game searches. Obtain independent brand/trademark review before major marketing spend; no brand identity/domain changed during this technical task.
- Next: check GSC Sitemaps until **Success** and 8 discovered URLs, inspect indexed pages and ranking queries, link the canonical studio and Neon game pages from legitimate Google Play listing/social/store profiles, consider useful developer content (original gameplay guides, release notes, accessibility, screenshots), measure mobile performance with PageSpeed Insights, and build natural links from game coverage. Avoid link buying or keyword stuffing. SEO does not guarantee position #1.
