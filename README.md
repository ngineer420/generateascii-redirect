# generateascii-redirect

This repository forwards the retired generateascii.com to inascii.com.

GitHub Pages serves one custom domain for each repository. The old domain thus needs
its own repository. Each URL that the old sitemap listed has a file here. Each URL
answers with status 200 and forwards, instead of a fall to 404.html.

Each stub forwards to the canonical URL that the same page declares on the new site.
404.html forwards all other paths and keeps the path.

A true 301 needs a Cloudflare Redirect Rule. The DNS-scope API token cannot make one.
This repository thus uses a canonical link, a meta refresh, and a JS replace.
