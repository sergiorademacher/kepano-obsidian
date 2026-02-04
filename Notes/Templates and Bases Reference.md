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

# Templates and Bases Reference

This document explains every template and base in this vault, how they work, and when to use each one.

---

## Understanding the Architecture

### How Templates Work
Templates are markdown files with YAML frontmatter that get inserted when you create new notes. They:
- Define the **properties** (metadata fields) for that note type
- Set the **category** link that connects the note to its collection
- Auto-fill dates using `{{date}}`
- Often embed **bases** to show related content

### How Bases Work
Bases (`.base` files) are database definitions that:
- **Filter** notes based on criteria (categories, tags, properties)
- **Display** selected columns with custom names
- **Sort** results by various fields
- **Calculate** formulas for derived values
- Provide **multiple views** for different contexts

### The Connection Pattern
```
Template creates Note → Note links to [[Category]] → Base queries notes with that category
```

---

## Content Templates (For Writing)

### Daily Note Template
**Purpose:** Daily journal entry
**Use When:** Creating a daily note (usually automatic via Obsidian settings)
**Properties:**
- `tags: [daily]`

**Body:** Embeds `![[Daily.base]]` to show related notes from that day.

**How to Use:**
1. Use Cmd/Ctrl+P → "Open today's daily note"
2. Write your daily reflections
3. Link to other notes with `[[Note Name]]`

---

### Journal Template
**Purpose:** Timestamped fleeting thoughts (Zettelkasten fleeting notes)
**Use When:** Capturing quick ideas throughout the day
**Properties:**
- `created: {{date}}`
- `tags: [note, journal]`

**How to Use:**
1. Press unique note hotkey (configured in zk-prefixer)
2. Auto-creates note named `YYYY-MM-DD HHmm`
3. Write your thought quickly
4. Review these periodically to extract evergreen ideas

---

### Monthly Note Template
**Purpose:** Monthly review and compilation
**Use When:** Creating monthly review notes
**Properties:**
- `aliases: [July 2023]` (human-readable month name)
- `previous: [[2023-06]]` (link to prior month)
- `next: [[2023-08]]` (link to next month)
- `tags: [monthly]`

**Body:** Embeds `![[Daily.base#Monthly]]` to show all entries from that month.

---

### Evergreen Template
**Purpose:** Permanent, atomic ideas (Zettelkasten permanent notes)
**Use When:** Distilling a concept into a standalone, titled idea
**Properties:**
- `created: {{date}}`
- `tags: [0🌲]` (evergreen marker)

**How to Use:**
1. Name the note as a proposition: "Everything is a remix"
2. Write one atomic idea per note
3. Link to related evergreen notes
4. These form your knowledge graph

---

### Post Template
**Purpose:** Written articles/essays for potential publication
**Use When:** Writing blog posts, essays, or articles
**Properties:**
- `categories: [[Posts]]`
- `author: [[Me]]`
- `url:` (link when published)
- `created: {{date}}`
- `published:` (date of publication)
- `topics: []`
- `status:` (Draft, Published, etc.)

---

### Clipping Template
**Purpose:** Saved excerpts from external sources (Zettelkasten literature notes)
**Use When:** Saving interesting content from the web, books, or articles
**Properties:**
- `categories: [[Clippings]]`
- `tags: [clippings]`
- `author: []`
- `url: ""` (source URL)
- `created: {{date}}`
- `published:` (original publication date)
- `topics: []`

**How to Use:**
1. Copy the interesting excerpt
2. Create note with Clipping Template
3. Fill in source attribution
4. Add topics for future discovery
5. Review clippings to extract evergreen ideas

---

### Quote Template
**Purpose:** Memorable quotes worth preserving
**Use When:** Saving a quote you want to remember
**Properties:**
- `categories: [[Quotes]]`
- `attribution: []` (who said it)
- `source:` (where you found it)
- `created: {{date}}`
- `topics: []`
- `via:` (who shared it with you)

---

### Meditation Template
**Purpose:** Contemplative journal entries
**Use When:** Recording meditation experiences or reflective moments
**Properties:**
- `categories: [[Meditations]]`
- `tags: [note, journal, meditation]`
- `created: {{date}}`
- `loc: []` (location)
- `topics: []`

---

