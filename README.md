# Ember & Salt — Deployed Site (gh-pages)

This branch contains only the **built output** of the Ember & Salt site,
served directly by GitHub Pages.

**This is not the source code.** Do not edit files here directly — any
changes will be overwritten the next time the site is redeployed.

## What's in this branch

The compiled, ready-to-serve version of the site:

- index.html
- menu.html
- contact.html
- style.css

(plus any other build assets — images, fonts, bundled JS, etc.)

## Where the real source lives

All source files, documentation, and design notes live on the `main`
branch. See that branch's README for:

- File structure and page-by-page breakdown
- Color palette and typography decisions
- The faceted-panel signature shape and design rationale
- Accessibility and responsive behavior notes
- Placeholder content that still needs to be replaced before launch

## How this branch gets updated

This branch is regenerated from `main` on each deploy — typically via
something like:

```bash
git checkout gh-pages && git merge main --no-edit
# build step, if any
git add . -f && git commit -m "Deployment commit"
git push origin gh-pages
git checkout main
```

If you need to make a change to the site, make it on `main`, then
redeploy — don't edit anything on `gh-pages` directly.

## Live site

Served via GitHub Pages from this branch's root. Check the Live URL:
https://jaysssmm.github.io/Restaurant-Page/

Served via GitHub Pages from this branch's root. Check the repo's
**Settings → Pages** for the live URL.
