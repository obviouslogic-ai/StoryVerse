# Deployment Guide

## Option 1: Vercel (Recommended)

### Step 1: Push to GitHub
```bash
git init
git add .
git commit -m "Initial commit: StoryVerse platform"
git branch -M main
git remote add origin https://github.com/yourusername/storyverse.git
git push -u origin main
```

### Step 2: Deploy to Vercel
1. Go to https://vercel.com
2. Click "New Project"
3. Import your GitHub repository
4. Click "Deploy"
5. Done! Your site is live

**No configuration needed** - Vercel auto-detects static HTML.

### Custom Domain (Optional)
1. Go to Project Settings > Domains
2. Add your custom domain
3. Update DNS records as instructed

---

## Option 2: Netlify

### Via Git
1. Push to GitHub (see above)
2. Go to https://netlify.com
3. Click "Add new site" > "Import an existing project"
4. Connect to GitHub
5. Deploy

### Drag & Drop
1. Zip your project folder
2. Go to https://app.netlify.com/drop
3. Drag and drop your zip
4. Instant deployment

---

## Option 3: GitHub Pages

1. Push to GitHub
2. Go to repository Settings > Pages
3. Source: Deploy from branch
4. Branch: main, folder: / (root)
5. Save
6. Access at: `https://yourusername.github.io/storyverse/`

---

## Option 4: AWS S3 + CloudFront

```bash
# Install AWS CLI
aws configure

# Create S3 bucket
aws s3 mb s3://storyverse-platform

# Upload files
aws s3 sync . s3://storyverse-platform --exclude ".git/*"

# Enable static website hosting
aws s3 website s3://storyverse-platform --index-document index.html

# Set public read policy
# (See AWS docs for bucket policy JSON)
```

---

## Environment Variables (Future)

When adding backend functionality, set these in Vercel:

```env
# API Keys
OPENAI_API_KEY=sk-...
ANTHROPIC_API_KEY=sk-ant-...

# Database
DATABASE_URL=postgresql://...
REDIS_URL=redis://...

# Auth
CLERK_SECRET_KEY=sk_...
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=pk_...

# Payments
STRIPE_SECRET_KEY=sk_...
STRIPE_WEBHOOK_SECRET=whsec_...

# Vector DB
PINECONE_API_KEY=...
PINECONE_ENVIRONMENT=...
```

---

## Performance Optimization

### Current (Static)
- Already optimized: Static HTML, CDN assets
- Page load: < 1s
- No build required

### Future (Production)
- Next.js: SSR/SSG for faster initial load
- Image optimization: next/image
- Code splitting: Automatic with Next.js
- Asset compression: Vercel handles automatically
- CDN: Vercel Edge Network

---

## Monitoring

### Add to index.html (Optional)

**Google Analytics**
```html
<!-- Add before </head> -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-XXXXXXXXXX');
</script>
```

**Plausible (Privacy-friendly)**
```html
<script defer data-domain="yourdomain.com" src="https://plausible.io/js/script.js"></script>
```
