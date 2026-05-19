# Portfolio Browse Skill

Browse William Zhang's data infrastructure engineering portfolio.

## What you can do

- **List projects** — view all 9 portfolio projects with descriptions, dates, and tech tags
- **Filter by technology** — narrow projects by stack (e.g. Rust, Kafka, DeFi, Spark)
- **Get contact info** — retrieve name, email, GitHub, and Telegram links
- **Get tech stack** — view the full technology stack organized by category

## How to use

This site exposes tools via the WebMCP API. If your browser supports `navigator.modelContext`, the following tools are available on page load:

- `get_contact_info()` — returns contact details
- `list_projects({ filter?: string })` — lists projects, optionally filtered by keyword
- `get_tech_stack()` — returns categorized technology skills

## Project detail pages

Each project has a detailed markdown page at `projects/<slug>.md` with architecture diagrams, design decisions, and metrics. These can be fetched directly.

## Site info

- **Owner**: Weixin (William) Zhang
- **Role**: AI and Data Infrastructure Engineer
- **Specialties**: Real-time streaming, ML feature stores, data lakes, DeFi/blockchain data platforms
- **URL**: https://williamwxz.github.io
