# Manus Skills Repository

A comprehensive skill library for the [Manus AI agent platform](https://manus.im). This repository contains **634+ skills** spanning business, technology, creative, legal, and operational domains — each designed to be loaded and executed by Manus agents on demand.

---

## What Is This Repository?

This is a structured knowledge base where each **skill** teaches a Manus agent how to perform a specific task or operate within a specific domain. Skills cover everything from cloud security and cinematography to sales analytics and litigation strategy.

Manus uses a three-level loading system:

1. **Metadata** (always loaded) — YAML frontmatter in each `SKILL.md` triggers skill activation based on context.
2. **SKILL.md body** (loaded on activation) — concise operational guide with frameworks, decision trees, and best practices.
3. **Reference files** (loaded on demand) — deep-dive content in `references/` subdirectories for specific topics.

## Repository Structure

```
manus/
├── README.md                          # This file
├── skill-name/
│   ├── SKILL.md                       # Main skill file (required)
│   └── references/                    # Detailed reference material (optional)
│       ├── topic-one.md
│       ├── topic-two.md
│       └── ...
├── another-skill/
│   ├── SKILL.md
│   └── references/
│       └── ...
└── ...  (634+ skill directories)
```

Each skill directory is self-contained. The directory name serves as the skill identifier (e.g., `cloud-security`, `sales-analytics`, `cinematography`).

## Skill Categories

| Category | Examples |
|---|---|
| **Advertising & Marketing** | Meta Ads, Google Ads, LinkedIn Ads, TikTok Ads, SEO |
| **Business & Operations** | Sales Analytics, Account Management, Customer Success |
| **Creative & Production** | Cinematography, Video Editing, Lighting Techniques |
| **Finance & Accounting** | Financial Modeling, Budgeting, Tax Planning |
| **Legal & Compliance** | Litigation, Compliance Management, Contract Review |
| **Project Management** | Agile, Product Roadmapping, Feature Prioritization |
| **Technology & Engineering** | Cloud Security, API Development, DevOps |

## How to Use

### For Manus Agents
Skills are automatically discovered and loaded by the Manus platform. The `description` field in each skill's YAML frontmatter serves as the primary trigger — Manus reads it to decide when to activate a skill.

### For Contributors
1. Each skill follows a consistent format: YAML frontmatter + Markdown body in `SKILL.md`.
2. Reference files in `references/` provide deeper content that agents load on demand.
3. Keep `SKILL.md` under 500 lines — use reference files for detailed material.
4. Use the skill template (`Template.md`) for creating new skills.

### Browsing Skills
Browse skill directories to explore available capabilities. Each `SKILL.md` contains:
- **Frontmatter**: title, description, category, tags, difficulty, prerequisites, related skills
- **Body**: operational frameworks, decision guides, best practices, and reference file pointers

## Contributing

To add a new skill:
1. Create a directory with a kebab-case name (e.g., `my-new-skill/`)
2. Add a `SKILL.md` following the standard template format
3. Optionally add `references/` with supporting deep-dive documents
4. Ensure cross-references point to existing skills

## License

This repository is maintained as part of the Manus AI platform ecosystem.