### Email Template
**Purpose:** Important email threads worth preserving
**Use When:** Saving significant email conversations
**Properties:**
- `categories: [[Emails]]`
- `created: {{date}}`
- `org: []` (organization)
- `people: []` (participants)
- `url:` (link to email)
- `topics:`

---

## Media Templates (For Tracking Consumption)

### Book Template
**Purpose:** Track books read and to-read
**Use When:** Adding a book to your library
**Properties:**
- `categories: [[Books]]`
- `author: []`
- `cover:` (image URL)
- `genre: []`
- `pages:`
- `isbn:` / `isbn13:`
- `year:`
- `rating:` (1-7 scale)
- `topics: []`
- `created: {{date}}`
- `last:` (date finished)
- `via: ""` (who recommended it)
- `tags: [to-read]` (remove when finished)

**Workflow:**
1. Add book with `to-read` tag
2. When finished, add `rating` and `last` date
3. Remove `to-read` tag

---

### Movie Template
**Purpose:** Track movies watched and watchlist
**Use When:** Adding a movie
**Properties:**
- `categories: [[Movies]]`
- `cover:`
- `genre: []`
- `director:`
- `cast: []`
- `runtime:` (minutes)
- `rating:`
- `year:`
- `last: {{date}}` (when watched)
- `imdbId:`
- `via:` (recommendation source)

**Views Available:**
- All movies, To-watch (no rating/last), Favorites (rating > 6)
- By Actor, Genre, Director, Soundtrack, Theater

---

### Show Template
**Purpose:** Track TV series
**Properties:**
- `categories: [[Shows]]`
- `genre: []`
- `year:`
- `cast: []`
- `rating:`
- `created: {{date}}`
- `last: {{date}}`

---

### Show Episode Template
**Purpose:** Track individual episodes (for detailed tracking)
**Properties:**
- `categories: [[Show episodes]]`
- `show:` (link to show)
- `season:`
- `episode:`
- `rating:`
- `published:`

---

### Album Template
**Purpose:** Track music albums
**Properties:**
- `categories: [[Albums]]`
- `genre: []`
- `artist: ""`
- `year:`
- `created: {{date}}`
- `rating:`

---

### Video Game Template
**Purpose:** Track video games
**Properties:**
- `categories: [[Games]]`
- `maker:` (studio)
- `genre: []`
- `year:`
- `system:` (platform)
- `rating:`
- `created: {{date}}`
- `last: {{date}}`

---

### Board Game Template
**Purpose:** Track board games
**Properties:**
- `categories: [[Board games]]`
- `type: []`
- `maker:`
- `year:`
- `rating:`
- `last: {{date}}`

---

### Podcast Template
**Purpose:** Track podcast shows
**Properties:**
- `categories: [[Podcasts]]`
- `host: []`
- `rating:`

**Body:** Embeds `![[Podcast episodes.base#Show]]` to list episodes.

---

### Podcast Episode Template
**Purpose:** Track individual podcast episodes
**Properties:**
- `categories: [[Podcast episodes]]`
- `tags: [podcast, episodes]`
- `show:` (link to podcast)
- `guests:`
- `topics: []`
- `episode:`
- `url:`
- `rating:`
- `published:`
- `last: {{date}}`

---

## People & Organization Templates

### People Template
**Purpose:** Track people you know (personal CRM)
**Properties:**
- `categories: [[People]]`
- `birthday:`
- `org: []` (organizations)
- `created: {{date}}`

**Body:** Embeds `![[Meetings.base#Person]]` to show all meetings with this person.

---

### Contact Template
**Purpose:** Quick contact info (simpler than People)
**Properties:**
- `categories: [[People]]`
- `phone:`
- `twitter:`
- `org:`

---

### Company Template
**Purpose:** Track companies/organizations
**Properties:**
- `categories: [[Companies]]`
- `type: []`
- `people: []`
- `url:`

---

### Project Template
**Purpose:** Track projects
**Properties:**
- `categories: [[Projects]]`
- `type: []`
- `org: []`
- `start:`
- `year:`
- `url:`
- `status:`

---

### Meeting Template
**Purpose:** Document meetings
**Use When:** Taking meeting notes
**Properties:**
- `categories: [[Meetings]]`
- `type: []` (1:1, Team, Client, etc.)
- `date: {{date}}`
- `org:`
- `loc:`
- `people: []`
- `topics: []`

---

### Meeting Type Template
**Purpose:** Define meeting types (for filtering)
**Properties:**
- `tags: [meetings/type]`

