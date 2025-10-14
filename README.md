# Intro to Git Slides

This repository contains presentation slides for an introductory Git/GitHub workshop, built using [mkslides](https://martenbe.github.io/mkslides) and [Reveal.js](https://revealjs.com/).

## Overview

The slides are written in Markdown and converted to an interactive HTML presentation that is hosted via GitHub Pages.

- **Source file**: `intro-to-git.md` - The Markdown source file containing the slide content
- **Output directory**: `docs/` - Contains the generated HTML and assets for GitHub Pages
- **Live presentation**: The slides are served via GitHub Pages from the `docs/` folder

## Prerequisites

To edit and regenerate the slides, you'll need:

- Python 3.7 or higher
- pip (Python package manager)

## Installation

Install mkslides using pip:

```bash
pip install mkslides
```

This will install mkslides and all its dependencies, including support for Reveal.js presentations.

## Editing the Slides

The slide content is in `intro-to-git.md`. This file uses:

1. **YAML frontmatter** - Configuration for the Reveal.js presentation (at the top of the file)
2. **Markdown content** - The actual slide content
3. **Slide separators** - Three dashes (`---`) separate individual slides

### Example Structure

```markdown
---
revealjs:
  width: 1280
  height: 700
  margin: 0.04
  minScale: 0.2
  maxScale: 2.0
---

# First Slide Title

Content for the first slide

---

## Second Slide Title

Content for the second slide
```

### Reveal.js Configuration Options

You can customize the presentation behavior in the frontmatter:

- `width` / `height`: Presentation dimensions
- `margin`: Space around slide content
- `minScale` / `maxScale`: Zoom limits
- `slideNumber`: Show slide numbers (e.g., "c/t" for current/total)
- `history`: Enable browser history for slides

See the [Reveal.js documentation](https://revealjs.com/config/) for all available options.

## Generating the Slides

After editing `intro-to-git.md`, regenerate the presentation:

```bash
mkslides build intro-to-git.md -o docs/
```

This command:
1. Reads the Markdown source file (`intro-to-git.md`)
2. Converts it to a Reveal.js HTML presentation
3. Outputs the result to the `docs/` directory
4. Includes all necessary Reveal.js assets and themes

### Build Options

mkslides supports several options:

- `-o, --output`: Specify output directory (default: `docs/`)
- `--theme`: Choose a Reveal.js theme (black, white, league, etc.)
- `--highlight-theme`: Choose a code highlighting theme

Example with custom theme:

```bash
mkslides build intro-to-git.md -o docs/ --theme white
```

## Preview the Slides Locally

To preview your slides before publishing:

```bash
mkslides serve intro-to-git.md
```

This starts a local web server and opens your slides in a browser. Changes to the Markdown file will be reflected when you refresh the page.

Alternatively, you can serve the `docs/` directory with any static file server:

```bash
# Using Python's built-in server
cd docs
python -m http.server 8000
```

Then navigate to `http://localhost:8000` in your browser.

## Publishing to GitHub Pages

The slides are automatically published via GitHub Pages from the `docs/` folder on the `main` branch.

### Setup (One-time)

If not already configured:

1. Go to your repository's Settings
2. Navigate to Pages (in the left sidebar)
3. Under "Source", select:
   - Branch: `main`
   - Folder: `/docs`
4. Click Save

GitHub will build and deploy your slides automatically when you push changes to the `docs/` directory.

### Publishing Workflow

1. Edit `intro-to-git.md`
2. Generate the slides: `mkslides build intro-to-git.md -o docs/`
3. Commit and push your changes:
   ```bash
   git add intro-to-git.md docs/
   git commit -m "Update slides"
   git push
   ```
4. GitHub Pages will automatically deploy the updated slides (usually within a minute)

## Repository Structure

```
.
├── README.md              # This file
├── intro-to-git.md        # Slide content (Markdown source)
└── docs/                  # Generated presentation (GitHub Pages)
    ├── index.html         # Main presentation file
    └── assets/            # Reveal.js assets (CSS, JS, themes)
```

## Tips

- **Slide separators**: Use `---` on its own line to create a new horizontal slide
- **Vertical slides**: Use `----` (four dashes) for vertical slides within a section
- **Speaker notes**: Add notes after `Notes:` on a slide (press 's' during presentation to view)
- **Code blocks**: Use standard Markdown code fences with language specification
- **Fragment animations**: Individual bullets can be animated (see mkslides documentation)

## Resources

- [mkslides Documentation](https://martenbe.github.io/mkslides)
- [Reveal.js Documentation](https://revealjs.com/)
- [Markdown Guide](https://www.markdownguide.org/)

## License

The content of this presentation is licensed under the terms specified in the repository. Reveal.js is MIT licensed.
