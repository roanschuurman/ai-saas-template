# SaaS Development Instructions (Next.js/TypeScript)

## Development Environment Requirements

### Node.js & Package Manager
- **Node.js**: 20.10.0+ (LTS)
- **Package Manager**: npm 10.2.0+ or pnpm 8.10.0+ (preferred)
- **TypeScript**: 5.3.0+

### IDE Setup
- **Primary**: VS Code with essential extensions
- **Required Extensions**:
  - TypeScript Importer (pmneo.tsimporter)
  - Tailwind CSS IntelliSense (bradlc.vscode-tailwindcss)
  - ESLint (dbaeumer.vscode-eslint)
  - Prettier (esbenp.prettier-vscode)
  - Auto Rename Tag (formulahendry.auto-rename-tag)

### Browser Development Tools
- Chrome DevTools with React Developer Tools
- Lighthouse for performance auditing
- axe DevTools for accessibility testing

## Code Quality Standards

### TypeScript Configuration
```json
// tsconfig.json (strict configuration required)
{
  "compilerOptions": {
    "target": "ES2022",
    "lib": ["dom", "dom.iterable", "es6"],
    "allowJs": true,
    "skipLibCheck": true,
    "strict": true,
    "noEmit": true,
    "esModuleInterop": true,
    "module": "esnext",
    "moduleResolution": "bundler",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "jsx": "preserve",
    "incremental": true,
    "plugins": [{ "name": "next" }],
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"],
      "@/components/*": ["./src/components/*"],
      "@/lib/*": ["./src/lib/*"]
    }
  },
  "include": ["next-env.d.ts", "**/*.ts", "**/*.tsx", ".next/types/**/*.ts"],
  "exclude": ["node_modules"]
}
```

### ESLint & Prettier Configuration
```json
// .eslintrc.json
{
  "extends": [
    "next/core-web-vitals",
    "@typescript-eslint/recommended",
    "prettier"
  ],
  "rules": {
    "@typescript-eslint/no-unused-vars": "error",
    "@typescript-eslint/no-explicit-any": "error",
    "prefer-const": "error",
    "no-var": "error"
  }
}
```

```json
// .prettierrc
{
  "semi": true,
  "trailingComma": "es5",
  "singleQuote": true,
  "tabWidth": 2,
  "useTabs": false
}
```

### Dependency Management
```json
// package.json - exact versions for production
{
  "dependencies": {
    "next": "14.0.4",
    "react": "18.2.0",
    "react-dom": "18.2.0",
    "typescript": "5.3.3",
    "@supabase/supabase-js": "2.38.4",
    "@supabase/auth-helpers-nextjs": "0.8.7",
    "tailwindcss": "3.4.1",
    "@radix-ui/react-dialog": "1.0.5",
    "zod": "3.22.4",
    "react-hook-form": "7.48.2"
  },
  "devDependencies": {
    "@types/node": "20.10.5",
    "@types/react": "18.2.45",
    "@types/react-dom": "18.2.18",
    "eslint": "8.56.0",
    "eslint-config-next": "14.0.4",
    "prettier": "3.1.1",
    "vitest": "1.1.0",
    "@testing-library/react": "14.1.2",
    "playwright": "1.40.1"
  }
}
```

## Architecture Patterns

### Next.js App Router Structure
```
src/
├── app/                    # App Router (Next.js 13+)
│   ├── layout.tsx         # Root layout
│   ├── page.tsx           # Home page
│   ├── globals.css        # Global styles
│   ├── api/               # API routes
│   └── modules/           # Feature-based organization
│       └── {feature}/
│           ├── components/    # Feature UI components
│           ├── hooks/         # Custom React hooks
│           ├── services/      # Data fetching & business logic
│           ├── types/         # TypeScript type definitions
│           ├── utils/         # Feature-specific utilities
│           └── tests/         # Feature tests
├── components/             # Shared/reusable components
│   ├── ui/                # Base UI components (shadcn/ui)
│   └── layout/            # Layout components
├── lib/                   # Shared utilities
│   ├── supabase/          # Database client & types
│   ├── auth/              # Authentication utilities
│   ├── validations/       # Zod schemas
│   └── utils/             # General utilities
└── types/                 # Global type definitions
```

