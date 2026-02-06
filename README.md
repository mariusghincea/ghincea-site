# ghincea.eu — Personal Academic Website

Built with [Hugo](https://gohugo.io/) and [HugoBlox Academic CV](https://github.com/HugoBlox/hugo-theme-academic-cv).

## Prerequisites

1. **Git**: [Install Git](https://git-scm.com/downloads)
2. **Hugo Extended** (v0.144+): [Install Hugo](https://gohugo.io/installation/)
   - macOS: `brew install hugo`
   - Windows: `choco install hugo-extended` or `winget install Hugo.Hugo.Extended`
   - Linux: `sudo snap install hugo`
3. **Go** (v1.21+): [Install Go](https://go.dev/dl/) (required for Hugo modules)

## First-Time Setup

### Recommended: Start from the official template, then swap in your content

The `go.mod` in this project references HugoBlox modules. The cleanest
setup path is:

```bash
# 1. Create a fresh site from the official template
npx hugoblox create site --template academic-cv ghincea-fresh
cd ghincea-fresh

# 2. Copy your customized content files over the template defaults:
#    - Copy the entire content/ directory from this project
#    - Copy config/_default/*.yaml files
#    - Copy hugoblox.yaml, netlify.toml, package.json, .gitignore
#    - Copy assets/css/custom.css
#    - Copy layouts/ directory

# 3. Initialize and verify
hugo mod tidy
hugo server --disableFastRender
```

### Alternative: Use this project directly

```bash
git clone https://github.com/YOUR_USERNAME/ghincea-site.git
cd ghincea-site

# Initialize Hugo modules (this downloads the HugoBlox theme)
# You may need to run `hugo mod get -u` to resolve correct versions
hugo mod get -u
hugo mod tidy

hugo server --disableFastRender
```

Open http://localhost:1313 in your browser.

> **Note:** If you get Go module errors, the recommended approach above
> (starting from the official template) is more reliable, since it generates
> a correct `go.mod` and `go.sum` automatically.

## Project Structure

```
ghincea-site/
├── config/_default/
│   ├── hugo.yaml          # Main Hugo config (baseURL, title)
│   ├── params.yaml        # Site parameters (theme, SEO, footer)
│   ├── menus.yaml         # Navigation menu
│   └── languages.yaml     # Language settings
├── content/
│   ├── _index.md          # HOMEPAGE (block-based layout)
│   ├── authors/admin/
│   │   └── _index.md      # YOUR PROFILE (bio, social links, photo)
│   ├── publication/       # Each publication = one folder
│   │   ├── enlargement-jepp-2025/
│   │   │   └── index.md
│   │   └── ...
│   ├── research/
│   │   └── _index.md      # Research agenda page
│   ├── teaching/
│   │   └── _index.md      # Teaching page
│   ├── media/
│   │   └── _index.md      # Media appearances & commentary
│   └── post/              # Blog posts (add as needed)
├── assets/
│   ├── media/             # Profile photo goes here (avatar.jpg)
│   └── css/custom.css     # CSS overrides
├── static/uploads/        # CV PDF and other downloadable files
├── go.mod                 # Hugo module dependencies
├── hugoblox.yaml          # HugoBlox theme config
└── netlify.toml           # Netlify deployment config
```

## Key Tasks

### Add your profile photo
Place your photo as `assets/media/avatar.jpg` (or `.png`).
Recommended: square crop, at least 400x400px.

### Add your CV
Place your CV as `static/uploads/cv.pdf`.

### Update your email
The current site uses your EUI email. Update it in:
- `content/authors/admin/_index.md` (social links section)

### Add a new publication
```bash
# Create a new folder under content/publication/
mkdir content/publication/my-new-paper
```

Create `content/publication/my-new-paper/index.md`:
```yaml
---
title: "Paper Title"
authors:
  - admin              # Use 'admin' for yourself
  - Coauthor Name
date: '2025-01-01'
publication_types: ['article-journal']  # or: chapter, book, manuscript
publication: '*Journal Name*, Volume(Issue): Pages'
doi: '10.xxxx/xxxxx'
abstract: "Abstract text here."
tags:
  - relevant-tag
featured: false        # Set true to highlight on homepage
---
```

### Add a blog post
```bash
mkdir content/post/my-post-slug
```

Create `content/post/my-post-slug/index.md`:
```yaml
---
title: "Post Title"
date: 2025-01-15
tags:
  - European security
summary: "One-line summary."
---

Post content in Markdown here.
```

### Fill in the media page
The file `content/media/_index.md` has placeholder entries marked with HTML comments.
Replace them with your actual media appearances and links.

## Deployment

### Option A: Netlify (Recommended)

1. Push this repo to GitHub
2. Go to [netlify.com](https://www.netlify.com/), sign in with GitHub
3. Click "New site from Git" and select your repository
4. Netlify auto-detects the config from `netlify.toml`
5. Set your custom domain: In Netlify dashboard → Domain settings → Add `ghincea.eu`
6. Update your domain's DNS to point to Netlify (they provide instructions)

### Option B: GitHub Pages

1. Push to GitHub
2. Add a GitHub Actions workflow (see Hugo docs: https://gohugo.io/hosting-and-deployment/hosting-on-github/)
3. Configure your custom domain in repo Settings → Pages

## Updating Content

The workflow for ongoing maintenance:

```bash
# Edit files locally in your text editor (VS Code recommended)
# Preview changes:
hugo server --disableFastRender

# When satisfied, commit and push:
git add .
git commit -m "Add new publication / Update bio / etc."
git push
```

Netlify (or GitHub Actions) will automatically rebuild and deploy.

## Customization

### Change the color theme
Edit `config/_default/params.yaml`, change the `appearance.theme_day` value.
Options: minimal, earth, rose, forest, coffee, etc.
See: https://docs.hugoblox.com/guides/theming/

### Change fonts
Edit `config/_default/params.yaml`, change `appearance.font`.
Options: native, minimal, classic, etc.

## Important Notes

- The `go.mod` file may need updating when you first run `hugo mod get -u`. Hugo will generate a `go.sum` file automatically.
- If you encounter module errors, try: `hugo mod tidy`
- HugoBlox documentation: https://docs.hugoblox.com/
- Hugo documentation: https://gohugo.io/documentation/
