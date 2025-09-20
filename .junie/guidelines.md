# Junie AI Assistant Guidelines for 10x-task-manager

This document provides comprehensive guidelines for Junie AI Assistant when working on the 10x-task-manager project.

## Project Overview

You are working on a **10x-task-manager** - a productivity application built with modern web technologies. Your role is to assist with development, maintenance, and enhancement of this application while following established patterns and best practices.

## Tech Stack

- **Astro 5** - Static site generator and web framework
- **TypeScript 5** - Type-safe JavaScript
- **React 19** - UI framework for interactive components
- **Tailwind 4** - Utility-first CSS framework
- **Shadcn/ui** - Component library
- **Supabase** - Backend services and database

## Project Structure

Always follow this directory structure when making changes:

```
./src/                     - Source code
├── layouts/               - Astro layouts
├── pages/                 - Astro pages
│   └── api/              - API endpoints
├── middleware/
│   └── index.ts          - Astro middleware
├── db/                   - Supabase clients and types
├── types.ts              - Shared types (Entities, DTOs)
├── components/           - Client-side components
│   ├── ui/              - Shadcn/ui components
│   └── hooks/           - Custom React hooks
├── lib/
│   └── services/        - Business logic and services
└── assets/              - Static internal assets
./public/                 - Public assets
```

**Important**: When modifying the directory structure, always update this documentation.

## Development Guidelines

### Code Quality Principles

1. **Error Handling First**
   - Handle errors and edge cases at the beginning of functions
   - Use early returns for error conditions to avoid deep nesting
   - Implement guard clauses for preconditions and invalid states
   - Use custom error types for consistent error handling

2. **Clean Code Practices**
   - Use feedback from linters to improve code quality
   - Avoid unnecessary else statements; prefer if-return pattern
   - Place the happy path last in functions for better readability
   - Implement proper error logging with user-friendly messages

3. **Type Safety**
   - Leverage TypeScript's type system fully
   - Use Zod for runtime validation, especially in API routes
   - Define shared types in `src/types.ts`

## Frontend Development

### Astro Guidelines

- **Component Usage**
  - Use `.astro` components for static content and layouts
  - Only use React components when interactivity is required
  - Leverage View Transitions API with ClientRouter for smooth navigation

- **API Routes**
  - Use uppercase HTTP methods (`GET`, `POST`, etc.) for endpoint handlers
  - Add `export const prerender = false` for dynamic API routes
  - Validate inputs with Zod schemas
  - Extract business logic to services in `src/lib/services`

- **Performance**
  - Use image optimization with Astro Image integration
  - Implement hybrid rendering with SSR where needed
  - Leverage `import.meta.env` for environment variables
  - Use `Astro.cookies` for server-side cookie management

### React Guidelines

- **Component Patterns**
  - Use functional components with hooks (no class components)
  - **Never use "use client"** or other Next.js directives
  - Extract logic into custom hooks in `src/components/hooks`
  - Use `React.memo()` for expensive components with stable props

- **Performance Optimization**
  - Use `React.lazy()` and `Suspense` for code-splitting
  - Apply `useCallback` for event handlers passed to children
  - Use `useMemo` for expensive calculations
  - Consider `useOptimistic` for optimistic UI updates
  - Use `useTransition` for non-urgent state updates

- **Accessibility**
  - Use `useId()` for generating unique IDs for accessibility attributes
  - Implement proper ARIA attributes (see Accessibility section)

### Styling with Tailwind

- **Organization**
  - Use `@layer` directive for components, utilities, and base layers
  - Leverage arbitrary values with square brackets: `w-[123px]`
  - Use the `theme()` function in CSS for accessing theme values

- **Responsive Design**
  - Use responsive variants: `sm:`, `md:`, `lg:`, `xl:`
  - Implement dark mode with `dark:` variant
  - Apply state variants: `hover:`, `focus-visible:`, `active:`

### Accessibility Requirements

#### ARIA Best Practices
- Use ARIA landmarks to identify page regions (`main`, `navigation`, `search`)
- Apply appropriate ARIA roles to custom elements lacking semantic HTML
- Set `aria-expanded` and `aria-controls` for expandable content
- Use `aria-live` regions with appropriate politeness for dynamic updates
- Apply `aria-hidden` to decorative or duplicative content
- Use `aria-label` or `aria-labelledby` for elements without visible labels
- Implement `aria-describedby` for associating descriptive text
- Use `aria-current` for indicating current items in navigation
- **Avoid redundant ARIA** that duplicates native HTML semantics

## Backend Development

