---
categories:
  - "[[Posts]]"
author:
  - "[[Me]]"
created: 2026-02-04
topics:
  - "[[Evergreen]]"
tags:
  - note
---

# Understanding This Vault's Methodology

This vault uses a **bottom-up approach** to note-taking, designed for speed and laziness. Rather than forcing content into predefined hierarchies, structure emerges organically through links, tags, and categories.

## Core Philosophy

### File Over App
Notes are just markdown files you control. No proprietary formats, no lock-in. This ensures your knowledge persists beyond any single tool.

### Embrace Chaos
Don't overthink where things go. The system is designed so you can throw notes anywhere and find them later through links and queries.

### Speed Over Organization
The overhead of "where should this go?" kills momentum. This system minimizes that friction.

---

## Key Principles

| Principle | Implementation |
|-----------|----------------|
| Avoid multiple vaults | Everything in one place |
| Avoid folders for organization | Use links and tags instead |
| Always pluralize categories | `[[Books]]` not `[[Book]]` |
| Use internal links profusely | Link first mentions |
| Use YYYY-MM-DD dates | Consistent sorting |
| Use 7-point rating scale | Simple, meaningful ratings |
| Unresolved links are valuable | Breadcrumbs for future connections |

---

## The Three-Layer System

### Layer 1: Categories (What it IS)
Categories define the **type** of content. A note belongs to one primary category based on what it fundamentally is.

**Current Categories:**
- Media: `[[Books]]`, `[[Movies]]`, `[[Shows]]`, `[[Albums]]`, `[[Games]]`, `[[Podcasts]]`
- Content: `[[Posts]]`, `[[Clippings]]`, `[[Evergreen]]`, `[[Journal]]`
- Organization: `[[People]]`, `[[Companies]]`, `[[Places]]`, `[[Projects]]`
- Life: `[[Meetings]]`, `[[Events]]`, `[[Trips]]`, `[[Recipes]]`, `[[Products]]`

### Layer 2: Topics (What it's ABOUT)
Topics describe the **subject matter**. A note can have multiple topics because ideas cross domains.

Example: A book about AI might have:
```yaml
categories:
  - "[[Books]]"
topics:
  - "[[Artificial Intelligence]]"
  - "[[Philosophy]]"
  - "[[Technology]]"
```

### Layer 3: Tags (Status/State)
Tags mark **transient states** or special designations:
- `to-read`, `to-watch` - Queue markers
- `0🌲` - Evergreen note marker
- `note`, `journal` - Note type markers
- `categories` - Marks category hub pages

---

## How Dependencies Work

### Templates → Categories
Each template creates notes that link back to their category:
```yaml
categories:
  - "[[Books]]"  # This links the note to the Books category
```

### Categories → Bases (Databases)
Each category page embeds a `.base` file that queries all notes linking to it:
```markdown
![[Books.base]]
```

### Bases → Filters
The `.base` files use formulas to filter and display related content:
```yaml
filters:
  and:
    - tags.contains("0🌲")
    - '!file.name.contains("Template")'
```

### The Flow
```
Template → creates Note → links to Category → displayed via Base query
```

---

## Zettelkasten Implementation

This vault adapts Zettelkasten principles in a practical way:

### Fleeting Notes → Journal Fragments
Use the **unique note hotkey** (Cmd/Ctrl+Shift+N) to capture quick thoughts. These get timestamped `YYYY-MM-DD HHmm` automatically.

The Journal Template creates fleeting notes:
```yaml
tags:
  - note
  - journal
```

### Literature Notes → Clippings
When you read something worth preserving, use the **Clipping Template**:
```yaml
categories:
  - "[[Clippings]]"
author: []
url: ""
topics: []
```

Clippings preserve source material with attribution. They're raw material for future thinking.

### Permanent Notes → Evergreen Notes
When ideas crystallize, create an **Evergreen Note** using the Evergreen Template:
```yaml
tags:
  - 0🌲
```

Evergreen notes are:
- **Atomic**: One idea per note
- **Titled as propositions**: "[[Everything is a remix]]", "[[Calmness is a superpower]]"
- **Composable**: Built from and linked to other ideas
- **Timeless**: The idea, not the source

### The Zettelkasten Workflow in This Vault

```
1. Capture (Journal) → Quick thoughts throughout the day
         ↓
2. Process (Clipping) → Extract interesting ideas from sources
         ↓
3. Distill (Evergreen) → Transform into atomic, titled concepts
         ↓
4. Connect → Link evergreen notes to each other
```

### Key Differences from Traditional Zettelkasten
| Traditional | This Vault |
|-------------|------------|
| Numeric IDs | Date-prefixed or descriptive titles |
| Physical cards | Markdown files |
| Slip-box | Categories + Bases |
| Manual index | Automatic backlinks + queries |

