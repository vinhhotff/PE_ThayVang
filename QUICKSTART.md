# Quick Start Guide

## 🚀 Get Started in 5 Minutes

### Step 1: Install Dependencies
```bash
cd book-collection
npm install
```

### Step 2: Set Up Supabase

1. Go to [supabase.com](https://supabase.com) and create a free account
2. Create a new project (choose a region close to you)
3. Wait for the project to be ready (~2 minutes)
4. Go to SQL Editor (left sidebar)
5. Click "New Query" and paste this SQL:

```sql
CREATE TABLE books (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  title TEXT NOT NULL,
  author TEXT NOT NULL,
  tags TEXT[],
  cover_image TEXT,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT TIMEZONE('utc', NOW())
);

ALTER TABLE books ENABLE ROW LEVEL SECURITY;

CREATE POLICY "Allow all operations" ON books
  FOR ALL USING (true) WITH CHECK (true);
```

6. Click "Run" to execute the SQL

### Step 3: Get Your Credentials

1. In Supabase, go to Settings > API
2. Copy your "Project URL"
3. Copy your "anon public" key

### Step 4: Configure Environment

1. Create `.env.local` file in the `book-collection` folder:
```
NEXT_PUBLIC_SUPABASE_URL=paste_your_project_url_here
NEXT_PUBLIC_SUPABASE_ANON_KEY=paste_your_anon_key_here
```

### Step 5: Run the App

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser!

## 📝 What You Can Do

- **Add Books**: Click "Add Book" button
- **Search**: Type in the search box to find books by title
- **Filter**: Select a tag to filter books
- **Sort**: Choose A-Z or Z-A sorting
- **Edit**: Click "Edit" on any book card
- **Delete**: Click "Delete" (with confirmation)

## 🌐 Deploy to Production

See [DEPLOYMENT.md](DEPLOYMENT.md) for detailed deployment instructions.

Quick version:
1. Push code to GitHub
2. Connect to Vercel
3. Add environment variables
4. Deploy!

## 📚 Sample Data (Optional)

Want some test data? Run this in Supabase SQL Editor:

```sql
INSERT INTO books (title, author, tags, cover_image) VALUES
  ('Clean Code', 'Robert C. Martin', ARRAY['Programming', 'Software Engineering'], 'https://m.media-amazon.com/images/I/51E2055ZGUL._SY466_.jpg'),
  ('The Pragmatic Programmer', 'Andrew Hunt', ARRAY['Programming', 'Career'], 'https://m.media-amazon.com/images/I/51cUVaBWZzL._SY466_.jpg'),
  ('JavaScript: The Good Parts', 'Douglas Crockford', ARRAY['JavaScript', 'Programming'], 'https://m.media-amazon.com/images/I/5188424863L._SY466_.jpg');
```

## ❓ Need Help?

- Check [README.md](README.md) for full documentation
- Check [SETUP.md](SETUP.md) for database setup details
- Check [DEPLOYMENT.md](DEPLOYMENT.md) for deployment guide
