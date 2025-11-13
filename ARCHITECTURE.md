# System Architecture

## 🏗️ High-Level Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                         USER                                 │
│                    (Web Browser)                             │
└────────────────────────┬────────────────────────────────────┘
                         │
                         │ HTTPS
                         ▼
┌─────────────────────────────────────────────────────────────┐
│                    VERCEL (CDN)                              │
│              Next.js Application                             │
│  ┌─────────────────────────────────────────────────────┐   │
│  │  Frontend (React + TypeScript)                       │   │
│  │  - Book List Page (/)                                │   │
│  │  - Create Book Page (/create)                        │   │
│  │  - Edit Book Page (/edit/[id])                       │   │
│  │  - Tailwind CSS Styling                              │   │
│  └─────────────────────────────────────────────────────┘   │
└────────────────────────┬────────────────────────────────────┘
                         │
                         │ REST API
                         │ (Supabase Client)
                         ▼
┌─────────────────────────────────────────────────────────────┐
│                   SUPABASE                                   │
│  ┌─────────────────────────────────────────────────────┐   │
│  │  PostgreSQL Database                                 │   │
│  │  ┌──────────────────────────────────────────────┐  │   │
│  │  │  books table                                  │  │   │
│  │  │  - id (UUID, Primary Key)                     │  │   │
│  │  │  - title (TEXT, Required)                     │  │   │
│  │  │  - author (TEXT, Required)                    │  │   │
│  │  │  - tags (TEXT[], Optional)                    │  │   │
│  │  │  - cover_image (TEXT, Optional)               │  │   │
│  │  │  - created_at (TIMESTAMP)                     │  │   │
│  │  └──────────────────────────────────────────────┘  │   │
│  │                                                      │   │
│  │  Row Level Security (RLS)                           │   │
│  │  Auto-generated REST API                            │   │
│  └─────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
```

## 📊 Data Flow Diagrams

### 1. View Books (Read)
```
User Opens App
      │
      ▼
  page.tsx
      │
      ├─ useEffect() triggers
      │
      ▼
fetchBooks()
      │
      ├─ supabase.from('books').select('*')
      │
      ▼
  Supabase
      │
      ├─ Query books table
      │
      ▼
Return books[]
      │
      ▼
setBooks(data)
      │
      ▼
Re-render UI
      │
      ▼
Display book cards
```

### 2. Create Book
```
User clicks "Add Book"
      │
      ▼
Navigate to /create
      │
      ▼
User fills form
      │
      ▼
User clicks "Create"
      │
      ▼
handleSubmit()
      │
      ├─ Validate inputs
      │
      ▼
supabase.from('books').insert()
      │
      ▼
  Supabase
      │
      ├─ Insert new row
      ├─ Generate UUID
      ├─ Set created_at
      │
      ▼
Return success
      │
      ▼
router.push('/')
      │
      ▼
Redirect to home
      │
      ▼
Fetch updated list
```

### 3. Edit Book
```
User clicks "Edit"
      │
      ▼
Navigate to /edit/[id]
      │
      ▼
fetchBook()
      │
      ├─ supabase.from('books').select().eq('id', id)
      │
      ▼
  Supabase
      │
      ├─ Query single book
      │
      ▼
Return book data
      │
      ▼
Pre-fill form
      │
      ▼
User modifies fields
      │
      ▼
User clicks "Save"
      │
      ▼
handleSubmit()
      │
      ├─ supabase.from('books').update().eq('id', id)
      │
      ▼
  Supabase
      │
      ├─ Update row
      │
      ▼
Return success
      │
      ▼
router.push('/')
      │
      ▼
Redirect to home
```

### 4. Delete Book
```
User clicks "Delete"
      │
      ▼
Show confirmation
      │
      ├─ User confirms
      │
      ▼
deleteBook(id)
      │
      ├─ supabase.from('books').delete().eq('id', id)
      │
      ▼
  Supabase
      │
      ├─ Delete row
      │
      ▼
Return success
      │
      ▼
fetchBooks()
      │
      ▼
Refresh list
```

## 🔄 Component Hierarchy

```
RootLayout (layout.tsx)
│
├─ <html>
│  └─ <body>
│     └─ {children}
│
├─ Home Page (page.tsx)
│  │
│  ├─ Header
│  │  ├─ Title: "Book Collection"
│  │  └─ "Add Book" Button
│  │
│  ├─ Filters Section
│  │  ├─ Search Input
│  │  ├─ Tag Filter Dropdown
│  │  └─ Sort Dropdown
│  │
│  └─ Book Grid
│     └─ Book Card (for each book)
│        ├─ Cover Image
│        ├─ Title
│        ├─ Author
│        ├─ Tags
│        ├─ Edit Button
│        └─ Delete Button
│
├─ Create Page (create/page.tsx)
│  │
│  ├─ Header
│  │  ├─ Back Link
│  │  └─ Title: "Add New Book"
│  │
│  └─ Form
│     ├─ Title Input (required)
│     ├─ Author Input (required)
│     ├─ Tags Input (optional)
│     ├─ Cover Image Input (optional)
│     ├─ Create Button
│     └─ Cancel Button
│
└─ Edit Page (edit/[id]/page.tsx)
   │
   ├─ Header
   │  ├─ Back Link
   │  └─ Title: "Edit Book"
   │
   └─ Form (pre-filled)
      ├─ Title Input (required)
      ├─ Author Input (required)
      ├─ Tags Input (optional)
      ├─ Cover Image Input (optional)
      ├─ Save Button
      └─ Cancel Button
