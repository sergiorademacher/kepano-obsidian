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

| Group | Categories |
|-------|------------|
| **Media** | `[[Books]]`, `[[Movies]]`, `[[Shows]]`, `[[Albums]]`, `[[Games]]`, `[[Podcasts]]` |
| **Content** | `[[Posts]]`, `[[Clippings]]`, `[[Evergreen]]`, `[[Journal]]` |
| **Organization** | `[[People]]`, `[[Companies]]`, `[[Places]]`, `[[Projects]]` |
| **Life** | `[[Meetings]]`, `[[Events]]`, `[[Trips]]`, `[[Recipes]]`, `[[Products]]` |
| **Knowledge** | `[[How-tos]]`, `[[Reference]]`, `[[Topics]]`, `[[Courses]]` |
| **Business** | `[[Work Documents]]` (proposals, invoices, contracts) |
| **Health** | `[[Workouts]]`, `[[Habits]]` |

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

Use the **Topic Template** to create dedicated topic notes that become hubs through backlinks.

### Layer 3: Tags (Status/State)
Tags mark **transient states** or special designations:
- `to-read`, `to-watch` - Queue markers
- `0🌲` - Evergreen note marker
- `note`, `journal` - Note type markers
- `how-to`, `reference`, `topic` - Note type markers
- `categories` - Marks category hub pages
- `processed` - Marks journal entries that have been reviewed

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

**Processing Workflow:** Use `![[Inbox.base]]` to see unprocessed journal entries. Add the `processed` tag after reviewing.

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
2. Review (Inbox.base) → See unprocessed entries
         ↓
3. Process (Clipping) → Extract interesting ideas from sources
         ↓
4. Distill (Evergreen) → Transform into atomic, titled concepts
         ↓
5. Connect → Link evergreen notes to each other
```

### Key Differences from Traditional Zettelkasten
| Traditional | This Vault |
|-------------|------------|
| Numeric IDs | Date-prefixed or descriptive titles |
| Physical cards | Markdown files |
| Slip-box | Categories + Bases |
| Manual index | Automatic backlinks + queries |

---

## New Category Systems

### How-tos (Personal Procedures)
For recurring tasks you need to remember how to do.

**Template:** How-to Template
```yaml
categories:
  - "[[How-tos]]"
topics: []
frequency: Weekly    # Daily, Weekly, Monthly, Yearly
last: 2026-01-28     # When you last did it
```

**Views:** All, By Topic, Recently Done

**Use for:** Pool maintenance, car care, home repairs, software setup procedures.

---

### Reference (Permanent Information)
For static information you need to look up occasionally.

**Template:** Reference Template
```yaml
categories:
  - "[[Reference]]"
type: []              # Bank accounts, Insurance, Subscriptions, Documents
institution:
account:
expires:
```

**Views:** All, By Type, Expiring Soon

**Use for:** Bank accounts, insurance policies, subscriptions, important documents.

**Security Note:** Don't store sensitive credentials - use a password manager. Store only reference info (last 4 digits, contact numbers, etc.).

---

### Topics (Subject Hubs)
For creating explicit topic notes that aggregate related content.

**Template:** Topic Template
```yaml
tags:
  - topic
aliases: []
related: []
```

**Body:** Includes `![[Related.base]]` to automatically show connected notes.

**Use for:** Any subject you want to track across multiple notes (AI, Philosophy, Home maintenance).

---

### Work Documents (Business)
Unified system for proposals, invoices, contracts, and quotes.

**Template:** Work Document Template
```yaml
categories:
  - "[[Work Documents]]"
type: []              # Proposal, Invoice, Contract, Quote
customer: []
project: []
status: Draft         # Draft, Sent, Accepted, Rejected, Paid, Expired
value:
sent:
due:
paid:
```

**Views:** All, Pipeline, Proposals, Invoices, Unpaid, By Customer, By Project, Won, Lost

**Workflow:**
```
Draft → Sent → Accepted → (Create Project)
            → Rejected/Expired

Invoice: Draft → Sent → Paid
```

---

### Courses (Learning)
For tracking online courses and learning resources.

**Template:** Course Template
```yaml
categories:
  - "[[Courses]]"
