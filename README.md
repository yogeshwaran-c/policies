# YC Policies — Multi-App Legal Pages

This directory is structured to live as a **separate public repository**
(e.g. `yogeshwaran-c/policies`) with GitHub Pages enabled. It hosts the
privacy policy and any future legal documents for every app published
under your name — one source of truth, one URL pattern, easy to add the
next app.

## URL pattern

When GitHub Pages is enabled on `yogeshwaran-c/policies` (default
branch `main`, source `/` root), the resulting URLs become:

```
https://yogeshwaran-c.github.io/policies/                  ← landing page (index of all apps)
https://yogeshwaran-c.github.io/policies/dropzone/         ← per-app landing
https://yogeshwaran-c.github.io/policies/dropzone/privacy  ← DROPZONE privacy
https://yogeshwaran-c.github.io/policies/dropzone/terms    ← DROPZONE terms (future)
https://yogeshwaran-c.github.io/policies/<next-app>/privacy
```

The DROPZONE privacy URL goes into the Play Console Privacy Policy
field. When you ship a second app, copy `dropzone/` to a new subdir,
edit the contents, and the new URL is immediately live.

## Directory layout

```
policies/
├── README.md                ← this file (won't be served)
├── index.html               ← root landing page listing all apps
├── _shared/
│   └── style.css            ← single shared stylesheet, light/dark aware
└── dropzone/
    ├── index.html           ← DROPZONE legal landing (links to privacy)
    └── privacy.html         ← DROPZONE privacy policy
```

Adding a second app later:

```
policies/
├── ...
├── dropzone/
└── newapp/
    ├── index.html
    └── privacy.html
```

## Spinning it up as a separate public repo

1. Create a new empty public repository on GitHub: `yogeshwaran-c/policies`.

2. Copy the **contents** of this `policies/` directory (not the directory
   itself) into the root of the new repo:

   ```powershell
   cd C:\path\to\local\workspace
   git clone git@github.com:yogeshwaran-c/policies.git
   cd policies
   # Copy everything inside the tetris repo's policies/ directory into here
   Copy-Item -Path "C:\Users\YogeshwaranChandraka\Projects\yc\tetris\policies\*" -Destination . -Recurse
   git add .
   git commit -m "feat: initial DROPZONE privacy policy"
   git push
   ```

3. Enable GitHub Pages: repo Settings → Pages → Source = "Deploy from
   branch", Branch = `main`, Folder = `/ (root)`. Save. Wait ~30s.

4. Verify the URL resolves:
   `https://yogeshwaran-c.github.io/policies/dropzone/privacy`

5. Paste that URL into:
   - Play Console → App content → Privacy policy → URL
   - The "Privacy" link in any in-app About screen if you want to deep-link

6. Delete the `policies/` directory from this tetris repo (or keep it as
   an editable mirror — either works, but having one source of truth in
   the dedicated repo is cleaner). Recommended:

   ```powershell
   git rm -r policies/
   git commit -m "chore: move policies to yogeshwaran-c/policies"
   ```

## Editing later

Every change is a normal commit in the policies repo. Push, GitHub Pages
rebuilds automatically within seconds. The URLs don't change.

If you want a richer authoring experience (markdown source, templates,
preview server), wrap this in Astro / 11ty later — the URL pattern can
stay identical so nothing breaks.

## Why a separate repo

- **Clean separation of concerns.** The app code repo doesn't need to
  carry legal HTML.
- **Reusable across apps.** One URL prefix, one stylesheet, one
  domain to remember.
- **Public by default.** App code repos may be private; legal pages
  must be publicly fetchable.
- **No build pipeline needed.** GitHub Pages serves static HTML
  directly; no Node, no React, no JAMstack overhead.
