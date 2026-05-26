# Research Source Organizer (Generic) — CLAUDE.md

## Project overview

Single-file HTML tool for students at any institution to organize research sources, assign stances relative to a thesis, visualize argument structure, and export annotated bibliographies in MLA/APA/Chicago.

**File:** `source-organizer.html` (entire app lives here)

---

## Stack

- Vanilla HTML/CSS/JavaScript — no framework, no build step
- **PDF.js 3.11.174** (CDN) — client-side PDF text extraction
- **Mammoth.js 1.6.0** (CDN) — client-side DOCX extraction
- `localStorage` — data persistence under key `research_sources`
- Inter (Google Fonts) — neutral system-grade font, no institutional branding

---

## Key sections inside source-organizer.html

| Function | What it does |
|---|---|
| `addSource()` | Validates form, parses tags[], pushes to `sources[]`, saves |
| `clearAddForm()` | Resets all Add Source form fields |
| `loadSampleData()` | Loads 6 demo sources on social media + mental health topic |
| `renderTable()` | Filters by search/stance/type/tag and renders Browse tab table |
| `deleteSource(id)` | Removes by id, re-renders table |
| `openEdit(id)` | Populates edit modal from source object |
| `saveEdit()` | Validates and updates source in array |
| `renderThemeMap()` | Groups sources by tag, renders stance-colored cards |
| `formatCitation(s, format)` | Returns HTML citation string for mla/apa/chicago |
| `renderBibliography()` | Renders all citations + annotations sorted A-Z |
| `setFormat(fmt, btn)` | Switches bib format and re-renders |
| `copyAllBib()` | Copies full bibliography to clipboard as plain text |
| `downloadBib()` | Downloads bibliography as TXT file |
| `openCite(id)` | Opens citation modal with all three formats for one source |
| `renderOutline()` | Groups sources by stance into four paper sections |
| `downloadOutline()` | Downloads structured outline as TXT |
| `extractPDF(file)` | PDF.js page-by-page text extraction |
| `extractDOCX(file)` | Mammoth.js raw text extraction |
| `handleDocImport(event)` | Dispatches to extractPDF or extractDOCX, fills src-text field |
| `saveData()` | Writes `sources[]` to localStorage under `research_sources` |
| `downloadFile(content, name, mime)` | Blob URL download helper |

---

## Data model

```js
{
  id,            // Date.now() + Math.random() — float, used as stable key
  title,         // string
  author,        // "Last, First" or organization name
  year,          // integer
  publication,   // journal, publisher, or website name
  url,           // optional string
  source_type,   // "article" | "book" | "website" | "newspaper" | "video" | "other"
  stance,        // "supports" | "challenges" | "background" | "neutral"
  tags,          // string[] — lowercase, comma-parsed
  annotation,    // student's 2-3 sentence summary (required)
  text,          // optional full/partial source text for keyword search
  word_count,    // integer
  date_added     // ISO string
}
```

---

## Color tokens

| Token | Hex | Usage |
|---|---|---|
| `--primary` | `#1E3A5F` | Header, nav active, table headers, primary buttons |
| `--accent` | `#2563EB` | Interactive elements, focus rings, tab indicator |
| `--accent-lt` | `#DBEAFE` | Tag chips, hover row, background stance |
| `--bg` | `#F1F5F9` | Page background |
| `--green` | `#16A34A` | Supports stance |
| `--red` | `#DC2626` | Challenges stance |
| `--amber` | `#D97706` | Warning toasts |
| `--gray` | `#64748B` | Neutral stance, muted text |

---

## Stance color coding

| Stance | Border / Badge color | CSS class |
|---|---|---|
| supports | `--green` (#16A34A) | `.badge-supports` |
| challenges | `--red` (#DC2626) | `.badge-challenges` |
| background | `--accent` (#2563EB) | `.badge-background` |
| neutral | `--gray` (#64748B) | `.badge-neutral` |

---

## Citation formatting rules

**MLA 9th:**
- Book: `Last, First. *Title*. Publisher, Year.`
- Article/Other: `Last, First. "Title." *Publication*, Year.`

**APA 7th:**
`Last, F. (Year). *Title*. Publication. URL`

**Chicago:**
- Book: `Last, First. *Title*. Publisher, Year.`
- Article: `Last, First. "Title." *Publication* (Year).`

All formats sorted A-Z by reversed author name. `authorReversed()` and `authorAPA()` handle name inversion.

---

## Common tasks

**Add a new stance option:**
1. Add a radio button + label in the Add Source form (`stance-group` div)
2. Add matching option to `<select id="edit-stance">` in the edit modal
3. Add CSS for `.badge-NEWSTANCE` and `.theme-card.NEWSTANCE`
4. Add to `stanceLabel()` helper and the outline groups array in `renderOutline()`

**Add a new source type:**
Add `<option>` to both `<select id="src-type">` (Add tab) and `<select id="edit-type">` (Edit modal), then add a label to the `typeLabels` object in `renderTable()`.

**Add a new bibliography format:**
1. Add a `<button class="format-btn">` in the bib controls
2. Add a `format === 'newformat'` branch in `formatCitation()`
3. Update `downloadBib()` header label object

**Retheme for an institution:**
Update the CSS variables in `:root`. Change the font `<link>` if needed.

**Change sample data topic:**
Edit the `samples` array in `loadSampleData()`. Keep 5–6 sources covering all four stances and at least two different tags for a good demo.

---

## Relationship to STLCC version

This is a stripped, rebrandable version of the STLCC Library Source Organizer. The STLCC-branded version lives in the parent directory (`../source-organizer.html`) and should not be modified here. Key differences: font (Inter vs Source Sans Pro), color palette (neutral blue vs STLCC navy), localStorage key (`research_sources` vs `stlcc_sources`), header (generic icon vs STLCC logo).
