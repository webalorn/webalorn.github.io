---
name: update_website
description: Update the website
---

# Updating Publications from Google Scholar

This guide explains how to update the publication list from the Google Scholar profile at `https://scholar.google.com/citations?user=JQ512oQAAAAJ`.

## Step 1: Fetch Publications from Google Scholar

Use the `fetch_webpage` tool to retrieve publications:

```
fetch_webpage(
  urls: ["https://scholar.google.com/citations?user=JQ512oQAAAAJ"],
  query: "list all publications with titles, authors, venue, year, and citation counts"
)
```

Extract the following information for each publication:
- **Title**: Full paper title
- **Authors**: List of all authors
- **Venue**: Conference, journal, or workshop name
- **Year**: Publication year
- **Link**: URL to the paper (if available)

## Step 2: Check Existing Publications

List all existing publication files:
```
ls _publications/
```

Read each existing file to understand what's already tracked. Compare with Google Scholar results to identify:
- New publications to add
- Existing publications that need updates (new citations, venue changes, etc.)

## Step 3: Create Publication Files

For each new publication, create a file in `_publications/` with the naming format: `YYYY-MM-DD-slug.md`

### File Format

```yaml
---
title: "Full Paper Title"
collection: publications
category: conferences  # One of: conferences | workshop | manuscripts | books
permalink: /publications/YYYY-MM-DD-slug
excerpt: 'Brief 1-2 sentence description of the paper'
date: YYYY-MM-DD
venue: 'Conference/Journal Name with Year'
authors: 'Author One, Author Two, Author Three'  # Full author list
paperurl: 'https://arxiv.org/abs/...'   # Link to paper PDF (arxiv preferred)
codeurl: 'https://github.com/...'       # Link to source code (if available)
# slidesurl: 'https://...'              # Link to slides (if available)
---

Abstract: *Copy the abstract here in italics*
```

### Category Guidelines

Choose the correct category based on publication type:
- `conferences`: Full conference papers (CVPR, NeurIPS, ICML, ECCV, ICCV, etc.)
- `workshop`: Workshop papers at conferences
- `manuscripts`: Journal articles or arxiv preprints
- `books`: Book chapters or full books

### Date Format

- Use the publication/acceptance date in format `YYYY-MM-DD`
- If only year is known, use `YYYY-01-01`
- If month and year are known, use `YYYY-MM-01`
- The date determines the file name and sorting order

### Slug Guidelines

- Use lowercase with hyphens
- Include key identifying words from the title
- Keep it short but recognizable
- Example: `2024-03-20-depalm` for "Improved Baselines for Data-efficient Perceptual Augmentation of LLMs"

## Step 4: Find Additional Paper Details

For each new publication, search for additional links:

1. **ArXiv link**: Search Google or the paper title to find arxiv.org link
2. **Code repository**: Check if there's an associated GitHub repo
3. **Abstract**: Copy from arxiv or the paper PDF

Use `fetch_webpage` to get abstracts from arxiv pages:
```
fetch_webpage(
  urls: ["https://arxiv.org/abs/PAPER_ID"],
  query: "abstract"
)
```

## Step 5: Validate the Changes

After creating/updating publication files:

1. **Check for errors**: Run the Jekyll build to verify syntax
   ```bash
   bundle exec jekyll build
   ```

2. **Preview locally**: Start the development server
   ```bash
   bundle exec jekyll serve -l -H localhost
   ```

3. **Verify rendering**: Check that publications appear correctly on the `/publications/` page

## Example Publication File

Here's a complete example:

```yaml
---
title: "Improved Baselines for Data-efficient Perceptual Augmentation of LLMs"
collection: publications
category: workshop
permalink: /publications/2024-03-20-depalm
excerpt: 'Experimental evaluation and improvements of data-efficient multi-modal adaptation of single-modality LLM and perceptual backbones.'
date: 2024-03-20
venue: '1st Workshop on Green Foundation Models, ECCV'
authors: 'Théophane Vallaeys, Mustafa Shukor, Matthieu Cord, Jakob Verbeek'
paperurl: 'https://arxiv.org/abs/2403.13499'
codeurl: 'https://github.com/facebookresearch/DePALM'
---

Abstract: *The abilities of large language models (LLMs) have recently progressed to unprecedented levels...*
```

## Checklist

Before finishing, verify:
- [ ] All new publications from Google Scholar have been added
- [ ] Each file has correct front matter (title, collection, category, permalink, date, venue, authors)
- [ ] Authors list is complete and accurate
- [ ] Categories are correctly assigned (conferences/workshop/manuscripts/books)
- [ ] Paper URLs are valid (preferably arxiv)
- [ ] Code URLs are included where available
- [ ] Excerpts are concise and descriptive
- [ ] File names follow `YYYY-MM-DD-slug.md` format
- [ ] Jekyll build succeeds without errors