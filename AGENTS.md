# Agent Instructions

This repository is configured with specific guidelines for AI agents operating on the project.

## Agent skills

### Issue tracker

Issues are tracked using GitHub Issues. External PRs are not treated as a request surface. See `docs/agents/issue-tracker.md`.

### Triage labels

Triage uses the default labels (`needs-triage`, `needs-info`, `ready-for-agent`, `ready-for-human`, `wontfix`). See `docs/agents/triage-labels.md`.

### Domain docs

Configured as a multi-context repo using `CONTEXT-MAP.md` at the root. See `docs/agents/domain.md`.

## Current Tech Stack & Dependencies

The following core dependencies and versions are installed in this project. Agents should refer to this list when deciding which library versions or patterns to use.

### Core Framework
- **Next.js**: 16.2.9
- **React / React DOM**: 19.2.4

### Backend & Services
- **Supabase SSR**: ^0.12.0 (`@supabase/ssr`)
- **Supabase JS Client**: ^2.108.2 (`@supabase/supabase-js`)
- **Resend (Email)**: ^6.14.0

### UI & Styling
- **Tailwind CSS**: ^4 (using `@tailwindcss/postcss`)
- **shadcn/ui**: ^4.11.0
- **Radix UI**: ^1.6.0
- **Lucide Icons**: ^1.21.0
- **Tailwind Merge**: ^3.6.0
- **tw-animate-css**: ^1.4.0

### Forms & Validation
- **React Hook Form**: ^7.80.0
- **Zod**: ^4.4.3
- **Hookform Resolvers**: ^5.4.0

### Data Display & Utilities
- **TanStack Table**: ^8.21.3
- **date-fns**: ^4.4.0

### Development
- **TypeScript**: ^5
- **ESLint**: ^9
