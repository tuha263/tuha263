# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Architecture

This personal branding project consists of two interconnected repositories:

### Main Repository (tuha263)
- **README.md**: GitHub profile README with dynamic badges, stats, and activity tracking
- **GitHub Workflow**: `.github/workflows/update-readme.yml` - Automated README updates every 6 hours using github-activity-readme action

### GitHub Pages Repository (tuha263.github.io)
- **index.html**: Interactive personal website with retro gaming theme
- **main.js**: Frontend logic for animated stats, typewriter effects, and Snake game initialization
- **snake-game.js**: Complete Snake game implementation with ES6 modules
- **styles.css**: Pixel-art themed CSS with scanlines, animations, and retro aesthetics

## Common Development Commands

### GitHub Actions Workflow
```bash
# Manually trigger README update
gh workflow run update-readme.yml

# View workflow runs
gh run list --workflow=update-readme.yml
```

### Local Development (GitHub Pages)
```bash
# Navigate to GitHub Pages repository
cd ../tuha263.github.io

# Serve locally for testing
python -m http.server 8000
# or
npx serve .
```

### Git Operations
```bash
# Update both repositories simultaneously
cd /mnt/Work/1M/PersonalBranding/tuha263 && git pull && cd ../tuha263.github.io && git pull

# Push changes to both repositories
cd /mnt/Work/1M/PersonalBranding/tuha263 && git push && cd ../tuha263.github.io && git push
```

## Key Components and Architecture

### Profile README Features
- **Dynamic Stats**: GitHub stats, streak stats, and language statistics using Vercel API
- **Activity Section**: Auto-updated via GitHub Actions using jamesgeorge007/github-activity-readme
- **Badge System**: Comprehensive skill and tool badges with for-the-badge style
- **Gaming Theme**: Consistent retro/pixel art aesthetic across all sections

### Personal Website Architecture
- **Modular JavaScript**: ES6 modules with clean separation of concerns
- **Animation System**: Custom counter animations and typewriter effects
- **Snake Game**: Fully functional browser game with high score persistence
- **Responsive Design**: Mobile-friendly with pixel-perfect retro styling
- **Sound Effects**: Hover sound effects using data URIs

### Styling Conventions
- **Theme**: Synthwave/cyberpunk color scheme (#F85D7F, #F8D866, #0D1117)
- **Typography**: Monospace fonts with pixel-art inspired elements
- **Animations**: CSS keyframes for scanlines, glowing effects, and transitions
- **Layout**: Flexbox-based responsive grid system

## Content Management

### README Updates
- Activity section updates automatically via GitHub Actions
- Manual badge updates require editing README.md directly
- Stats are pulled from external APIs (no manual intervention needed)

### Website Updates
- Content changes require editing index.html
- Interactive features controlled via main.js
- Game logic isolated in snake-game.js module
- Visual changes managed through styles.css

## Development Guidelines

### Code Style
- Use ES6+ features consistently in JavaScript
- Maintain modular architecture with clear separation
- Follow semantic HTML structure
- Use CSS custom properties for theme colors
- Implement progressive enhancement for interactive features

### Content Guidelines
- Maintain gaming/developer theme consistency
- Use retro computing terminology and references
- Keep performance metrics realistic and updated
- Ensure all external links remain functional

### Cross-Repository Coordination
- README.md and website should reflect consistent personal branding
- Contact information must be synchronized between both repos
- Theme colors and visual style should remain consistent
- Featured projects should be updated in both locations when relevant