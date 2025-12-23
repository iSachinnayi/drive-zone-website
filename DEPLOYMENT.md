# 🚀 Deployment Guide - Drive Zone Auto Parts

This guide walks you through deploying the website to **DigitalOcean App Platform (Free Tier)** and adding a custom domain.

---

## Prerequisites

1. A [GitHub](https://github.com) account (free)
2. A [DigitalOcean](https://www.digitalocean.com) account (free tier available)

---

## Step 1: Push Code to GitHub

### Option A: Create New Repository on GitHub

1. Go to [github.com/new](https://github.com/new)
2. Repository name: `drive-zone-website`
3. Keep it **Public** or **Private** (your choice)
4. **Don't** initialize with README (we already have one)
5. Click **Create repository**

### Option B: Push Your Code

After creating the repository, run these commands in the project folder:

```bash
# Add GitHub as remote (replace YOUR_USERNAME with your GitHub username)
git remote add origin https://github.com/YOUR_USERNAME/drive-zone-website.git

# Push to GitHub
git branch -M main
git push -u origin main
```

---

## Step 2: Deploy to DigitalOcean App Platform

### 2.1 Create App

1. Go to [cloud.digitalocean.com/apps](https://cloud.digitalocean.com/apps)
2. Click **Create App**
3. Select **GitHub** as the source
4. Authorize DigitalOcean to access your GitHub (if first time)
5. Select your repository: `drive-zone-website`
6. Select branch: `main`
7. Click **Next**

### 2.2 Configure Build Settings

DigitalOcean should auto-detect the settings, but verify:

| Setting | Value |
|---------|-------|
| **Type** | Static Site |
| **Build Command** | `npm run build` |
| **Output Directory** | `dist` |

Click **Next**

### 2.3 Choose Plan

1. Select **Starter** plan (Free!)
   - Includes 3 static sites
   - 1 GB bandwidth/month
   - Automatic HTTPS

2. Click **Next**

### 2.4 Review and Create

1. App Name: `drive-zone-website` (or your preference)
2. Region: Choose closest to UAE (e.g., Frankfurt or Singapore)
3. Click **Create Resources**

### 2.5 Wait for Deployment

- DigitalOcean will build and deploy your site
- This takes 2-5 minutes
- You'll get a URL like: `drive-zone-website-xxxxx.ondigitalocean.app`

---

## Step 3: Add Custom Domain (Optional)

### 3.1 In DigitalOcean

1. Go to your App → **Settings** → **Domains**
2. Click **Add Domain**
3. Enter your domain: `drivezoneautoparts.ae` (or your domain)
4. Click **Add Domain**

### 3.2 Configure DNS

DigitalOcean will show you DNS records to add. You have two options:

#### Option A: Using DigitalOcean DNS (Recommended)

1. Add your domain to DigitalOcean: **Networking** → **Domains**
2. Update nameservers at your registrar to:
   - `ns1.digitalocean.com`
   - `ns2.digitalocean.com`
   - `ns3.digitalocean.com`

#### Option B: Using Your Current DNS Provider

Add these records at your domain registrar:

| Type | Name | Value |
|------|------|-------|
| **CNAME** | `www` | `drive-zone-website-xxxxx.ondigitalocean.app` |
| **A** | `@` | (DigitalOcean will provide IP) |

Or use **ALIAS/ANAME** record if your provider supports it.

### 3.3 Enable HTTPS

- DigitalOcean automatically provisions free SSL certificates via Let's Encrypt
- This happens automatically after DNS propagation (can take up to 48 hours)

---

## Step 4: Update Site URL

After deployment, update the site URL in `astro.config.mjs`:

```javascript
export default defineConfig({
  site: 'https://drivezoneautoparts.ae', // Your actual domain
  // ... rest of config
});
```

Then push the change:

```bash
git add .
git commit -m "Update site URL for production"
git push
```

DigitalOcean will automatically redeploy.

---

## Automatic Deployments

Every time you push to the `main` branch, DigitalOcean will automatically:
1. Pull the latest code
2. Run `npm run build`
3. Deploy the new version

---

## Updating Content

To update website content:

1. Edit `src/data/site.json` for business info, services, FAQ, etc.
2. Commit and push:
   ```bash
   git add .
   git commit -m "Update content"
   git push
   ```
3. DigitalOcean auto-deploys in ~2 minutes

---

## Monitoring & Analytics

### Built-in DigitalOcean Features
- **Insights**: View bandwidth usage in App dashboard
- **Logs**: Build logs available in **Activity** tab

### Recommended: Add Google Analytics (Free)
1. Create account at [analytics.google.com](https://analytics.google.com)
2. Get your Measurement ID (G-XXXXXXXXXX)
3. Add to `src/layouts/BaseLayout.astro` in the `<head>`:

```html
<!-- Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-XXXXXXXXXX');
</script>
```

---

## Troubleshooting

### Build Fails
- Check **Activity** tab for error logs
- Ensure `package.json` has correct dependencies
- Test locally with `npm run build`

### Domain Not Working
- DNS propagation can take 24-48 hours
- Verify DNS records with [dnschecker.org](https://dnschecker.org)
- Check domain settings in DigitalOcean App dashboard

### SSL Certificate Issues
- Wait for DNS to fully propagate
- Check domain verification status in DigitalOcean

---

## Cost Summary

| Service | Cost |
|---------|------|
| DigitalOcean Static Site | **FREE** (Starter plan) |
| GitHub Repository | **FREE** |
| Custom Domain | ~$10-15/year (from registrar) |
| SSL Certificate | **FREE** (Let's Encrypt via DO) |

**Total: $0/month** (excluding domain registration)

---

## Alternative Deployment Options

### Cloudflare Pages (Also Free)
```bash
# Install Wrangler CLI
npm install -g wrangler

# Login and deploy
wrangler login
npx wrangler pages deploy dist
```

### GitHub Pages (Also Free)
See main README.md for GitHub Actions workflow.

---

## Support

For issues:
- DigitalOcean: [docs.digitalocean.com](https://docs.digitalocean.com/products/app-platform/)
- Astro: [docs.astro.build](https://docs.astro.build)

---

**Drive Zone Auto Parts & Car Accessories**  
Al Marmouyiah Street, Mussaffah 6, Abu Dhabi, UAE  
📞 +971 52 706 4648

