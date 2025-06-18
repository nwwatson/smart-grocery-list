# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

# Smart Grocery List Application

A Progressive Web Application built with Next.js that learns user buying patterns and intelligently suggests grocery items based on purchase history and frequency. The application integrates recipe management, meal planning, nutritional tracking, and family collaboration features with real-time synchronization.

## Project Overview

### Core Features
- **Intelligent Grocery Lists**: AI-powered suggestions based on buying patterns
- **Recipe Management**: Scan or input recipes with automatic ingredient extraction and image support
- **Image Integration**: Hero images and step-by-step instruction photos with optimization
- **Nutritional Tracking**: Comprehensive nutrition data with USDA API integration
- **Family Collaboration**: Shared lists and recipes with role-based permissions and real-time collaboration
- **Real-time Shopping**: Live updates when family members add/purchase items simultaneously
- **Meal Planning**: Weekly meal plans with automatic grocery list generation
- **Progressive Web App**: Offline-first functionality with Next.js PWA capabilities and SSR/SSG optimization

### Technology Stack

#### Frontend
- **Framework**: Next.js 14+ with App Router and TypeScript
- **Rendering**: Server-Side Rendering (SSR), Static Site Generation (SSG), and Client Components
- **State Management**: Zustand for client state, React Query/TanStack Query for server state
- **Styling**: Tailwind CSS with Headless UI components
- **PWA**: next-pwa package for service worker and manifest management
- **Image Optimization**: Next.js Image component with automatic optimization
- **Testing**: Jest for unit tests, Playwright for E2E testing

#### Backend
- **Runtime**: Node.js 18+ with Express.js
- **Database**: MongoDB Atlas with Mongoose ODM
- **Authentication**: Custom JWT-based system with multiple providers
- **Caching**: Redis for session management and API caching
- **Real-time Communication**: Socket.IO for WebSocket connections
- **Message Queue**: Redis Pub/Sub for real-time event distribution
- **File Storage**: AWS S3 or Cloudinary for images with automatic optimization
- **Image Processing**: Next.js Image component with Sharp.js optimization
- **CDN**: Vercel Edge Network or Cloudinary CDN for global delivery
- **Email Service**: SendGrid for transactional emails

#### External APIs
- **Nutrition Data**: USDA FoodData Central API (free, public domain)
- **OCR**: Google Cloud Vision API for recipe scanning
- **NLP**: OpenAI GPT API for ingredient extraction from text
- **Social Auth**: Google OAuth 2.0 and Apple Sign In

## Project Structure

