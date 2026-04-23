# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repo Is

Static GitHub Pages portfolio site for William Zhang, a Data Infrastructure Engineer. No build system, no dependencies — everything is plain HTML/CSS/Markdown deployed directly via GitHub Pages.

## Structure

- `index.html` — single-page portfolio (all CSS inline in `<style>`, no external frameworks)
- `projects/*.md` — one Markdown file per project, linked from `index.html` as `href="projects/foo.md"`
- `sitemap.xml`, `robots.txt` — SEO files (robots.txt includes Content Signals for AI preferences)
- `.well-known/agent-skills/index.json` — Agent Skills Discovery index (RFC v0.2.0)
- `.well-known/agent-skills/portfolio-browse/SKILL.md` — skill describing what agents can do on this site

## How to Deploy

Push to `master`. GitHub Pages auto-deploys from the root. There is no build step.

## Editing the Site

**To add or update a project card in `index.html`:** Copy an existing `.project-card` `<a>` block. Keep the `href` pointing to the corresponding `projects/*.md` file.

**Tag color semantics:**
- `tag` (blue) — neutral tech stack items (Kafka, Rust, S3, etc.)
- `tag.ai` (purple) — AI/ML, feature stores, autonomous systems, IoT
- `tag.web3` (orange) — blockchain, crypto, DeFi, Solidity

**To add a project detail page:** Create `projects/<slug>.md` with a frontmatter-style header (`# Title`, `**Timeline:** ...`, `**Stack:** ...`), then sections: `## Overview`, `## Architecture` (ASCII diagram preferred), `## Key Technical Decisions`, `## Results` — match the pattern in existing files.

**Project ordering in `index.html`:** Most impactful / most recent work first. Not strictly chronological.

## When Adding a New Project — Sync Checklist

All three of these must be updated together:

1. **`projects/<slug>.md`** — new detail page
2. **`index.html`** — new `.project-card` block in the Projects section
3. **`sitemap.xml`** — new `<url>` entry with `https://williamwxz.github.io/projects/<slug>` (no `.md` extension in sitemap)

Also check: the JSON-LD `knowsAbout` array in `index.html` `<head>` if new technologies are introduced.

## AI Agent Readiness

The site implements three agent-discoverability standards (the ones feasible on static GitHub Pages):

1. **Content Signals in `robots.txt`** — `ai-train=no, search=yes, ai-input=yes`. Opts out of AI training but allows search indexing and agent input (reading content to answer questions).

2. **WebMCP tools in `index.html`** — a `<script>` at the bottom registers three tools via `navigator.modelContext.provideContext()`: `get_contact_info`, `list_projects` (with optional keyword filter), `get_tech_stack`. The script is a no-op in browsers that don't support WebMCP. When updating projects, the `projects` array in this script must be kept in sync with the project cards above it.

3. **Agent Skills Discovery at `/.well-known/agent-skills/`** — `index.json` follows the Agent Skills Discovery RFC v0.2.0 schema. Points to `portfolio-browse/SKILL.md`. If the SKILL.md content changes, regenerate its SHA-256 digest and update the `digest` field in `index.json`.

**Not feasible on GitHub Pages** (would require Cloudflare or server-side logic): Link response headers (RFC 8288), Markdown content negotiation (Accept: text/markdown), OAuth/OIDC discovery, MCP Server Card.

## When Adding a New Project — WebMCP Sync

In addition to the sync checklist below, also update the `projects` array inside the WebMCP `<script>` block at the bottom of `index.html` with the new project's name, dates, tags, URL, and description.

## Content Rules (from parent CLAUDE.md)

- Title/tagline: "Data Infrastructure Engineer" (NOT "AI Data Infrastructure Engineer")
- Do NOT fabricate projects or metrics — only use details William has confirmed
- Do NOT add "AI" to project names unless it genuinely applies (ML Feature Store is the exception)
- The Snowflake native agent in the Feature Store project uses **Snowflake Cortex**, not LangChain or Claude
- Languages ordered by proficiency in Skills section: Python, Rust, TypeScript, Go, Java, SQL, Solidity
