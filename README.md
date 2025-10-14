# Intro to Git (Quarto Reveal.js Slides)

This repository contains a Quarto Reveal.js slide deck: `intro-to-git.qmd`. A GitHub Actions workflow automatically renders and publishes the presentation to the `gh-pages` branch (for GitHub Pages hosting) whenever changes are pushed to the `main` branch (or the workflow is run manually).

---

## TOC

- [Intro to Git (Quarto Reveal.js Slides)](#intro-to-git-quarto-revealjs-slides)
  - [TOC](#toc)
  - [✏️ Editing the Slides](#️-editing-the-slides)
    - [Useful Slide Enhancements](#useful-slide-enhancements)
  - [🛠 Project Configuration (`_quarto.yml`)](#-project-configuration-_quartoyml)
  - [▶️ Local Preview \& Rendering](#️-local-preview--rendering)
  - [🚀 Publishing Flow (GitHub Actions)](#-publishing-flow-github-actions)
    - [Enabling GitHub Pages (one-time setup)](#enabling-github-pages-one-time-setup)
    - [Updating the Slides](#updating-the-slides)
  - [🧪 Testing Changes Before Publishing](#-testing-changes-before-publishing)
  - [🤝 Contributing / Workflow Tips](#-contributing--workflow-tips)
  - [📚 Further Reading](#-further-reading)
  - [✅ Quick Reference](#-quick-reference)

---

## ✏️ Editing the Slides

Edit the source file: `intro-to-git.qmd`.

Basic structure:

- `# Heading` (level 1) starts a new slide
- `## Subheading` (level 2) can create nested (vertical) slides
- Use standard Markdown: lists, bold/italic, images, fenced code blocks
- Incremental list example:

```markdown
::: incremental
- Point 1
- Point 2
:::
```

Reveal.js feature reference: <https://quarto.org/docs/presentations/revealjs/>

### Useful Slide Enhancements

| Feature | How (example) |
|---------|---------------|
| Speaker notes | Add `::: notes` block inside a slide |
| Incremental lists | Wrap list in `::: incremental ... :::` |
| Slide background | `# Title {background-image="img/bg.png" background-size=cover}` |
| Fragments | Use incremental list or inline `{.fragment}` class |
| Columns | `:::{.columns}` then two `::: {.column}` blocks |

---
## 🛠 Project Configuration (`_quarto.yml`)

The `_quarto.yml` file defines global settings:

```yaml
project:
  type: default
  output-dir: docs

format:
  revealjs:
    theme: dark
    slide-number: true
    hash: true
    controls: true
    progress: true
    overview: true
    transition: slide
    code-copy: true
```

Key points:

- `format.revealjs` block controls the presentation look & behavior.
- Change `theme:` (e.g. `theme: [dark, solarized]` or a custom SCSS file).
- `hash: true` enables deep‑linking to individual slides.
- `output-dir: docs` is used for local renders; the publish Action ignores this and pushes rendered HTML directly to `gh-pages`.

More options: <https://quarto.org/docs/presentations/revealjs/>

---
## ▶️ Local Preview & Rendering

1. Install Quarto (if not already): <https://quarto.org/docs/get-started/>
2. From the repo root, live preview while editing:

```bash
quarto preview intro-to-git.qmd
```

This starts a local server with auto-reload.

1. Produce a one-time render:

```bash
quarto render intro-to-git.qmd
```

The HTML output goes into `docs/` (per `_quarto.yml`). Open the generated `.html` in a browser.

Tip: Commit only the source (`.qmd`) and config; the GitHub Action will produce the published output.

---
## 🚀 Publishing Flow (GitHub Actions)

Workflow file: `.github/workflows/publish.yml`:

```yaml
on:
  workflow_dispatch:
  push:
    branches: [main]

name: Quarto Publish

jobs:
  build-deploy:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - uses: actions/checkout@v4
      - uses: quarto-dev/quarto-actions/setup@v2
      - uses: quarto-dev/quarto-actions/publish@v2
        with:
          target: gh-pages
          path: intro-to-git.qmd
          render: true
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

How it works:

1. Trigger: push to `main`.
1. Action checks out the repo and installs Quarto.
1. It renders `intro-to-git.qmd` (because `render: true`).
1. It publishes the rendered presentation to the special orphan branch `gh-pages`.
1. GitHub Pages serves the site from that branch.

### Enabling GitHub Pages (one-time setup)

1. In the repository on GitHub: Settings → Pages.
2. Set Source = `Deploy from a branch`.
3. Select branch: `gh-pages` / root.
4. Save. After the workflow runs, the site will be available at:  
  `https://<org-or-user>.github.io/<repo>/`

A `.nojekyll` file (already present) ensures GitHub Pages does not process the site with Jekyll.

### Updating the Slides

1. Edit `intro-to-git.qmd`.
2. (Optional) Preview locally with `quarto preview`.
3. Commit and push:

```bash
git add intro-to-git.qmd
git commit -m "Update slides: add branching section"
git push
```

Wait for the GitHub Action (check Actions tab). When it finishes, refresh the published URL.

## 🧪 Testing Changes Before Publishing

You can render locally exactly like the workflow does:

```bash
quarto render intro-to-git.qmd --to revealjs
```

If you need to replicate a clean environment, use a container or a GitHub Codespace.

## 🤝 Contributing / Workflow Tips

- Keep commits focused; use descriptive messages.
- Use Pull Requests for review before publishing.
- Avoid committing rendered HTML (Action produces deployable output).

## 📚 Further Reading

- Quarto Reveal.js docs: <https://quarto.org/docs/presentations/revealjs/>
- Quarto project basics: <https://quarto.org/docs/projects/>
- GitHub Actions for Quarto: <https://github.com/quarto-dev/quarto-actions>

---

## ✅ Quick Reference

| Task | Command |
|------|---------|
| Live preview | `quarto preview intro-to-git.qmd` |
| Render once | `quarto render intro-to-git.qmd` |
| Publish (CI) | Push to `main` branch |
| Manual publish | Trigger workflow dispatch in Actions tab |