```
smart-grocery-list/
├── frontend/                    # Next.js Application
│   ├── app/                     # App Router directory
│   │   ├── (marketing)/         # Route group for public pages
│   │   │   ├── page.tsx         # Landing page (SSG)
│   │   │   ├── about/           # About page (SSG)
│   │   │   ├── recipes/         # Public recipe discovery (SSG/ISR)
│   │   │   │   ├── page.tsx     # Recipe listing
│   │   │   │   └── [id]/        # Individual recipe pages
│   │   │   └── layout.tsx       # Marketing layout
│   │   ├── (app)/               # Route group for authenticated app
│   │   │   ├── dashboard/       # User dashboard (SSR)
│   │   │   ├── grocery-lists/   # Grocery list management (Client)
│   │   │   ├── recipes/         # Personal recipes (SSR)
│   │   │   ├── meal-planning/   # Meal planning interface (Client)
│   │   │   ├── family/          # Family management (SSR)
│   │   │   ├── shopping/        # Live shopping sessions (Client)
│   │   │   └── layout.tsx       # App layout with auth
│   │   ├── api/                 # API routes (optional - can use external API)
│   │   │   ├── auth/            # Authentication endpoints
│   │   │   ├── webhooks/        # External service webhooks
│   │   │   └── health/          # Health check endpoints
│   │   ├── globals.css          # Global styles
│   │   ├── layout.tsx           # Root layout
│   │   ├── loading.tsx          # Global loading UI
│   │   ├── error.tsx            # Global error UI
│   │   └── not-found.tsx        # 404 page
│   ├── components/              # Reusable UI components
│   │   ├── ui/                  # Base UI components (shadcn/ui style)
│   │   ├── ImageUpload/         # Image upload and management
│   │   ├── Gallery/             # Image gallery and viewer
│   │   ├── Recipe/              # Recipe-specific components
│   │   ├── GroceryList/         # Grocery list components
│   │   ├── Family/              # Family management components
│   │   ├── RealTimeIndicators/  # Live collaboration indicators
│   │   └── Layout/              # Layout components
│   ├── hooks/                   # Custom React hooks
│   │   ├── useAuth.ts           # Authentication hook
│   │   ├── useRealTimeGroceryList.ts # Real-time grocery list
│   │   ├── useFamilyCollaboration.ts # Family collaboration
│   │   └── useImageUpload.ts    # Image upload handling
│   ├── lib/                     # Utility libraries
│   │   ├── auth.ts              # Authentication utilities
│   │   ├── api.ts               # API client configuration
│   │   ├── socket.ts            # Socket.IO client setup
│   │   ├── utils.ts             # General utilities
│   │   └── validations.ts       # Form validation schemas
│   ├── stores/                  # Zustand state stores
│   │   ├── authStore.ts         # Authentication state
│   │   ├── groceryStore.ts      # Grocery list state
│   │   ├── familyStore.ts       # Family collaboration state
│   │   └── settingsStore.ts     # User settings state
│   ├── types/                   # TypeScript type definitions
│   │   ├── auth.ts              # Authentication types
│   │   ├── grocery.ts           # Grocery list types
│   │   ├── recipe.ts            # Recipe types
│   │   └── api.ts               # API response types
│   ├── public/                  # Static assets
│   │   ├── icons/               # PWA icons
│   │   ├── images/              # Static images
│   │   └── manifest.json        # PWA manifest
│   ├── middleware.ts            # Next.js middleware for auth
│   ├── next.config.js           # Next.js configuration
│   ├── tailwind.config.js       # Tailwind CSS configuration
│   └── package.json
├── backend/                     # Node.js API server
│   ├── src/
│   │   ├── routes/              # Express route handlers
│   │   ├── models/              # Mongoose data models
│   │   ├── services/            # Business logic services
│   │   │   ├── ImageService.js  # Image upload and processing
│   │   │   ├── CDNService.js    # CDN integration service
│   │   │   └── RealtimeService.js # WebSocket and real-time collaboration
│   │   ├── middleware/          # Express middleware
│   │   │   ├── imageUpload.js   # Multer image upload middleware
│   │   │   └── socketAuth.js    # Socket.IO authentication middleware
│   │   ├── utils/               # Utility functions
│   │   │   ├── imageProcessor.js # Sharp.js image processing
│   │   │   └── eventEmitter.js  # Custom event handling for real-time updates
│   │   ├── sockets/             # Socket.IO event handlers
│   │   │   ├── groceryList.js   # Grocery list real-time events
│   │   │   └── shopping.js      # Shopping session management
│   │   └── types/               # TypeScript type definitions
│   ├── tests/                   # Backend tests
│   └── package.json
├── shared/                      # Shared types and utilities
│   ├── types/                   # Common TypeScript interfaces
│   └── utils/                   # Shared utility functions
├── docs/                        # Documentation
└── package.json                # Root package.json for monorepo
```

## Environment Variables

### Application Configuration
```bash
# Application
APP_URL=http://localhost:3000
API_URL=http://localhost:3001
NODE_ENV=development

# Next.js Configuration
NEXT_PUBLIC_APP_URL=http://localhost:3000
NEXT_PUBLIC_API_URL=http://localhost:3001
NEXTAUTH_SECRET=your-nextauth-secret
NEXTAUTH_URL=http://localhost:3000

# PWA Configuration
NEXT_PUBLIC_PWA_ENABLED=true
NEXT_PUBLIC_VAPID_PUBLIC_KEY=your-vapid-public-key
```

### Real-time Features
```bash
# Real-time Features
NEXT_PUBLIC_SOCKET_URL=http://localhost:3001
SOCKET_IO_ORIGINS=http://localhost:3000,https://yourdomain.com
REDIS_PUBSUB_URL=redis://localhost:6379
ENABLE_REAL_TIME_COLLABORATION=true
MAX_CONCURRENT_SHOPPERS=10
EDIT_LOCK_TIMEOUT=30000  # 30 seconds in milliseconds
PRESENCE_TIMEOUT=60000   # 1 minute in milliseconds
```

