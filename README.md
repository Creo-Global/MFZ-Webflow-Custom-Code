# MFZ Webflow Custom Code

Version-controlled custom code for Meydan Free Zone (MFZ) Webflow. Source of truth before paste into **Project Settings → Custom Code**.

Remote: [Creo-Global/MFZ-Webflow-Custom-Code](https://github.com/Creo-Global/MFZ-Webflow-Custom-Code)

## CSS

| File | Purpose |
|------|---------|
| `css/mfz-head.css` | Readable source — edit this |
| `css/mfz-head.min.css` | Minified build for Webflow head or CDN |

### Build minified CSS

```bash
npm install
npm run build:css
```

Regenerate `css/mfz-head.min.css` after every change to `css/mfz-head.css`. Commit **both** files so production matches git without requiring Node on every machine.

### Webflow

Wrap the min (or source) file in a single head embed:

```html
<style>
  /* paste contents of css/mfz-head.min.css or mfz-head.css */
</style>
```

Or host `mfz-head.min.css` and link it (only if you control caching and deploy).

## Status

- Git remote: `origin` → `https://github.com/Creo-Global/MFZ-Webflow-Custom-Code.git`
- More assets (full `header.html`, footer JS) can be added under `css/` and `snippets/` later.
