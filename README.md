# Organization Management Service - Frontend

A **React + TypeScript** desktop web application for managing organizations with a beautiful UI built with **Tailwind CSS** and **Framer Motion** animations. This frontend connects to a FastAPI backend with multi-tenant architecture.

## 📋 Overview

This frontend application provides a complete user interface for:
- Admin authentication and login
- Create new organizations
- View, update, and delete organizations
- JWT token-based session management
- Interactive dashboard with real-time data management

## ✨ Features

✅ **Modern React UI** - Built with latest React 18+ with TypeScript
✅ **Pixel-Perfect Design** - Tailwind CSS for responsive styling
✅ **Smooth Animations** - Framer Motion for interactive transitions
✅ **Authentication** - JWT-based admin login system
✅ **Organization CRUD** - Create, read, update, delete operations
✅ **Form Validation** - Client-side validation with error handling
✅ **Responsive Design** - Desktop-first development (optimized for desktop)
✅ **Error Handling** - Comprehensive error messages and user feedback
✅ **Loading States** - Beautiful loading indicators
✅ **Session Management** - Persistent JWT token storage

## 🛠️ Tech Stack

- **Frontend Framework**: React 18+ with TypeScript
- **Build Tool**: Vite (fast development server)
- **Styling**: Tailwind CSS
- **Animations**: Framer Motion
- **HTTP Client**: Axios
- **Routing**: React Router v6
- **State Management**: React Hooks + Context API
- **UI Components**: Custom components with Tailwind CSS

## 📁 Project Structure

```
org-management-service-frontend/
├── public/
│   └── favicon.ico
├── src/
│   ├── components/
│   │   ├── Auth/
│   │   │   ├── Login.tsx
│   │   │   ├── Register.tsx
│   │   │   └── ProtectedRoute.tsx
│   │   ├── Organization/
│   │   │   ├── OrgList.tsx
│   │   │   ├── OrgForm.tsx
│   │   │   ├── OrgDetail.tsx
│   │   │   └── OrgDelete.tsx
│   │   ├── Common/
│   │   │   ├── Navbar.tsx
│   │   │   ├── Sidebar.tsx
│   │   │   ├── LoadingSpinner.tsx
│   │   │   └── ErrorAlert.tsx
│   ├── pages/
│   │   ├── HomePage.tsx
│   │   ├── LoginPage.tsx
│   │   ├── DashboardPage.tsx
│   │   ├── CreateOrgPage.tsx
│   │   ├── EditOrgPage.tsx
│   │   └── NotFoundPage.tsx
│   ├── services/
│   │   └── api.ts (Axios API setup)
│   ├── types/
│   │   └── index.ts (TypeScript interfaces)
│   ├── context/
│   │   └── AuthContext.tsx
│   ├── hooks/
│   │   └── useAuth.ts
│   ├── styles/
│   │   └── globals.css
│   ├── App.tsx
│   └── main.tsx
├── index.html
├── package.json
├── vite.config.ts
├── tsconfig.json
├── tailwind.config.js
└── README.md
```

## 🚀 Setup and Installation

### Prerequisites
- Node.js 16+ (with npm or yarn)
- Backend API running (see backend repository)
- MongoDB set up and running

### Local Setup

**1. Clone the repository:**
```bash
git clone https://github.com/KODAVATISANJAY/org-management-service-frontend.git
cd org-management-service-frontend
```

**2. Install dependencies:**
```bash
npm install
# or
yarn install
```

**3. Create `.env.local` file:**
```env
VITE_API_BASE_URL=http://localhost:8000
VITE_JWT_EXPIRY=3600000
```

**4. Start development server:**
```bash
npm run dev
# or
yarn dev
```

Server will run at `http://localhost:5173`

## 📄 Environment Variables

Create `.env.local` file with:

```
VITE_API_BASE_URL=http://localhost:8000  # Backend API URL
VITE_JWT_EXPIRY=3600000                   # JWT token expiry in ms
VITE_APP_NAME=Org Management Service      # App name
```

## 🎨 Pages and Features

### 1. **Landing/Home Page**
- Welcome screen with app description
- Quick links to Login and Register
- Feature highlights

### 2. **Login Page**
- Admin email and password input fields
- Form validation and error messages
- Forgot password link (optional)
- Smooth animations on form submission
- JWT token storage on successful login

### 3. **Registration Page**
- Create new organization form
- Organization name input
- Admin email input
- Password strength indicator
- Confirm password field
- Form validation with real-time feedback

### 4. **Dashboard Page**
- Display list of organizations
- Search and filter functionality
- Action buttons (Edit, Delete, View)
- Create new organization button
- Loading states and error handling

### 5. **Organization Detail Page**
- View full organization details
- Admin information
- Edit and delete options
- Back to dashboard button

