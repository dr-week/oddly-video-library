.film-card{padding:0;border:0;text-align:left;color:inherit;background:transparent;width:100%}.film-card:focus-visible,.button:focus-visible,.chip:focus-visible,.icon-button:focus-visible{outline:2px solid var(--accent);outline-offset:3px}.ai-badge{position:absolute;z-index:2;left:10px;top:10px;padding:5px 7px;border-radius:4px;background:var(--accent);color:#17190e;font-size:8px;font-weight:700;letter-spacing:.6px}.modal-backdrop{position:fixed;inset:0;z-index:20;background:#07080bcc;backdrop-filter:blur(4px);display:grid;place-items:center;padding:16px}.dialog{position:relative;width:min(480px,100%);max-height:90vh;overflow:auto;border:1px solid #3b3d44;border-radius:10px;background:#17191f;color:var(--text);padding:33px;box-shadow:0 25px 100px #000b}.dialog-close{position:absolute;right:17px;top:15px;border:0;background:none;color:#9b9da5;font-size:25px;cursor:pointer}.dialog h2{font:600 30px var(--display);letter-spacing:-1.4px;margin:12px 0 7px}.dialog-intro{font-size:12px;color:#9b9da5;line-height:1.6;margin:0 0 20px}.dialog form>label:not(.consent){display:block;color:#c9cbd0;font-size:11px;margin:13px 0}.dialog input:not([type=checkbox]),.dialog select{display:block;width:100%;height:39px;margin-top:7px;border-radius:5px;border:1px solid #393b43;background:#101115;color:var(--text);padding:0 11px;outline:0;font-size:12px}.dialog input:focus,.dialog select:focus{border-color:var(--accent)}.consent{display:flex;align-items:flex-start;gap:10px;color:#aeb0b6;font-size:10px;line-height:1.5;margin:17px 0}.consent input{accent-color:var(--accent);margin-top:2px}.submit-form-button{width:100%;justify-content:space-between}.form-note{font-size:9px;line-height:1.5;color:#747781;margin:13px 0 0}.form-success{margin-top:13px;background:#d2fc7619;color:var(--accent);padding:10px;border-radius:4px;font-size:11px}.clip-dialog .clip-preview{position:relative;overflow:hidden;aspect-ratio:16/9;border-radius:6px;margin-bottom:22px;background:#282a34}.clip-preview>.poster-art{position:absolute;inset:0}.preview-message{position:absolute;inset:0;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:9px;background:#1011158c;text-align:center}.preview-message span{font-size:34px;color:var(--accent)}.preview-message strong{font:600 12px var(--display);letter-spacing:1.4px}.preview-message small{font-size:10px;color:#cbcbd0}.hero-sticker{position:absolute;z-index:3;right:22px;bottom:21px;width:63px;height:63px;border-radius:50%;display:grid;place-content:center;text-align:center;background:var(--accent);color:#191b11;font:700 9px/1.5 var(--display);transform:rotate(12deg)}
+.light .dialog{background:#f7f7f3;color:#17181b}.light .dialog input:not([type=checkbox]),.light .dialog select{background:#fff;color:#17181b}.light .footer .brand{color:#17181b}
+'@ | Add-Content -Path $p -Encoding utf8
@'
# Oddly

A responsive short-video catalog prototype for AI-made comedy clips and creator-owned media. Built with Svelte 5, TypeScript, Vite, and SCSS. All listed titles and creators are fictional; posters are CSS artwork. No source-site videos are copied or embedded.

## Run locally

- Install Node.js 20.19+ or 22.12+.
- Run `npm install`.
- Run `npm run dev` to start the local site.
- Run `npm run build` to create the static `dist/` site.

## Free static hosting

Deploy the generated `dist/` directory to GitHub Pages, Cloudflare Pages, or Netlify free tiers. Build command: `npm run build`. Output directory: `dist`. The site is static; no server, database, or external video API is configured.

## Prototype limits

Search, category filters, theme switch, clip details, and submission UI work in-browser. Sample clip cards intentionally do not play video. The submission form does not upload or publish; connect a backend and a rights/consent review process before accepting public submissions. The ad slot is inactive and contains no ad network or tracking code.
