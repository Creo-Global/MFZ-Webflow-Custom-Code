# MFZ Webflow Custom Code

Version-controlled custom code for Meydan Free Zone (MFZ) Webflow. Source of truth before paste into **Project Settings → Custom Code**.

Remote: [Creo-Global/MFZ-Webflow-Custom-Code](https://github.com/Creo-Global/MFZ-Webflow-Custom-Code)

## CSS

| File | Purpose |
|------|------|
| `css/mfz-head.css` | Readable source — edit this |
| `css/mfz-head.min.css` | Minified build for Webflow head or CDN |

### Build minified CSS

```bash
npm install
npm run build:css
```

Regenerate `css/mfz-head.min.css` after every change to `css/mfz-head.css`. Commit **both** files and push to GitHub.

## Webflow head

### jsDelivr (public GitHub only)

If the file is available on a **public** GitHub repo, load it with a **pinned commit** (not `@main`):

```html
<!-- MFZ site head styles (gradients, CTAs, forms, blog, a11y) -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/Creo-Global/MFZ-Webflow-Custom-Code@COMMIT_SHA/css/mfz-head.min.css">
```

Replace `COMMIT_SHA` with the git commit that contains the `css/mfz-head.min.css` you want live.

Benefits:

- Smaller Webflow head custom code (no large inline `<style>` block).
- Production changes only when you bump the commit pin in Webflow.

| Topic | Guidance |
|--------|----------|
| **Load order** | Place **after** Webflow’s own CSS when you need overrides. |
| **Cache** | jsDelivr caches by URL; ship CSS in a new commit and update `@COMMIT_SHA`, then publish Webflow. |
| **First request** | One extra network request vs inline CSS. |
| **Private repo** | jsDelivr cannot serve private GitHub repos — use inline CSS or another CDN you control. |

### Inline (private repo or no CDN)

Paste into head custom code:

```html
<style>
  /* contents of css/mfz-head.min.css */
</style>
```

### Legacy reference

`webflow-headcode-legacy.html` is a full historical head snapshot (meta, tags, scripts, inline styles). Use it as a paste reference only — do not paste the `<html>` wrapper into Webflow; copy the fragments you need.

Keep `css/mfz-head.css` as the editable source in this repo and sync Webflow manually after each change.

## Deploy checklist

1. Edit `css/mfz-head.css`.
2. Run `npm run build:css`.
3. Commit `css/mfz-head.css` and `css/mfz-head.min.css`, push to `main`.
4. Copy the new commit SHA from GitHub (if using jsDelivr).
5. Update Webflow head (CDN link or inline `<style>` / legacy fragments).
6. Publish the Webflow site.

## Roadmap

Additional assets (full head snippets, footer code) may live under `css/` and `snippets/` later.
