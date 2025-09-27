# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Commands

- **Start development server**: `npm run dev` (runs Next.js on port 3000)
- **Quick start script**: `./start.sh` (auto-installs dependencies and starts dev server)
- **Build for production**: `npm run build`
- **Start production server**: `npm start`
- **Format code**: `prettier --write .` (uses config from `.prettierrc`)
- **Visual editing**: `stackbit dev` (requires `@stackbit/cli` installed globally)

## Architecture Overview

This is a **Content Ops Starter** built with Next.js and designed for Netlify deployment with visual editing capabilities via Stackbit.

### Key Technologies
- **Next.js 15.5.3** with React 19 for the frontend framework
- **TypeScript** for type safety
- **Tailwind CSS** for styling with custom theme integration
- **Stackbit** for visual editing and content management
- **Algolia** for search functionality
- **Marked & markdown-to-jsx** for markdown processing

### Core Architecture Patterns

#### Dynamic Component Registry
The system uses dynamic imports for components via `src/components/components-registry.ts`:
- Components are mapped by their model names (e.g., `getComponent('PostLayout')`)
- Enables conditional loading and code splitting
- Model names match content types for automatic component selection

#### Content-Driven Routing
- **Catch-all route**: `src/pages/[[...slug]].js` handles all page routing
- **Static generation**: Uses `getStaticPaths()` and `getStaticProps()` for SSG
- **URL mapping**: Defined in `stackbit.config.ts` siteMap function:
  - Blog posts: `/blog/[slug]`
  - Blog feed: `/blog`
  - Other pages: `/[slug]`

#### Content Processing Pipeline
1. **Content loading**: `src/utils/local-content.ts` processes markdown and JSON files
2. **Model validation**: Validates content against Stackbit models in `sources/local/models/`
3. **Reference resolution**: Handles cross-references between content files
4. **Static props**: Resolves page data at build time

#### Styling System
- **Theme-driven**: `tailwind.config.js` imports theme from `content/data/style.json`
- **Component styles**: Predefined classes for buttons, links, headings
- **Style mapping**: `src/utils/map-styles-to-class-names.ts` converts style objects to Tailwind classes
- **Dynamic styling**: Supports margin, padding, borders, and typography customization

### Project Structure

```
src/
├── components/
│   ├── blocks/          # Reusable content blocks (40+ components)
│   ├── sections/        # Page layout sections (Header, Footer, etc.)
│   └── components-registry.ts  # Dynamic component mapping
├── pages/
│   ├── [[...slug]].js   # Catch-all route handler
│   ├── _app.js          # App wrapper
│   └── api/reindex.js   # Algolia reindexing endpoint
├── utils/
│   ├── indexer/         # Algolia search indexing utilities
│   ├── local-content.ts # Content loading and processing
│   └── map-styles-to-class-names.ts  # Style utilities
└── css/                 # Global styles

content/
├── data/               # Site configuration (header, footer, style)
└── pages/              # Markdown content files
    └── blog/           # Blog posts

sources/local/
├── models/             # Stackbit content models (TypeScript definitions)
└── presets/            # Pre-configured content templates
```

### Content Management
- **Git-based CMS**: Content stored as markdown/JSON files in `content/`
- **Stackbit integration**: Visual editing via `stackbit.config.ts`
- **Model-driven**: 40+ content models define structure and validation
- **Asset management**: Images stored in `public/images/`, referenced statically

### Key Configuration Files
- `stackbit.config.ts` - Stackbit CMS configuration, content sources, and URL routing
- `next.config.js` - Next.js config with Stackbit preview mode support
- `tailwind.config.js` - Tailwind with dynamic theme and component styles
- `content/data/style.json` - Theme configuration (colors, typography, component styles)
- `content/data/header.json` & `footer.json` - Site navigation and branding

### Search Integration
**Algolia search** with automatic indexing:
- **Environment variables**:
  - `NEXT_PUBLIC_ALGOLIA_APP_ID`
  - `NEXT_PUBLIC_ALGOLIA_SEARCH_API_KEY` (search-only key)
  - `NEXT_PUBLIC_ALGOLIA_INDEX_NAME`
- **Indexing**: `/api/reindex` endpoint processes blog posts into searchable format
- **Content extraction**: Converts markdown to plain text for indexing

### Development Workflow
1. **Start development**: Run `./start.sh` or `npm run dev`
2. **Visual editing**: Install `@stackbit/cli` globally, then `stackbit dev`
3. **Content editing**:
   - Visual: http://localhost:8090/_stackbit
   - Direct: Edit markdown files in `content/pages/`
4. **Styling**: Modify `content/data/style.json` or Tailwind classes
5. **Components**: Add new models in `sources/local/models/` and register in `components-registry.ts`

### Important Notes
- **No linting/testing**: Project uses only Prettier for code formatting
- **Stackbit preview**: Special handling for visual editor mode via `STACKBIT_PREVIEW` env var
- **Static generation**: All pages are pre-rendered at build time
- **Image handling**: Images must be in `public/images/` for proper Stackbit asset management