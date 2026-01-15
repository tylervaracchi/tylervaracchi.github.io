# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a static portfolio website for Tyler Varacchi (Lead Technical Artist) hosted on GitHub Pages. It's a single-page application (`index.html`) with embedded CSS and vanilla JavaScript - no build system, no dependencies, no package manager.

## Architecture

**Single-file structure**: The entire website is contained in `index.html` (2192 lines):
- Lines 1-100: HTML head with CSS variables and base styles
- Lines 100-1000: Inline CSS (all styles embedded in `<style>` tag)
- Lines 1000-2070: HTML content (hero, work grid, modals, skills, about, footer)
- Lines 2077-2183: Inline JavaScript (modal handlers, password protection, lightbox)

**Modal-based navigation**: The site uses overlay modals for project details rather than separate pages. Each project card in the work grid opens a corresponding modal with full project details.

**Password protection**: NDA projects (e.g., Nike) require password authentication before viewing. Password is hardcoded in JavaScript at line 2083: `const PORTFOLIO_PASSWORD = 'portfolio2026'`

## Key Components

### Project Modals Structure
Each modal follows this pattern:
- Modal overlay container: `<div class="modal-overlay" id="modal-{project-name}">`
- Modal hero (video/image header) with portrait or landscape orientation
- Modal body with metadata (role, duration, team)
- Problem/Solution sections
- Process images (`.process-grid` with 2-column layout)
- Shipped examples or results
- Tools list (`.tools-list` with `.tool-tag` spans)

### Asset Organization
Assets are organized by project in `/assets/{project-name}/`:
- `aimocap/` - AI Character to Mocap pipeline images
- `burlington/` - Public sculpture renders and photos
- `nike/` - Product visualization colorways (password protected)
- `robot/` - Voice-controlled game screenshots
- `storyboard/` - StoryboardTo3D research images
- `superplastic/` - Mocap pipeline diagrams and process photos
- `thumbnails/` - Grid thumbnail images

### JavaScript Functions
- `openModal(modalId)` - Opens regular project modal, plays videos
- `openPasswordModal(modalId)` - Opens password gate for NDA projects
- `checkPassword()` - Validates password, shows shake animation on failure
- `closeModal()` - Closes modals, stops videos, resets iframes
- `openLightbox(src)` / `closeLightbox()` - Image zoom functionality

## Development Workflow

**No build process**: Edit `index.html` directly and refresh browser.

**Testing locally**:
```bash
# Simple HTTP server (Python 3)
python -m http.server 8000

# Or using Node.js (if available)
npx serve
```

**Deploying**: Changes pushed to `main` branch are automatically deployed via GitHub Pages.

## Design System

All colors, fonts, and spacing are defined in CSS variables (`:root`, lines 47-75):
- **Color scheme**: Dark theme (zinc palette) with blue accent
- **Typography**: Space Grotesk (display), JetBrains Mono (code/mono)
- **Responsive breakpoints**: 768px (tablet), 480px (mobile)

## Common Tasks

### Adding a New Project
1. Add thumbnail to `/assets/{project-name}/thumb-{project-name}.png`
2. Add work card to `.work-grid` (around line 1054) with `onclick="openModal('{project-name}')"`
3. Create modal structure after line 2069 with id `modal-{project-name}`
4. Add project assets to `/assets/{project-name}/`

### Updating Password
Change line 2083: `const PORTFOLIO_PASSWORD = 'your-new-password'`

### Modifying Colors
Edit CSS variables in `:root` (lines 47-75). Colors use Tailwind zinc palette naming.

### Embedded Media
- **Vimeo videos**: Use iframe with `?autoplay=1&muted=1&loop=1` parameters
- **Images**: Use relative paths `assets/{project}/filename.ext`
- **Sketchfab embeds**: Use iframe with `?ui_theme=dark&autostart=1` parameters

## Technical Notes

- **No JavaScript frameworks**: Vanilla JS only, no React/Vue/etc.
- **No CSS preprocessors**: Plain CSS with modern features (CSS variables, grid, flexbox)
- **Cloudflare email protection**: Email addresses are obfuscated via Cloudflare script
- **External dependencies**: Google Fonts only (Space Grotesk, JetBrains Mono)
- **Cross-browser compatibility**: Uses standard CSS/JS, targets modern browsers (CSS Grid, ES6)

## File References

- Portfolio password: `index.html:2083`
- Modal functions: `index.html:2086-2174`
- CSS variables: `index.html:47-75`
- Work grid: `index.html:1054-1142`
- Project modals start: `index.html:1332`
