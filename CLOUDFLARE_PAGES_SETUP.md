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