### Component Architecture
```tsx
// Required component pattern
import { cn } from '@/lib/utils';
import { type ComponentProps } from 'react';

interface ButtonProps extends ComponentProps<'button'> {
  variant?: 'primary' | 'secondary' | 'destructive';
  size?: 'sm' | 'md' | 'lg';
  loading?: boolean;
}

export function Button({
  className,
  variant = 'primary',
  size = 'md',
  loading = false,
  children,
  disabled,
  ...props
}: ButtonProps) {
  return (
    <button
      className={cn(
        'inline-flex items-center justify-center rounded-md font-medium transition-colors',
        'focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-offset-2',
        'disabled:opacity-50 disabled:pointer-events-none',
        {
          'bg-primary text-primary-foreground hover:bg-primary/90': variant === 'primary',
          'bg-secondary text-secondary-foreground hover:bg-secondary/80': variant === 'secondary',
          'bg-destructive text-destructive-foreground hover:bg-destructive/90': variant === 'destructive',
        },
        {
          'h-8 px-3 text-sm': size === 'sm',
          'h-10 px-4': size === 'md',
          'h-12 px-6 text-lg': size === 'lg',
        },
        className
      )}
      disabled={disabled || loading}
      {...props}
    >
      {loading && <Loader2 className="mr-2 h-4 w-4 animate-spin" />}
      {children}
    </button>
  );
}
```

## Database & API Standards

### Supabase Configuration
```typescript
// lib/supabase/client.ts
import { createClientComponentClient } from '@supabase/auth-helpers-nextjs';
import { Database } from './types';

export const supabase = createClientComponentClient<Database>();

// lib/supabase/server.ts (for Server Components)
import { createServerComponentClient } from '@supabase/auth-helpers-nextjs';
import { cookies } from 'next/headers';
import { Database } from './types';

export const createServerSupabaseClient = () =>
  createServerComponentClient<Database>({ cookies });
```

### Type-Safe Database Access
```typescript
// Generate types from Supabase schema
// npx supabase gen types typescript --project-id YOUR_PROJECT_ID > lib/supabase/types.ts

// Service pattern for data access
export class UserService {
  static async getUser(id: string): Promise<User | null> {
    const { data, error } = await supabase
      .from('users')
      .select('*')
      .eq('id', id)
      .single();
    
    if (error) {
      console.error('Error fetching user:', error);
      throw new Error(`Failed to fetch user: ${error.message}`);
    }
    
    return data;
  }
  
  static async updateUser(id: string, updates: Partial<User>): Promise<User> {
    const { data, error } = await supabase
      .from('users')
      .update(updates)
      .eq('id', id)
      .select()
      .single();
    
    if (error) {
      throw new Error(`Failed to update user: ${error.message}`);
    }
    
    return data;
  }
}
```

### Row Level Security (RLS) Patterns
```sql
-- Required: Enable RLS on all tables
ALTER TABLE users ENABLE ROW LEVEL SECURITY;

-- User can only see their own data
CREATE POLICY "Users can view own profile" ON users
  FOR SELECT USING (auth.uid() = id);

-- User can only update their own data
CREATE POLICY "Users can update own profile" ON users
  FOR UPDATE USING (auth.uid() = id);
```

## Authentication & Authorization

### Auth Configuration
```typescript
// lib/auth/config.ts
export const authConfig = {
  pages: {
    signIn: '/auth/signin',
    signUp: '/auth/signup',
    error: '/auth/error',
  },
  redirects: {
    afterSignIn: '/dashboard',
    afterSignUp: '/onboarding',
    afterSignOut: '/',
  },
};

// Middleware for protected routes
// middleware.ts
import { createMiddlewareClient } from '@supabase/auth-helpers-nextjs';
import { NextResponse } from 'next/server';
import type { NextRequest } from 'next/server';

export async function middleware(req: NextRequest) {
  const res = NextResponse.next();
  const supabase = createMiddlewareClient({ req, res });
  
  const {
    data: { session },
  } = await supabase.auth.getSession();
  
  // Protected routes
  if (req.nextUrl.pathname.startsWith('/dashboard') && !session) {
    return NextResponse.redirect(new URL('/auth/signin', req.url));
  }
  
  return res;
}

export const config = {
  matcher: ['/dashboard/:path*', '/admin/:path*'],
};
```

