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

Regenerate `css/mfz-head.min.css` after every change to `css/mfz-head.css`. Commit **both** files, push to GitHub, then update the jsDelivr URL commit pin in Webflow (see below).

## Webflow head — recommended: jsDelivr (GitHub)

Same pattern as MFZ phone validation:

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/Creo-Global/mfz-phone-validation@6006131/mfz-phone.min.css">
```

Use a **pinned commit** (not `@main`) so production does not change until you deliberately bump the hash:

```html
<!-- MFZ site head styles (gradients, CTAs, forms, blog, a11y) -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/Creo-Global/MFZ-Webflow-Custom-Code@COMMIT_SHA/css/mfz-head.min.css">
```

Replace `COMMIT_SHA` with the full or short git commit that contains the `css/mfz-head.min.css` you want live (copy from GitHub after push).

Example after you publish a release commit:

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/Creo-Global/MFZ-Webflow-Custom-Code@e00bfbd/css/mfz-head.min.css">
```

### Is this fine?

Yes, for MFZ this is a reasonable approach:

- Keeps Webflow **head custom code** small (no huge inline `<style>` block).
- Matches how you already ship `mfz-phone.min.css` from `Creo-Global` on jsDelivr.
- **Pin the commit** so a random push does not alter the live site.

Watch for:

| Topic | Guidance |
|--------|----------|
| **Load order** | Put this link **after** Webflow’s own CSS if you rely on overrides; keep **phone/email** validation CSS where it already works (often after intl-tel-input). |
| **Cache** | jsDelivr caches by URL; changing CSS requires a **new commit** and updating the `@COMMIT_SHA` in Webflow, then publish. |
| **First request** | One extra network request vs inline CSS; usually acceptable. |
| **Repo access** | jsDelivr serves **public** GitHub repos; private repos need another host or inline paste. |
| **Availability** | Site styles depend on jsDelivr + GitHub; same tradeoff as your phone CSS link. |

### Alternative: inline in Webflow

If you prefer zero external CSS dependency, paste into head custom code:

```html
<style>
  /* contents of css/mfz-head.min.css */
</style>
```

Useful for debugging or if the repo is private.

### Private repo (this project)

This GitHub repo is **private**, so jsDelivr `gh/Creo-Global/MFZ-Webflow-Custom-Code/...` will **not** work for production.

Options:

1. **Inline CSS** — paste `css/mfz-head.min.css` inside `<style>` in Webflow head (smallest external dependency).
2. **Public CSS mirror** — publish only `mfz-head.min.css` to a public repo or CDN you already use (same idea as `mfz-phone-validation` on jsDelivr).
3. **Legacy reference** — `webflow-headcode-legacy.html` is the full historical head snapshot (meta, GTM, scripts, inline styles). Use it as a paste reference; **do not** treat the `<html>` wrapper as Webflow head code—copy only the fragments you need.

Keep `css/mfz-head.css` as the editable source in this repo; sync Webflow manually after each change.

## Deploy checklist

1. Edit `css/mfz-head.css`.
2. Run `npm run build:css`.
3. Commit `css/mfz-head.css` and `css/mfz-head.min.css`, push to `main`.
4. Copy the new commit SHA from GitHub.
5. Update Webflow head: jsDelivr link (public mirror) **or** inline `<style>` / legacy paste (private repo).
6. Publish the Webflow site.

## Roadmap

Additional assets (full `header.html`, footer snippets) may live under `css/` and `snippets/` later.
