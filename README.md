# Policies

Privacy policies and legal documents for apps published by
[**Yogeshwaran Chandrakasan**](https://github.com/yogeshwaran-c).
Served as a static site via GitHub Pages.

**Live site:** https://yogeshwaran-c.github.io/policies/

## URL pattern

Every app gets a subdirectory and the same URL shape:

```
https://yogeshwaran-c.github.io/policies/                  ← index of all apps
https://yogeshwaran-c.github.io/policies/<app>/            ← per-app landing
https://yogeshwaran-c.github.io/policies/<app>/privacy     ← privacy policy
https://yogeshwaran-c.github.io/policies/<app>/terms       ← terms (optional)
```

These URLs are stable — they're what the Play Console / App Store have
on file, so once an app is published the path for that app should not
change.

## Apps published here

| App | Privacy |
|-----|---------|
| DROPZONE | [`/dropzone/privacy`](https://yogeshwaran-c.github.io/policies/dropzone/privacy) |

## Layout

```
.
├── .nojekyll            ← tells Pages to skip Jekyll so _shared/ is served
├── index.html           ← landing page listing all apps
├── _shared/
│   └── style.css        ← single shared stylesheet for every policy page
└── dropzone/
    ├── index.html       ← per-app legal landing
    └── privacy.html     ← DROPZONE privacy policy
```

`.nojekyll` is required: Pages defaults to Jekyll, which excludes any
directory whose name starts with `_` (including `_shared/`). The empty
sentinel file disables that and the shared stylesheet is published as-is.

## Adding a new app

1. Copy `dropzone/` to `<newapp>/`.
2. Edit `<newapp>/index.html` and `<newapp>/privacy.html` — adjust the
   app name, the "what stays on your device" bullets, the support email.
3. Add a row to the **Apps published here** table above.
4. Add a card link to the root `index.html`.
5. `git push`. Pages rebuilds in ~30 s and the new URL is live.

## Editing an existing policy

Every change is a normal commit; push triggers an auto-redeploy. The URL
stays identical, so nothing in any Play Console listing needs updating.

## License

The site structure (HTML, CSS) is MIT-licensed — see [`LICENSE`](LICENSE).
The policy *content* under each `<app>/` directory describes that specific
app and should not be copied verbatim; treat it as a template.
