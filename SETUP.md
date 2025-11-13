# Supabase Database Setup

## SQL Schema

Run this SQL in your Supabase SQL Editor:

```sql
-- Create books table
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
-- For production, you should implement proper authentication
CREATE POLICY "Allow all operations" ON books
  FOR ALL
  USING (true)
  WITH CHECK (true);

-- Optional: Insert sample data
INSERT INTO books (title, author, tags, cover_image) VALUES
  ('Clean Code', 'Robert C. Martin', ARRAY['Programming', 'Software Engineering'], 'https://images-na.ssl-images-amazon.com/images/I/41xShlnTZTL._SX376_BO1,204,203,200_.jpg'),
  ('The Pragmatic Programmer', 'Andrew Hunt', ARRAY['Programming', 'Career'], 'https://images-na.ssl-images-amazon.com/images/I/51W1sBPO7tL._SX380_BO1,204,203,200_.jpg'),
  ('Design Patterns', 'Gang of Four', ARRAY['Programming', 'Design'], 'https://images-na.ssl-images-amazon.com/images/I/51szD9HC9pL._SX395_BO1,204,203,200_.jpg');
```

## Getting Supabase Credentials

1. Go to your Supabase project dashboard
2. Click on Settings (gear icon) in the sidebar
3. Click on "API" under Project Settings
4. Copy the following:
   - Project URL (under "Project URL")
   - anon/public key (under "Project API keys")

## Environment Variables

Create a `.env.local` file in your project root:

```
NEXT_PUBLIC_SUPABASE_URL=https://your-project.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key-here
```

Replace with your actual values from the Supabase dashboard.
