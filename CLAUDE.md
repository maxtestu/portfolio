# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Jekyll-based portfolio website for artist Maxime Testu (maximetestu.com). The site showcases artwork through a photo gallery system with custom layouts and minimal design.

## Development Commands

### Ruby Version
This project uses Ruby 3.3.8 via rbenv. The version is specified in `.ruby-version`.

### Running the development server
```bash
bundle exec jekyll serve
```

Note: After changing `_config.yml`, you must restart the server for changes to take effect.

### Installing dependencies
```bash
bundle install
```

## Architecture

### Jekyll Configuration
- **Jekyll version**: 4.4.1
- **Ruby version**: 3.3.8
- **Theme**: Minima 2.5 (with custom overrides)
- **Markdown**: kramdown 2.5.1
- **Site URL**: https://www.maximetestu.com

### Collections System
The site uses Jekyll collections for portfolio items:
- Collection name: `portfolio`
- Location: `_portfolio/` directory
- Output: Individual pages generated for each portfolio item
- Permalink structure: `/:path/`
- Default layout: `photo`

### Portfolio Item Structure
Portfolio items are markdown files in `_portfolio/` with front matter:
```yaml
---
title: "Project Title"
permalink: project-url
photos: ["image1.jpg", "image2.jpg", "image3.jpg"]  # Array of image filenames
external_link: "https://example.com"  # Optional
external_link_text: "Link text"      # Optional
---

Project description content here.
```

All images are stored in `/images/` directory and referenced by filename only (not path).

### Layout System
Three main layouts in `_layouts/`:

1. **home.html** - Homepage layout
   - Displays header and footer
   - Uses Open Graph meta tags with first portfolio item's photo

2. **photo.html** - Portfolio item pages
   - Displays photo galleries using Slick carousel
   - Supports both `photos` array and single `photo` field
   - First photo is followed by content and optional external link
   - Includes back navigation to homepage

3. **page.html** - Standard content pages (e.g., About page)

### Includes System (`_includes/`)
- **header.html** - Site header with name, email, and CV link. Supports optional back navigation.
- **footer.html** - Contains JavaScript for Slick carousel initialization and responsive image sizing
- **image.html** - Reusable image component that takes `photo` parameter
- **head.html** - Meta tags, Open Graph tags, inline CSS includes, Slick carousel dependencies
- **css/reset.css** - CSS reset styles
- **css/style.css** - Custom site styles

### JavaScript Dependencies
Site uses external CDN-hosted libraries:
- jQuery 3.5.1
- Slick Carousel 1.9.0 (for photo galleries)

The footer.html contains custom JavaScript that:
- Initializes Slick carousel for photo galleries
- Handles responsive image sizing
- Waits for all images to load before initializing carousel
- Sets uniform height for gallery images

## Content Management

### Adding New Portfolio Items
1. Create new markdown file in `_portfolio/` directory
2. Use numerical prefix for ordering (e.g., `12-project-name.md`)
3. Add required front matter with title, permalink, and photos array
4. Place images in `/images/` directory
5. Portfolio items appear on homepage in order

### Static Pages
- `index.md` - Homepage (uses home layout)
- `about.md` - About page
- `les-petits-maitres.md` - Teaching/workshop page

## Important Notes

- Image paths in portfolio items should be filenames only, not full paths (e.g., `"photo.jpg"` not `"/images/photo.jpg"`)
- The site uses inline CSS (included via Liquid tags in head.html) rather than separate CSS files
- Slick carousel is initialized dynamically after all images load to ensure proper sizing
- The homepage displays only portfolio items from the `_portfolio` collection
