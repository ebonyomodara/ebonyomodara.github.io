# Ebony Omodara — Portfolio

Static portfolio site. No build step, no framework. Edit content in markdown and JSON, push to GitHub, site updates automatically.


## Quick start

1. Create a GitHub repo named `yourusername.github.io`
2. Upload this entire folder to the repo
3. Go to Settings > Pages > Source: main branch, root
4. Site is live at `https://yourusername.github.io` within a minute


## Folder structure

```
index.html                   Homepage (all sections: hero, projects, about, feeds, contact)
project.html                 Template that renders any project detail page
project-styles.css           Styles for project detail pages

content/
  about.md                   Your about me text (editable)
  projects.json              Project list: titles, descriptions, categories, pills (editable)
  projects/
    project-01.md            Full case study for project 01 (editable)
    project-02.md            Stub — fill in your content
    ...through project-08

assets/
  projects/
    project-01-cover.jpg     ← Replace the .README file with your actual image
    ...                      One cover image per project
  photos/
    profile-01.jpg           ← Your main profile photo (circular, shown in hero)
    profile-02.jpg           ← Second photo (cycles on hover)
    profile-03.jpg           ← Third photo (cycles on hover)
    about-photo.jpg          ← Photo for the about section (portrait, 4:5 ratio)
```


## How to edit

### Change project titles, descriptions, order, or categories

Edit `content/projects.json`. Each project has:

```json
{
  "id": 1,
  "slug": "project-01",          ← Must match the markdown filename
  "title": "Your Project Name",
  "desc": "One-line description shown on the homepage card.",
  "category": "Product Design",  ← Must match a filter button name
  "pills": ["Product Design", "Live App"],
  "cover": "assets/projects/project-01-cover.jpg",
  "coverColor": "linear-gradient(135deg, #1B4DFF 0%, #6B8AFF 100%)",
  "featured": true               ← Shows under the Featured filter
}
```

### Write or edit a case study

Edit `content/projects/project-XX.md`. Format:

```markdown
---
title: Project Name
category: Product Design
pills: [Product Design, Live App]
tools: [Figma, AppSheet]
cover: assets/projects/project-XX-cover.jpg
---

## Section Heading

Your paragraph text here.

- Bullet point
- Another point

**Bold text** for emphasis.
```

### Change your about text

Edit `content/about.md`. Plain markdown.

### Add images

1. Delete the `.README` placeholder in the right folder
2. Add your image with the exact filename referenced in `projects.json` or in the HTML

**Project covers**: `assets/projects/project-XX-cover.jpg`
- Recommended: 1600×900px (16:9), JPG or PNG

**Profile photos**: `assets/photos/profile-01.jpg`, `profile-02.jpg`, `profile-03.jpg`
- These cycle when someone hovers over your photo in the hero
- Square aspect ratio, at least 400×400px

**About photo**: `assets/photos/about-photo.jpg`
- Portrait orientation (4:5 ratio), at least 600×750px

After adding images, update the references in `index.html`:
- Search for `photo-slide` to find where profile photos go
- Search for `about-image` to find the about photo spot
- Project covers are loaded automatically from `projects.json`

### Add a new project

1. Add an entry to `content/projects.json` (copy an existing one, bump the id and slug)
2. Create `content/projects/project-XX.md` (copy a stub, fill it in)
3. Add a cover image to `assets/projects/`
4. Commit

### Change links (LinkedIn, email)

Search `index.html` for `linkedin` and `mailto:` and replace with your real URLs.


## Categories

The filter buttons on the homepage are: Featured, Product Design, Research, Publications. To change them, edit the `<button>` elements in `index.html` (search for `filters`). Make sure the `data-cat` value matches what you use in `projects.json`.


## Previewing locally

Browsers block local `fetch` requests, so you can't just open `index.html` directly. Run:

```
python3 -m http.server 8000
```

Then visit `http://localhost:8000`.


## Design changes

Text and content changes can all be done in GitHub's web editor. For visual/layout changes (CSS, new sections, restructuring), use Claude Code: open the folder, describe what you want, review the diff, push.
