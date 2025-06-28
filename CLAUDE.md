# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a GitHub Pages site called "dev-guides" that hosts development guides and technical documentation. The site is built using Jekyll and contains guides organized by category, starting with a comprehensive Claude Code WSL guide.

## Project Structure

```
dev-guides/
├── docs/                           # Main guides directory
│   ├── claude-code-wsl/           # Claude Code WSL guide
│   │   └── index.md
│   └── desenvolvimento/           # Meta-documentation (excluded from site)
│       ├── README.md
│       └── historico-criacao-site-jekyll-github-pages.md
├── assets/                        # Static assets
│   ├── favicon.svg               # Custom favicon
│   └── site.webmanifest         # PWA manifest
├── _includes/                     # Jekyll includes
│   └── head-custom.html          # Custom meta tags (not used)
├── _layouts/                      # Custom Jekyll layouts
│   └── default.html              # Main layout with favicon
├── _pages/                        # Jekyll pages
│   └── guides.md                 # Guides index page
├── screenshots/                   # Local screenshots (gitignored)
├── _config.yml                   # Jekyll configuration
├── .gitignore                    # Git ignore rules
├── index.md                      # Homepage
├── README.md                     # Repository description (Portuguese)
├── Gemfile                       # Ruby dependencies
└── CLAUDE.md                     # This file
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
- URL: `https://varantes.github.io`
- Theme: Minima (~> 2.5)
- Language: Portuguese (pt-BR)
- Plugins: jekyll-feed, jekyll-sitemap, jekyll-seo-tag, jekyll-tagging
- Markdown: Kramdown
- Syntax Highlighter: Rouge

### Excluded from Site Build
- `docs/desenvolvimento/` - Meta-documentation (versioned but not published)
- `screenshots/` - Local screenshots for development

## Content Guidelines

### File Naming
- Use English for file and directory names
- Use Portuguese for content text
- Follow Jekyll naming conventions

### Guide Structure
Each guide should include:
- Front matter with layout, title, parent, nav_order
- Consistent sections: Pré-requisitos, Instalação, Configuração, Uso Básico, Dicas e Truques, Solução de Problemas, Recursos Adicionais

### Front Matter Template for New Guides
```yaml
---
layout: default
title: Guide Name
parent: Guias de Desenvolvimento
nav_order: X
description: "Concise description for SEO"
tags: [tag1, tag2, tag3, technical-keywords]
keywords: "keyword1, keyword2, keyword3"
canonical_url: "https://varantes.github.io/dev-guides/docs/guide-name/"
author: "Valdemar Arantes Neto"
date: YYYY-MM-DD
last_modified_at: YYYY-MM-DD
---
```

### Adding New Guides
1. Create directory under `docs/`
2. Add `index.md` with proper front matter
3. Update navigation in `_config.yml` if needed
4. Update guides listing in `_pages/guides.md`
5. Include badges for visual identity: `![Badge](https://img.shields.io/badge/Technology-Color?style=flat&logo=logo&logoColor=white)`

## Meta-Documentation

### docs/desenvolvimento/
This directory contains development documentation that is:
- **Versioned in Git** for transparency
- **Excluded from Jekyll build** (not published on GitHub Pages)
- Used for project history, decisions, and process documentation

### Adding Development Documentation
1. Create files in `docs/desenvolvimento/`
2. Use descriptive filenames: `historico-feature-X.md`, `decisoes-arquitetura-Y.md`
3. Commit to Git normally - Jekyll will exclude from site automatically

## SEO and Optimization

### Tags and Keywords
- Use `tags:` array in front matter for functional tagging
- Include `keywords:` string for search optimization
- Optimize for both traditional search engines and LLMs
- Include technical terms and variations

### Favicon and PWA
- Custom SVG favicon in `assets/favicon.svg`
- PWA manifest in `assets/site.webmanifest`
- Theme color: `#2B2D42`

## Git Workflow

### SSH Setup (Required)
```bash
ssh-keyscan github.com >> ~/.ssh/known_hosts
git remote set-url origin git@github.com:varantes/dev-guides.git
ssh -T git@github.com  # Test connection
```

### Commit Conventions
- `feat:` - New features or guides
- `docs:` - Documentation updates
- `fix:` - Bug fixes
- `style:` - Formatting, badges, visual improvements
- `config:` - Configuration changes
- `chore:` - Maintenance tasks

## Site Configuration Details