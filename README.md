# Drive Zone Auto Parts - Website

A professional, mobile-first static website for **Drive Zone Auto Parts & Car Accessories** in Abu Dhabi, UAE.

![Drive Zone Logo](public/logo/logo-primary.svg)

## 🚀 Features

- **Modern Design**: Clean, professional aesthetic with custom branding
- **Mobile-First**: Responsive design optimized for all devices
- **Fast Performance**: Static site with minimal JavaScript
- **SEO Optimized**: Meta tags, JSON-LD schema, sitemap, and robots.txt
- **Local Business Focus**: Click-to-call, WhatsApp integration, Google Maps
- **Easy Content Management**: Single JSON config file for all content

## 📁 Project Structure

```
drive-zone-website/
├── public/
│   ├── logo/              # SVG logo variants
│   ├── images/            # Store photos
│   ├── favicon.svg
│   └── robots.txt
├── src/
│   ├── components/
│   │   ├── Header.astro
│   │   ├── Footer.astro
│   │   └── sections/      # Page sections
│   ├── data/
│   │   └── site.json      # ⭐ Main content config file
│   ├── layouts/
│   │   └── BaseLayout.astro
│   ├── pages/
│   │   ├── index.astro    # Home page
│   │   ├── about.astro
│   │   ├── contact.astro
│   │   ├── privacy.astro
│   │   ├── terms.astro
│   │   ├── 404.astro
│   │   └── services/
│   │       ├── auto-parts.astro
│   │       ├── car-accessories.astro
│   │       └── delivery.astro
│   └── styles/
│       └── global.css
├── astro.config.mjs
├── tailwind.config.mjs
├── package.json
└── README.md
```

## 🛠️ Tech Stack

