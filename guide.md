# Edge Computing Group Website UPRM - Maintenance Guide

## Overview
This comprehensive guide explains how to maintain and update the Edge Computing Group website at UPRM. It covers the essential files and folders you'll need to work with, along with detailed instructions for common tasks.

**Author:** Jacob M. Delgado López

## Directory Structure

### Core Data Folders
- `_data/`
  - Contains structured data in YAML format
  - Key files:
    - `members.yml`: Lab member information (names, roles, images)
    - `publications.yml`: Research publications database

### Template Components
- `_includes/`
  - HTML components for website elements
  - Notable modifications:
    - Footer template (modified to include UPRM logo)

### Layout and Content
- `_layouts/`
  - Base HTML templates for page structures
  - ⚠️ No modifications needed for basic maintenance

- `_posts/`
  - Blog post storage (potential future News section)
  - ⚠️ Currently unused

### Assets
- `assets/`
  - `css/`
    - `beautifuljekyll.css`: Main styling file (customized)
  - `img/`
    - Original template images
    - ⚠️ Preserve as reference
  - `js/`
    - Jekyll JavaScript files
    - ⚠️ No modifications needed

### Media Content
- `images/`
  - `lab_photos/`: Group photographs
  - `members/`: Individual member portraits

### Content Pages
- `pages/`
  - Markdown files for navbar-linked pages
  - Each file corresponds to a navigation menu item

## Key Files for Regular Updates

### 1. Homepage (`index.html`)
Commonly updated elements:
- Home image
- Welcome text
- PI's contact information

### 2. Configuration (`_config.yml`)
Critical settings:
- Navigation bar structure
- Website color scheme
- Global site parameters

### 3. Team Information (`members.yml`)
To add a new member:
1. Locate appropriate section (Postdoc/PhD/Master's)
2. Copy an existing entry as template
3. Update with new member's information:
   ```yaml
   - name: "Name"
     role: "Role"
     image: "path/to/image.jpg"
     # Additional fields as needed
   ```

### 4. Publications (`publications.yml`)
To add new research:
1. Copy existing entry format
2. Update with publication details:
   ```yaml
   - title: "Paper Title"
     authors: "Author List"
     venue: "Conference/Journal"
     year: YYYY
     # Additional fields as needed
   ```

### 5. Lab Photos (`lab_photos.md`)
- Displays chronological group photos
- Add new photos in reverse chronological order

## Best Practices
1. Always backup files before making changes
2. Test changes locally before deploying
3. Maintain consistent formatting in YAML files
4. Use optimized images to maintain site performance

## Support
If you need assistance, contact:
- Current lab administrator
- Dr. Wilfredo for access permissions

## Legacy Note
From the original author:
> I hope this guide helps maintain and improve the website! Please say hello to Dr. Wilfredo and the lab members for me. Best wishes for your research!

---
*Last updated: December 2024*