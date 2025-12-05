# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Mintlify documentation site for incident.io. Mintlify is a static site generator for documentation that uses MDX files and a `docs.json` configuration file.

## Development Commands

**Start local development server:**
```bash
mint dev
```
The site will be available at `http://localhost:3000` with hot-reloading.

**Start on custom port:**
```bash
mint dev --port 3333
```

**Update Mintlify CLI:**
```bash
npm mint update
```

**Validate links:**
```bash
mint broken-links
```

**Install Mintlify CLI globally (if not installed):**
```bash
npm i -g mint
```

## Architecture

### Configuration System

- **docs.json**: Central configuration file that controls:
  - Site theme, colors, logo, and branding
  - Navigation structure (tabs, groups, and pages)
  - Global anchors and navbar links
  - Contextual features (copy, view, chatgpt, claude, perplexity, etc.)
  - Footer social links

### Navigation

The navigation is hierarchical: Tabs → Groups → Pages. Pages must be explicitly registered in `docs.json` to appear in the sidebar. Hidden pages (not in `docs.json`) are still accessible via search and direct links.

Current navigation structure:
- **Guides tab**: Getting started, Customization, Writing content, AI tools
- **API reference tab**: API documentation, Endpoint examples

### Content Organization

- All documentation pages are `.mdx` files (MDX = Markdown + JSX)
- Pages can be organized in folders; folder structure maps to URL paths
- Example: `/your-folder/your-page.mdx` → `https://site.com/your-folder/your-page`
- Cannot use top-level `api` folder (reserved by Next.js); use `api-reference` instead

### Content Locations

- `/ai-tools/`: Guides for AI tools (Cursor, Claude Code, Windsurf)
- `/api-reference/`: API documentation and endpoint examples
- `/essentials/`: Core documentation about writing and customizing
- `/snippets/`: Reusable content snippets
- `/images/` and `/logo/`: Static assets
- Root-level `.mdx` files: Main landing pages (index, quickstart, development)

### Duplicate Structure

There appears to be a `/docs/` subdirectory with duplicated content and a `/docs/testing/` directory with testing content. The main documentation root is at the repository root, not in `/docs/`.

## Key Workflows

### Adding a New Page

1. Create the `.mdx` file in the appropriate folder
2. Add the page path (without `.mdx` extension) to `docs.json` navigation
3. Pages not in `docs.json` won't appear in sidebar but are searchable

### Updating Site Branding

Edit these fields in `docs.json`:
- `name`: Site name
- `colors.primary`: Primary brand color
- `colors.light` and `colors.dark`: Light and dark theme colors
- `logo.light` and `logo.dark`: Logo paths
- `favicon`: Favicon path

### Deployment

Changes pushed to the main branch are automatically deployed via the Mintlify GitHub app (configured in dashboard).

## Troubleshooting

- **Dev server not running**: Run `mint update` to get latest CLI version
- **404 errors**: Ensure `mint dev` is run from a directory containing `docs.json`
- **"sharp" module error on darwin-arm64**: Upgrade to Node.js v19+ and reinstall CLI
- **Unknown errors**: Delete `~/.mintlify` folder and restart