## Form Handling & Validation

### Zod Schemas
```typescript
// lib/validations/auth.ts
import { z } from 'zod';

export const signUpSchema = z.object({
  email: z.string().email('Invalid email address'),
  password: z.string().min(8, 'Password must be at least 8 characters'),
  confirmPassword: z.string(),
}).refine((data) => data.password === data.confirmPassword, {
  message: "Passwords don't match",
  path: ["confirmPassword"],
});

export type SignUpFormData = z.infer<typeof signUpSchema>;
```

### React Hook Form Integration
```tsx
// components/auth/SignUpForm.tsx
import { useForm } from 'react-hook-form';
import { zodResolver } from '@hookform/resolvers/zod';
import { signUpSchema, type SignUpFormData } from '@/lib/validations/auth';

export function SignUpForm() {
  const {
    register,
    handleSubmit,
    formState: { errors, isSubmitting },
  } = useForm<SignUpFormData>({
    resolver: zodResolver(signUpSchema),
  });

  const onSubmit = async (data: SignUpFormData) => {
    try {
      await authService.signUp(data);
      // Handle success
    } catch (error) {
      // Handle error
    }
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)} className="space-y-4">
      <div>
        <Input
          {...register('email')}
          type="email"
          placeholder="Email"
          aria-invalid={errors.email ? 'true' : 'false'}
        />
        {errors.email && (
          <p className="mt-1 text-sm text-red-600">{errors.email.message}</p>
        )}
      </div>
      
      <Button type="submit" loading={isSubmitting} className="w-full">
        Sign Up
      </Button>
    </form>
  );
}
```

## Testing Standards

### Test Coverage Targets
- **Unit Tests**: >85% for utilities/services
- **Component Tests**: >80% for components
- **E2E Tests**: Critical user journeys only

### Unit Testing (Vitest)
```typescript
// vitest.config.ts
import { defineConfig } from 'vitest/config';
import react from '@vitejs/plugin-react';

export default defineConfig({
  plugins: [react()],
  test: {
    environment: 'jsdom',
    setupFiles: ['./src/test/setup.ts'],
  },
});

// Example test
import { describe, it, expect } from 'vitest';
import { render, screen } from '@testing-library/react';
import { Button } from '@/components/ui/Button';

describe('Button', () => {
  it('renders with correct text', () => {
    render(<Button>Click me</Button>);
    expect(screen.getByRole('button', { name: 'Click me' })).toBeInTheDocument();
  });

  it('shows loading state', () => {
    render(<Button loading>Submit</Button>);
    expect(screen.getByRole('button')).toBeDisabled();
  });
});
```

### E2E Testing (Playwright)
```typescript
// tests/auth.spec.ts
import { test, expect } from '@playwright/test';

test.describe('Authentication', () => {
  test('user can sign up', async ({ page }) => {
    await page.goto('/auth/signup');
    
    await page.fill('[data-testid="email-input"]', 'test@example.com');
    await page.fill('[data-testid="password-input"]', 'password123');
    await page.fill('[data-testid="confirm-password-input"]', 'password123');
    
    await page.click('[data-testid="signup-button"]');
    
    await expect(page).toHaveURL('/onboarding');
  });
});
```

## Performance Standards

### Core Web Vitals Targets
- **LCP**: <2.5s (First Contentful Paint)
- **FID**: <100ms (First Input Delay)
- **CLS**: <0.1 (Cumulative Layout Shift)

### Performance Optimization
```typescript
// Required: Image optimization
import Image from 'next/image';

function ProfileImage({ user }: { user: User }) {
  return (
    <Image
      src={user.avatar_url}
      alt={`${user.name}'s avatar`}
      width={100}
      height={100}
      className="rounded-full"
      priority={false} // Only true for above-the-fold images
    />
  );
}

