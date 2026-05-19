# GEMINI.md

Instructional context for Gemini CLI when working with the `williamwxz.github.io` project.

## Project Overview
This repository contains the source code for [williamwxz.github.io](https://williamwxz.github.io), the personal project portfolio of William Zhang, an **AI and Data Infrastructure Engineer**. The site serves as a professional showcase of high-scale data platforms, ML infrastructure, and Web3 systems.

### Key Technologies
- **Static Frontend:** Plain HTML5 and CSS3 (no frameworks, no build system).
- **Content:** Markdown for project details (`projects/`) and resumes (`resumes/`).
- **Discovery & SEO:** XML Sitemaps, JSON-LD structured data.
- **AI Agent Integration:** 
  - **WebMCP:** Custom tools exposed via JavaScript (`get_contact_info`, `list_projects`, `get_tech_stack`).
  - **Agent Skills:** RFC-compliant discovery via `.well-known/agent-skills/`.
  - **Content Signals:** Opt-out of training while allowing agent input in `robots.txt`.

## Project Structure
- `index.html`: The main landing page. Contains all styling, project cards, and WebMCP script.
- `projects/`: Markdown files for individual project technical deep dives.
- `resumes/`: Markdown versions of professional resumes.
- `.well-known/agent-skills/`: Metadata for AI agent capability discovery.
- `CLAUDE.md` / `AGENTS.md`: Detailed developer and agent-specific editing instructions.

## Building and Running
As a static site, there is no build process.
- **Local Preview:** Open `index.html` in any web browser.
- **Deployment:** Automatic via GitHub Pages on push to the `master` (default) branch.

## Development Conventions

### Content Guidelines
- **Title/Tagline:** Always use **"AI and Data Infrastructure Engineer"**.
- **Accuracy:** Never fabricate metrics or project details. Only use verified information.
- **Formatting:** Project deep dives should use ASCII diagrams for architecture and maintain a consistent section structure (Overview, Architecture, Key Technical Decisions, Results).

### Site Updates (Sync Checklist)
When adding or updating a project, the following three components **must** be kept in sync:
1. `projects/<slug>.md`: New or updated detail page.
2. `index.html`: Corresponding `.project-card` block and the `projects` array in the WebMCP script.
3. `sitemap.xml`: Entry for the project (without the `.md` extension).

### Styling & UI
- **Tag Colors:**
  - Blue (`tag`): Neutral technologies (Rust, Kafka, S3).
  - Purple (`tag.ai`): AI, ML, Feature Stores, IoT, Autonomous systems.
  - Orange (`tag.web3`): Blockchain, Crypto, DeFi, Solidity.
- **Layout:** Responsive, mobile-first, and print-optimized.

## AI Agent Interaction
This repository is "Agent-Ready." When acting as an agent:
- Refer to `CLAUDE.md` for specific technical editing rules.
- Maintain the JSON-LD `knowsAbout` schema when new skills are added to the portfolio.
- Ensure the `projects` metadata in the `index.html` script remains an accurate reflection of the HTML project cards.
