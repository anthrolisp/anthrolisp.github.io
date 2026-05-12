# Personal site — Justin Shaffner

Single-page static site, built for GitHub Pages.

## Files

- `index.html` — the page (HTML + CSS inlined for portability)
- `portrait.jpg` — photo, 600×800, ~78 KB; referenced as `portrait.jpg` (same directory as index.html)

That's the whole site. No build step, no dependencies.

## Deployment to GitHub Pages

1. Create a GitHub repo. For a user-level site, name it `<your-username>.github.io` (e.g. `justinshaffner.github.io`); the URL becomes `https://<your-username>.github.io/`. For a project-level site, name it anything; the URL becomes `https://<your-username>.github.io/<repo-name>/`.
2. Copy `index.html` and `portrait.jpg` into the repo root.
3. Commit and push.
4. In the repo: **Settings → Pages → Source: Deploy from a branch → `main`, root `/`**. Save.
5. Wait 30–60 seconds. The URL above is now live.

## Deployment from the command line

Two ways, depending on whether you have the GitHub CLI (`gh`) installed. The `gh` path is shorter.

### With `gh` (recommended)

From inside the site folder (where `index.html` lives):

```bash
git init -b main
git add .
git commit -m "Initial site"
gh repo create justinshaffner.github.io --public --source=. --push
```

That's it. For a repo named `<username>.github.io`, GitHub auto-enables Pages on the default branch — wait ~30–60 seconds and the site is live at `https://justinshaffner.github.io/`.

If `gh` isn't installed: `brew install gh` on macOS, or see `https://cli.github.com/`. First run `gh auth login` once to authenticate.

### With plain `git`

Create the empty repo on the web first at `https://github.com/new` (name it `justinshaffner.github.io`, leave it empty — no README, no .gitignore). Then locally:

```bash
git init -b main
git add .
git commit -m "Initial site"
git remote add origin git@github.com:justinshaffner/justinshaffner.github.io.git
git push -u origin main
```

(Use `https://github.com/justinshaffner/justinshaffner.github.io.git` for the remote URL if you prefer HTTPS over SSH.)

Then visit `Settings → Pages` in the repo and confirm the source is `main` / root — for user sites this is usually pre-set.

### Updating the live site

After the initial push, any edit goes live with three commands:

```bash
git add .
git commit -m "Update content"
git push
```

GitHub rebuilds the Pages site within ~30–60 seconds of the push.

### Custom domain (optional, command line)

To point a domain like `justinshaffner.com` at the Pages site:

1. With your DNS provider, add the four `A` records GitHub publishes (`185.199.108.153`, `.109.153`, `.110.153`, `.111.153`) for the apex domain, and a `CNAME` for `www` pointing at `<your-username>.github.io`.
2. From the repo: `echo "justinshaffner.com" > CNAME && git add CNAME && git commit -m "Add custom domain" && git push`
3. In `Settings → Pages`, the custom domain field will pick up the `CNAME` file automatically. Tick **Enforce HTTPS** once the certificate provisions (a few minutes).

## Replacing the photo

Drop a new image into the repo root with filename `portrait.jpg`. Push. Done.

If you want a different filename, change the two references in `index.html`:
- The `<img src="portrait.jpg" …>` tag in the header
- The `<meta property="og:image" content="portrait.jpg">` tag (used for link previews on social media)

For best results: portrait orientation, roughly 3:4 ratio, 600px wide minimum, JPEG or PNG. The CSS uses `object-position: center 30%;` so faces in the upper portion of the frame display well; adjust that value if the new photo needs a different focal point.

## Editing content

The HTML is straightforward; section headings are `<h2>` and each section has an anchor ID (e.g. `#orientation`, `#the-nggiwe-event`) that matches the slug. These IDs are what future subpages would route from — so don't change them unless you also update any links pointing at them.

The CSS variables at the top of the `<style>` block control palette, typography, and layout width. Adjust there for global changes.

## Custom domain (optional)

If you want a domain like `justinshaffner.com` pointing at the GitHub Pages site:

1. In the repo: **Settings → Pages → Custom domain**. Enter the domain. Save.
2. With your DNS provider, add the records GitHub specifies (typically four `A` records pointing at GitHub's IPs, plus a `CNAME` for `www`).
3. GitHub creates a `CNAME` file in the repo with the domain name. Don't delete it.
4. Wait for DNS propagation (minutes to hours). Enforce HTTPS in the same Pages settings screen once it's available.

## Fonts

Fraunces and Noto Naskh Arabic are loaded from Google Fonts. If you want fully offline / self-hosted fonts later, that's a one-line change in the `<link>` tag plus uploading the font files.
