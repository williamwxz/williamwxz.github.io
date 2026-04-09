# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repo Is

Static GitHub Pages portfolio site for William Zhang, a Data Infrastructure Engineer. No build system, no dependencies — everything is plain HTML/CSS/Markdown deployed directly via GitHub Pages.

## Structure

- `index.html` — single-page portfolio (all CSS inline in `<style>`, no external frameworks)
- `projects/*.md` — one Markdown file per project, linked from `index.html` as `href="projects/foo.md"`
- `sitemap.xml`, `robots.txt` — SEO files

## How to Deploy

Push to `master`. GitHub Pages auto-deploys from the root. There is no build step.

## Editing the Site

**To add or update a project card in `index.html`:** Copy an existing `.project-card` `<a>` block. Keep the `href` pointing to the corresponding `projects/*.md` file. Use existing CSS classes: `tag`, `tag.ai`, `tag.web3`, `skill-tag`.

**To add a project detail page:** Create `projects/<slug>.md` with frontmatter-style header (`# Title`, `**Timeline:** ...`, `**Stack:** ...`), then an `## Overview`, `## Architecture` (ASCII diagram preferred), `## Key Technical Decisions`, and `## Results` section — match the pattern in existing files.

**Project ordering in `index.html`:** Most recent first.

## Content Rules (from parent CLAUDE.md)

- Title/tagline: "Data Infrastructure Engineer" (NOT "AI Data Infrastructure Engineer")
- Do NOT fabricate projects or metrics — only use details William has confirmed
- Do NOT add "AI" to project names unless it genuinely applies (ML Feature Store is the exception)
- The Snowflake native agent in the Feature Store project uses **Snowflake Cortex**, not LangChain or Claude
- Languages ordered by proficiency in Skills section: Python, Rust, TypeScript, Go, Java, SQL, Solidity
