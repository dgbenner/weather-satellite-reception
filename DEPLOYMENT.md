# Meteor-M Highland Park Station - Deployment Guide

## What You Have

Complete website template with:
- `index.html` - Main page with fixed header/footer, image gallery
- `style.css` - Black background styling, responsive layout
- `images/` - Placeholder images (satellite images + maps)
- `README.md` - Repository documentation

## File Structure

```
meteor-station/
├── index.html              # Main website
├── style.css               # Styling
├── README.md               # GitHub documentation
└── images/
    ├── placeholder-satellite-1.jpg   # 2048×4000 tall image
    ├── placeholder-satellite-2.jpg   # 2048×4000 tall image
    ├── placeholder-satellite-3.jpg   # 2048×4000 tall image
    ├── placeholder-regional-map.jpg  # 300×200 map
    └── placeholder-global-map.jpg    # 300×200 map
```

## Deploy to GitHub Pages

### Step 1: Create GitHub Repository

1. Go to https://github.com/new
2. Repository name: `meteor-highland-park` (or your choice)
3. Description: "Live weather satellite imagery from Highland Park, St. Paul, MN"
4. Public repository
5. **DO NOT** initialize with README (you already have one)
6. Click "Create repository"

### Step 2: Push Your Files

```bash
# Navigate to the meteor-station folder
cd /path/to/meteor-station

# Initialize git (if not already done)
git init

# Add all files
git add .

# First commit
git commit -m "Initial commit: Meteor-M Highland Park Station template"

# Add GitHub remote (replace YOUR-USERNAME and REPO-NAME)
git remote add origin https://github.com/YOUR-USERNAME/meteor-highland-park.git

# Push to GitHub
git branch -M main
git push -u origin main
```

### Step 3: Enable GitHub Pages

1. Go to your repository on GitHub
2. Click **Settings** tab
3. Click **Pages** in left sidebar
4. Under "Source":
   - Branch: `main`
   - Folder: `/ (root)`
5. Click **Save**
6. Wait 1-2 minutes for deployment

Your site will be live at: `https://YOUR-USERNAME.github.io/meteor-highland-park`

## Customization Before Deploying

### Update README.md

Line 3: Change `your-github-username` to your actual GitHub username

Line 76: Change `your-github-username` to your actual GitHub username

### Update index.html (Optional)

You can edit placeholder dates/times if you want, but they'll be replaced with real data after your first capture anyway.

## Adding Your First Real Image

After you capture and process your first satellite pass:

### Step 1: Process with SatDump

SatDump will output:
- Composite RGB image (the main one you'll display)
- Individual channel images
- Ground track map (if enabled)

### Step 2: Rename and Add to Website

```bash
# Copy processed image to images folder
cp ~/satdump-output/meteor_composite.png images/20241226_1430_M2-3.jpg

# If you have ground track maps:
cp ~/satdump-output/groundtrack.png images/20241226_1430_regional.jpg
```

### Step 3: Update index.html

Add new entry at the **top** of the `<main class="gallery">` section:

```html
<article class="image-entry">
    <div class="image-header">
        <div class="metadata">
            <h2 class="satellite-name">METEOR-M N°2-3</h2>
            <p class="capture-time">Captured: December 26, 2024 14:30 CST</p>
            <p class="processed-time">Processed: December 26, 2024 15:15 CST</p>
        </div>
    </div>
    
    <div class="image-container">
        <div class="satellite-image">
            <a href="images/20241226_1430_M2-3.jpg" target="_blank">
                <img src="images/20241226_1430_M2-3.jpg" alt="METEOR-M N°2-3 satellite image from December 26, 2024">
            </a>
        </div>
        
        <div class="maps">
            <div class="map-item">
                <h3>Regional Coverage</h3>
                <img src="images/20241226_1430_regional.jpg" alt="Regional coverage map">
            </div>
            <div class="map-item">
                <h3>Global Orbit</h3>
                <img src="images/placeholder-global-map.jpg" alt="Global orbital path">
            </div>
        </div>
    </div>
</article>
```

### Step 4: Push Updates

```bash
git add images/20241226_1430_M2-3.jpg
git add index.html
git commit -m "Add first Meteor-M capture from Dec 26"
git push
```

Site updates automatically within 1-2 minutes!

## Image Management

### When You Have Many Images

Keep the 10-20 most recent images on the site. Archive older ones:

```bash
# Create archive folder
mkdir -p archive/

# Move old images
mv images/old-image.jpg archive/

# Update git
git add -A
git commit -m "Archive older images"
git push
```

### Storage Limits

- GitHub Pages: Soft limit of 1GB per repository
- Each processed image: ~2-5MB
- Room for ~200+ images before needing to archive

## Website Features

- **Fixed header/footer**: Always visible while scrolling
- **Click to zoom**: Click any satellite image to open full-size in new tab
- **Responsive**: Works on mobile, tablet, desktop
- **Fast loading**: Static HTML/CSS, no JavaScript frameworks
- **Map overlays**: Shows what region of Earth was captured

## Troubleshooting

**Site not updating after push?**
- Wait 2-3 minutes for GitHub Pages to rebuild
- Check Settings → Pages to see build status
- Hard refresh your browser (Cmd+Shift+R on Mac)

**Images not displaying?**
- Check file paths match exactly (case-sensitive)
- Verify images are in `images/` folder
- Check image file extensions (.jpg vs .png)

**Need help?**
- GitHub Pages docs: https://docs.github.com/pages
- Check repository Actions tab for build errors

---

Ready to deploy! Let me know when you capture your first satellite image.
