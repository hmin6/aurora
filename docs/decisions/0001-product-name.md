# 1. Product name: Boreale

**Status:** Accepted
**Date:** 2026-11-07
**Issue:** #1

## Context
"Aurora" was a working name. It is generic and collides with other repos and apps. The
name goes into the Python package, the CLI (`uv run <name> evaluate`), both repo names and
the site's URL. Renaming after code exists means touching package names and imports, so
the name is fixed now, before the scaffold (#2) and the first code (#3).

A candidate had to pass five checks:
1. The GitHub repo name is free under `hmin6`.
2. `<name>.vercel.app` is free.
3. The name is free on PyPI.
4. No well-known app or product with the same name exists in astronomy or weather.
5. It is easy to spell after hearing it (said aloud and typed on a phone).

## Options considered
Checks 1–4 were run live on 2026-11-06 and re-run for Boreale on 2026-11-07.

- **GitHub:** `gh api repos/hmin6/<name>`. A 404 means the name is free.
- **Vercel:** `curl -sI https://<name>.vercel.app`. `X-Vercel-Error: DEPLOYMENT_NOT_FOUND`
  means nothing is deployed there. Any other reply (200, a redirect, 402) means the name
  is in use.
- **PyPI:** `https://pypi.org/pypi/<name>/json` and `https://pypi.org/simple/<name>/`.
  A 404 on both means the name isn't registered.
- **Products:** the App Store search API (`itunes.apple.com/search?entity=software`),
  Google Play search, and web searches for the name with aurora, astronomy and weather.

| Name | GitHub | .vercel.app | PyPI | Astronomy/weather product with this name | Result |
|---|---|---|---|---|---|
| **Boreale** | free | free | free | None. Search results are crowded by "Borealis" aurora apps and the Italian phrase "aurora boreale". | **Chosen** |
| Viewline | free | free | free | No app. NOAA SWPC used "viewline" in its experimental tonight aurora map (2022, removed May 2026). | Passed |
| Ovalcast | free | free | free | None. A similar-sounding AuroraCast app exists. | Passed |
| Oval | free | in use (redirects to oval.tv) | taken (reserved placeholder) | Generic science term | Failed |
| Auroracle | free | free | free | "Auroracle: Aurora Forecast", an App Store Weather app | Failed |
| Skyledger | free | in use (air-freight site) | free | None | Failed |
| Northline | free | in use (disabled deployment) | free | None | Failed |
| Glowcast | free | in use (redirects elsewhere) | free | "GlowCast: Sunrise & Sunset" and "Glowcast: UV Index", both Weather apps | Failed |
| Skycall | free | in use | free | None | Failed |
| Albore | free | in use | free | None | Failed |
| Chiaro | free | in use | taken (graphics library) | None | Failed |
| Notturno | free | in use (redirects elsewhere) | taken (web framework) | None | Failed |
| Aria | free | in use | taken | None, but very crowded | Failed |

Why the other two passing names lost:
- **Viewline:** two plain English words, but it could read as an official NOAA product.
- **Ovalcast:** "oval" is jargon to most people. "-cast" is already common among aurora
  apps (AuroraCast) and brings up screen-casting apps on Google Play.

## Decision
The product is **Boreale** (bo-reh-AH-leh), Italian for "northern", as in *aurora
boreale*. It passed checks 1–4, and it passed check 5 when said aloud and typed on a
phone.

It is always written lowercase as `boreale` in code and URLs:
- repos: `hmin6/boreale` and `hmin6/boreale-archive`
- Python package and CLI: `boreale` (`uv run boreale evaluate`)
- site: `boreale.vercel.app`

## Consequences
- **Mishearing.** English speakers may hear and type it as "boreal" or "borealis".
  Mitigations:
  - the README gives the pronunciation and meaning
  - the name passed the said-aloud and typed-on-a-phone check
  - the spelling is always `boreale`, with no variants
- **Search.** Results for "boreale" are crowded by "Borealis" aurora apps and the Italian
  phrase for the northern lights. Mitigations:
  - the tagline carries the searchable words (northern lights, aurora)
  - links to the site and repos are shared directly rather than relying on search
- **NOAA.** The data comes from NOAA SWPC, so the README states that Boreale is not
  affiliated with NOAA or NWS.
- **Redirects.** Both repos are renamed. GitHub redirects the old URLs only as long as no
  new repo takes the old name, so `hmin6/aurora` and `hmin6/aurora-archive` must never be
  created again.
- **Not reserved yet.** `boreale.vercel.app` is free but unclaimed. It is claimed when the
  Vercel project is created; if it has gone by then, this ADR is revisited. The PyPI name
  only matters if Boreale is ever published as a package, and nothing in the plan does
  that. `uv run boreale` works from the local project without it, so the PyPI name is not
  reserved.
- **Archive.** The archive's package name, User-Agent and docs change to the new name. Its
  devlog keeps "Aurora", because it is a record of what was true then.