---

## Creating a Topics Category

**Should you create a `[[Topics]]` category?**

Generally **no** - topics work differently than categories:

### Topics Are Not a Category
Topics are a **property** on notes, not a category of content. A topic like `[[Artificial Intelligence]]` is linked via the `topics:` field, not the `categories:` field.

### What You SHOULD Do Instead

**Option 1: Topic Notes (Recommended)**
Create notes for each topic you want to track. These become natural hubs through backlinks:

```markdown
# Artificial Intelligence.md
---
tags:
  - topic
---

AI encompasses machine learning, neural networks, and cognitive systems.

![[Related.base]]
```

**Option 2: Topic as Evergreen**
Some topics are themselves ideas worth capturing:
```markdown
# Emergence.md
---
tags:
  - 0🌲
---

Emergence is when complex behavior arises from simple rules.
```

**Option 3: Base Query for Topics**
Create a base that shows all notes with a specific topic:
```yaml
filters:
  - topics.contains("[[Artificial Intelligence]]")
```

---

## Handling Different Note Types

### Temporary/Fleeting Notes
**Where:** `Notes/` folder or root
**Template:** Journal Template
**Lifecycle:** Review every few days, then either:
- Delete if not valuable
- Promote to Clipping if it's from a source
- Promote to Evergreen if it's a distilled idea
- Keep as a working note

### Literature Notes (Clippings)
**Where:** `Clippings/` folder
**Template:** Clipping Template
**Purpose:** Preserve source material with attribution
**Lifecycle:** Permanent reference material; mine for Evergreen ideas

### Permanent Notes (Evergreen)
**Where:** `Notes/` folder (or root)
**Template:** Evergreen Template
**Purpose:** Atomic, composable ideas
**Lifecycle:** Permanent; continuously refined and connected

### Working Notes
**Where:** `Notes/` folder
**Template:** None specific (or Journal)
**Purpose:** Active thinking, research, projects
**Lifecycle:** May become posts, may be archived, may spawn Evergreen notes

---

## Suggested How-To Guides

Based on this methodology, here are guides that would be valuable:

### Essential Guides
1. **How to Capture Fleeting Thoughts** - Using the unique note hotkey and journal workflow
2. **How to Process Clippings into Evergreen Notes** - The transformation workflow
3. **How to Create Composable Evergreen Notes** - Writing atomic, linkable ideas
4. **How to Use the Daily Review Workflow** - Fractal review process (daily → weekly → monthly)

### Category-Specific Guides
5. **How to Track Books and Reading** - Using the Book template and rating system
6. **How to Maintain a Personal CRM** - People, meetings, and relationship tracking
7. **How to Plan and Document Trips** - Trip template and place connections
8. **How to Track Media Consumption** - Movies, shows, podcasts, games

### Advanced Guides
9. **How to Create Custom Bases (Databases)** - Building filtered views
10. **How to Add a New Category** - Template, category page, and base creation
11. **How to Connect Ideas Across Domains** - Using topics and links effectively
12. **How to Use Unresolved Links Strategically** - Breadcrumbs for future thinking

### Workflow Guides
13. **How to Do Weekly Reviews** - Compiling journal fragments
14. **How to Search and Find Notes** - Using backlinks, tags, and queries
15. **How to Maintain the Vault Long-Term** - Pruning, refining, and evolving

---

## Quick Reference: Note Type Decision Tree

```
Is it a quick thought or observation?
  → Journal Template (fleeting note)

Is it from an external source?
  → Clipping Template (literature note)

Is it a distilled, atomic idea?
  → Evergreen Template (permanent note)

Is it tracking something specific (book, movie, person)?
  → Use the appropriate media/entity template

Is it active work or research?
  → Keep as a working note in Notes/
```

---

## The Fractal Review Process

Steph Ango's workflow creates layers of review:

```
Daily: Capture thoughts with unique note hotkey
  ↓
Every few days: Review journal fragments, extract salient points
  ↓
Monthly: Review the reviews, identify themes
  ↓
Yearly: Review monthly reviews, see the big picture
```

This creates a "fractal web" where you can trace ideas from inception to development.

---

## Summary

This vault prioritizes:
- **Speed** over perfect organization
- **Links** over folders
- **Emergence** over hierarchy
- **Composability** over completeness

The system works because it's designed for how humans actually think - messily, associatively, and iteratively.

---

**Sources:**
- [How I use Obsidian — Steph Ango](https://stephango.com/vault)
- [kepano/kepano-obsidian on GitHub](https://github.com/kepano/kepano-obsidian)