### Image Processing
```bash
# Image Processing
MAX_IMAGE_SIZE=10485760  # 10MB in bytes
SUPPORTED_IMAGE_FORMATS=jpg,jpeg,png,webp
THUMBNAIL_SIZE=300
MEDIUM_SIZE=800
LARGE_SIZE=1200
```

### Push Notifications
```bash
# Push Notifications
VAPID_PUBLIC_KEY=your-vapid-public-key
VAPID_PRIVATE_KEY=your-vapid-private-key
NOTIFICATION_EMAIL=notifications@yourdomain.com
```

### Database & Caching
```bash
# Database
MONGODB_URI=mongodb://localhost:27017/smart-grocery-list
REDIS_URL=redis://localhost:6379

# Authentication
JWT_SECRET=your-jwt-secret
GOOGLE_CLIENT_ID=your-google-client-id
GOOGLE_CLIENT_SECRET=your-google-client-secret
APPLE_CLIENT_ID=your-apple-client-id

# External APIs
USDA_API_KEY=your-usda-api-key
GOOGLE_CLOUD_API_KEY=your-google-cloud-key
OPENAI_API_KEY=your-openai-key

# Email
SENDGRID_API_KEY=your-sendgrid-key
FROM_EMAIL=noreply@yourdomain.com

# File Storage & Images
AWS_S3_BUCKET=your-s3-bucket-name
AWS_ACCESS_KEY_ID=your-aws-access-key
AWS_SECRET_ACCESS_KEY=your-aws-secret-key
AWS_REGION=us-east-1

# Alternative: Cloudinary
CLOUDINARY_CLOUD_NAME=your-cloud-name
CLOUDINARY_API_KEY=your-api-key
CLOUDINARY_API_SECRET=your-api-secret

# CDN
CDN_BASE_URL=https://your-cdn-domain.com
```

## Development Guidelines

### Code Style & Standards
- **TypeScript**: Strict mode enabled, no `any` types
- **ESLint**: Next.js recommended configuration with TypeScript rules
- **Prettier**: Automatic code formatting on save
- **Naming Conventions**: 
  - Components: PascalCase (e.g., `GroceryListItem`)
  - Files: kebab-case for components (e.g., `grocery-list-item.tsx`)
  - Pages: lowercase for App Router (e.g., `app/grocery-lists/page.tsx`)
  - Variables/Functions: camelCase (e.g., `createGroceryList`)
  - Constants: SCREAMING_SNAKE_CASE (e.g., `API_BASE_URL`)

### Component Architecture
- **Server Components**: Default for data fetching and static content
- **Client Components**: Use "use client" directive for interactivity and real-time features
- **Custom Hooks**: Extract reusable logic into custom hooks
- **Component Composition**: Prefer composition over prop drilling
- **Error Boundaries**: Implement error boundaries for graceful error handling

### State Management
- **Server State**: React Query/TanStack Query for API data and caching
- **Client State**: Zustand stores for app-wide client state
- **Local State**: useState for component-specific state
- **Form State**: React Hook Form for complex forms
- **Real-time State**: Custom hooks with Socket.IO for live collaboration

### API Design
- **Next.js API Routes**: Optional API routes for webhooks and auth callbacks
- **External API**: Primary API server for business logic
- **Server Actions**: Use Next.js Server Actions for simple server operations
- **Error Handling**: Consistent error response format
- **Validation**: Zod for both client and server-side validation
- **Rate Limiting**: Implement rate limiting for API protection

## Key Development Areas

### 1. Authentication System
**Priority**: High | **Phase**: 1

Implement passwordless authentication with multiple providers using Next.js:
- Email magic links with 6-digit codes
- Google OAuth 2.0 integration  
- Apple Sign In support
- JWT-based session management with Next.js middleware
- Device tracking and session management