**Body:** Embeds `![[Meetings.base#Type]]` to show meetings of this type.

---

### Meetings List Template
**Purpose:** Embed a meetings list anywhere
**Body:** Just `![[Meetings.base#Person]]`

---

### Event Template
**Purpose:** Track events (concerts, conferences, etc.)
**Properties:**
- `categories: [[Events]]`
- `tags: [events]`
- `type:`
- `start:`
- `end:`
- `loc:`

---

### Conference Template
**Purpose:** Track conferences specifically
**Properties:**
- `categories: [[Events]]`
- `type: [[Conferences]]`
- `series:`
- `start:`
- `end:`
- `loc:`
- `tags: [events, conferences]`

---

### Conference Session Template
**Purpose:** Track talks/sessions at conferences
**Properties:**
- `categories: [[Conference sessions]]`
- `conference:`
- `speaker:`
- `topics: []`
- `rating:`
- `last: {{date}}`
- `tags: [conferences, sessions, events]`

---

### Trip Template
**Purpose:** Document trips/travel
**Properties:**
- `categories: [[Trips]]`
- `start:`
- `end:`
- `loc:`

---

### Job Interview Template
**Purpose:** Track job interviews
**Properties:**
- `categories: [[Meetings]]`
- `type: [[Job Interviews]]`
- `org:`
- `people: []`
- `date: {{date}}`
- `role:`
- `rating:`

**Body:** Sections for "Questions and topics" and "Notes"

---

### Hosting Template
**Purpose:** Track when you host guests
**Properties:**
- `categories: [[Hosting]]`
- `start:`
- `end:`
- `loc:`
- `people: []`

---

## Place Templates

### Place Template
**Purpose:** Track places you've visited
**Properties:**
- `categories: [[Places]]`
- `type: []` (Restaurant, Park, etc.)
- `loc: []` (city/region)
- `rating:`
- `created: {{date}}`
- `last: {{date}}`

---

### City Template
**Purpose:** Track cities with geographic data
**Properties:**
- `categories: [[Places]]`
- `type: [[Cities]]`
- `loc:`
- `rating:`
- `created: {{date}}`
- `last:`
- `coordinates: ["lat", "long"]`

**Body:** Embeds trips, map, and places in that city.

---

### Restaurant Template
**Purpose:** Track restaurants (specialization of Place)
**Properties:**
- `categories: [[Places]]`
- `type: [[Restaurants]]`
- `loc:`
- `rating:`
- `created: {{date}}`
- `last: {{date}}`

---

### Place Type Template
**Purpose:** Define place types for filtering
**Properties:**
- `tags: [places/types]`

**Body:** Embeds `![[Map.base#Type]]` and `![[Places.base#Type]]`

---

### Real Estate Template
**Purpose:** Track real estate properties
**Properties:**
- `categories: [[Places]]`
- `type: []`
- `address:`
- `rating:`
- `created: {{date}}`
- `url:`
- `year:` (built)
- `price:`
- `sqft:`
- `lotsqft:`
- `loc: []`
- `status:`

---

## Product Templates

### Product Template
**Purpose:** Track owned products with cost-per-use analysis
**Properties:**
- `categories: [[Products]]`
- `type:`
- `maker:`
- `model:`
- `rating:`
- `price:`
- `acquired: {{date}}`
- `monthly-uses:`

**Base calculates:**
- Months owned
- Total uses
- Cost per use

---

### Product Type Template
**Purpose:** Define product types for filtering
**Properties:**
- `tags: [products/types]`

**Body:** Embeds `![[Products.base#Type]]`

---

### App Template
**Purpose:** Track apps/software
**Properties:**
- `categories: [[Apps]]`
- `maker: ""`
- `rating:`

---

### Recipe Template
**Purpose:** Store recipes
**Properties:**
- `categories: [[Recipes]]`
- `cuisine:`
- `type: []`
- `ingredients:`
- `author: []`
- `url:`
- `rating:`
- `created: {{date}}`
- `last: {{date}}`

**Body:** Sections for Ingredients, Directions, Notes

---

### Food Template
**Purpose:** Track food products
**Properties:**
- `categories: [[Food]]`
- `maker:`
- `rating:`
- `price:`
- `last: {{date}}`
- `created: {{date}}`

---

