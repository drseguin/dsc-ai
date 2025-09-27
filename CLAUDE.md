# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Commands

- **Start development server**: `npm run dev` (runs Next.js on port 3000)
- **Build for production**: `npm run build`
- **Start production server**: `npm start`

## Architecture Overview

This is a **Content Ops Starter** built with Next.js and designed for Netlify deployment with visual editing capabilities via Stackbit.

### Key Technologies
- **Next.js 15.5.3** with React 19 for the frontend framework
- **TypeScript** for type safety
- **Tailwind CSS** for styling
- **Stackbit** for visual editing and content management
- **Algolia** for search functionality
- **Marked & markdown-to-jsx** for markdown processing

### Project Structure

```
src/
├── components/
│   ├── blocks/          # Content blocks (VideoBlock, TitleBlock, ImageBlock, FormBlock, etc.)
│   └── sections/        # Page sections (Footer, Section)
├── css/                 # Styling
└── utils/
    └── indexer/         # Algolia search indexing utilities

content/
├── data/               # Site configuration and data
└── pages/              # Markdown content files
    └── blog/           # Blog posts

sources/local/          # Stackbit content models and presets
```

### Content Management
- Content is stored as **markdown files** in the `content/` directory
- **Stackbit** provides visual editing capabilities via `stackbit.config.ts`
- Content models are defined in `sources/local/models`
- Site uses Git-based content source with content directory at `content/`

### Key Files
- `stackbit.config.ts` - Stackbit configuration defining content sources, models, and site mapping
- `next.config.js` - Next.js configuration with Stackbit preview support
- `tailwind.config.js` - Tailwind CSS configuration
- Content routing: Blog posts at `/blog/[slug]`, other pages at `/[slug]`

### Search Integration
- **Algolia search** integration requires environment variables:
  - `NEXT_PUBLIC_ALGOLIA_APP_ID`
  - `NEXT_PUBLIC_ALGOLIA_SEARCH_API_KEY`
  - `NEXT_PUBLIC_ALGOLIA_INDEX_NAME`

### Development Workflow
1. Run `npm run dev` for Next.js development server
2. For visual editing, install `@stackbit/cli` globally and run `stackbit dev`
3. Content changes can be made either through markdown files or the visual editor