# Sign-in Page Branding Checker

A lightweight, browser-based tool for reviewing the custom styling (CSS) that a
company applies to its Microsoft Entra sign-in page. It highlights styling rules
that can **move or stack elements** on the page, so reviewers can quickly see how
a tenant's branding affects the layout of the sign-in experience.

**Live tool (customer view):** https://gabrielgamy.github.io/signin-branding-checker/
**Support view:** https://gabrielgamy.github.io/signin-branding-checker/support.html

---

## Two views

The tool ships as **two separate pages** that share the same look and analysis
engine:

- **`index.html` — customer view (default).** A deliberately simple page with just
  **Check a styling link** and the results table. This is what external users see.
- **`support.html` — support view.** Everything the support/branding team needs:
  **check by company ID**, **check a styling link**, and the **positioning
  allowlist builder**.

> **Note — this is presentation-level separation, not access control.** Both pages
> are static files served publicly by GitHub Pages, and the repo is public. Anyone
> who knows or guesses the `support.html` URL can open it. It keeps the customer
> page clean; it does **not** restrict the support tools. If the support features
> ever need to be truly protected, they must move behind an authenticated backend
> (or be kept out of the public deployment entirely).

---

## What it does

- **Check a styling link** *(both views)* — paste the tenant's `customcss` web
  address and the tool downloads it and analyzes it directly. This is the most
  reliable path.
- **Check a company by its ID** *(support view only)* — enter a tenant ID or domain
  and the tool builds the sign-in URL and tries to locate the tenant's custom
  styling. If the browser blocks the automatic lookup, it shows simple steps to
  grab the styling link manually.
- **Results table** *(both views)* — lists each styling rule that can reposition or
  layer content, showing the affected page area, the CSS property, and its value,
  plus a short summary of how many settings and page areas are involved.
- **Positioning allowlist builder** *(support view only)* — collect the tenant IDs
  that should be allowed to use positioning styling. Each entry is timestamped,
  duplicates are blocked automatically, and the list can be exported to a JSON file
  to share, or re-imported later (merges without duplicates).

## How it works

Each page is a **single, self-contained HTML file**. All analysis runs entirely in
your browser — nothing is uploaded to a server, and no data leaves the page. CSS
is parsed with the browser's built-in engine, the same way a page would apply it.

## Using it

1. Open the live link above (customer view), or `support.html` for the full toolset.
2. For a quick check, use **Check a styling link**: paste a styling web address (it
   contains the word `customcss`) and click **Check the styling**.
3. Review the table of results.
4. On the **support view** (`support.html`), you can also build the allowlist: add
   tenant IDs under **Positioning allowlist** and use **Download list to share** to
   export the file.

> **Tip:** The working allowlist (support view) is saved in your browser. Click
> **Download list to share** before closing if you've added entries you want to keep.

## Notes

- Best experienced over HTTPS (the hosted link above). Opening the file from a
  document viewer or preview may block the styling download.
- The tool only **reads and reports** — it never changes any tenant configuration.

## Updating

Edit `index.html` (customer view) and/or `support.html` (support view) — they share
the same styling and analysis logic, so keep changes to the common parts in sync.
Then:

```bash
git commit -am "Update tool"
git push
```

The hosted pages redeploy automatically within a minute or two.