### Coffee Template
**Purpose:** Track coffee beans/roasts
**Properties:**
- `categories: [[Coffee]]`
- `maker:` (roaster)
- `producer:` (farm)
- `country: []`
- `variety:`
- `process:`
- `rating:`
- `last:`

---

### Stock Trade Template
**Purpose:** Track investment trades
**Properties:**
- `date: {{date}}`
- `trade:`
- `tags: [investment, trade]`
- `price:`
- `shares:`

---

## Creator Templates (For Linking)

These create People entries with specialized views:

### Author Template
**Properties:** `categories: [[People]]`, `type: [[Authors]]`
**Body:** Embeds `![[Books.base#Author]]`

### Director Template
**Properties:** `categories: [[People]]`, `type: [[Directors]]`
**Body:** Embeds `![[Movies.base#Director]]`

### Actor Template
**Properties:** `categories: [[People]]`, `type: [[Actors]]`
**Body:** Embeds `![[Movies.base#Actor]]`

### Musician Template
**Properties:** `categories: [[People]]`, `type: [[Musicians]]`
**Body:** Embeds `![[Albums.base#Artist]]`

### Game Studio Template
**Properties:** `categories: [[Companies]]`, `type: [[Game studios]]`
**Body:** Embeds `![[Games.base#Studio]]`

---

## Genre Templates

These create genre notes that filter media:

### Genre Template
`tags: [genres]` → Embeds `![[Genre.base]]`

### Music Genre Template
`tags: [music/genres]` → Embeds `![[Albums.base#Genre]]`

### Movie Genre Template
`tags: [movies/genres]` → Embeds `![[Movies.base#Genre]]`

### Video Game Genre Template
`tags: [games/genres]` → Embeds `![[Games.base#Genre]]`

---

## Base Reference

### Utility Bases

#### Related.base
**Purpose:** Find notes related to the current note
**Logic:** Shows notes that share 2+ links OR directly link to/from current note
**Formulas:**
- `LinksOverlap`: Count of shared links
- `TagsOverlap`: Count of shared tags
- `BacklinksCount`: Number of backlinks

**Use:** Embed `![[Related.base]]` in any note to see related content.

---

#### Backlinks.base
**Purpose:** Show all notes linking to current note
**Views:**
- Backlinks: All backlinks with categories
- Recent entries: Last 20 backlinks

---

#### Daily.base
**Purpose:** Context-aware daily note display
**Logic:** Shows notes where:
- Filename contains the current date
- `created`, `start`, or `end` matches the date
- Note links to current file

**Views:**
- Daily notes: For daily note pages
- Monthly: For monthly review pages
- Yearly: For yearly review pages

---

#### Everything.base
**Purpose:** Browse all files in vault
**Views:**
- All files: Table of everything
- Images: Card view of images
- Images in posts: Cards of embedded images

---

#### Evergreen.base
**Purpose:** List all evergreen notes
**Filter:** `tags.contains("0🌲")`

---

#### Journal.base
**Purpose:** List all journal entries
**Filter:** `tags.contains("journal")`

---

#### Ratings.base
**Purpose:** Show all rated items across categories
**Filter:** `rating > 0`
**Views:**
- Ratings: All rated items
- Recent: Last 60 days

---

#### Genre.base
**Purpose:** Generic genre filter
**Filter:** `list(genre).contains(this)`
Shows all items where genre includes the current note.

---

#### Templates.base
**Purpose:** List all templates
**Filter:** `file.path.contains("/Templates")`

---

#### Attachments.base
**Purpose:** Manage attachment files
**Views:**
- Images: Cards of images linked from current note
- All images: All images in vault
- Unused attachments: Images with no backlinks (candidates for deletion)

---

#### Map.base
**Purpose:** Display places on a map
**Filter:** `categories.contains(link("Places"))`
**Formulas:**
- `Icon`: Gets icon from place type
- `Color`: Gets color from place type

**Views:**
- Map: All places on world map
- Location: Places in a specific city/region
- Type: Places of a specific type

---

### Category Bases

#### Books.base
**Filter:** `categories.contains(link("Books"))`
**Views:**
- Books: All books
- Top rated: Sorted by rating
- Author: Books by specific author (contextual)
- Genre: Books in specific genre (contextual)

---

