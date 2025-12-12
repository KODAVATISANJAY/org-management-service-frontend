# Quick Start Guide - 5 Minutes Setup

## Get Running Instantly

### 1. Clone (1 min)
```bash
git clone https://github.com/KODAVATISANJAY/org-management-service-frontend.git
cd org-management-service-frontend
```

### 2. Install (2-3 min)
```bash
npm install
```

### 3. Configure (1 min)
Create `.env.local`:
```env
VITE_API_BASE_URL=http://localhost:8000
VITE_JWT_EXPIRY=3600000
```

### 4. Run (instant)
```bash
npm run dev
```

Open: http://localhost:5173

---

## What's Included

✅ Repository created - `org-management-service-frontend`
✅ README.md - Full documentation
✅ SETUP_GUIDE.md - Detailed instructions
✅ This Quick Start guide
✅ .gitignore - Node.js config
✅ Ready for component development

---

## Next: Create Core Files

After `npm install`, create 8 key files:

1. `src/types/index.ts` - TypeScript interfaces
2. `src/services/api.ts` - Axios setup with JWT
3. `src/context/AuthContext.tsx` - Auth state
4. `src/hooks/useAuth.ts` - Auth hook
5. `src/components/Common/LoadingSpinner.tsx` - Spinner
6. `src/components/Common/ErrorAlert.tsx` - Errors
7. `src/components/Auth/Login.tsx` - Login form
8. `src/App.tsx` - Main app with router

All code examples available in SETUP_GUIDE.md

---

## Key Commands

```bash
npm run dev         # Development
npm run build       # Production build
npm run preview     # Preview build
npm run type-check  # TypeScript check
```

---

## Pages to Build

- HomePage (landing)
- LoginPage (admin login)
- RegisterPage (create org)
- DashboardPage (list orgs)
- EditOrgPage (update org)
- DetailPage (org details)
- NotFoundPage (404)

---

## Backend API Endpoints

```
POST   /admin/login      - Login
POST   /org/create       - Create
GET    /org/get          - Get
PUT    /org/update       - Update  
DELETE /org/delete       - Delete
```

---

## Troubleshooting

**Port in use?**
```bash
npm run dev -- --port 3000
```

**Node modules issue?**
```bash
rm -r node_modules package-lock.json
npm install
```

---

## Deploy to Vercel

1. Push to GitHub
2. vercel.com → New Project
3. Select repo
4. Set VITE_API_BASE_URL
5. Deploy!

---

## Full Docs

- README.md - Complete reference
- SETUP_GUIDE.md - Detailed instructions
- Backend: https://github.com/KODAVATISANJAY/org-management-service-backend

**Ready to code! Happy development! 🚀**
