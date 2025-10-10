# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a personal blog/website built with Hugo static site generator. The site uses a custom theme called "zhubert" located in `themes/zhubert/`. The site is deployed to GitHub Pages and served from the `public/` directory.

## Writing Style

When assisting with blog posts or other written content for this site, refer to `STYLEGUIDE.md` for detailed guidance on Zack's writing voice and style patterns.

## Architecture

- **Hugo Configuration**: Main config is in `hugo.yaml` at the root, with theme-specific config in `themes/zhubert/hugo.toml`
- **Content**: Blog articles and pages are in `content/` directory, written in Markdown
- **Custom Theme**: Located in `themes/zhubert/` with layouts, assets, and styling
- **Static Assets**: Files in `static/` are copied directly to the published site
- **Generated Site**: Hugo builds the site into the `public/` directory for deployment

## Common Commands

**Note**: Hugo must be installed first (`brew install hugo` on macOS)

### Development
- `hugo server` - Start development server with live reload
- `hugo server --drafts` - Include draft content in development server
- `hugo server --bind 0.0.0.0` - Make server accessible on network

### Building
- `hugo` - Build the site for production (outputs to `public/`)
- `hugo --buildDrafts` - Build including draft content
- `hugo --minify` - Build with minified output

### Content Management
- `hugo new articles/new-post.md` - Create a new article
- `hugo new about/index.md` - Create a new page

## Theme Structure

The custom theme in `themes/zhubert/` contains:
- `layouts/`: HTML templates for different page types
- `assets/css/`: Stylesheets (main.css, normalize.css)
- `assets/js/`: JavaScript files
- `static/`: Theme-specific static assets

## Deployment

The site appears to be configured for GitHub Pages deployment, with a `CNAME` file pointing to `zhubert.com`. The `public/` directory contains the built site ready for deployment.

## Requirements

- Hugo minimum version: 0.116.0 (extended version not required)
- Custom theme is self-contained in the repository