#### Movies.base
**Filter:** `categories.contains(link("Movies"))`
**Views:**
- All: Every movie
- To-watch: `last.isEmpty() && rating.isEmpty()`
- Favorites: `rating > 6`
- Last seen: Recent watches (limit 20)
- Actor: Movies with specific actor
- Genre: Movies in specific genre
- Director: Movies by specific director
- Soundtrack: Movies with specific composer
- Theater: Movies linked from current note (for theater pages)

---

#### Shows.base
**Filter:** `categories.contains(link("Shows"))`
**Views:** All, Favorites, Last seen, Actor, Genre, Director

---

#### Albums.base
**Filter:** `categories.contains(link("Albums"))`
**Views:** Albums, Artist, Genre

---

#### Games.base
**Filter:** `categories.contains(link("Games"))`
**Views:** Games, Studio, Genre

---

#### Board games.base
**Filter:** `categories.contains(link("Board games"))`
**Views:** Table (simple list)

---

#### Podcasts.base
**Filter:** `categories.contains(link("Podcasts"))`
**Views:** Table (name and host)

---

#### Podcast episodes.base
**Filter:** `categories.contains(link("Podcast episodes"))`
**Views:** All episodes, Show (episodes of specific podcast), Guest

---

#### People.base
**Filter:** `categories.contains(link("People"))`
**Formulas:** `Age: (now() - birthday).years.floor()`
**Views:** All people (with calculated age)

---

#### Meetings.base
**Filter:** `categories.contains(link("Meetings"))`
**Views:**
- Meetings: All meetings
- Person: Meetings with specific person
- Type: Meetings of specific type

---

#### Companies.base
**Filter:** `categories.contains(link("Companies"))`
**Views:** Companies (name, URL, people)

---

#### Projects.base
**Filter:** `categories.contains(link("Projects"))`
**Views:** Table (sorted by status, year)

---

#### Places.base
**Filter:** `categories.contains(link("Places"))`
**Views:**
- Places: All places
- Location: Places in specific city
- Type: Places of specific type
- Related: Places linked from current note
- Metatype: Complex type matching

---

#### Products.base
**Filter:** `categories.contains(link("Products"))`
**Formulas:**
- `Owned`: Months since acquired
- `totalUses`: monthly-uses × months owned
- `perUse`: price / total uses

**Views:**
- Products: All with cost analysis
- Cost per use: Only items with monthly-uses > 0
- Maker: Products by specific maker
- Type: Products of specific type

---

#### Trips.base
**Filter:** `categories.contains(link("Trips"))`
**Views:** All trips, Location (trips to specific place)

---

#### Events.base
**Filter:** `categories.contains(link("Events"))`
**Views:** Events, Type, Location

---

#### Recipes.base
**Filter:** `categories.contains(link("Recipes"))`
**Views:** Recipes (name, type, cuisine, author, rating)

---

#### Clippings.base
**Filter:** `categories.contains(link("Clippings"))`
**Views:** Clippings, Author

---

#### Posts.base
**Filter:** `categories.contains(link("Posts"))`
**Views:** All (sorted by published date)

---

## How to Add a New Category

1. **Create the Category Page:**
   ```markdown
   # New Category.md (in Categories/)
   ---
   tags:
     - categories
   ---
   ![[New Category.base]]
   ```

2. **Create the Base:**
   ```yaml
   # New Category.base (in Templates/Bases/)
   filters:
     and:
       - categories.contains(link("New Category"))
       - '!file.name.contains("Template")'
   properties:
     file.name:
       displayName: Name
   views:
     - type: table
       name: All
       order:
         - file.name
   ```

3. **Create the Template:**
   ```markdown
   # New Category Template.md (in Templates/)
   ---
   categories:
     - "[[New Category]]"
   created: {{date}}
   ---
   ```

---

## Quick Reference: Which Template for What

| I want to... | Use Template |
|--------------|--------------|
| Write a quick thought | Journal |
| Save something from the web | Clipping |
| Distill an idea | Evergreen |
| Write an article | Post |
| Track a book | Book |
| Track a movie | Movie |
| Document a meeting | Meeting |
| Track a person | People |
| Track a place | Place |
| Track an owned item | Product |

---

## Quick Reference: Base View Syntax

To embed a specific view from a base:
```markdown
![[BaseName.base#ViewName]]
```

Examples:
- `![[Movies.base#Director]]` - Shows movies by that director
- `![[Meetings.base#Person]]` - Shows meetings with that person
- `![[Daily.base#Monthly]]` - Shows entries for that month
