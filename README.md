# Research Source Organizer

**Live:** https://yuliabrusova85-ship-it.github.io/source-organizer/

A single-file HTML tool for students to organize research sources, build annotated bibliographies, and map argument structure. No login, no server, no API key — works in any browser and saves data locally.

## Usage

Open `source-organizer.html` in any browser. Data persists in `localStorage` between sessions.

## Features

### Add Source
- Manual entry form: title, author, year, publication, URL, source type
- Stance tagging: Supports / Challenges / Background / Neutral (relative to your thesis)
- Topic tags (comma-separated) for theme grouping
- Required annotation field (2–3 sentence summary)
- Optional full-text field for keyword search
- PDF and DOCX text extraction (runs locally, no upload to any server)

### Browse Sources
- Filter by stance, source type, and topic tag
- Full-text search across title, author, annotation, and tags
- Edit and delete individual sources
- Per-source citation generator (all three formats)
- Stats strip showing stance breakdown

### Theme Map
- Sources grouped by topic tag
- Color-coded by stance for visual argument mapping

### Bibliography
- MLA 9th, APA 7th, and Chicago formats
- Alphabetical by author (reversed format)
- Annotations included below each citation
- Copy individual entries or the full bibliography
- Download as `.txt`

### Outline Helper
- Enter your thesis statement
- Sources automatically sorted into paper sections by stance
- Download structured outline as `.txt`

## Source types supported

Journal Article, Book, Website, Newspaper, Video / Documentary, Other

## Data storage

All data is saved to `localStorage` under the key `research_sources`. Nothing is sent to any server. Clearing browser storage will delete your sources — use the Download options to keep backups.

## Deployment

Drop `source-organizer.html` anywhere — a web server, shared drive, LMS, or email it. No configuration needed. The PDF/DOCX extraction libraries load from CDN on first use.
