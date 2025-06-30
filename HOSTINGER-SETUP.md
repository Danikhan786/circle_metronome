# 🚀 Quick Hostinger Deployment Guide

## ⚠️ Important Notice

Your app includes **Apple Sign-In authentication** which requires server-side hosting. Hostinger's basic shared hosting only supports static files.

## 🎯 Recommended Solutions

### Option 1: Use Vercel (Recommended)
```bash
# Install Vercel CLI
npm i -g vercel

# Deploy with full Next.js features
vercel --prod
```

### Option 2: Use Netlify
1. Connect your GitHub repository
2. Build command: `npm run build`
3. Publish directory: `out` (after static export)

### Option 3: Use Railway
1. Connect your GitHub repository
2. Set environment variables
3. Automatic deployment

## 🔧 If You Still Want Hostinger

### Step 1: Create Static Version
Remove authentication features and create a static-only version:

1. **Remove these files:**
   - `app/api/auth/[...nextauth]/route.ts`
   - `app/auth/` (entire directory)
   - `app/dashboard/page.tsx`
   - `middleware.ts`
   - `lib/apple-auth.ts`
   - `lib/prisma.ts`
   - `prisma/` (entire directory)

2. **Update Next.js config:**
   ```javascript
   // next.config.mjs
   const nextConfig = {
     output: 'export',
     images: { unoptimized: true },
     trailingSlash: true
   };
   ```

3. **Build static version:**
   ```bash
   npm run build
   ```

### Step 2: Upload to Hostinger

1. **Access Hostinger Control Panel**
   - Log in to [hostinger.com](https://hostinger.com)
   - Go to **Hosting** → **Manage**
   - Click **File Manager**

2. **Upload Files**
   - Navigate to `public_html` folder
   - Upload all files from the `out` directory
   - Include the `.htaccess` file

3. **Configure Domain**
   - Go to **Domains** → **Manage**
   - Point your domain to the hosting
   - Wait for DNS propagation

4. **Enable SSL**
   - Enable SSL certificate in control panel
   - Force HTTPS redirects

## 📁 Files to Upload

After building, upload these files to `public_html`:

```
public_html/
├── .htaccess
├── index.html
├── _next/
├── public/
└── [other static files]
```

## 🔐 Authentication Alternative

If you want to keep authentication on Hostinger:

1. **Use External Auth Service:**
   - [Auth0](https://auth0.com)
   - [Firebase Auth](https://firebase.google.com/docs/auth)
   - [Supabase Auth](https://supabase.com/docs/guides/auth)

2. **Use Hostinger's Node.js Hosting** (if available)
   - Upgrade to Node.js hosting plan
   - Deploy full Next.js application

## 🚀 Quick Deploy Commands

```bash
# Option 1: Vercel (Recommended)
npm i -g vercel
vercel --prod

# Option 2: Netlify
npm run build
# Then drag 'out' folder to Netlify

# Option 3: Railway
# Connect GitHub repo to Railway
```

## 📞 Support

- **Vercel**: [vercel.com](https://vercel.com) - Best for Next.js
- **Netlify**: [netlify.com](https://netlify.com) - Great for static sites
- **Railway**: [railway.app](https://railway.app) - Full-stack hosting
- **Hostinger**: [support.hostinger.com](https://support.hostinger.com)

## ✅ Checklist

- [ ] Choose hosting platform
- [ ] Set up authentication (if needed)
- [ ] Configure domain
- [ ] Enable SSL
- [ ] Test application
- [ ] Set up analytics

---

**Recommendation**: Use **Vercel** for the best Next.js experience with full authentication support! 