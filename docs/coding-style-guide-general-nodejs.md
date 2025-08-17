# Node.js JavaScript / TypeScript Coding Style Guide

*Version 1.1 – Last updated 2025-08-08*

gist: [lemyskaman/TS-JS-nodejs-react-vite-style-guide.md](https://gist.github.com/lemyskaman/ddb1de4af45ff6c342910c64eba031ce)

A comprehensive coding style guide for full-stack Node.js applications with React frontend, TypeScript, and Vite compiler. This guide extends the base Node.js standards to include modern full-stack development patterns.

***

## Table of Contents

- [Node.js JavaScript / TypeScript Coding Style Guide](#nodejs-javascript--typescript-coding-style-guide)
  - [Table of Contents](#table-of-contents)
  - [Enhanced Project Structure (Full-Stack Monorepo)](#enhanced-project-structure-full-stack-monorepo)
    - [Recommended Full-Stack Monorepo Structure^1^3](#recommended-full-stack-monorepo-structure13)
    - [Key Principles](#key-principles)
  - [React + TypeScript Guidelines](#react--typescript-guidelines)
    - [Component Structure \& Naming^11](#component-structure--naming11)
    - [React Hooks Best Practices](#react-hooks-best-practices)
    - [React Component Organization](#react-component-organization)
  - [Vite Configuration \& Optimization](#vite-configuration--optimization)
    - [Essential Vite Configuration](#essential-vite-configuration)
    - [TypeScript Configuration for Vite](#typescript-configuration-for-vite)
  - [Shared Component Libraries](#shared-component-libraries)
    - [Component Library Structure^8](#component-library-structure8)
    - [Storybook Configuration^8](#storybook-configuration8)
  - [State Management Patterns](#state-management-patterns)
    - [Redux Toolkit Setup](#redux-toolkit-setup)
    - [React Query Alternative](#react-query-alternative)
  - [API Integration \& Data Flow](#api-integration--data-flow)
    - [HTTP Client Setup](#http-client-setup)
  - [Full-Stack Development Tooling](#full-stack-development-tooling)
    - [Package.json Scripts (Root)](#packagejson-scripts-root)
  - [Testing Strategy (Full-Stack)](#testing-strategy-full-stack)
    - [Frontend Testing Setup^13](#frontend-testing-setup13)
    - [Component Testing Example](#component-testing-example)
  - [Build \& Deployment Pipeline](#build--deployment-pipeline)
    - [Docker Configuration](#docker-configuration)
  - [Performance Optimization (Full-Stack)](#performance-optimization-full-stack)
    - [React Performance Patterns](#react-performance-patterns)
    - [Vite Bundle Analysis](#vite-bundle-analysis)
  - [Summary](#summary)
    - [Key Takeaways^17^9](#key-takeaways179)

***

## Enhanced Project Structure (Full-Stack Monorepo)

### Recommended Full-Stack Monorepo Structure[^1][^2][^3][^4]

Based on modern best practices for React + Node.js full-stack applications, here's the optimal project organization:

```
project-root/
├── apps/                         # Applications
│   ├── web/                      # React web app (Vite)
│   │   ├── public/
│   │   │   ├── index.html
│   │   │   └── favicon.ico
│   │   ├── src/
│   │   │   ├── app/              # App-level setup
│   │   │   │   ├── App.tsx
│   │   │   │   ├── main.tsx
│   │   │   │   └── router.tsx
│   │   │   ├── features/         # Feature-based organization
│   │   │   │   ├── auth/
│   │   │   │   │   ├── components/
│   │   │   │   │   │   ├── LoginForm/
│   │   │   │   │   │   │   ├── LoginForm.tsx
│   │   │   │   │   │   │   ├── LoginForm.test.tsx
│   │   │   │   │   │   │   └── LoginForm.module.css
│   │   │   │   │   │   └── SignupForm/
│   │   │   │   │   ├── hooks/
│   │   │   │   │   │   ├── useAuth.ts
│   │   │   │   │   │   └── useLogin.ts
│   │   │   │   │   ├── services/
│   │   │   │   │   │   └── authApi.ts
│   │   │   │   │   ├── store/
│   │   │   │   │   │   └── authSlice.ts
│   │   │   │   │   ├── types/
│   │   │   │   │   │   └── auth.types.ts
│   │   │   │   │   └── pages/
│   │   │   │   │       ├── LoginPage.tsx
│   │   │   │   │       └── SignupPage.tsx
│   │   │   │   ├── user-management/
│   │   │   │   └── dashboard/
│   │   │   ├── shared/           # Shared frontend concerns
│   │   │   │   ├── components/   # Reusable UI components
│   │   │   │   │   ├── ui/        # Basic UI elements
│   │   │   │   │   │   ├── Button/
│   │   │   │   │   │   ├── Input/
│   │   │   │   │   │   ├── Modal/
│   │   │   │   │   │   └── index.ts
│   │   │   │   │   ├── layout/
│   │   │   │   │   │   ├── Header/
│   │   │   │   │   │   ├── Sidebar/
│   │   │   │   │   │   └── Footer/
│   │   │   │   │   └── forms/
│   │   │   │   ├── hooks/        # Shared custom hooks
│   │   │   │   ├── services/     # API clients, utilities
│   │   │   │   ├── store/        # Global state management
│   │   │   │   ├── types/        # Shared TypeScript types
│   │   │   │   ├── utils/        # Helper functions
│   │   │   │   └── styles/       # Global styles & themes
│   │   │   ├── assets/           # Static assets
│   │   │   └── __tests__/        # Global test utilities
│   │   ├── vite.config.ts
│   │   ├── tsconfig.json
│   │   ├── package.json
│   │   └── .env.example
│   │
│   └── api/                      # Node.js backend
│       ├── src/
│       │   ├── features/         # Vertical slice architecture
│       │   ├── shared/
│       │   ├── types/
│       │   ├── config/
│       │   └── app.js
│       └── ...
│
├── packages/                     # Shared packages
│   ├── shared-types/            # Shared TypeScript definitions
│   ├── ui-components/           # Shared React component library
│   └── eslint-config/           # Shared ESLint configuration
│
├── tools/                       # Development & build tools
│   ├── scripts/
│   └── generators/
│
├── docs/                        # Documentation
├── .github/                     # GitHub workflows
├── package.json                 # Root package.json (workspaces)
├── tsconfig.base.json          # Base TypeScript config
├── docker-compose.yml          # Development environment
└── README.md
```


### Key Principles

1. **Monorepo Organization**: Use npm/yarn workspaces for dependency management[^2][^4]
2. **Feature-First Structure**: Both frontend and backend organized by business features[^5][^6]
3. **Shared Packages**: Common types, components, and configurations[^7][^8]
4. **Tool Separation**: Different tools for different concerns (Vite for frontend, Node.js for backend)[^9][^10]

***

## React + TypeScript Guidelines

### Component Structure \& Naming[^11][^12]

```tsx
// ✅ Good - Functional component with TypeScript
import React from 'react';
import styles from './UserCard.module.css';

interface User {
  id: string;
  name: string;
  email: string;
  avatar?: string;
}

interface UserCardProps {
  user: User;
  onEdit?: (userId: string) => void;
  isEditable?: boolean;
  className?: string;
}

export const UserCard: React.FC<UserCardProps> = ({ 
  user, 
  onEdit, 
  isEditable = false,
  className 
}) => {
  const handleEditClick = () => {
    onEdit?.(user.id);
  };

  return (
    <div className={`${styles.userCard} ${className || ''}`}>
      <img 
        src={user.avatar || '/default-avatar.png'} 
        alt={`${user.name}'s avatar`}
        className={styles.avatar}
      />
      <div className={styles.info}>
        <h3 className={styles.name}>{user.name}</h3>
        <p className={styles.email}>{user.email}</p>
        {isEditable && (
          <button onClick={handleEditClick} className={styles.editButton}>
            Edit
          </button>
        )}
      </div>
    </div>
  );
};

export default UserCard;
```


### React Hooks Best Practices

```tsx
// ✅ Good - Custom hook with TypeScript
import { useState, useEffect, useCallback } from 'react';

interface UseApiOptions {
  immediate?: boolean;
}

interface UseApiReturn<T> {
  data: T | null;
  loading: boolean;
  error: string | null;
  refetch: () => Promise<void>;
}

export const useApi = <T>(
  apiCall: () => Promise<T>,
  options: UseApiOptions = {}
): UseApiReturn<T> => {
  const { immediate = true } = options;
  
  const [data, setData] = useState<T | null>(null);
  const [loading, setLoading] = useState<boolean>(false);
  const [error, setError] = useState<string | null>(null);

  const fetchData = useCallback(async () => {
    try {
      setLoading(true);
      setError(null);
      const result = await apiCall();
      setData(result);
    } catch (err) {
      setError(err instanceof Error ? err.message : 'An error occurred');
    } finally {
      setLoading(false);
    }
  }, [apiCall]);

  useEffect(() => {
    if (immediate) {
      fetchData();
    }
  }, [fetchData, immediate]);

  return {
    data,
    loading,
    error,
    refetch: fetchData
  };
};
```


### React Component Organization

| Component Type | Location | Naming Convention | Example |
| :-- | :-- | :-- | :-- |
| Feature Components | `features/[feature]/components/` | PascalCase | `UserProfile.tsx` |
| Shared UI Components | `shared/components/ui/` | PascalCase | `Button.tsx` |
| Layout Components | `shared/components/layout/` | PascalCase | `Header.tsx` |
| Page Components | `features/[feature]/pages/` | PascalCase + "Page" | `UserListPage.tsx` |
| Hook Files | `hooks/` or `features/[feature]/hooks/` | camelCase + "use" prefix | `useAuth.ts` |


***

## Vite Configuration \& Optimization

### Essential Vite Configuration

```typescript
// vite.config.ts
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import { resolve } from 'path';
import { loadEnv } from 'vite';

export default defineConfig(({ command, mode }) => {
  // Load environment variables
  const env = loadEnv(mode, process.cwd(), '');
  
  return {
    plugins: [
      react({
        // Enable React Fast Refresh
        fastRefresh: true,
        // JSX runtime configuration
        jsxRuntime: 'automatic'
      })
    ],
    
    // Path resolution
    resolve: {
      alias: {
        '@': resolve(__dirname, 'src'),
        '@/components': resolve(__dirname, 'src/shared/components'),
        '@/hooks': resolve(__dirname, 'src/shared/hooks'),
        '@/utils': resolve(__dirname, 'src/shared/utils'),
        '@/types': resolve(__dirname, 'src/shared/types'),
        '@/assets': resolve(__dirname, 'src/assets')
      }
    },

    // Development server configuration
    server: {
      port: 3000,
      open: true,
      proxy: {
        '/api': {
          target: env.VITE_API_URL || 'http://localhost:8000',
          changeOrigin: true,
          secure: false
        }
      }
    },

    // Build optimizations
    build: {
      outDir: 'dist',
      sourcemap: mode !== 'production',
      minify: 'terser',
      terserOptions: {
        compress: {
          drop_console: mode === 'production'
        }
      },
      rollupOptions: {
        output: {
          manualChunks: {
            vendor: ['react', 'react-dom'],
            router: ['react-router-dom'],
            ui: ['@radix-ui/react-dialog', '@radix-ui/react-dropdown-menu']
          }
        }
      },
      chunkSizeWarningLimit: 1000
    },

    // Environment variables prefix
    envPrefix: 'VITE_',

    // CSS configuration
    css: {
      modules: {
        localsConvention: 'camelCase'
      },
      preprocessorOptions: {
        scss: {
          additionalData: `@import "@/styles/variables.scss";`
        }
      }
    },

    // Testing configuration (Vitest)
    test: {
      environment: 'jsdom',
      setupFiles: ['./src/__tests__/setup.ts'],
      globals: true,
      css: true
    }
  };
});
```


### TypeScript Configuration for Vite

```json
// tsconfig.json
{
  "compilerOptions": {
    "target": "ES2020",
    "lib": ["ES2020", "DOM", "DOM.Iterable"],
    "module": "ESNext",
    "skipLibCheck": true,
    
    // Bundler mode
    "moduleResolution": "bundler",
    "allowImportingTsExtensions": true,
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "react-jsx",
    
    // Linting
    "strict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noFallthroughCasesInSwitch": true,
    
    // Path mapping (matches Vite aliases)
    "baseUrl": ".",
    "paths": {
      "@/*": ["src/*"],
      "@/components/*": ["src/shared/components/*"],
      "@/hooks/*": ["src/shared/hooks/*"],
      "@/utils/*": ["src/shared/utils/*"],
      "@/types/*": ["src/shared/types/*"],
      "@/assets/*": ["src/assets/*"]
    }
  },
  "include": ["src/**/*", "src/**/*.tsx", "vite-env.d.ts"],
  "exclude": ["node_modules", "dist"]
}
```


***

## Shared Component Libraries

### Component Library Structure[^8][^7]

```typescript
// packages/ui-components/src/components/Button/Button.tsx
import React from 'react';
import styles from './Button.module.css';

export interface ButtonProps 
  extends React.ButtonHTMLAttributes<HTMLButtonElement> {
  variant?: 'primary' | 'secondary' | 'destructive' | 'outline' | 'ghost';
  size?: 'sm' | 'md' | 'lg';
  loading?: boolean;
  icon?: React.ReactNode;
}

export const Button = React.forwardRef<HTMLButtonElement, ButtonProps>(
  ({ 
    className, 
    variant = 'primary', 
    size = 'md', 
    loading, 
    icon, 
    children, 
    disabled, 
    ...props 
  }, ref) => {
    const classes = [
      styles.button,
      styles[variant],
      styles[size],
      className
    ].filter(Boolean).join(' ');

    return (
      <button
        ref={ref}
        className={classes}
        disabled={disabled || loading}
        {...props}
      >
        {loading && <span className={styles.spinner} />}
        {icon && <span className={styles.icon}>{icon}</span>}
        {children}
      </button>
    );
  }
);

Button.displayName = 'Button';
```


### Storybook Configuration[^8]

```typescript
// packages/ui-components/.storybook/main.ts
import type { StorybookConfig } from '@storybook/react-vite';

const config: StorybookConfig = {
  stories: ['../src/**/*.stories.@(js|jsx|ts|tsx|mdx)'],
  addons: [
    '@storybook/addon-essentials',
    '@storybook/addon-a11y',
    '@storybook/addon-design-tokens'
  ],
  framework: {
    name: '@storybook/react-vite',
    options: {}
  },
  viteFinal: (config) => {
    return config;
  }
};

export default config;
```


***

## State Management Patterns

### Redux Toolkit Setup

```typescript
// apps/web/src/shared/store/store.ts
import { configureStore } from '@reduxjs/toolkit';
import { authSlice } from '@/features/auth/store/authSlice';
import { userSlice } from '@/features/user-management/store/userSlice';

export const store = configureStore({
  reducer: {
    auth: authSlice.reducer,
    users: userSlice.reducer
  },
  middleware: (getDefaultMiddleware) =>
    getDefaultMiddleware({
      serializableCheck: {
        ignoredActions: ['persist/PERSIST']
      }
    }),
  devTools: process.env.NODE_ENV !== 'production'
});

export type RootState = ReturnType<typeof store.getState>;
export type AppDispatch = typeof store.dispatch;
```


### React Query Alternative

```typescript
// apps/web/src/shared/hooks/useQueryClient.ts
import { useQuery, useMutation, useQueryClient } from '@tanstack/react-query';

export const useUsers = () => {
  return useQuery({
    queryKey: ['users'],
    queryFn: () => fetch('/api/users').then(res => res.json()),
    staleTime: 5 * 60 * 1000, // 5 minutes
  });
};

export const useCreateUser = () => {
  const queryClient = useQueryClient();
  
  return useMutation({
    mutationFn: (userData: CreateUserRequest) => 
      fetch('/api/users', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(userData)
      }).then(res => res.json()),
    onSuccess: () => {
      queryClient.invalidateQueries({ queryKey: ['users'] });
    }
  });
};
```


***

## API Integration \& Data Flow

### HTTP Client Setup

```typescript
// apps/web/src/shared/services/httpClient.ts
import axios, { AxiosInstance, AxiosRequestConfig } from 'axios';

class HttpClient {
  private instance: AxiosInstance;

  constructor() {
    this.instance = axios.create({
      baseURL: import.meta.env.VITE_API_URL || 'http://localhost:8000',
      timeout: 10000,
      headers: {
        'Content-Type': 'application/json'
      }
    });

    this.setupInterceptors();
  }

  private setupInterceptors() {
    // Request interceptor - Add auth token
    this.instance.interceptors.request.use(
      (config) => {
        const token = localStorage.getItem('token');
        if (token) {
          config.headers.Authorization = `Bearer ${token}`;
        }
        return config;
      },
      (error) => Promise.reject(error)
    );

    // Response interceptor - Handle errors
    this.instance.interceptors.response.use(
      (response) => response,
      (error) => {
        if (error.response?.status === 401) {
          localStorage.removeItem('token');
          window.location.href = '/login';
        }
        return Promise.reject(error);
      }
    );
  }

  async get<T>(url: string, config?: AxiosRequestConfig): Promise<T> {
    const response = await this.instance.get(url, config);
    return response.data;
  }

  async post<T>(url: string, data?: any, config?: AxiosRequestConfig): Promise<T> {
    const response = await this.instance.post(url, data, config);
    return response.data;
  }

  async put<T>(url: string, data?: any, config?: AxiosRequestConfig): Promise<T> {
    const response = await this.instance.put(url, data, config);
    return response.data;
  }

  async delete<T>(url: string, config?: AxiosRequestConfig): Promise<T> {
    const response = await this.instance.delete(url, config);
    return response.data;
  }
}

export const httpClient = new HttpClient();
```


***

## Full-Stack Development Tooling

### Package.json Scripts (Root)

```json
{
  "name": "fullstack-app",
  "private": true,
  "workspaces": [
    "apps/*",
    "packages/*"
  ],
  "scripts": {
    "dev": "concurrently \"npm run dev:api\" \"npm run dev:web\"",
    "dev:api": "npm run dev --workspace=apps/api",
    "dev:web": "npm run dev --workspace=apps/web",
    "build": "npm run build --workspaces",
    "test": "npm run test --workspaces",
    "test:e2e": "playwright test",
    "lint": "npm run lint --workspaces",
    "lint:fix": "npm run lint:fix --workspaces",
    "type-check": "npm run type-check --workspaces",
    "storybook": "npm run storybook --workspace=packages/ui-components",
    "clean": "npm run clean --workspaces && rm -rf node_modules"
  },
  "devDependencies": {
    "concurrently": "^8.2.2",
    "@playwright/test": "^1.40.0",
    "husky": "^8.0.3",
    "lint-staged": "^15.2.0"
  }
}
```


***

## Testing Strategy (Full-Stack)

### Frontend Testing Setup[^13]

```typescript
// apps/web/src/__tests__/setup.ts
import '@testing-library/jest-dom';
import { expect, afterEach, vi } from 'vitest';
import { cleanup } from '@testing-library/react';
import * as matchers from '@testing-library/jest-dom/matchers';

expect.extend(matchers);

// Cleanup after each test
afterEach(() => {
  cleanup();
});

// Mock fetch
global.fetch = vi.fn();

// Mock localStorage
const localStorageMock = {
  getItem: vi.fn(),
  setItem: vi.fn(),
  removeItem: vi.fn(),
  clear: vi.fn(),
};
vi.stubGlobal('localStorage', localStorageMock);
```


### Component Testing Example

```typescript
// apps/web/src/shared/components/ui/Button/Button.test.tsx
import { render, screen, fireEvent } from '@testing-library/react';
import { Button } from './Button';

describe('Button', () => {
  it('renders correctly', () => {
    render(<Button>Click me</Button>);
    expect(screen.getByRole('button', { name: /click me/i })).toBeInTheDocument();
  });

  it('calls onClick when clicked', () => {
    const handleClick = vi.fn();
    render(<Button onClick={handleClick}>Click me</Button>);
    
    fireEvent.click(screen.getByRole('button'));
    expect(handleClick).toHaveBeenCalledTimes(1);
  });

  it('shows loading state', () => {
    render(<Button loading>Loading</Button>);
    expect(screen.getByRole('button')).toBeDisabled();
  });

  it('applies correct variant classes', () => {
    render(<Button variant="secondary">Secondary</Button>);
    expect(screen.getByRole('button')).toHaveClass('secondary');
  });
});
```


***

## Build \& Deployment Pipeline

### Docker Configuration

```dockerfile
# apps/web/Dockerfile
FROM node:18-alpine as build

WORKDIR /app

# Copy package files
COPY package*.json ./
COPY apps/web/package*.json ./apps/web/
COPY packages/*/package*.json ./packages/

# Install dependencies
RUN npm ci --only=production

# Copy source code
COPY apps/web ./apps/web
COPY packages ./packages

# Build the application
WORKDIR /app/apps/web
RUN npm run build

# Production image
FROM nginx:alpine

# Copy built assets
COPY --from=build /app/apps/web/dist /usr/share/nginx/html

# Copy nginx configuration
COPY apps/web/nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
```


***

## Performance Optimization (Full-Stack)

### React Performance Patterns

```tsx
// Lazy loading components
import { lazy, Suspense } from 'react';

const UserManagementPage = lazy(() => 
  import('../features/user-management/pages/UserManagementPage')
);

const AppRoutes = () => (
  <Routes>
    <Route 
      path="/users" 
      element={
        <Suspense fallback={<div>Loading...</div>}>
          <UserManagementPage />
        </Suspense>
      } 
    />
  </Routes>
);

// Memoization for expensive components
import { memo, useMemo } from 'react';

interface UserListProps {
  users: User[];
  searchTerm: string;
}

export const UserList = memo<UserListProps>(({ users, searchTerm }) => {
  const filteredUsers = useMemo(() => 
    users.filter(user => 
      user.name.toLowerCase().includes(searchTerm.toLowerCase())
    ),
    [users, searchTerm]
  );

  return (
    <div>
      {filteredUsers.map(user => (
        <UserCard key={user.id} user={user} />
      ))}
    </div>
  );
});
```


### Vite Bundle Analysis

```typescript
// vite.config.ts - Bundle analysis
import { defineConfig } from 'vite';
import { visualizer } from 'rollup-plugin-visualizer';

export default defineConfig({
  plugins: [
    // ... other plugins
    visualizer({
      filename: 'dist/stats.html',
      open: true
    })
  ],
  build: {
    rollupOptions: {
      output: {
        manualChunks: {
          // Separate vendor chunks
          'react-vendor': ['react', 'react-dom'],
          'router-vendor': ['react-router-dom'],
          // Feature-based chunks
          'auth-feature': ['./src/features/auth'],
          'user-feature': ['./src/features/user-management']
        }
      }
    }
  }
});
```


***

## Summary

This enhanced full-stack coding style guide provides a comprehensive foundation for building modern, scalable Node.js applications with React frontends. The combination of:

- **Vertical Slice Architecture** on the backend
- **Feature-based organization** on the frontend[^6][^5]
- **Monorepo structure** for code sharing[^3][^4][^2]
- **TypeScript** throughout the stack[^12][^11]
- **Vite** for optimal development experience[^14][^15][^16]

Creates a robust development environment that scales with team size and application complexity.

### Key Takeaways[^17][^10][^9]

1. **Consistency Across Stack**: Use TypeScript and consistent patterns in both frontend and backend
2. **Feature-First Organization**: Structure both React and Node.js code around business features
3. **Shared Code**: Leverage monorepo benefits for shared types, components, and utilities[^7][^8]
4. **Developer Experience**: Vite + TypeScript + Hot reload = fast development cycles
5. **Production Ready**: Include testing, linting, building, and deployment considerations from day one

Remember to adapt these guidelines to your specific project needs while maintaining the core principles of maintainability, scalability, and developer productivity.

<div style="text-align: center">⁂</div>

[^1]: https://dev.to/shubhadip_bhowmik/best-folder-structure-for-react-complex-projects-432p

[^2]: https://www.dhiwise.com/post/best-practices-for-structuring-your-react-monorepo

[^3]: https://mayallo.com/nx-monorepo-nodejs-react/

[^4]: https://dev.to/hardikidea/master-full-stack-monorepos-a-step-by-step-guide-2196

[^5]: https://www.robinwieruch.de/react-folder-structure/

[^6]: https://www.thatsoftwaredude.com/content/14110/creating-a-good-folder-structure-for-your-vite-app

[^7]: https://dev.to/ricardo_maia_eb9c7a906560/sharing-components-micro-frontends-2p61

[^8]: https://dzone.com/articles/component-library-with-lerna-monorepo-vite-and-sto

[^9]: https://www.linkedin.com/pulse/best-practices-combining-reactjs-nodejs-modern-web-applications-4yswf

[^10]: https://dev.to/shanu001x/how-to-setup-full-stack-project-for-production-in-nodejs-environment-2d7l

[^11]: https://react-typescript-style-guide.com

[^12]: https://mkosir.github.io/typescript-style-guide/

[^13]: https://dev.to/janoskocs/setting-up-a-react-project-using-vite-typescript-vitest-2gl2

[^14]: https://www.robinwieruch.de/vite-typescript/

[^15]: https://javascript.plainenglish.io/setting-up-a-react-typescript-project-with-vite-eslint-prettier-and-husky-ef7c9dada761

[^16]: https://vite.dev/config/

[^17]: https://jurnal.itscience.org/index.php/brilliance/article/view/5971

[^18]: https://www.cambridge.org/core/product/identifier/S2059866123005666/type/journal_article

[^19]: https://fepbl.com/index.php/ijmer/article/view/936

[^20]: http://www.tandfonline.com/doi/abs/10.1080/09544120100000011

[^21]: https://www.frontiersin.org/articles/10.3389/frsle.2023.1329405/full

[^22]: https://www.mdpi.com/2071-1050/14/21/13949

[^23]: https://pubs.acs.org/doi/10.1021/acs.jcim.2c01522

[^24]: https://www.cambridge.org/core/product/identifier/S2732527X22002292/type/journal_article

[^25]: https://ieeexplore.ieee.org/document/9927790/

[^26]: https://tobaccocontrol.bmj.com/lookup/doi/10.1136/tobaccocontrol-2021-056825

[^27]: https://arxiv.org/html/2504.03884v1

[^28]: https://www.mdpi.com/2079-9292/12/15/3291/pdf?version=1690792565

[^29]: https://arxiv.org/html/2503.07358v1

[^30]: https://arxiv.org/pdf/2307.12489.pdf

[^31]: http://arxiv.org/pdf/2410.12114.pdf

[^32]: https://dx.plos.org/10.1371/journal.pcbi.1009809

[^33]: http://thesai.org/Downloads/Volume6No11/Paper_20-Proactive_Software_Engineering_Approach_to_Ensure_Rapid_Software_Development.pdf

[^34]: https://arxiv.org/html/2406.16386v1

[^35]: https://arxiv.org/pdf/2107.10164.pdf

[^36]: http://arxiv.org/pdf/2308.02843.pdf

[^37]: https://google.github.io/styleguide/tsguide.html

[^38]: https://blog.stackademic.com/crafting-the-perfect-react-project-a-comprehensive-guide-to-directory-structure-and-essential-9bb0e32ba7aa

[^39]: https://www.reddit.com/r/reactjs/comments/wsiogb/how_do_you_create_monorepo_for_fullstack/

[^40]: https://react.dev/learn/typescript

[^41]: https://www.youtube.com/watch?v=Mm6_DlO5vvs

[^42]: https://blog.stackademic.com/building-a-full-stack-todo-app-with-node-js-react-and-react-native-in-a-monorepo-f298ee004097

[^43]: https://ts.dev/style/

[^44]: https://www.reddit.com/r/reactjs/comments/153vjsf/react_folder_structure_best_practice_s/

[^45]: https://www.youtube.com/watch?v=ACDGXHR_YmI

[^46]: https://www.sitepoint.com/react-with-typescript-best-practices/

[^47]: https://devchallenges.io/learn/4-frontend-libraries/setting-up-react

[^48]: https://blog.nrwl.io/building-full-stack-react-applications-in-a-monorepo-7dfa1714b988

[^49]: https://www.mdpi.com/1424-8220/24/7/2165

[^50]: https://ijsrem.com/download/vidyasetu-smart-solutions-for-rural-education/

[^51]: https://ojs.iscram.org/index.php/Proceedings/article/view/189

[^52]: https://ijsrem.com/download/application-to-enhance-educational-infrastructure-and-connectivity-in-rural-areas/

[^53]: https://heraldts.khmnu.edu.ua/index.php/heraldts/article/view/1608

[^54]: https://ieeexplore.ieee.org/document/10297434/

[^55]: https://www.semanticscholar.org/paper/4a5bb1b4faf3425206008f426e2714bd87f9c87a

[^56]: https://vottp.khmnu.edu.ua/index.php/vottp/article/view/425

[^57]: https://jacow.org/ipac2021/doi/JACoW-IPAC2021-THPAB259.html

[^58]: https://arxiv.org/pdf/2108.08027.pdf

[^59]: https://arxiv.org/pdf/2101.04622.pdf

[^60]: https://arxiv.org/pdf/2403.14940.pdf

[^61]: https://arxiv.org/pdf/2408.11954.pdf

[^62]: https://arxiv.org/pdf/2205.06349v1.pdf

[^63]: https://arxiv.org/pdf/2302.12163.pdf

[^64]: https://drops.dagstuhl.de/opus/volltexte/2015/5218/pdf/8.pdf

[^65]: http://arxiv.org/pdf/2410.10779.pdf

[^66]: https://arxiv.org/pdf/2210.03629.pdf

[^67]: https://arxiv.org/pdf/2501.18225.pdf

[^68]: https://ph.pollub.pl/index.php/jcsi/article/view/6248

[^69]: https://jibin.tech/blog/monorepo-with-create-react-app/

[^70]: https://www.reddit.com/r/learnjavascript/comments/1ch1tb5/starting_my_first_fullstack_project_with_js_react/

[^71]: https://dev.to/mbarzeev/adding-a-react-components-package-to-a-monorepo-3ol5

[^72]: https://www.einfochips.com/blog/building-a-full-stack-application-with-react-js-and-node-js/

[^73]: https://blog.logrocket.com/how-to-build-react-typescript-app-vite/

[^74]: https://stackoverflow.com/questions/73854158/should-we-bundle-shared-component-library-separately-in-lerna-monorepo

[^75]: https://www.cisin.com/coffee-break/using-react-js-and-node-js-for-full-stack-web-development.html

[^76]: https://www.youtube.com/watch?v=RbZyQWOEmD0

[^77]: https://github.com/shadcn-ui/ui/discussions/6570

[^78]: https://www.fullstack.com/labs/resources/blog/best-practices-for-scalable-secure-react-node-js-apps-in-2025

[^79]: https://adictosaltrabajo.com/2024/06/12/setup-inicial-react-vite-typescript-herramientas/

[^80]: https://www.reddit.com/r/Frontend/comments/1bj0mxr/building_a_shared_component_library_skinning_on/