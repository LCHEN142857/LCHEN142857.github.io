# LCHEN Knowledge Base

This repository contains a lightweight technical knowledge base built with [Docsify](https://docsify.js.org/). Articles are written in Markdown and rendered directly in the browser, so there is no static-site build step.

## Repository Structure

```text
.
├── docs/
│   ├── index.html          # Docsify configuration and site entry point
│   ├── README.md           # Docsify homepage
│   ├── _sidebar.md         # Site navigation
│   ├── _coverpage.md       # Site cover page
│   ├── _media/             # Images and other site assets
│   └── <Topic>/            # Topic-specific Markdown articles
└── README.md               # This developer guide
```

## How the Site Works

Docsify loads `docs/index.html` and fetches Markdown files at runtime. The important configuration is:

- `loadSidebar: true` uses `docs/_sidebar.md` for navigation.
- `coverpage: true` uses `docs/_coverpage.md`.
- `search: auto` enables client-side search.
- `maxLevel: 4` and `subMaxLevel: 2` control heading extraction.

Because rendering happens in the browser, adding an article usually means adding one Markdown file and registering it in the sidebar.

## Run Locally

From the repository root, serve the `docs` directory:

```bash
npx docsify-cli serve docs
```

Then open the URL shown in the terminal, normally:

```text
http://localhost:3000
```

Any static file server works too. For example:

```bash
python -m http.server 3000 --directory docs
```

## Add a New Article

1. Create a Markdown file in the appropriate topic folder:

   ```text
   docs/<Topic>/<article-slug>.md
   ```

   Use lowercase hyphenated file names, for example:

   ```text
   docs/Docker/docker-compose-basics.md
   ```

2. Start the article with a clear `#` title:

   ```markdown
   # Docker Compose Basics
   ```

3. Add concise sections using `##` headings:

   ```markdown
   # Docker Compose Basics

   Docker Compose defines and runs multi-container applications.

   ## Installation

   ## Common Commands

   ## Example
   ```

4. Add the article to `docs/_sidebar.md` without the `.md` extension:

   ```markdown
   - Docker
       * [Docker Compose Basics](Docker/docker-compose-basics)
   ```

5. Run the site locally and confirm that:

   - the article opens from the sidebar;
   - headings appear in the expected order;
   - code blocks and tables render correctly;
   - links and images work.

## Writing Conventions

- Keep the `#` title as the first heading in the article.
- Prefer short sections and examples over long paragraphs.
- Use fenced code blocks with a language identifier:

  ````markdown
  ```bash
  git status
  ```
  ````

- Use tables for commands, options, formats, or comparisons.
- Add a link only when it is necessary; make the link text describe the destination.
- Store site images in `docs/_media/` and reference them relative to the Markdown file when possible:

  ```markdown
  ![Architecture diagram](../_media/airplane.svg)
  ```

## Publish

The site is published through GitHub Pages. Push changes to the default branch and GitHub Pages will serve the latest version of the repository.

Before pushing:

1. Preview the article locally.
2. Check that `docs/_sidebar.md` links to the new file.
3. Verify all modified Markdown files render as intended.
