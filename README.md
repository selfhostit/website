# selfhostit website

The selfhostit site: the app menu, the one-line installer and the custom-order page. It is
plain HTML and CSS with no build step, served by GitHub Pages. The install guide it links to
is in [selfhostit/docs](https://github.com/selfhostit/docs).

- `index.html`: the page
- `style.css`: styles, with a light and a dark theme
- `img/`: app icons and screenshots, copied from the app repositories and resized
- `.github/ISSUE_TEMPLATE/request.yml`: the form behind "Tell us what you need"

To see it, open `index.html` in a browser, or run `python3 -m http.server` here and open
http://localhost:8000.

## Adding an app to the menu

Copy one `<article class="app">` block in `index.html`, put a 160px icon and a 480px wide
screenshot in `img/`, and link the app's repository.

## Publishing with GitHub Pages and a Porkbun domain

1. On GitHub: Settings > Pages > Build and deployment: **Deploy from a branch**, branch
   `main`, folder `/ (root)`. The site goes live at `https://selfhostit.github.io/website/`.
2. Still under Pages, enter your domain (for example `selfhostit.com`) under **Custom
   domain** and save. GitHub adds a `CNAME` file to the repository.
3. On Porkbun: Domain Management > your domain > **DNS**. Delete the default parking records
   (the `ALIAS` or `A` records for the bare domain and the `*` and `www` `CNAME`s), then add:

   | Type | Host | Answer |
   |---|---|---|
   | A | (blank) | 185.199.108.153 |
   | A | (blank) | 185.199.109.153 |
   | A | (blank) | 185.199.110.153 |
   | A | (blank) | 185.199.111.153 |
   | CNAME | www | selfhostit.github.io |

   Porkbun's DNS page also has a **Quick DNS config** menu with a GitHub Pages option that
   adds the same records.
4. Back on GitHub, wait until the DNS check passes (minutes, sometimes an hour), then tick
   **Enforce HTTPS**.

Every push to `main` then updates the site within a minute.

Optional: to stop anyone else from claiming the domain on GitHub Pages, verify it in the
organization settings under Pages > Add a domain.
