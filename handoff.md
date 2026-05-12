# Session Handoff — raghadalsaka.github.io

Last updated: May 2026

---

## Goal

Maintain Raghad Alsaka's academic website at [raghadalsaka.com](https://raghadalsaka.com) so that it:

1. Stays up to date with the upstream [Academic Pages](https://github.com/academicpages/academicpages.github.io) Jekyll template
2. Accurately reflects the current CV at all times — no placeholders, no stale information, no invented content
3. Remains clean and professional for university job applications

The site is a GitHub Pages Jekyll site. The repo is:
`https://github.com/raghadalsaka/raghadalsaka.github.io`

---

## Current State of the Code (May 2026)

**Branch:** `master` — fully up to date with `origin/master`

**Recent commits:**
- `1817aa4` Merge branch 'master' (pulled automated talkmap update from GitHub Actions)
- `8fe9f6f` Merge template-sync-academicpages into master
- `14f2f55` Update website content to match new CV (May 2026)
- `027b7f0` Automated update of talk locations (GitHub Actions bot)
- `7ebd236` Template sync academicpages (#1) (GitHub PR merge)
- `ac383ac` Fix JS module error: add type="module" to main.min.js
- `425f2ef` Sync template from upstream Academic Pages

**What was done this session:**

### Template sync (from upstream Academic Pages)
- Added new dark/light theme system: 12 new SCSS theme files in `_sass/theme/`
- Added `_layouts/cv-layout.html` (new layout for JSON-based CV pages)
- Added `_sass/layout/_json_cv.scss`
- Added `assets/js/theme.js` (Plotly chart theme exports for dark/light mode)
- Updated `_layouts/single.html` with bibtex download support
- Updated `_includes/author-profile.html` with new platform links and performance fix
- Updated `_includes/social-share.html` with Bluesky and Mastodon buttons
- Updated `_includes/scripts.html`: added `type="module"` to the main.min.js script tag (see bug below), added `comments-providers/scripts.html` include
- Updated `assets/css/main.scss` to dual light/dark theme import system
- Updated `Gemfile` with `connection_pool 2.5.0`
- Updated most other `_includes/`, `_layouts/`, `_sass/`, `assets/js/` files from upstream

### Content updates (from CV)
- `_pages/about.md`: Rewritten — completed Ph.D. (May 2026), research interests, correct education dates
- `_pages/cv.md`: Full rewrite — all CV sections, no placeholders, no emoji
- `_config.yml`: Updated `description` and `bio`; cleared placeholder Google Scholar and ResearchGate URLs
- `_data/navigation.yml`: Added "Talks" to main nav
- `_teaching/2023-fall-edci321.md`: Updated title, type, body; removed emoji and "Currently Ongoing"
- `_teaching/2024-spring-edci409.md`: Updated role to Co-Teacher / Teaching Support
- `_teaching/2024-fall-edci201.md`: **New** — EDCI 201/EDCI 550: Contexts in Education
- `_talks/2026-04-01-aera-2026.md`: **New** — AERA 2026 Best Paper Award presentation

### Placeholder/demo content removed
- 4 template publications (Paper Title Number 1–4)
- 4 template talks (UC San Francisco, Berkeley, London, Los Angeles)
- 2 template portfolio items (portfolio-1.md, portfolio-2.html)

---

## Files Actively Being Maintained

These are the files that change with each CV update:

| File | Purpose |
|---|---|
| `_pages/about.md` | Home/About page — bio, research interests, education summary |
| `_pages/cv.md` | Full CV page — all sections rendered in HTML |
| `_config.yml` | Sidebar bio, description, and author social links |
| `_data/navigation.yml` | Top navigation bar links |
| `_teaching/*.md` | One file per course taught |
| `_talks/*.md` | One file per conference presentation |
| `_publications/*.md` | One file per published paper (currently empty — none confirmed yet) |

These template/infrastructure files are updated only when syncing the upstream template:

- `_includes/`, `_layouts/`, `_sass/`, `assets/js/`, `assets/css/`
- `Gemfile`, `package.json`, `Dockerfile`, `docker-compose.yaml`

These personal files are never overwritten by template syncs:

- `CNAME` (raghadalsaka.com)
- `images/` (profile photo, favicons)
- `files/` (CV PDF, paper PDFs)
- `_posts/` (blog posts)
- `_data/authors.yml`, `_data/ui-text.yml`

---

## Everything We Tried and Fixed

### Bug: `Uncaught SyntaxError: Cannot use import statement outside a module`
- **What happened:** After the template sync, the site threw a JS error on every page.
- **Root cause:** The upstream `main.min.js` now bundles Plotly.js and includes an ES module `import` statement (in `assets/js/_main.js` line 57: `import { plotlyDarkLayout, plotlyLightLayout } from './theme.js'`). Loading the bundle with a plain `<script>` tag instead of `<script type="module">` caused the browser to reject it.
- **Fix:** Updated `_includes/scripts.html` to use `type="module"` on the `main.min.js` script tag — matching the upstream version we had missed in the initial sync.
- **File:** `_includes/scripts.html`

### Issue: Push to master rejected after merging branch locally
- **What happened:** After merging `template-sync-academicpages` into local master and pushing, git rejected the push because the remote master had already merged the branch as a GitHub PR, plus an automated talkmap commit from GitHub Actions.
- **Why:** The PR was merged on GitHub before we added the CV content updates commit to the branch. So the remote had the template sync changes but not the CV changes.
- **Fix:** `git pull origin master --no-rebase` to merge in the automated talkmap commit cleanly, then pushed. No content conflicts.

### Note: `future: false` in `_config.yml`
- The config has `future: false`, which suppresses posts/talks with a future date. The AERA 2026 talk is dated `2026-04-01`, which is in the past as of May 2026, so it displays correctly. Watch for this if adding future-dated entries.

---

## What Still Needs Manual Action

These items are missing from the site because the CV had placeholders for them:

| Item | Status | Action needed |
|---|---|---|
| **CV PDF** | Old `Raghad_Alsaka_CV.pdf` still linked | Upload updated PDF to `/files/`, update link in `_pages/cv.md` if filename changes |
| **Google Scholar URL** | Cleared (was placeholder) | Add real URL to `_config.yml` → `author.googlescholar:` |
| **ResearchGate URL** | Cleared (was placeholder) | Add real URL to `_config.yml` → `author.researchgate:` if profile exists |
| **AECT presentations** | Not added — all had `[Year]`/`[Location]` placeholders | Add each as a `_talks/YYYY-MM-DD-slug.md` file once dates and locations are confirmed |
| **Publications** | None added — all CV entries were placeholders | Add each as a `_publications/YYYY-MM-DD-slug.md` file once published |
| **AERA 2026 exact date** | Filed as `2026-04-01` (approximate) | Update `date:` and `location:` in `_talks/2026-04-01-aera-2026.md` |
| **Pronouns** | Empty in `_config.yml` | Add `"she/her"` or preferred pronouns under `author.pronouns:` |

---

## Next Steps When Given an Updated CV

When Raghad provides a new version of her CV, follow this checklist:

### 1. Check for completed education
- If Ph.D. is listed with a new date, update `_pages/about.md`, `_pages/cv.md`, and `_config.yml` bio.

### 2. Check for new publications
- Any paper with a full citation (author, year, title, journal, volume, pages) → create `_publications/YYYY-MM-DD-slug.md`
- Use the front matter format:
  ```yaml
  ---
  title: "Full Paper Title"
  collection: publications
  category: manuscripts   # or: conferences, books
  permalink: /publication/YYYY-MM-DD-slug
  excerpt: 'One sentence description.'
  date: YYYY-MM-DD
  venue: 'Journal or Conference Name'
  paperurl: '/files/filename.pdf'   # if PDF is available
  citation: 'Alsaka, R. (Year). "Title." <i>Venue</i>. Vol(Issue).'
  ---
  ```
- Skip any entry that still has `[Year]`, `[Title]`, or other placeholders.
- Once real publications exist, add "Publications" back to `_data/navigation.yml`.

### 3. Check for new conference presentations
- Any presentation with a confirmed year and location → create `_talks/YYYY-MM-DD-slug.md`
- Use the front matter format:
  ```yaml
  ---
  title: "Presentation Title"
  collection: talks
  type: "Conference Paper Presentation"   # or: Poster, Invited Talk, etc.
  permalink: /talks/YYYY-MM-DD-slug
  venue: "Conference Name"
  date: YYYY-MM-DD
  location: "City, State"
  ---
  ```

### 4. Check for new teaching entries
- Any new course → create `_teaching/YYYY-semester-course.md`
- Match the front matter pattern in existing teaching files.

### 5. Update `_pages/cv.md` and `_pages/about.md`
- For any section that changed: awards, experience, certifications, memberships, skills.
- Never invent or carry over placeholder text from the CV.

### 6. Update `_config.yml` if social links changed
- Google Scholar, ResearchGate, LinkedIn, email.

### 7. Commit and push
```bash
git add <specific files>
git commit -m "Update website content — [month year]"
git push origin master
```

---

## How to Preview Locally

Ruby is not installed on this machine. Use Docker (requires Docker Desktop to be running):

```bash
docker-compose up
# then open http://localhost:4000
```

Or, if Ruby/Bundler is installed:

```bash
bundle install
bundle exec jekyll serve
```

GitHub Pages will also build and validate the site automatically on every push to `master`.

---

## Upstream Template Sync (future)

When the Academic Pages template has major updates worth pulling in:

```bash
git checkout -b template-sync-YYYY-MM
git fetch upstream master
# selectively checkout updated template files:
git checkout upstream/master -- _layouts/ _includes/ _sass/ assets/js/ assets/css/main.scss Gemfile
# do NOT overwrite: _config.yml, _data/, _pages/, _publications/, _talks/, _teaching/, _posts/, images/, files/, CNAME
git push -u origin template-sync-YYYY-MM
# open PR on GitHub, check build passes, then merge
```

The upstream remote should already be configured:
```bash
git remote -v
# upstream  https://github.com/academicpages/academicpages.github.io.git
```