- **[Astro](https://astro.build/)** - Static site generator
- **[Tailwind CSS](https://tailwindcss.com/)** - Utility-first CSS framework
- **Google Fonts** - Inter font family

## 📝 Editing Content

All business content is stored in a single file: `src/data/site.json`

### What You Can Edit:

| Section | Description |
|---------|-------------|
| `business` | Name, phone, address, coordinates |
| `hours` | Business operating hours |
| `hero` | Homepage headline and subheadline |
| `services` | Service descriptions and features |
| `categories` | Product categories displayed |
| `faq` | Frequently asked questions |
| `gallery` | Store images |
| `seo` | Page titles and descriptions |

### Example: Updating Business Hours

```json
"hours": {
  "display": [
    { "days": "Sunday - Wednesday", "time": "08:00 - 22:00" },
    { "days": "Thursday", "time": "08:30 - 22:00" },
    { "days": "Friday", "time": "08:00 - 12:00, 15:00 - 22:00" },
    { "days": "Saturday", "time": "Closed" }
  ]
}
```

### Adding Gallery Images

1. Add your image to `public/images/`
2. Update `site.json`:

```json
"gallery": [
  {
    "src": "/images/your-new-image.webp",
    "alt": "Description of the image",
    "caption": "Caption shown on hover"
  }
]
```

## 🖥️ Local Development

### Prerequisites

- [Node.js](https://nodejs.org/) v18 or higher
- npm or yarn

### Setup

```bash
# Navigate to project folder
cd drive-zone-website

# Install dependencies
npm install

# Start development server
npm run dev
```

The site will be available at `http://localhost:4321`

### Build for Production

```bash
npm run build
```

The static files will be generated in the `dist/` folder.

### Preview Production Build

```bash
npm run preview
```

## 🚀 Deployment Options

### Option 1: DigitalOcean App Platform (Free Tier)

1. Push your code to a GitHub repository

2. Go to [DigitalOcean App Platform](https://cloud.digitalocean.com/apps)

3. Click **Create App** → Select your GitHub repo

4. Configure the app:
   - **Type**: Static Site
   - **Build Command**: `npm run build`
   - **Output Directory**: `dist`

5. Click **Deploy**

6. (Optional) Add a custom domain in Settings → Domains

### Option 2: Cloudflare Pages (Free)

1. Push your code to GitHub

2. Go to [Cloudflare Pages](https://pages.cloudflare.com/)

3. Click **Create a project** → Connect to Git

4. Select your repository

5. Configure build settings:
   - **Framework preset**: Astro
   - **Build command**: `npm run build`
   - **Build output directory**: `dist`

6. Click **Save and Deploy**

### Option 3: GitHub Pages (Free)

1. In your repo, go to **Settings** → **Pages**

2. Set Source to **GitHub Actions**

3. Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [main]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: npm
      - run: npm ci
      - run: npm run build
      - uses: actions/upload-pages-artifact@v3
        with:
          path: dist

  deploy:
    needs: build
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - uses: actions/deploy-pages@v4
        id: deployment
```

4. Update `astro.config.mjs` with your GitHub Pages URL:

```javascript
export default defineConfig({
  site: 'https://yourusername.github.io',
  base: '/your-repo-name',
  // ... rest of config
});
```

### Option 4: Netlify (Free Tier)

1. Push code to GitHub

2. Go to [Netlify](https://app.netlify.com/)

3. Click **Add new site** → **Import an existing project**

4. Connect to GitHub and select repo

5. Build settings:
   - **Build command**: `npm run build`
   - **Publish directory**: `dist`

6. Click **Deploy site**

## 🔧 Customization

### Changing Colors

Edit `tailwind.config.mjs`:

```javascript
colors: {
  'brand': {
    'dark': '#0F1115',      // Main dark color
    'amber': '#D4A017',     // Primary accent
    'amber-light': '#E8B92E',
    // Add more colors...
  }
}
```

### Updating the Logo

Replace the SVG files in `public/logo/`:
- `logo-primary.svg` - Main logo (dark text)
- `logo-light.svg` - Light variant for dark backgrounds
- `logo-horizontal.svg` - Header logo
- `logo-icon.svg` - Icon only version

### Adding a New Page

1. Create a new `.astro` file in `src/pages/`
2. Import the BaseLayout
3. Add SEO info to `site.json`

Example:

```astro
---
import BaseLayout from '../layouts/BaseLayout.astro';
---

<BaseLayout title="New Page" description="Description here">
  <section class="section">
    <div class="container-custom">
      <h1>Your content</h1>
    </div>
  </section>
</BaseLayout>
```

## 📊 SEO Features

- ✅ Unique title and meta description per page
- ✅ Open Graph tags for social sharing
- ✅ Twitter Card meta tags
- ✅ JSON-LD LocalBusiness schema
- ✅ Automatic sitemap generation
- ✅ robots.txt file
- ✅ Canonical URLs

## 🖼️ Logo Files

| File | Usage |
|------|-------|
| `logo-primary.svg` | Main logo for light backgrounds |
| `logo-light.svg` | Logo for dark backgrounds |
| `logo-horizontal.svg` | Header logo (compact) |
| `logo-horizontal-light.svg` | Header logo for dark nav |
| `logo-icon.svg` | Icon only (for favicons, app icons) |
| `logo-icon-light.svg` | Icon for dark backgrounds |

## 📱 Contact Integration

- **Click-to-call**: All phone numbers are clickable
- **WhatsApp**: Floating button + direct links
- **Google Maps**: Embedded map + directions link

## 🤝 Support

For questions about the website, contact the development team or refer to:
- [Astro Documentation](https://docs.astro.build/)
- [Tailwind CSS Documentation](https://tailwindcss.com/docs)

## 📄 License

This project is proprietary and created for Drive Zone Auto Parts & Car Accessories.

---

**Drive Zone Auto Parts & Car Accessories**  
Al Marmouyiah Street, Mussaffah 6, Abu Dhabi, UAE  
📞 +971 52 706 4648

