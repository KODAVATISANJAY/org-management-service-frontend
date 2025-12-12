# Frontend Setup Guide - Complete Step-by-Step Instructions

## Overview
This guide will help you set up the Organization Management Service Frontend locally on your Windows machine.

## Prerequisites

Before starting, ensure you have:
1. **Node.js 16+** - Download from https://nodejs.org/ (LTS version recommended)
2. **npm or yarn** - Comes with Node.js
3. **Git** - Download from https://git-scm.com/
4. **VS Code** - Download from https://code.visualstudio.com/ (optional but recommended)
5. **Backend API running** - Must have the backend service running locally or deployed

### Check Installations
Open Command Prompt/PowerShell and run:
```bash
node --version
npm --version
git --version
```

## Step 1: Clone the Repository

1. Open Command Prompt or PowerShell
2. Navigate to where you want to store the project:
```bash
cd D:\Projects
# or your preferred location
```

3. Clone the repository:
```bash
git clone https://github.com/KODAVATISANJAY/org-management-service-frontend.git
cd org-management-service-frontend
```

## Step 2: Install Dependencies

Install all required npm packages:
```bash
npm install
```

This will install:
- React 18+
- React Router v6
- TypeScript
- Vite
- Tailwind CSS
- Framer Motion
- Axios
- And other dependencies

**Installation time:** ~2-5 minutes depending on internet speed

## Step 3: Configure Environment Variables

1. In the root project directory, create a file named `.env.local`

2. Add the following content:
```env
VITE_API_BASE_URL=http://localhost:8000
VITE_JWT_EXPIRY=3600000
VITE_APP_NAME=Org Management Service
```

**Note:** 
- If backend is deployed elsewhere, update `VITE_API_BASE_URL` accordingly
- `VITE_JWT_EXPIRY` is in milliseconds (3600000 = 1 hour)

## Step 4: Start Development Server

Run the development server:
```bash
npm run dev
```

You should see output like:
```
  VITE v4.x.x  build 0.00s
  ✓ ready in xxxx ms
  
  ➣  Local:   http://localhost:5173/
  ➣  Press q to quit
```

Open your browser and go to: **http://localhost:5173**

## Step 5: Verify Backend Connection

Before testing login:
1. Make sure your backend API is running at `http://localhost:8000`
2. Test backend with: `http://localhost:8000/docs` (Swagger documentation)

## Frontend Project Structure (After Initialization)

The project will be organized as:

```
org-management-service-frontend/
├── src/
│   ├── components/
│   │   ├── Auth/
│   │   ├── Organization/
│   │   └── Common/
│   ├── pages/
│   ├── services/
│   ├── types/
│   ├── context/
│   ├── hooks/
│   ├── styles/
│   ├── App.tsx
│   └── main.tsx
├── public/
├── .env.local
├── package.json
├── vite.config.ts
├── tsconfig.json
├── tailwind.config.js
├── postcss.config.js
└── README.md
```

## Key Files to Create (After npm install)

### 1. `src/types/index.ts` - TypeScript Interfaces
```typescript
export interface LoginRequest {
  email: string;
  password: string;
}

export interface LoginResponse {
  access_token: string;
  token_type: string;
}

export interface Organization {
  organization_name: string;
  collection_name: string;
  admin_email: string;
}

export interface CreateOrgRequest {
  organization_name: string;
  email: string;
  password: string;
}
```

### 2. `src/services/api.ts` - Axios Configuration
```typescript
import axios from 'axios';

const API_BASE_URL = import.meta.env.VITE_API_BASE_URL || 'http://localhost:8000';

const api = axios.create({
  baseURL: API_BASE_URL,
  headers: {
    'Content-Type': 'application/json',
  },
});

// Request interceptor - add JWT token
api.interceptors.request.use((config) => {
  const token = localStorage.getItem('token');
  if (token) {
    config.headers.Authorization = `Bearer ${token}`;
  }
  return config;
});

// Response interceptor - handle errors
api.interceptors.response.use(
  (response) => response,
  (error) => {
    if (error.response?.status === 401) {
      localStorage.removeItem('token');
      window.location.href = '/login';
    }
    return Promise.reject(error);
  }
);

export default api;
```

### 3. `src/context/AuthContext.tsx` - Authentication Context
```typescript
import React, { createContext, useState, ReactNode } from 'react';

export interface AuthContextType {
  isAuthenticated: boolean;
  token: string | null;
  login: (token: string) => void;
  logout: () => void;
}

export const AuthContext = createContext<AuthContextType | undefined>(undefined);

export const AuthProvider: React.FC<{ children: ReactNode }> = ({ children }) => {
  const [token, setToken] = useState<string | null>(() =>
    localStorage.getItem('token')
  );

  const login = (newToken: string) => {
    setToken(newToken);
    localStorage.setItem('token', newToken);
  };

  const logout = () => {
    setToken(null);
    localStorage.removeItem('token');
  };

  return (
    <AuthContext.Provider
      value={{
        isAuthenticated: !!token,
        token,
        login,
        logout,
      }}
    >
      {children}
    </AuthContext.Provider>
  );
};
```

