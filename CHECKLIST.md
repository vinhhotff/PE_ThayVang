# ✅ Complete Checklist

## Phase 1: Local Setup (30 minutes)

### Install & Configure
- [ ] Navigate to project: `cd book-collection`
- [ ] Install dependencies: `npm install`
- [ ] Wait for installation to complete

### Supabase Setup
- [ ] Go to [supabase.com](https://supabase.com)
- [ ] Create free account
- [ ] Create new project
- [ ] Wait for project initialization (~2 min)
- [ ] Go to SQL Editor
- [ ] Run the SQL schema (from SETUP.md)
- [ ] Verify table created (check Table Editor)

### Get Credentials
- [ ] Go to Settings → API in Supabase
- [ ] Copy Project URL
- [ ] Copy anon/public key
- [ ] Create `.env.local` file in project root
- [ ] Paste credentials in `.env.local`

### Test Locally
- [ ] Run `npm run dev`
- [ ] Open http://localhost:3000
- [ ] Click "Add Book"
- [ ] Add a test book
- [ ] Verify book appears in list
- [ ] Test search functionality
- [ ] Test filter by tag
- [ ] Test sort A-Z / Z-A
- [ ] Test edit book
- [ ] Test delete book (with confirmation)

## Phase 2: Version Control (10 minutes)

### Git Setup
- [ ] Initialize git: `git init`
- [ ] Add files: `git add .`
- [ ] Commit: `git commit -m "Initial commit"`

### GitHub
- [ ] Go to [github.com](https://github.com)
- [ ] Create new repository
- [ ] Name it "book-collection"
- [ ] Make it PUBLIC (important!)
- [ ] Don't initialize with README
- [ ] Copy the repository URL

### Push Code
- [ ] Add remote: `git remote add origin YOUR_REPO_URL`
- [ ] Push: `git push -u origin main`
- [ ] Verify code is on GitHub

## Phase 3: Deployment (20 minutes)

### Vercel Setup
- [ ] Go to [vercel.com](https://vercel.com)
- [ ] Sign up with GitHub
- [ ] Click "Add New Project"
- [ ] Import your book-collection repository
- [ ] Framework: Next.js (auto-detected)

### Environment Variables
- [ ] In Vercel, click "Environment Variables"
- [ ] Add `NEXT_PUBLIC_SUPABASE_URL`
- [ ] Add `NEXT_PUBLIC_SUPABASE_ANON_KEY`
- [ ] Use same values from your `.env.local`

### Deploy
- [ ] Click "Deploy"
- [ ] Wait for build (~2 minutes)
- [ ] Click "Visit" to see your live site
- [ ] Copy the deployment URL

### Test Production
- [ ] Open deployed URL
- [ ] Add a book
- [ ] Edit a book
- [ ] Delete a book
- [ ] Test search
- [ ] Test filter
- [ ] Test sort
- [ ] Verify everything works

## Phase 4: Documentation (15 minutes)

### Create Report
- [ ] Create Word document
- [ ] Name it: `QE123456_Exam.docx` (your Student ID)

### Add Content
- [ ] Add GitHub repository link
- [ ] Add deployed website link
- [ ] Write brief feature description
- [ ] List all implemented features
- [ ] Take screenshot of working app
- [ ] Insert screenshot in document

### Screenshot Tips
- [ ] Show book list with 2-3 books
- [ ] Include search/filter/sort controls
- [ ] Make sure URL is visible
- [ ] Use full-screen browser window

## Phase 5: Final Verification (10 minutes)

### GitHub Check
- [ ] Repository is PUBLIC
- [ ] All code is pushed
- [ ] README.md is visible
- [ ] No `.env.local` in repository (should be in .gitignore)

### Deployment Check
- [ ] Site is accessible
- [ ] No errors in browser console
- [ ] All features work
- [ ] Images load correctly
- [ ] Mobile responsive (test on phone)

### Report Check
- [ ] Correct filename format
- [ ] GitHub link is correct and public
- [ ] Deployed link is correct and working
- [ ] Feature description is clear
- [ ] Screenshot is included
- [ ] Document is saved

## Phase 6: Submission

### Before Submitting
- [ ] Test GitHub link in incognito/private window
- [ ] Test deployed link in incognito/private window
- [ ] Verify all features work for a fresh visitor
- [ ] Double-check report filename
- [ ] Save final version of report

### Submit
- [ ] Upload report document
- [ ] Submit on time
- [ ] Keep backup copy

## 🎉 You're Done!

Total estimated time: ~90 minutes

## ⚠️ Common Mistakes to Avoid

- ❌ GitHub repository is private (must be PUBLIC)
- ❌ Forgot to add environment variables in Vercel
- ❌ Wrong Student ID in report filename
- ❌ Screenshot doesn't show working features
- ❌ Links in report are broken or incorrect
- ❌ Didn't test deployed site before submitting

## 📞 Emergency Troubleshooting

### "npm install" fails
- Check internet connection
- Try: `npm cache clean --force`
- Try: `npm install --legacy-peer-deps`

### Can't connect to Supabase
- Verify credentials in `.env.local`
- Check Supabase project is active
- Ensure SQL schema was executed

### Vercel build fails
- Run `npm run build` locally first
- Check for TypeScript errors
- Verify all files are committed to GitHub

### Site works locally but not on Vercel
- Check environment variables in Vercel
- Redeploy after adding variables
- Check Vercel deployment logs

Good luck! 🚀