**Key Files to Create:**
- `backend/src/services/auth/EmailAuthManager.js`
- `backend/src/services/auth/SocialAuthManager.js`
- `backend/src/middleware/auth.js`
- `app/api/auth/` # Next.js API routes for auth callbacks
- `app/(auth)/login/page.tsx` # Login page (SSR)
- `app/(auth)/verify/page.tsx` # Email verification page
- `hooks/useAuth.ts`
- `lib/auth.ts`
- `middleware.ts` # Next.js middleware for route protection

### 2. Grocery List Management
**Priority**: High | **Phase**: 1

Core grocery list functionality with smart suggestions and real-time collaboration:
- CRUD operations for grocery lists
- Item categorization and organization
- Purchase history tracking
- Pattern-based suggestions
- Offline synchronization with Next.js PWA
- Real-time collaboration for simultaneous shoppers
- Live item status updates (purchased, added, modified)
- Shopping session management with active user tracking

**Key Files to Create:**
- `backend/src/models/GroceryList.js`
- `backend/src/models/ActiveShopper.js`
- `backend/src/models/GroceryListEvent.js`
- `backend/src/services/GroceryListService.js`
- `backend/src/services/RealtimeService.js`
- `backend/src/services/PurchasePatternAnalyzer.js`
- `backend/src/sockets/groceryList.js`
- `backend/src/sockets/shopping.js`
- `app/(app)/grocery-lists/page.tsx` # Grocery lists overview (SSR)
- `app/(app)/grocery-lists/[id]/page.tsx` # Individual list (Client Component)
- `app/(app)/shopping/[id]/page.tsx` # Live shopping session (Client)
- `components/GroceryList/` # All grocery list components
- `hooks/useRealTimeGroceryList.ts`
- `stores/groceryStore.ts`
- `lib/socket.ts` # Socket.IO client setup

### 3. Recipe Management
**Priority**: Medium | **Phase**: 2

Recipe creation, storage, and sharing with comprehensive image support:
- Manual recipe input with rich editor
- OCR recipe scanning functionality
- Ingredient parsing with NLP
- Recipe variations and modifications
- Nutritional calculation per serving
- Hero image upload and management
- Step-by-step instruction images
- Image optimization with Next.js Image component
- SEO-optimized public recipe pages

**Key Files to Create:**
- `backend/src/models/Recipe.js`
- `backend/src/models/RecipeImage.js`
- `backend/src/services/RecipeService.js`
- `backend/src/services/ImageService.js`
- `backend/src/services/OCRService.js`
- `backend/src/services/NutritionCalculator.js`
- `backend/src/middleware/imageUpload.js`
- `backend/src/utils/imageProcessor.js`
- `app/(marketing)/recipes/page.tsx` # Public recipe discovery (SSG)
- `app/(marketing)/recipes/[id]/page.tsx` # Public recipe view (SSG/ISR)
- `app/(app)/recipes/page.tsx` # Personal recipes (SSR)
- `app/(app)/recipes/create/page.tsx` # Recipe creation (Client)
- `app/(app)/recipes/[id]/edit/page.tsx` # Recipe editing (Client)
- `components/Recipe/` # All recipe components
- `components/ImageUpload/` # Image upload components
- `hooks/useImageUpload.ts`
- `lib/imageUtils.ts`

### 4. Family Collaboration
**Priority**: Medium | **Phase**: 3

Family unit management and real-time sharing:
- Family creation and invitation system
- Role-based permissions (admin, adult, teen, child)
- Shared grocery lists and recipes
- Real-time collaboration features with conflict resolution
- Family meal planning
- Live shopping session management
- Push notifications for real-time updates

**Key Files to Create:**
- `backend/src/models/FamilyUnit.js`
- `backend/src/services/FamilyManager.js`
- `backend/src/services/InvitationService.js`
- `backend/src/services/CollaborationService.js`
- `backend/src/sockets/family.js`
- `app/(app)/family/page.tsx` # Family overview (SSR)
- `app/(app)/family/invite/page.tsx` # Family invitations (Client)
- `app/(app)/family/settings/page.tsx` # Family settings (SSR)
- `app/api/family/invite/route.ts` # Next.js API route for invitations
- `components/Family/` # Family management components
- `components/RealTimeIndicators/` # Live collaboration indicators
- `hooks/useFamilyCollaboration.ts`
- `stores/familyStore.ts`

