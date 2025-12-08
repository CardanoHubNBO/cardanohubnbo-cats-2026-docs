# WARP.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.

## Core Architecture

This is a documentation website for Prisma (an action-learning incubator) built with:
- **Next.js 15** with TypeScript and Turbopack for development
- **Nextra** theme for documentation sites with built-in search and navigation
- **MDX** for content with custom React components
- **Tailwind CSS** for styling with custom theming
- **pnpm** for package management

### Directory Structure

- `content/` - Main documentation content in MDX format, organized by topics (collaborators, patterns, processes, etc.)
- `app/` - Next.js App Router with API routes and layout
- `components/` - Custom React components used in MDX content
- `contexts/` - React Context providers for app state
- `public/` - Static assets including images and icons
- `scripts/` - Build and utility scripts

## Development Commands

```bash
# Install dependencies
pnpm install

# Start development server with Turbopack
pnpm dev

# Build for production
pnpm build

# Start production server
pnpm start

# Generate search index (runs after build)
pnpm postbuild

# Run recording script
pnpm record
```

## Content Management

### MDX Files Structure
- Content lives in `content/` directory with nested organization
- Each MDX file can have frontmatter with `sidebarTitle`, `aliases`, and other metadata
- Wiki-style links use `[text](/path/to/page)` format
- Custom components are available in all MDX files via `mdx-components.js`

### Available Custom Components
The following components can be used in any MDX file:
- `<StandardButton>` - Styled button component  
- `<TeamCards>` - Team member display
- `<ContributorChart>` - GitHub contributor analytics
- `<CohortCards>` - Course/cohort display
- `<EventCard>` - Event information display
- `<GraphVisualisation>` and `<GraphRenderer>` - Network visualization
- `<SystemDiagramPI>` - System architecture diagrams
- `<PageGate>` - Access control component
- `<FeatureText>` - Highlighted text with navigation

### Content Editing Workflow
- Uses Obsidian integration for content editing (see `OBSIDIAN_SETUP.md`)
- Content editors can use Obsidian with Git plugin for visual editing
- All content changes should go through git workflow
- Content structure supports cross-references and wiki-style linking

## API Architecture

### Available Endpoints
- `/api/participants/[handle]` - Fetches participant data from external timelining API
- `/api/contributors` - GitHub contributor statistics with retry logic
- `/api/graph` - Graph data for visualizations
- `/api/cohort` - Cohort information
- `/api/chats/[chatId]` and `/api/chats/list` - Chat functionality
- `/api/serve/[...path]` - File serving endpoint

### External Integrations
- **GitHub API** for contributor data (requires `PRISMA_DOCS_GITHUB_TOKEN`, `PRISMA_DOCS_GITHUB_OWNER`, `PRISMA_DOCS_GITHUB_REPO`)
- **External timelining API** at `timelining-prisma-collective.vercel.app`
- **Vercel Analytics** for usage tracking
- **Lu.ma** calendar integration for events

## Styling and Theming

- Uses Nextra dark theme by default
- Custom Tailwind configuration with Prisma brand colors (`prisma-a`, `prisma-b`, `prisma-c`, `prisma-d`)
- Custom CSS in `styles.css` for additional styling
- Components use consistent hover effects with random color selection

## Search and Navigation

- **Pagefind** powers the site search, built during postbuild step
- Nextra provides automatic sidebar generation from file structure
- Wiki-link support through `remark-wiki-link` plugin
- Navigation configured in `next.config.mjs` with custom redirects

## Development Notes

- Uses ES modules (`"type": "module"` in package.json)
- TypeScript configuration includes path aliases (`@/*` maps to root)
- Development server uses Turbopack for fast builds
- Search indexing happens in `.next/server/app` output to `public/_pagefind`
- Context provider `ActiveJourneyProvider` manages active journey state

## Deployment

- Configured for Vercel deployment via `vercel.json`
- Uses pnpm as build tool
- Repository links point to `prisma-collective/docs` on GitHub
- Site URL: `docs.prisma.events`