// Required: Dynamic imports for code splitting
import dynamic from 'next/dynamic';

const HeavyComponent = dynamic(() => import('./HeavyComponent'), {
  loading: () => <Skeleton className="h-32 w-full" />,
});
```

### Bundle Analysis
```bash
# Required: Regular bundle analysis
npm run build
npx @next/bundle-analyzer
```

## Security Requirements

### Environment Variables
```bash
# .env.local (never commit)
NEXT_PUBLIC_SUPABASE_URL=your_supabase_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_anon_key
SUPABASE_SERVICE_ROLE_KEY=your_service_role_key
NEXTAUTH_SECRET=your_nextauth_secret
STRIPE_SECRET_KEY=your_stripe_secret
```

### Content Security Policy
```typescript
// next.config.js
const nextConfig = {
  async headers() {
    return [
      {
        source: '/(.*)',
        headers: [
          {
            key: 'Content-Security-Policy',
            value: `
              default-src 'self';
              script-src 'self' 'unsafe-eval' 'unsafe-inline';
              style-src 'self' 'unsafe-inline';
              img-src 'self' data: https:;
              font-src 'self';
            `.replace(/\s{2,}/g, ' ').trim()
          }
        ],
      },
    ];
  },
};
```

## Accessibility Standards

### Required Patterns
```tsx
// Semantic HTML and ARIA labels
function SearchForm() {
  return (
    <form role="search" aria-label="Search products">
      <label htmlFor="search-input" className="sr-only">
        Search products
      </label>
      <input
        id="search-input"
        type="search"
        placeholder="Search..."
        aria-describedby="search-help"
      />
      <div id="search-help" className="sr-only">
        Enter keywords to search for products
      </div>
      <button type="submit" aria-label="Submit search">
        <SearchIcon aria-hidden="true" />
      </button>
    </form>
  );
}
```

### Color Contrast Requirements
- Normal text: 4.5:1 ratio minimum
- Large text: 3:1 ratio minimum
- UI components: 3:1 ratio minimum

## Error Handling & Monitoring

### Error Boundaries
```tsx
// components/ErrorBoundary.tsx
'use client';

import { Component, type ReactNode } from 'react';

interface Props {
  children: ReactNode;
  fallback?: ReactNode;
}

interface State {
  hasError: boolean;
  error?: Error;
}

export class ErrorBoundary extends Component<Props, State> {
  constructor(props: Props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error: Error): State {
    return { hasError: true, error };
  }

  componentDidCatch(error: Error, errorInfo: any) {
    console.error('Error caught by boundary:', error, errorInfo);
    // Send to monitoring service
  }

  render() {
    if (this.state.hasError) {
      return this.props.fallback || <ErrorFallback />;
    }

    return this.props.children;
  }
}
```

### Logging & Monitoring
```typescript
// lib/monitoring.ts
export const logger = {
  error: (message: string, error?: Error, context?: Record<string, any>) => {
    console.error(message, error, context);
    // Send to monitoring service (Sentry, LogRocket, etc.)
  },
  
  warn: (message: string, context?: Record<string, any>) => {
    console.warn(message, context);
  },
  
  info: (message: string, context?: Record<string, any>) => {
    console.info(message, context);
  },
};
```

## Deployment & CI/CD

### Build Configuration
```bash
# Production build
npm run build
npm run start

# Type checking
npm run type-check

# Linting
npm run lint
npm run lint:fix
```

### Required CI/CD Pipeline
1. **Install Dependencies**: `npm ci`
2. **Type Check**: `npm run type-check`
3. **Lint**: `npm run lint`
4. **Test**: `npm run test`
5. **Build**: `npm run build`
6. **E2E Tests**: `npm run test:e2e`
7. **Security Audit**: `npm audit`
8. **Deploy**: Platform-specific deployment

### Environment Strategy
- **Development**: Local development with hot reload
- **Preview**: Branch deployments for testing
- **Production**: Main branch deployments only

---
*This document is living and should be updated as standards evolve.*
