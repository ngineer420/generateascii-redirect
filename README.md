# generateascii-redirect

This repository forwards the retired generateascii.com to inascii.com.

GitHub Pages serves one custom domain for each repository. The old domain thus needs
its own repository. Each URL that the old sitemap listed has a file here. Each URL
answers with status 200 and forwards, instead of a fall to 404.html.

Each stub forwards to the canonical URL that the same page declares on the new site.
404.html catches all other paths.

Each page forwards two ways, because a static file cannot send a 301:

- A meta refresh, for a client with no JavaScript. It carries one fixed URL, so a stub
  loses the query string, and 404.html loses the path.
- A `location.replace` call, which keeps the query and the hash. On 404.html it also
  keeps the path. Googlebot runs this one.

No stub carries `noindex`. A cross-domain canonical is the only way to move the ranking
signal without a 301, and `noindex` stops Google from following it.

A true 301 needs a Cloudflare Redirect Rule. The DNS-scope API token cannot make one.
This repository thus uses a canonical link, a meta refresh, and a JS replace.