### 5. Nutritional Integration
**Priority**: Medium | **Phase**: 2

USDA API integration and caching with Next.js optimization:
- USDA FoodData Central API wrapper
- Intelligent caching strategy with Next.js cache
- Nutrition calculation engine
- Dietary restriction filtering
- Meal planning optimization

**Key Files to Create:**
- `backend/src/services/USDAAPIService.js`
- `backend/src/services/NutritionCacheManager.js`
- `backend/src/models/USDAFoodCache.js`
- `backend/src/services/MealPlanningService.js`
- `app/(app)/meal-planning/page.tsx` # Meal planning interface (Client)
- `app/(app)/nutrition/page.tsx` # Nutrition tracking (SSR)
- `app/api/nutrition/search/route.ts` # Next.js API route for nutrition search
- `components/Nutrition/` # Nutrition components
- `hooks/useNutritionData.ts`

## Performance Considerations

### Caching Strategy
- **API Responses**: Redis caching for external API calls
- **User Sessions**: Redis session storage
- **USDA Data**: MongoDB caching with TTL
- **Static Assets**: Next.js automatic static optimization and Vercel Edge Network
- **Image Optimization**: Next.js Image component with automatic optimization and caching
- **Progressive Loading**: Thumbnail-first loading strategy
- **Real-time State**: Redis for active shopping sessions and live user presence
- **Event Cache**: Short-term caching of recent grocery list events for quick sync
- **Page Cache**: Next.js ISR (Incremental Static Regeneration) for dynamic pages

### Database Optimization
- **Connection Pooling**: MongoDB connection pooling
- **Query Optimization**: Explain plan analysis for slow queries
- **Aggregation Pipelines**: Efficient data aggregation
- **Data Archiving**: Archive old purchase history

### Frontend Performance
- **Code Splitting**: Automatic code splitting with Next.js App Router
- **Lazy Loading**: Component and image lazy loading with Next.js Image
- **Image Optimization**: WebP/AVIF format support with automatic format selection
- **Progressive Loading**: Thumbnail-to-full-resolution image loading
- **Service Worker**: next-pwa for aggressive caching and offline functionality
- **Bundle Analysis**: @next/bundle-analyzer for bundle size monitoring
- **Streaming**: React Suspense for incremental page loading

## Testing Strategy

### Unit Testing
- **Coverage Target**: 80% code coverage minimum
- **Test Files**: Co-locate tests with source files
- **Mocking**: Mock external dependencies
- **Test Data**: Use factories for test data generation

### Integration Testing
- **API Testing**: Test all endpoints with various scenarios
- **Database Testing**: Test data persistence and retrieval
- **External Services**: Mock external API calls

### End-to-End Testing
- **User Journeys**: Test complete user workflows
- **Cross-Browser**: Test on major browsers
- **Mobile Testing**: Test responsive design and touch interactions
- **Accessibility**: Test screen reader compatibility

## Getting Started

### Prerequisites
- Node.js 18+ and npm/yarn
- MongoDB (local or Atlas)
- Redis (local or cloud)
- Git for version control

### Initial Setup Commands
```bash
# Clone repository
git clone https://github.com/nwwatson/smart-grocery-list.git
cd smart-grocery-list

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env.local
# Edit .env.local with your configuration

# Start development servers
npm run dev:backend    # Start Express server
npm run dev           # Start Next.js development server
npm run dev:redis     # Start Redis (if local)

# Build for production
npm run build         # Build Next.js application
npm run start         # Start production server

# Run tests
npm run test          # Run all tests
npm run test:watch    # Run tests in watch mode
```

## Common Development Tasks

### Adding a New Feature
1. Create feature branch: `git checkout -b feature/feature-name`
2. Add database models if needed in backend
3. Create API endpoints with validation
4. **For real-time features**: Add Socket.IO event handlers
5. **For collaboration**: Implement conflict resolution logic
6. Write unit tests for business logic
7. **Create Next.js pages/components**:
   - Determine if Server Component (SSG/SSR) or Client Component
   - Add proper TypeScript types
   - Implement error boundaries and loading states
