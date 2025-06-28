# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a GitHub Pages site called "dev-guides" that hosts development guides and technical documentation. The site is built using Jekyll and contains guides organized by category, starting with a comprehensive Claude Code WSL guide.

## Project Structure

```
dev-guides/
├── docs/                    # Main guides directory
│   └── claude-code-wsl/    # Claude Code WSL guide
├── _pages/                 # Jekyll pages
│   └── guides.md          # Guides index page
├── _layouts/              # Jekyll layouts (custom layouts)
├── _config.yml            # Jekyll configuration
├── index.md              # Homepage
├── README.md             # Repository description (Portuguese)
├── Gemfile               # Ruby dependencies
└── CLAUDE.md             # This file
```

## Development Setup

### Prerequisites
- Ruby and Bundler installed
- Jekyll gem installed

### Local Development Commands

```bash
# Install dependencies
bundle install

# Serve site locally
bundle exec jekyll serve

# Build site
bundle exec jekyll build

# Clean build files
bundle exec jekyll clean
```

### GitHub Pages Deployment

The site is configured for GitHub Pages with Jekyll. Push to main branch to deploy automatically.

## Content Guidelines

### File Naming
- Use English for file and directory names
- Use Portuguese for content text
- Follow Jekyll naming conventions

### Guide Structure
Each guide should include:
- Front matter with layout, title, parent, nav_order
- Consistent sections: Pré-requisitos, Instalação, Configuração, Uso Básico, Dicas e Truques, Solução de Problemas, Recursos Adicionais

### Adding New Guides
1. Create directory under `docs/`
2. Add `index.md` with proper front matter
3. Update navigation in `_config.yml` if needed
4. Update guides listing in `_pages/guides.md`

## Site Configuration

- Base URL: `/dev-guides`
- Theme: Minima
- Language: Portuguese (pt-BR)
- Plugins: jekyll-feed, jekyll-sitemap, jekyll-seo-tag