```

## 🔐 Security Model

```
┌─────────────────────────────────────────────────────────┐
│  Client-Side (Browser)                                   │
│  - No authentication required (public app)               │
│  - Form validation                                       │
│  - Input sanitization                                    │
└────────────────────┬────────────────────────────────────┘
                     │
                     │ HTTPS Only
                     │
┌────────────────────▼────────────────────────────────────┐
│  Supabase                                                │
│  ┌────────────────────────────────────────────────┐    │
│  │  Row Level Security (RLS)                       │    │
│  │  - Policy: "Allow all operations"               │    │
│  │  - FOR ALL: SELECT, INSERT, UPDATE, DELETE      │    │
│  │  - USING (true): Allow all reads                │    │
│  │  - WITH CHECK (true): Allow all writes          │    │
│  └────────────────────────────────────────────────┘    │
│                                                          │
│  Note: For production, implement proper auth:           │
│  - User authentication                                  │
│  - User-specific policies                               │
│  - USING (auth.uid() = user_id)                         │
└─────────────────────────────────────────────────────────┘
```

## 🌐 Deployment Architecture

```
┌─────────────────────────────────────────────────────────┐
│  Developer                                               │
│  - Writes code locally                                   │
│  - Tests with npm run dev                                │
└────────────────────┬────────────────────────────────────┘
                     │
                     │ git push
                     ▼
┌─────────────────────────────────────────────────────────┐
│  GitHub                                                  │
│  - Stores source code                                    │
│  - Version control                                       │
│  - Public repository                                     │
└────────────────────┬────────────────────────────────────┘
                     │
                     │ Webhook trigger
                     ▼
┌─────────────────────────────────────────────────────────┐
│  Vercel                                                  │
│  1. Clone repository                                     │
│  2. Install dependencies (npm install)                   │
│  3. Build application (npm run build)                    │
│  4. Deploy to CDN                                        │
│  5. Assign URL: https://project.vercel.app               │
└────────────────────┬────────────────────────────────────┘
                     │
                     │ API calls
                     ▼
┌─────────────────────────────────────────────────────────┐
│  Supabase                                                │
│  - Always running                                        │
│  - Handles database queries                              │
│  - Returns JSON responses                                │
└─────────────────────────────────────────────────────────┘
```

## 📦 File Dependencies

```
app/page.tsx
├─ imports React hooks (useState, useEffect)
├─ imports Next.js (Link, Image)
├─ imports lib/supabase.ts
│  └─ imports @supabase/supabase-js
└─ imports app/globals.css
   └─ imports Tailwind CSS

app/create/page.tsx
├─ imports React hooks (useState)
├─ imports Next.js (useRouter, Link)
└─ imports lib/supabase.ts

app/edit/[id]/page.tsx
├─ imports React hooks (useState, useEffect)
├─ imports Next.js (useRouter, Link)
└─ imports lib/supabase.ts

lib/supabase.ts
├─ imports @supabase/supabase-js
├─ reads NEXT_PUBLIC_SUPABASE_URL
├─ reads NEXT_PUBLIC_SUPABASE_ANON_KEY
└─ exports supabase client & Book type
```

## 🎯 Request Flow Example

### User adds a book:

```
1. Browser
   └─ User fills form at /create
   
2. Client-Side
   └─ handleSubmit() validates inputs
   
3. Supabase Client
   └─ supabase.from('books').insert([{...}])
   
4. Network
   └─ POST https://[project].supabase.co/rest/v1/books
      Headers: apikey, Authorization
      Body: { title, author, tags, cover_image }
   
5. Supabase Server
   ├─ Authenticate request (check API key)
   ├─ Check RLS policies
   ├─ Validate data types
   ├─ Generate UUID for id
   ├─ Set created_at timestamp
   └─ INSERT INTO books (...)
   
6. PostgreSQL
   └─ Execute INSERT query
   
7. Response
   └─ 201 Created
      Body: { id, title, author, ... }
   
8. Client-Side
   └─ router.push('/') → Navigate home
   
9. Home Page
   └─ fetchBooks() → Display updated list
```

## 💾 State Management

```
Component State (useState)
├─ books: Book[]           # All books from database
├─ searchTerm: string      # Search input value
├─ selectedTag: string     # Selected tag filter
├─ sortOrder: 'asc'|'desc' # Sort direction
├─ loading: boolean        # Loading state
├─ title: string           # Form input
├─ author: string          # Form input
├─ tags: string            # Form input
└─ coverImage: string      # Form input

Derived State (computed)
├─ allTags                 # Unique tags from all books
└─ filteredBooks           # Books after search/filter/sort

Side Effects (useEffect)
└─ fetchBooks()            # Load data on mount
```

This architecture ensures a clean separation of concerns, scalability, and maintainability.