### 6. **Edit Organization Page**
- Pre-filled form with current data
- Update organization name
- Update admin email
- Update admin password
- Cancel and save buttons
- Loading state during submission

## 🔌 API Integration

The frontend communicates with backend APIs:

**Authentication:**
- `POST /admin/login` - Admin login

**Organization Operations:**
- `POST /org/create` - Create new organization
- `GET /org/get?organization_name=X` - Get organization details
- `PUT /org/update` - Update organization
- `DELETE /org/delete` - Delete organization

**Headers:**
- All requests include `Content-Type: application/json`
- Protected routes include `Authorization: Bearer <token>`

## 🎯 Key Components

### AuthContext.tsx
Manages authentication state:
- User login status
- JWT token storage
- User information
- Logout functionality

### api.ts
Axios instance configuration:
- Base URL setup
- Request/response interceptors
- JWT token injection
- Error handling

### ProtectedRoute.tsx
- Route protection for authenticated pages
- Redirects to login if not authenticated
- Token validation

### LoadingSpinner.tsx
- Animated loading indicator
- Used during API calls

### ErrorAlert.tsx
- Displays error messages
- Dismissible alerts

## 🎬 Animations

Using Framer Motion for:
- Page transitions
- Form interactions
- Button hover effects
- Modal animations
- List item animations
- Loading spinners

## 🧪 Development

**Build for production:**
```bash
npm run build
```

**Preview production build:**
```bash
npm run preview
```

**Type checking:**
```bash
npm run type-check
```

**Format code:**
```bash
npm run format
```

## 🚢 Deployment on Vercel

**Step 1:** Push to GitHub
```bash
git add .
git commit -m "Initial frontend setup"
git push origin main
```

**Step 2:** Deploy on Vercel
1. Go to [vercel.com](https://vercel.com)
2. Click "New Project"
3. Select GitHub repository
4. Set environment variables:
   - `VITE_API_BASE_URL` = Your backend API URL
5. Click "Deploy"

**Step 3:** Configure backend URL
- Update `VITE_API_BASE_URL` in Vercel environment variables
- It should point to your deployed backend

## 📊 Form Validation

### Login Form
- Email: Valid email format required
- Password: Minimum 6 characters

### Register (Create Org) Form
- Organization Name: 3-50 characters, alphanumeric
- Email: Valid email format
- Password: Minimum 8 characters, at least 1 uppercase, 1 number
- Confirm Password: Must match password field

### Update Organization Form
- Same validations as Create Org
- Current organization name required

## 🔐 Security

- JWT tokens stored in localStorage
- XSS protection through React's built-in escaping
- CORS handled by backend
- Sensitive data not logged to console
- Token expiry validation
- Protected routes require valid token

## 🎨 Styling Guide

### Color Scheme
- Primary: `#3B82F6` (Blue)
- Secondary: `#10B981` (Green)
- Danger: `#EF4444` (Red)
- Background: `#F9FAFB` (Light Gray)

### Responsive Breakpoints
- Mobile: `< 640px`
- Tablet: `640px - 1024px`
- Desktop: `> 1024px`
(Optimized for desktop)

## 📝 Code Style

- ESLint configuration for code quality
- Prettier for code formatting
- TypeScript strict mode enabled
- Component naming: PascalCase
- File naming: PascalCase for components, camelCase for utilities

## 🐛 Error Handling

- Network errors: Display friendly error messages
- Validation errors: Show field-specific feedback
- Authentication errors: Redirect to login
- Server errors (5xx): Generic error message with retry option
- Not found errors (404): Navigate to 404 page

## 📚 API Response Examples

### Login Response
```json
{
  "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "token_type": "bearer"
}
```

### Organization Response
```json
{
  "organization_name": "SRM",
  "collection_name": "org_srm",
  "admin_email": "admin@srm.com"
}
```

## 📱 Browser Support

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)

## 🤝 Contributing

Contributions are welcome! Please:
1. Fork the repository
2. Create a feature branch: `git checkout -b feature/AmazingFeature`
3. Commit changes: `git commit -m 'Add some AmazingFeature'`
4. Push to branch: `git push origin feature/AmazingFeature`
5. Open a Pull Request

## 📄 License

MIT License - See LICENSE file for details

## 👤 Author

**Sanjay Kodavati** (@KODAVATISANJAY)
- Email: kodavatisanjay@example.com
- GitHub: https://github.com/KODAVATISANJAY

## 🙏 Support

If you have questions or encounter issues:
1. Check the backend repository for API documentation
2. Review the component documentation
3. Open an issue in GitHub
4. Contact the author

## 🔗 Related Projects

- [Backend Repository](https://github.com/KODAVATISANJAY/org-management-service-backend)
- [API Documentation](https://github.com/KODAVATISANJAY/org-management-service-backend#api-endpoints)

---

**Last Updated:** December 2025
**Status:** In Development ✅
