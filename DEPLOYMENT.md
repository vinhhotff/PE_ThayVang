# Deployment Guide

## Prerequisites

- GitHub account
- Vercel account (free)
- Supabase account (free)

## Step-by-Step Deployment

### 1. Prepare Your Code

1. Initialize git repository (if not already done):
```bash
git init
git add .
git commit -m "Initial commit"
```

2. Create a GitHub repository and push your code:
```bash
git remote add origin https://github.com/your-username/book-collection.git
git branch -M main
git push -u origin main
```

### 2. Deploy to Vercel

1. Go to [vercel.com](https://vercel.com) and sign in with GitHub
2. Click "Add New Project"
3. Import your `book-collection` repository
4. Configure your project:
   - Framework Preset: Next.js (auto-detected)
   - Root Directory: `./`
   - Build Command: `npm run build` (default)
   - Output Directory: `.next` (default)

5. Add Environment Variables:
   - Click "Environment Variables"
   - Add `NEXT_PUBLIC_SUPABASE_URL` with your Supabase URL
   - Add `NEXT_PUBLIC_SUPABASE_ANON_KEY` with your Supabase anon key

6. Click "Deploy"

7. Wait for deployment to complete (usually 1-2 minutes)

8. Your app will be live at `https://your-project.vercel.app`

### 3. Verify Deployment

1. Visit your deployed URL
2. Test all features:
   - View book list
   - Add a new book
   - Edit a book
   - Delete a book
   - Search and filter functionality

### 4. Custom Domain (Optional)

1. In Vercel dashboard, go to your project
2. Click "Settings" > "Domains"
3. Add your custom domain
4. Follow DNS configuration instructions

## Continuous Deployment

Vercel automatically deploys:
- Every push to `main` branch → Production
- Every pull request → Preview deployment

## Troubleshooting

### Build Fails
- Check build logs in Vercel dashboard
- Ensure all dependencies are in `package.json`
- Verify TypeScript has no errors locally

### Environment Variables Not Working
- Make sure variables start with `NEXT_PUBLIC_`
- Redeploy after adding/changing environment variables
- Check Vercel dashboard > Settings > Environment Variables

### Database Connection Issues
- Verify Supabase credentials are correct
- Check Supabase project is active
- Ensure RLS policies are set up correctly

## Production Checklist

- [ ] Code pushed to GitHub
- [ ] Supabase database created and configured
- [ ] Environment variables added to Vercel
- [ ] App deployed successfully
- [ ] All features tested on production
- [ ] README updated with live URL
- [ ] GitHub repository is public (for submission)

## Monitoring

- View deployment logs in Vercel dashboard
- Check Supabase logs for database queries
- Use Vercel Analytics (optional) for traffic insights
