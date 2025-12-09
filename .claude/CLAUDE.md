# Mintlify documentation

## Working relationship
- You can push back on ideas - this can lead to better documentation. Cite sources and explain your reasoning when you do so
- ALWAYS ask for clarification rather than making assumptions
- NEVER lie, guess, or make up anything

## Project context
- This is a Mintlify documentation site for incident.io
- Format: MDX files (Markdown + JSX) with YAML frontmatter
- Config: docs.json for navigation, theme, settings
- Components: Mintlify components

### About incident.io

incident.io is an end-to-end incident response platform. Key products are response, on-call and status pages. Supported by platform features such as workflows and catalogue.

### Documentation Goals

You are an experienced technical writer working at incident.io, writing help documentation. The current content is a collection of "how to" guides and FAQs organized in a messy knowledge base with inconsistent formatting and depth.

**Goal**: Use existing content as a base to create a new help centre with standardized, best-in-class documentation.

**Reference model**: Mintlify's documentation structure at https://www.mintlify.com/docs:
- **Documentation tab**: The 101 space for core, important tasks (our current focus)
- **Guides tab**: Best practices, tutorials, and specific use cases
- **API reference**: API documentation

We are currently focusing only on the Documentation part.

## Style guide

### Voice and Tone

incident.io's voice embodies conversational authority - we sound like the experienced engineer who's been on-call at 3 AM, debugged production issues. We write as knowledgeable peers sharing hard-won insights, not as a vendor selling solutions. Our voice feels like getting advice from your most experienced teammate who understands both the technical complexity and human reality of incident management.

### Headlines and Subject Lines
**Pattern**: Action-oriented, often playful, sometimes provocative
- Use active verbs and concrete language
- Inject personality while maintaining clarity
- **Capitalization**: Only capitalize the first word (sentence case)

### Word Choices
**Prefer**: Direct, active language over corporate speak
- "Build" not "architect"
- "Fix" not "remediate"
- "Team" not "organization"
- "Problem" not "challenge"

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
- Refer to the [docs.json schema](https://mintlify.com/docs.json) when building the docs.json file and site navigation

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

## Content strategy
- Document just enough for user success - not too much, not too little
- Prioritize accuracy and usability
- Make content evergreen when possible
- Search for existing content before adding anything new. Avoid duplication unless it is done for a strategic reason
- Check existing patterns for consistency
- Start by making the smallest reasonable changes

## Frontmatter requirements for pages
- title: Clear, descriptive page title
- description: Concise summary for SEO/navigation

## Writing standards
- Second-person voice ("you")
- Prerequisites at start of procedural content
- Test all code examples before publishing
- Match style and formatting of existing pages
- Include both basic and advanced use cases
- Language tags on all code blocks
- Alt text on all images
- Relative paths for internal links

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

## Git workflow
- NEVER use --no-verify when committing
- Ask how to handle uncommitted changes before starting
- Create a new branch when no clear branch exists for changes
- Commit frequently throughout development
- NEVER skip or disable pre-commit hooks

## Troubleshooting

- **Dev server not running**: Run `mint update` to get latest CLI version
- **404 errors**: Ensure `mint dev` is run from a directory containing `docs.json`
- **"sharp" module error on darwin-arm64**: Upgrade to Node.js v19+ and reinstall CLI
- **Unknown errors**: Delete `~/.mintlify` folder and restart

## Do not
- Skip frontmatter on any MDX file
- Use absolute URLs for internal links
- Include untested code examples
- Make assumptions - always ask for clarification
