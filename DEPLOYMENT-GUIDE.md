# 🚀 Hostinger Deployment Guide

This guide will help you deploy your Next.js Circular Metronome application to Hostinger.

## 📋 Prerequisites

1. **Hostinger Account**: Sign up at [hostinger.com](https://hostinger.com)
2. **Domain Name**: Purchase or connect your domain
3. **Apple Developer Account**: For Apple Sign-In functionality

## 🔧 Step 1: Prepare Your Application

### 1.1 Update Environment Variables

Create a `.env.production` file in your project root:

```env
# Apple Authentication (Update with your actual values)
APPLE_ID_CLIENT_ID=your.app.bundle.id
APPLE_ID_TEAM_ID=your_team_id
APPLE_ID_PRIVATE_KEY="-----BEGIN PRIVATE KEY-----\nYOUR_PRIVATE_KEY_HERE\n-----END PRIVATE KEY-----"
APPLE_ID_KEY_ID=your_key_id

# NextAuth Configuration
NEXTAUTH_URL=https://yourdomain.com
NEXTAUTH_SECRET=your-production-nextauth-secret-key-here

# Database (Use a cloud database like PlanetScale, Supabase, or Railway)
DATABASE_URL="your-production-database-url"

# Production mode
NODE_ENV=production
```

### 1.2 Update Apple Developer Console

1. Go to [Apple Developer Console](https://developer.apple.com/account/)
2. Update your Service ID with production domain:
   - **Return URLs**: `https://yourdomain.com/api/auth/callback/apple`
3. Ensure your App ID and Key are configured correctly

### 1.3 Build Your Application

```bash
npm run build
```

This will create a `out` folder with static files.

## 📁 Step 2: Prepare Files for Upload

### 2.1 Files to Upload

Upload these folders/files to your Hostinger public_html directory:

```
public_html/
├── .htaccess                    # Apache configuration
├── index.html                   # Main entry point
├── _next/                       # Next.js static assets
├── public/                      # Static assets (images, fonts)
└── [other static files]
```

### 2.2 Important Notes

- **Database**: Since this is a static export, you'll need to handle authentication differently
- **API Routes**: Static export doesn't support API routes, so you'll need to modify the authentication flow
- **Environment Variables**: These need to be set in your hosting environment

## 🌐 Step 3: Hostinger Setup

### 3.1 Access Hostinger Control Panel

1. Log in to your Hostinger account
2. Go to **Hosting** → **Manage**
3. Click **File Manager**

### 3.2 Upload Files

1. Navigate to `public_html` folder
2. Upload all files from your `out` directory
3. Ensure `.htaccess` is in the root directory

### 3.3 Configure Domain

1. Go to **Domains** → **Manage**
2. Point your domain to the hosting
3. Wait for DNS propagation (up to 24 hours)

## 🔐 Step 4: Authentication Setup

### 4.1 Option A: Use External Authentication Service

Since static hosting doesn't support server-side authentication, consider:

- **Auth0**: External authentication service
- **Firebase Auth**: Google's authentication service
- **Supabase Auth**: Open-source alternative

### 4.2 Option B: Modify for Static Hosting

Remove server-side authentication and use client-side only:

1. Remove NextAuth.js dependencies
2. Use localStorage for session management
3. Implement client-side Apple Sign-In

### 4.3 Option C: Use Hostinger's Node.js Hosting

If available, upgrade to Node.js hosting to support full Next.js features.

## 🛠️ Step 5: Alternative Deployment Options

### 5.1 Vercel (Recommended for Next.js)

```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel --prod
```

### 5.2 Netlify

1. Connect your GitHub repository
2. Build command: `npm run build`
3. Publish directory: `out`

### 5.3 Railway

1. Connect your GitHub repository
2. Set environment variables
3. Deploy automatically

## 🔧 Step 6: Post-Deployment

### 6.1 Test Your Application

1. Visit your domain
2. Test all features
3. Check mobile responsiveness
4. Verify Apple Sign-In

### 6.2 SSL Certificate

1. Enable SSL in Hostinger control panel
2. Force HTTPS redirects
3. Update Apple Developer Console with HTTPS URLs

### 6.3 Performance Optimization

1. Enable Gzip compression
2. Set up CDN if available
3. Optimize images
4. Enable browser caching

## 🐛 Troubleshooting

### Common Issues

1. **404 Errors**: Check `.htaccess` file
2. **Authentication Issues**: Verify environment variables
3. **CORS Errors**: Update Apple Developer Console URLs
4. **Build Errors**: Check Node.js version compatibility

### Support

- **Hostinger Support**: [support.hostinger.com](https://support.hostinger.com)
- **Next.js Documentation**: [nextjs.org/docs](https://nextjs.org/docs)
- **Apple Developer**: [developer.apple.com](https://developer.apple.com)

## 📊 Monitoring

### 6.1 Set Up Analytics

- Google Analytics
- Hostinger Analytics
- Performance monitoring

### 6.2 Error Tracking

- Sentry for error tracking
- Hostinger error logs
- Browser console monitoring

## 🔄 Continuous Deployment

### 6.1 GitHub Actions

Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy to Hostinger
on:
  push:
    branches: [main]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-node@v2
        with:
          node-version: '18'
      - run: npm ci
      - run: npm run build
      - name: Deploy to Hostinger
        uses: easingthemes/ssh-deploy@main
        env:
          SSH_PRIVATE_KEY: ${{ secrets.SSH_PRIVATE_KEY }}
          REMOTE_HOST: ${{ secrets.REMOTE_HOST }}
          REMOTE_USER: ${{ secrets.REMOTE_USER }}
          SOURCE: "out/"
          TARGET: "/public_html/"
```

## ✅ Checklist

- [ ] Environment variables configured
- [ ] Apple Developer Console updated
- [ ] Application built successfully
- [ ] Files uploaded to Hostinger
- [ ] Domain configured
- [ ] SSL certificate enabled
- [ ] Authentication working
- [ ] Mobile responsiveness tested
- [ ] Performance optimized
- [ ] Analytics configured

## 🎉 Success!

Your Circular Metronome application is now live on Hostinger!

**Next Steps:**
1. Share your website
2. Monitor performance
3. Gather user feedback
4. Plan future updates

---

**Need Help?** Check the troubleshooting section or contact Hostinger support. 