instructor: []
platform:             # Coursera, Udemy, YouTube, etc.
status: Not Started   # Not Started, In Progress, Completed
progress:             # Percentage or module number
rating:
```

**Views:** All, In Progress, To Start, Completed, By Topic, By Instructor

---

### Workouts (Health)
For tracking exercise sessions.

**Template:** Workout Template
```yaml
categories:
  - "[[Workouts]]"
type: []              # Strength, Cardio, Yoga, etc.
duration:
intensity:            # Low, Medium, High
date: {{date}}
```

**Views:** All, Recent, By Type, This Week, This Month

---

### Habits (Tracking)
For building and tracking habits.

**Template:** Habit Template
```yaml
categories:
  - "[[Habits]]"
frequency: Daily      # Daily, Weekly, Monthly
target:               # What you're aiming for
streak: 0
status: Active        # Active, Paused
```

**Views:** All, Active, Daily, Weekly, Paused

**Structure:** Each habit note includes sections for Why, Cue, Routine, and Reward (based on habit loop science).

---

## Utility Bases

These bases work across categories and can be embedded anywhere.

### Inbox.base
Shows unprocessed journal entries for Zettelkasten workflow.
```markdown
![[Inbox.base]]
```
**Views:** Unprocessed (last 30 days), Recent (7 days), All Unprocessed

**Workflow:** Review entries, then add `processed` tag to clear them from inbox.

---

### Review.base
Shows items needing periodic review based on their frequency setting.
```markdown
![[Review.base]]
```
**Views:** Needs Review, How-tos Due, Never Reviewed

**Works with:** Any note that has `frequency` and `last` properties.

---

### Calendar.base
Shows all dated items in chronological views.
```markdown
![[Calendar.base]]
```
**Views:** Upcoming (30 days), This Week, Past Week, All Dated Items

**Works with:** Any note with `date`, `start`, or `created` properties.

---

### Related.base
Shows notes related to the current note based on shared links.
```markdown
![[Related.base]]
```
Already included in Topic Template. Useful for finding unexpected connections.

---

### Backlinks.base
Shows all notes linking to the current note.
```markdown
![[Backlinks.base]]
```
**Views:** Backlinks, Recent entries

---

## Enhanced Existing Features

### People Template (CRM)
Now includes full CRM capabilities:
```yaml
type: []              # Client, Friend, Family, Colleague
role:
email:
phone:
location:
met:                  # When you first met
last-contact:         # Last interaction
topics: []
```

**Body:** Shows meetings AND work documents for that person.

### People.base New Views
- **Birthdays this month** - Never miss a birthday
- **By Organization** - See all people at a company

### Meetings.base New Views
- **This Week** - Quick view of recent meetings
- **Last 7 Days** - Recent meeting history
- **Recent** - Last 20 meetings

### Products.base New Views
- **Warranties Expiring** - Products with warranties expiring in 90 days

### Everything.base New Views
- **Recently Modified** - Last 30 modified markdown files

---

## Quick Reference: Note Type Decision Tree

```
Is it a quick thought or observation?
  → Journal Template (fleeting note)

Is it from an external source?
  → Clipping Template (literature note)

Is it a distilled, atomic idea?
  → Evergreen Template (permanent note)

Is it a procedure I need to remember?
  → How-to Template

Is it permanent reference info (accounts, docs)?
  → Reference Template

Is it a subject I want to track?
  → Topic Template

Is it tracking something specific (book, movie, person)?
  → Use the appropriate media/entity template

Is it a business document?
  → Work Document Template

Is it tracking learning?
  → Course Template

Is it tracking exercise?
  → Workout Template

Is it a habit to build?
  → Habit Template
```

---

## The Fractal Review Process

Steph Ango's workflow creates layers of review:

```
Daily: Capture thoughts with unique note hotkey
  ↓
Every few days: Review Inbox.base, process journal fragments
  ↓
Weekly: Check Review.base for items needing attention
  ↓
Monthly: Review the month, identify themes
  ↓
Yearly: Review monthly reviews, see the big picture
```

This creates a "fractal web" where you can trace ideas from inception to development.

---

## Getting Started

See [[Getting Started]] for an onboarding checklist that walks through:
- Initial setup
- Understanding the structure
- Trying core workflows
- Customizing for your needs

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
