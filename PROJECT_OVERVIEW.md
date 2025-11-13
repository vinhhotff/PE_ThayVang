# Book Collection Manager - Project Overview

## 🎯 Project Goal

Create a full-stack web application for managing a personal book collection with CRUD operations, search, filter, and sort capabilities.

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────┐
│                     User Browser                         │
└────────────────────┬────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────┐
│              Next.js Frontend (Vercel)                   │
│  - React Components (TypeScript)                         │
│  - Tailwind CSS Styling                                  │
│  - Client-side State Management                          │
└────────────────────┬────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────┐
│           Supabase Backend (PostgreSQL)                  │
│  - Books Table                                           │
│  - Row Level Security                                    │
│  - REST API (auto-generated)                             │
└─────────────────────────────────────────────────────────┘
```

## 📁 Project Structure

```
book-collection/
│
├── app/                          # Next.js App Router
│   ├── page.tsx                  # Home page (book list)
│   ├── layout.tsx                # Root layout
│   ├── globals.css               # Global styles
│   ├── create/
│   │   └── page.tsx              # Create book page
│   └── edit/
│       └── [id]/
│           └── page.tsx          # Edit book page (dynamic route)
│
├── lib/
│   └── supabase.ts               # Supabase client & TypeScript types
│
├── Configuration Files
│   ├── package.json              # Dependencies
│   ├── tsconfig.json             # TypeScript config
│   ├── tailwind.config.ts        # Tailwind CSS config
│   ├── next.config.js            # Next.js config
│   ├── postcss.config.mjs        # PostCSS config
│   └── .eslintrc.json            # ESLint config
│
├── Environment
│   ├── .env.local.example        # Environment template
│   └── .gitignore                # Git ignore rules
│
└── Documentation
    ├── README.md                 # Main documentation
    ├── QUICKSTART.md             # Quick start guide
    ├── SETUP.md                  # Database setup
    ├── DEPLOYMENT.md             # Deployment guide
    ├── SUBMISSION.md             # Submission checklist
    └── PROJECT_OVERVIEW.md       # This file
```

## 🔧 Technology Stack

### Frontend
- **Next.js 15**: React framework with App Router
- **React 18**: UI library
- **TypeScript**: Type-safe JavaScript
- **Tailwind CSS**: Utility-first CSS framework

### Backend
- **Supabase**: Backend-as-a-Service
  - PostgreSQL database
  - Auto-generated REST API
  - Row Level Security (RLS)

### Deployment
- **Vercel**: Frontend hosting (free tier)
- **Supabase**: Database hosting (free tier)

## 📊 Database Schema

```sql
Table: books
┌──────────────┬──────────────┬──────────────┬──────────┐
│ Column       │ Type         │ Constraints  │ Notes    │
├──────────────┼──────────────┼──────────────┼──────────┤
│ id           │ UUID         │ PRIMARY KEY  │ Auto-gen │
│ title        │ TEXT         │ NOT NULL     │ Required │
│ author       │ TEXT         │ NOT NULL     │ Required │
│ tags         │ TEXT[]       │ NULL         │ Optional │
│ cover_image  │ TEXT         │ NULL         │ Optional │
│ created_at   │ TIMESTAMP    │ DEFAULT NOW  │ Auto-gen │
└──────────────┴──────────────┴──────────────┴──────────┘
```

## 🎨 Features Implementation

### 1. Book List Page (/)
- **Display**: Grid layout showing all books
- **Search**: Real-time search by title
- **Filter**: Dropdown to filter by tag
- **Sort**: Toggle between A-Z and Z-A
- **Actions**: Edit and Delete buttons on each card

### 2. Create Book Page (/create)
- **Form Fields**:
  - Title (required, text input)
  - Author (required, text input)
  - Tags (optional, comma-separated)
  - Cover Image (optional, URL input)
- **Validation**: Client-side required field validation
- **Navigation**: Back button and Cancel button

### 3. Edit Book Page (/edit/[id])
- **Dynamic Route**: Uses book ID from URL
- **Pre-filled Form**: Loads existing book data
- **Same Fields**: As create page
- **Actions**: Save Changes or Cancel

### 4. Delete Functionality
- **Confirmation**: Browser confirm dialog
- **Immediate Update**: Refreshes list after deletion

## 🔄 Data Flow

### Reading Books
```
User → Page Load → Supabase Query → Display Books
```

### Creating Book
```
User → Fill Form → Submit → Supabase Insert → Redirect to List
```

### Updating Book
```
User → Click Edit → Load Data → Modify → Save → Supabase Update → Redirect
```

### Deleting Book
```
User → Click Delete → Confirm → Supabase Delete → Refresh List
```

## 🚀 Getting Started

1. **Install**: `npm install`
2. **Configure**: Create `.env.local` with Supabase credentials
3. **Run**: `npm run dev`
4. **Deploy**: Push to GitHub → Connect Vercel → Deploy

## 📝 Key Files Explained

### `lib/supabase.ts`
- Creates Supabase client
- Exports TypeScript type for Book
- Used by all pages to interact with database

### `app/page.tsx`
- Main book list page
- Implements search, filter, sort
- Handles delete with confirmation

### `app/create/page.tsx`
- Form to add new books
- Client-side validation
- Redirects after successful creation

### `app/edit/[id]/page.tsx`
- Dynamic route for editing
- Fetches book data on load
- Updates existing record

## 🎓 Learning Outcomes

By completing this project, you will learn:
- Next.js App Router and file-based routing
- React hooks (useState, useEffect)
- TypeScript for type safety
- Tailwind CSS for styling
- Supabase for backend services
- Environment variables management
- Deployment to Vercel
- Git and GitHub workflow

## 📚 Resources

- [Next.js Documentation](https://nextjs.org/docs)
- [Supabase Documentation](https://supabase.com/docs)
- [Tailwind CSS Documentation](https://tailwindcss.com/docs)
- [Vercel Deployment](https://vercel.com/docs)

## ✅ Requirements Checklist

- [x] Display books with title, author, tags, cover image
- [x] Search by title
- [x] Filter by tag
- [x] Sort A-Z / Z-A
- [x] Add new book
- [x] Edit existing book
- [x] Delete with confirmation
- [x] Deployed on free hosting
- [x] Using free database
- [x] Public GitHub repository
