# Staging copy of the website

This repository is a sandbox for trying changes to the research website before they go live.

| | Repository | Address |
|---|---|---|
| Production | `alizia369/alizia369.github.io` | https://alizia369.github.io (and www.ali-zia.me) |
| Staging | this repository | https://alizia369.github.io/site-staging/ |

## How it differs from production

- `.github/workflows/pages-staging.yml` builds the site with `SITE_BASE=/<repo name>` and publishes it to GitHub Pages. Every page gets an orange "Staging preview" bar and a `noindex` tag so search engines ignore it.
- The production workflows are removed here: no FTP upload to Solid Hosting and no scheduled Google Scholar commits.
- Everything else (data files, `build.py`, `assets/`, committed HTML) is kept identical in form to production, so changes can be promoted as they are.

## Working here

1. Edit data files, `build.py` or `assets/` as usual.
2. Run `python3 build.py` (no `SITE_BASE`) and commit the generated HTML, exactly as in production.
3. Push to `main`. The preview updates in about a minute.

## Promoting a change to production

Copy over only the commits you want, and never the files in `.github/` or this file. For example, from a clone of the production repository with this repository added as a remote named `staging`:

```
git fetch staging
git cherry-pick <commit>     # one commit at a time
python3 build.py && git commit -am "Rebuild"   # if the cherry-pick touched data or build.py
git push origin main
```