### Supabase Integration
- Follow Supabase security and performance guidelines
- Use proper RLS (Row Level Security) policies
- Implement efficient database queries
- Use Supabase client types for type safety

### Data Validation
- Use Zod schemas for all data validation
- Validate inputs at API boundaries
- Implement proper error responses with appropriate HTTP status codes

## Shadcn UI Components

This project uses @shadcn/ui for user interface components. These are beautifully designed, accessible components that you can customize for your application.

### Finding installed components

Components are available in the `src/components/ui` folder, according to the aliases from the `components.json` file.

### Using a component

Import the component according to the configured `@/` alias.

```tsx
import { Button } from "@/components/ui/button"
import { Tabs, TabsContent, TabsList, TabsTrigger } from "@/components/ui/tabs"
import { Card, CardContent, CardDescription, CardFooter, CardHeader, CardTitle } from "@/components/ui/card"
```

Example usage of components:

```tsx
<Button variant="outline">Click me</Button>

<Card>
  <CardHeader>
    <CardTitle>Card Title</CardTitle>
    <CardDescription>Card Description</CardDescription>
  </CardHeader>
  <CardContent>
    <p>Card Content</p>
  </CardContent>
  <CardFooter>
    <p>Card Footer</p>
  </CardFooter>
</Card>
```

### Installing additional components

Many other components are available, but they are not currently installed. A full list can be found at https://ui.shadcn.com/r

To install a new component, use the shadcn CLI.

```bash
npx shadcn@latest add [component-name]
```

For example, to add the accordion component:

```bash
npx shadcn@latest add accordion
```

Important: `npx shadcn-ui@latest` has been deprecated, use `npx shadcn@latest`.

Some popular components are:

- Accordion
- Alert
- AlertDialog
- AspectRatio
- Avatar
- Calendar
- Checkbox
- Collapsible
- Command
- ContextMenu
- DataTable
- DatePicker
- Dropdown Menu
- Form
- Hover Card
- Menubar
- Navigation Menu
- Popover
- Progress
- Radio Group
- ScrollArea
- Select
- Separator
- Sheet
- Skeleton
- Slider
- Switch
- Table
- Textarea
- Sonner (previously Toast)
- Toggle
- Tooltip

### Component Styling

This project uses the "new-york" style variant with a "neutral" base color and CSS variables for theming, as configured in the `components.json` section.

## Supabase Astro Initialization

This document provides a reproducible guide to create the necessary file structure for integrating Supabase with your Astro project.

### Prerequisites

- Your project should use Astro 5, TypeScript 5, React 19, and Tailwind 4.
- Install the `@supabase/supabase-js` package.
- Ensure that `/supabase/config.toml` exists
- Ensure that a file `/src/db/database.types.ts` exists and contains the correct type definitions for your database.

IMPORTANT: Check prerequisites before perfoming actions below. If they're not met, stop and ask a user for the fix.

### File Structure and Setup

#### 1. Supabase Client Initialization

Create the file `/src/db/supabase.client.ts` with the following content:

```ts
import { createClient } from '@supabase/supabase-js';

import type { Database } from '../db/database.types.ts';

const supabaseUrl = import.meta.env.SUPABASE_URL;
const supabaseAnonKey = import.meta.env.SUPABASE_KEY;

export const supabaseClient = createClient<Database>(supabaseUrl, supabaseAnonKey);
```

This file initializes the Supabase client using the environment variables `SUPABASE_URL` and `SUPABASE_KEY`.


#### 2. Middleware Setup

Create the file `/src/middleware/index.ts` with the following content:

```ts
import { defineMiddleware } from 'astro:middleware';

import { supabaseClient } from '../db/supabase.client.ts';

export const onRequest = defineMiddleware((context, next) => {
  context.locals.supabase = supabaseClient;
  return next();
});
```

This middleware adds the Supabase client to the Astro context locals, making it available throughout your application.


#### 3. TypeScript Environment Definitions

Create the file `src/env.d.ts` with the following content:

```ts
/// <reference types="astro/client" />

import type { SupabaseClient } from '@supabase/supabase-js';
import type { Database } from './db/database.types.ts';

declare global {
  namespace App {
    interface Locals {
      supabase: SupabaseClient<Database>;
    }
  }
}

interface ImportMetaEnv {
  readonly SUPABASE_URL: string;
  readonly SUPABASE_KEY: string;
}

interface ImportMeta {
  readonly env: ImportMetaEnv;
}
```

This file augments the global types to include the Supabase client on the Astro `App.Locals` object, ensuring proper typing throughout your application.

## Database: Create migration

You are a Postgres Expert who loves creating secure database schemas.

This project uses the migrations provided by the Supabase CLI.