8. **For real-time UI**: Add WebSocket integration and optimistic updates
9. Add integration tests including Next.js specific features
10. Update documentation
11. Submit pull request

### Next.js Specific Development Workflow
1. **Pages**: Create in `app/` directory using App Router conventions
2. **Server Components**: Default for data fetching and static content
3. **Client Components**: Add "use client" directive for interactivity
4. **API Routes**: Use for webhooks, auth callbacks, and simple endpoints
5. **Middleware**: Handle authentication and route protection
6. **Image Optimization**: Always use Next.js Image component for recipe photos

### Real-Time Development Workflow
1. **Backend**: Create Socket.IO event handlers in `src/sockets/`
2. **Frontend**: Use custom hooks like `useRealTimeGroceryList` in Client Components
3. **Testing**: Test real-time features with multiple browser windows
4. **Conflict Resolution**: Handle simultaneous edits gracefully
5. **Offline Support**: Queue changes using Next.js PWA capabilities

### Performance Optimization for Next.js
1. **Optimize Pages**: Choose appropriate rendering strategy (SSG/SSR/ISR)
2. **Image Optimization**: Use Next.js Image component with proper sizing
3. **Bundle Analysis**: Use @next/bundle-analyzer to monitor bundle size
4. **Caching**: Leverage Next.js built-in caching and Vercel Edge Network
5. **Real-Time Updates**: Batch updates and debounce frequent changes
6. **Loading States**: Implement proper loading.tsx and error.tsx files

## Development Phases

### Phase 1: MVP Foundation (8-10 weeks)
**Goal**: Core functionality for individual users with Next.js foundation

**Key Features:**
- User authentication (email + social) with Next.js middleware
- Basic grocery list management with real-time updates
- Manual recipe creation with Next.js Image optimization
- Simple purchase history
- Next.js PWA setup with next-pwa package

**Deliverables:**
- Working Next.js application with App Router
- Authentication system with middleware protection
- Basic grocery list CRUD with Server and Client Components
- Recipe creation with image upload using Next.js Image
- MongoDB data models
- PWA configuration with offline functionality

### Phase 2: Intelligence Layer (6-8 weeks)
**Goal**: Smart features and nutritional data with SEO optimization

**Key Features:**
- USDA API integration and caching with Next.js optimization
- Purchase pattern analysis
- Smart grocery suggestions
- Recipe nutrition calculations
- Basic meal planning interface
- SEO-optimized public recipe pages (SSG/ISR)

**Deliverables:**
- Nutrition calculation engine
- Purchase pattern analyzer
- Suggestion algorithm
- Public recipe discovery with SSG
- Meal planning interface with Client Components
- Performance optimizations with Next.js Image and caching

### Phase 3: Family Collaboration (6-8 weeks)
**Goal**: Multi-user collaboration features

**Key Features:**
- Family unit management
- Shared grocery lists
- Recipe sharing with privacy controls
- Role-based permissions
- Real-time collaboration

**Deliverables:**
- Family management system
- Shared data models
- Permission system
- Real-time updates
- Collaboration UI

### Phase 4: Advanced Features (6-8 weeks)
**Goal**: Advanced functionality and optimization

**Key Features:**
- OCR recipe scanning
- Advanced ML recommendations
- Community features
- Advanced nutrition tracking
- Performance optimization

**Deliverables:**
- OCR service integration
- Community recipe discovery
- Advanced analytics
- Performance improvements
- Mobile app optimization

### Phase 5: Polish & Launch (4-6 weeks)
**Goal**: Production readiness with Next.js optimizations

**Key Features:**
- UI/UX refinements with Next.js best practices
- Performance optimization using Next.js built-in features
- Security hardening with Next.js middleware
- Beta testing with Vercel deployment
- SEO optimization for public pages

**Deliverables:**
- Polished user interface with Next.js App Router
- Security audit completion with middleware protection
- Performance benchmarks using Core Web Vitals
- Production deployment on Vercel
- SEO-optimized public pages with proper meta tags
- Comprehensive documentation

This guide should help Claude Code understand the project structure, requirements, and development approach for the Smart Grocery List application. The file provides comprehensive context for AI-assisted development while maintaining focus on practical implementation details.