### 4. `src/hooks/useAuth.ts` - Custom Hook
```typescript
import { useContext } from 'react';
import { AuthContext, AuthContextType } from '../context/AuthContext';

export const useAuth = (): AuthContextType => {
  const context = useContext(AuthContext);
  if (!context) {
    throw new Error('useAuth must be used within AuthProvider');
  }
  return context;
};
```

## Development Commands

### Start Development Server
```bash
npm run dev
```
Server runs at http://localhost:5173

### Build for Production
```bash
npm run build
```
Creates optimized production build in `dist/` folder

### Preview Production Build
```bash
npm run preview
```
Preview the production build locally

### Type Check
```bash
npm run type-check
```
Check for TypeScript errors

### Format Code (if configured)
```bash
npm run format
```

## Testing the Application

### 1. Test Login
- Go to http://localhost:5173/login
- Use credentials from a created organization
- Example: 
  - Email: `admin@srm.com`
  - Password: `StrongPass123`

### 2. Test Organization Creation
- Click "Create Organization" or "Register"
- Fill in form:
  - Organization Name: `Test Org`
  - Admin Email: `admin@test.com`
  - Password: `TestPass123!`
- Submit form

### 3. Test Organization List
- After login, view organization list on dashboard
- Test search and filter
- Try edit and delete functions

## Common Issues and Solutions

### Issue: Port 5173 already in use
**Solution:**
```bash
# Kill process on port 5173
npx kill-port 5173
# or specify different port
npm run dev -- --port 3000
```

### Issue: CORS Error from Backend
**Solution:**
- Ensure backend is running
- Check `VITE_API_BASE_URL` in `.env.local`
- Backend must have CORS enabled

### Issue: JWT Token not persisting
**Solution:**
- Clear localStorage: `localStorage.clear()` in browser console
- Check browser's Privacy/Incognito mode
- Verify token is saved: `localStorage.getItem('token')`

### Issue: Components not found or errors
**Solution:**
```bash
# Clear node_modules and reinstall
rm -r node_modules
npm install
```

### Issue: TypeScript errors
**Solution:**
- Check `tsconfig.json` configuration
- Ensure all types are properly defined
- Run `npm run type-check`

## Frontend Pages to Implement

### 1. **HomePage.tsx**
- Welcome screen
- Navigation buttons (Login, Register)
- Feature showcase

### 2. **LoginPage.tsx**
- Email input
- Password input
- Login button
- Error messages
- Loading state

### 3. **RegisterPage.tsx** (Create Organization)
- Organization name input
- Admin email input
- Password input with strength indicator
- Confirm password input
- Submit button

### 4. **DashboardPage.tsx**
- Organization list
- Search/filter functionality
- Edit/Delete/View buttons
- Create new organization button

### 5. **EditOrgPage.tsx**
- Pre-filled form with organization data
- Update fields
- Save/Cancel buttons
- Error handling

## Styling with Tailwind CSS

### Common Tailwind Classes Used
```
Container: max-w-6xl mx-auto px-4
Buttons: px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-600
Cards: bg-white p-6 rounded-lg shadow
Forms: w-full px-3 py-2 border border-gray-300 rounded
Text: text-gray-700 text-sm
```

### Color Palette
- Primary Blue: `bg-blue-500 text-blue-500`
- Success Green: `bg-green-500 text-green-500`
- Danger Red: `bg-red-500 text-red-500`
- Neutral Gray: `bg-gray-100 text-gray-700`

## API Integration Checklist

- [ ] Setup axios instance with base URL
- [ ] Configure JWT token interceptor
- [ ] Create TypeScript interfaces for API responses
- [ ] Implement login endpoint
- [ ] Implement create organization endpoint
- [ ] Implement get organizations endpoint
- [ ] Implement update organization endpoint
- [ ] Implement delete organization endpoint
- [ ] Add error handling for all requests
- [ ] Test all API calls

## Performance Optimization

1. **Code Splitting**: React Router handles automatic code splitting
2. **Lazy Loading**: Implement lazy loading for heavy components
3. **Image Optimization**: Optimize images before using
4. **CSS Purging**: Tailwind automatically removes unused CSS
5. **Production Build**: Use `npm run build` for optimized bundle

## Next Steps

1. ✅ Clone repository
2. ✅ Install dependencies
3. ✅ Configure environment variables
4. ✅ Start development server
5. Create components (Auth, Organization, Common)
6. Implement API integration
7. Add form validation
8. Test all features
9. Deploy to Vercel

## Deployment to Vercel

1. Push code to GitHub
2. Go to https://vercel.com
3. Click "New Project"
4. Select GitHub repository
5. Set environment variables:
   - `VITE_API_BASE_URL` = Your backend URL
6. Click "Deploy"
7. Your frontend is live!

## Useful Resources

- [React Documentation](https://react.dev)
- [Vite Documentation](https://vitejs.dev)
- [Tailwind CSS](https://tailwindcss.com)
- [Framer Motion](https://www.framer.com/motion)
- [TypeScript](https://www.typescriptlang.org)
- [Axios](https://axios-http.com)
- [Vercel Deployment](https://vercel.com/docs)

## Support

If you encounter any issues:
1. Check the main README.md
2. Review error messages carefully
3. Check console (F12) for detailed errors
4. Test backend API separately
5. Open an issue on GitHub

---

**Last Updated:** December 2025
**Frontend Status:** Ready for Development ✅
