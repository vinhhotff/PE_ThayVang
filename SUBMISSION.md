# Submission Checklist

## 📋 Before You Submit

### 1. Complete the Setup
- [ ] Install dependencies: `npm install`
- [ ] Create Supabase account and project
- [ ] Run SQL schema in Supabase (see SETUP.md)
- [ ] Create `.env.local` with your Supabase credentials
- [ ] Test locally: `npm run dev`
- [ ] Verify all features work

### 2. Deploy Your Application
- [ ] Push code to GitHub (make repository PUBLIC)
- [ ] Deploy to Vercel
- [ ] Add environment variables in Vercel
- [ ] Test deployed application
- [ ] Verify all features work in production

### 3. Create Your Report

Create a file named `QE123456_Exam.docx` (replace with your Student ID)

Include:
1. **GitHub Repository Link** (must be public)
   - Example: `https://github.com/yourusername/book-collection`

2. **Deployed Website Link**
   - Example: `https://book-collection-xyz.vercel.app`

3. **Feature Description** (brief report)
   - List implemented features
   - Explain how each requirement was met
   - Include at least one screenshot

4. **Screenshot**
   - Take a screenshot showing the working application
   - Show the book list with at least 2-3 books
   - Or show the add/edit book form

### 4. Verify Requirements

#### Main Page (Book List) ✅
- [x] Display all books with title, author, tags, cover image
- [x] Search books by title
- [x] Filter books by tag
- [x] Sort books by title (A-Z / Z-A)

#### Create Book ✅
- [x] Form with title (required)
- [x] Form with author (required)
- [x] Form with tags (optional)
- [x] Form with cover image (optional)

#### Edit Book ✅
- [x] Click on book navigates to edit page
- [x] Can modify title, author, tags, cover image
- [x] Redirects back to book list after saving

#### Delete Book ✅
- [x] Delete button on each book
- [x] Confirmation prompt before deletion

#### Deployment ✅
- [x] Code pushed to public GitHub repository
- [x] Deployed on Vercel (free hosting)
- [x] Using Supabase (free database)

## 📝 Sample Report Template

```
Student ID: QE123456
Project: Personal Book Collection Manager

GitHub Repository: https://github.com/yourusername/book-collection
Deployed Website: https://book-collection-xyz.vercel.app

Features Implemented:
1. Book List Page - Displays all books with search, filter, and sort functionality
2. Add Book - Form to create new books with validation
3. Edit Book - Update existing book information
4. Delete Book - Remove books with confirmation dialog
5. Responsive Design - Works on mobile and desktop

Technology Stack:
- Frontend: Next.js 15 with TypeScript and Tailwind CSS
- Backend: Supabase (PostgreSQL database)
- Deployment: Vercel

[Insert screenshot here]
```

## ⚠️ Common Issues

### Build Fails
- Run `npm run build` locally first to check for errors
- Fix any TypeScript errors before deploying

### Database Not Working
- Double-check environment variables
- Ensure Supabase SQL schema was executed
- Verify RLS policies are enabled

### Images Not Loading
- Use valid image URLs (https://)
- Test URLs in browser before adding to database

## 🎯 Final Check

Before submitting:
1. ✅ GitHub repository is PUBLIC
2. ✅ README.md is included
3. ✅ Application is deployed and accessible
4. ✅ All features work in production
5. ✅ Report document is created with correct filename
6. ✅ Screenshot is included in report

Good luck! 🚀
