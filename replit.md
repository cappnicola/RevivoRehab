# Replit.md

## Overview

This is a full-stack web application for "Revivo Riabilitazione," a physiotherapy and rehabilitation clinic in Riva del Garda, Italy. The application is built with modern web technologies and follows a client-server architecture with a focus on providing information about rehabilitation services, blog content, and contact functionality.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

The application follows a monorepo structure with three main layers:

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **UI Components**: shadcn/ui component library built on Radix UI primitives
- **Styling**: Tailwind CSS with custom CSS variables for theming
- **State Management**: TanStack Query (React Query) for server state management
- **Routing**: Wouter for client-side routing
- **Build Tool**: Vite for development and build processes

### Backend Architecture
- **Runtime**: Node.js with TypeScript
- **Framework**: Express.js for REST API
- **Database**: PostgreSQL with Drizzle ORM
- **Database Provider**: Neon Database (serverless PostgreSQL)
- **Session Storage**: In-memory storage with fallback to PostgreSQL session store

### Data Storage Solutions
- **Primary Database**: PostgreSQL hosted on Neon
- **ORM**: Drizzle ORM for type-safe database operations
- **Schema Management**: Drizzle Kit for migrations and schema management
- **Session Storage**: connect-pg-simple for PostgreSQL session storage

## Key Components

### Database Schema
The application uses three main database tables:
1. **blog_posts**: Stores blog articles with categories, content, and metadata
2. **contacts**: Stores contact form submissions from potential clients
3. **testimonials**: Stores client testimonials and ratings

### API Endpoints
- `GET /api/blog-posts`: Retrieve all blog posts or filter by category
- `GET /api/blog-posts/:id`: Retrieve a specific blog post
- `POST /api/contacts`: Submit contact form data
- `GET /api/testimonials`: Retrieve client testimonials (implied from storage interface)

### Frontend Pages and Components
- **Home Page**: Single-page application with multiple sections
- **Navigation**: Fixed navigation bar with smooth scrolling
- **Hero Section**: Landing area with call-to-action buttons
- **Services Section**: Overview of rehabilitation services
- **About Section**: Information about the clinic's approach
- **Blog Section**: Filterable blog posts display
- **Results Section**: Statistics and testimonials
- **Contact Section**: Contact form with validation
- **Footer**: Contact information and links

## Data Flow

1. **Client Requests**: Browser makes requests to Express.js server
2. **API Layer**: Express routes handle HTTP requests and validate data
3. **Data Layer**: Drizzle ORM queries PostgreSQL database
4. **Response**: JSON responses sent back to client
5. **State Management**: TanStack Query caches and manages server state
6. **UI Updates**: React components re-render based on state changes

### Contact Form Flow
1. User fills out contact form
2. Form validation using react-hook-form and Zod schemas
3. Data submitted via POST to `/api/contacts`
4. Server validates and stores in PostgreSQL
5. Success/error feedback displayed to user

### Blog Content Flow
1. Blog posts stored in database with categories
2. Frontend requests posts via GET endpoints
3. Category filtering supported on both client and server
4. Posts displayed with pagination and filtering UI

## External Dependencies

### Key Libraries
- **@tanstack/react-query**: Server state management and caching
- **drizzle-orm**: Type-safe database ORM
- **@neondatabase/serverless**: Serverless PostgreSQL client
- **react-hook-form**: Form handling and validation
- **zod**: Schema validation
- **@radix-ui/***: Accessible UI component primitives
- **tailwindcss**: Utility-first CSS framework
- **wouter**: Lightweight React router

### Development Tools
- **Vite**: Fast build tool and dev server
- **TypeScript**: Static type checking
- **ESBuild**: Fast JavaScript bundler for production
- **Drizzle Kit**: Database migration and introspection tool

## Deployment Strategy

The application is designed for deployment on Replit with the following characteristics:

### Build Process
- **Development**: `npm run dev` - Runs TypeScript directly with tsx
- **Production Build**: `npm run build` - Vite builds client, ESBuild bundles server
- **Deployment Fix**: `node scripts/fix-deployment.js` - Resolves path mismatches for deployment
- **Production Start**: `npm start` - Runs built Node.js application

### Deployment Path Resolution
Due to a mismatch between Vite's build output (`dist/public`) and server expectations (`server/public`), a deployment fix script ensures proper file placement:
- Creates symbolic link: `server/public` → `../dist/public` (for server access)
- Copies files: `dist/public/*` → `dist/*` (for deployment compatibility)
- Ensures index.html and assets are accessible in both locations

### Environment Configuration
- Uses `NODE_ENV` for environment detection
- Requires `DATABASE_URL` for PostgreSQL connection
- Supports Replit-specific development tools and plugins

### Database Management
- Database migrations handled via `npm run db:push`
- Schema defined in `shared/schema.ts` for type safety
- Supports both development and production database configurations

### Static Asset Serving
- Vite handles client-side asset bundling and optimization
- Express serves static files in production
- Assets optimized for web performance

The application is structured as a typical full-stack TypeScript application with clear separation between client, server, and shared code, making it maintainable and scalable for a small business website with content management needs.