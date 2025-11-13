# Book Collection Manager

A web application for managing your personal book collection built with Next.js and Supabase.

## Features

- ✅ Display all books with title, author, tags, and cover image
- ✅ Search books by title
- ✅ Filter books by tag
- ✅ Sort books alphabetically (A-Z / Z-A)
- ✅ Add new books with title, author, tags, and cover image
- ✅ Edit existing books
- ✅ Delete books with confirmation prompt
- ✅ Responsive design with Tailwind CSS

## Tech Stack

- **Frontend**: Next.js 15 (App Router), React 18, TypeScript, Tailwind CSS
- **Backend**: Supabase (PostgreSQL database)
- **Deployment**: Vercel (frontend), Supabase (database)

## Setup Instructions

### 1. Supabase Database Setup

1. Go to [supabase.com](https://supabase.com) and create a free account
2. Create a new project
3. Go to the SQL Editor and run this SQL to create the books table:

```sql
CREATE TABLE books (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  title TEXT NOT NULL,
  author TEXT NOT NULL,
  tags TEXT[],
  cover_image TEXT,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT TIMEZONE('utc', NOW())
);

-- Enable Row Level Security
ALTER TABLE books ENABLE ROW LEVEL SECURITY;

-- Create policy to allow all operations (for development)
CREATE POLICY "Allow all operations" ON books
  FOR ALL
  USING (true)
  WITH CHECK (true);
```

4. Get your project URL and anon key from Settings > API

### 2. Local Development

1. Install dependencies:
```bash
npm install
```

2. Create `.env.local` file in the root directory:
```
NEXT_PUBLIC_SUPABASE_URL=your_supabase_project_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
```

3. Run the development server:
```bash
npm run dev
```

4. Open [http://localhost:3000](http://localhost:3000)

### 3. Deployment

#### Deploy to Vercel

1. Push your code to GitHub
2. Go to [vercel.com](https://vercel.com) and import your repository
3. Add environment variables:
   - `NEXT_PUBLIC_SUPABASE_URL`
   - `NEXT_PUBLIC_SUPABASE_ANON_KEY`
4. Deploy!

Your app will be live at `https://your-project.vercel.app`

## Project Structure

```
book-collection/
├── app/
│   ├── create/
│   │   └── page.tsx          # Add new book page
│   ├── edit/
│   │   └── [id]/
│   │       └── page.tsx      # Edit book page
│   ├── globals.css           # Global styles
│   ├── layout.tsx            # Root layout
│   └── page.tsx              # Home page (book list)
├── lib/
│   └── supabase.ts           # Supabase client & types
├── .env.local.example        # Environment variables template
├── next.config.js            # Next.js configuration
├── package.json              # Dependencies
├── tailwind.config.ts        # Tailwind configuration
└── tsconfig.json             # TypeScript configuration
```

## Usage

### Adding a Book
1. Click "Add Book" button
2. Fill in title (required) and author (required)
3. Optionally add tags (comma-separated) and cover image URL
4. Click "Create Book"

### Editing a Book
1. Click "Edit" on any book card
2. Modify the fields
3. Click "Save Changes"

### Deleting a Book
1. Click "Delete" on any book card
2. Confirm the deletion in the prompt

### Searching and Filtering
- Use the search box to find books by title
- Select a tag from the dropdown to filter by tag
- Use the sort dropdown to order books A-Z or Z-A

## Screenshots

![Book List Page](screenshot-list.png)
![Add Book Page](screenshot-add.png)

## License

MIT