### Creating a migration file

Given the context of the user's message, create a database migration file inside the folder `supabase/migrations/`.

The file MUST following this naming convention:

The file MUST be named in the format `YYYYMMDDHHmmss_short_description.sql` with proper casing for months, minutes, and seconds in UTC time:

1. `YYYY` - Four digits for the year (e.g., `2024`).
2. `MM` - Two digits for the month (01 to 12).
3. `DD` - Two digits for the day of the month (01 to 31).
4. `HH` - Two digits for the hour in 24-hour format (00 to 23).
5. `mm` - Two digits for the minute (00 to 59).
6. `ss` - Two digits for the second (00 to 59).
7. Add an appropriate description for the migration.

For example:

```
20240906123045_create_profiles.sql
```


### SQL Guidelines

Write Postgres-compatible SQL code for Supabase migration files that:

- Includes a header comment with metadata about the migration, such as the purpose, affected tables/columns, and any special considerations.
- Includes thorough comments explaining the purpose and expected behavior of each migration step.
- Write all SQL in lowercase.
- Add copious comments for any destructive SQL commands, including truncating, dropping, or column alterations.
- When creating a new table, you MUST enable Row Level Security (RLS) even if the table is intended for public access.
- When creating RLS Policies
  - Ensure the policies cover all relevant access scenarios (e.g. select, insert, update, delete) based on the table's purpose and data sensitivity.
  - If the table  is intended for public access the policy can simply return `true`.
  - RLS Policies should be granular: one policy for `select`, one for `insert` etc) and for each supabase role (`anon` and `authenticated`). DO NOT combine Policies even if the functionality is the same for both roles.
  - Include comments explaining the rationale and intended behavior of each security policy

The generated SQL code should be production-ready, well-documented, and aligned with Supabase's best practices.

## Testing Strategy

### Unit Testing
- Test business logic in services
- Test custom hooks functionality
- Validate API endpoint behavior
- Test error handling paths

### Integration Testing
- Test component interactions
- Validate form submissions
- Test authentication flows
- Verify database operations

## Performance Guidelines

### Frontend Performance
- Minimize bundle size with code splitting
- Optimize images and assets
- Use efficient CSS with Tailwind
- Implement proper caching strategies

### Backend Performance
- Optimize database queries
- Implement proper indexing
- Use efficient data fetching patterns
- Monitor API response times

## Security Considerations

### Frontend Security
- Sanitize user inputs
- Implement proper form validation
- Use secure cookies for sensitive data
- Follow OWASP guidelines

### Backend Security
- Implement proper authentication
- Use parameterized queries
- Validate all inputs server-side
- Follow Supabase security best practices

## Development Workflow

### Code Changes
1. Analyze the existing codebase structure
2. Follow established patterns and conventions
3. Implement changes with proper error handling
4. Test changes thoroughly
5. Update documentation when needed

### File Modifications
- Always check existing patterns before implementing new solutions
- Maintain consistency with the established codebase
- Update related tests when modifying functionality
- Consider backward compatibility

## Common Patterns

### Error Handling Pattern
```typescript
export async function serviceFunction(input: InputType): Promise<Result<OutputType>> {
  // Early validation
  if (!input.requiredField) {
    return { error: 'Required field missing' };
  }

  try {
    // Main logic here
    const result = await performOperation(input);
    return { data: result };
  } catch (error) {
    console.error('Operation failed:', error);
    return { error: 'Operation failed' };
  }
}
```

### Component Pattern
```typescript
interface ComponentProps {
  // Define props with TypeScript
}

export function Component({ prop1, prop2 }: ComponentProps) {
  // Early returns for edge cases
  if (!prop1) return null;

  // Main component logic
  return (
    <div className="tailwind-classes">
      {/* Component content */}
    </div>
  );
}
```

## Key Reminders

1. **Always use TypeScript** - No plain JavaScript files
2. **Follow the project structure** - Don't create new top-level directories
3. **Use established patterns** - Check existing code before implementing new solutions
4. **Handle errors properly** - Implement error boundaries and proper error handling
5. **Maintain accessibility** - Follow ARIA guidelines and semantic HTML
6. **Optimize performance** - Consider bundle size and runtime performance
7. **Test your changes** - Ensure functionality works as expected
8. **Update documentation** - Keep this file and other docs current

## Getting Help

When you need clarification:
1. Examine existing similar implementations in the codebase
2. Check the project's package.json for available dependencies
3. Review test files for expected behavior patterns
4. Ask specific questions about implementation details

Remember: Your goal is to maintain code quality, follow established patterns, and deliver reliable functionality that enhances the 10x-task-manager application.
