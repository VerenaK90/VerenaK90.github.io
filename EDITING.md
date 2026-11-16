# Editing this site

Everything that changes routinely — papers, people, news, job ads — lives
in plain text files under `_data/`. You can edit all of them directly in
GitHub, in your browser, with no local setup:

1. Go to the file on github.com (e.g. `_data/publications.yml`).
2. Click the pencil icon ("Edit this file") in the top right.
3. Make your change.
4. Scroll down, add a short commit message, and click "Commit changes...".
5. Choose "Create a new branch and start a pull request" if you want someone
   to check the change first, or commit directly to `redesign`/`main` if
   you're confident. GitHub Pages rebuilds the site automatically within a
   minute or two of a commit to `main`.

Each `_data/*.yml` file starts with a comment block (lines starting with
`#`) explaining its own fields — read that first. The examples below are
ready to copy and paste; just change the values.

## Add a paper

Open `_data/publications.yml`, scroll to the top of the list (entries are
in no particular order in the file — the site sorts them by year itself),
and paste a new block like this:

```yaml
- title: "Title of the new paper"
  authors: "Smith J., **Körber V**, Jones A., et al."
  journal: Nature Genetics
  year: 2026
  volume: 58
  pages: 100-110
  doi: 10.1038/s41588-026-00000-0
  pmid: 40000000
  shared_first: false
  corresponding: false
  highlight: false
```

- Wrap Verena's name in two asterisks (`**Körber V**`) wherever it appears
  in the author list — the site bolds it automatically.
- Set `shared_first: true` if she shares first authorship, and
  `corresponding: true` if she is a (shared) corresponding author.
- Set `highlight: true` to show this paper on the home page (keep it to
  two or three at a time).
- If you don't have a DOI or PMID yet, write `TODO` instead of leaving it
  blank — that way it's easy to find later and the site won't show a
  broken link.

## Add a person

Open `_data/team.yml` and paste a new block like this:

```yaml
- name: Jane Doe
  role: DPhil student
  bio: One or two sentences about Jane's background and what she works on.
  email: jane.doe@ndcls.ox.ac.uk
  photo: doe-j.png
  alumnus: false
```

- `photo` is just the filename — the actual image file needs to be
  uploaded to `assets/images/team/` first (same "Add file" → "Upload
  files" button works in the GitHub web UI), cropped to a 4:5 portrait,
  same treatment as the others.
- When someone leaves the group, don't delete their entry — instead set
  `alumnus: true` and add `now: their current position` if you know it.
  They'll automatically move to the alumni list at the bottom of the
  Team page.

## Add a news item

Open `_data/news.yml` and paste a new block at the top (entries are shown
newest first, in the order they appear in the file):

```yaml
- date: 2026-03-01
  text: "Our paper on clonal selection in blood ageing is out in Nature Genetics."
  link: https://doi.org/10.1038/s41588-025-00000-0
```

- `date` must be in `YYYY-MM-DD` format.
- `link` is optional — leave it out if there's nothing to link to.

## Things to avoid

- Don't rename the files in `_data/` or change the field names (the text
  before each `:`) — the page templates expect those exact names.
- Don't remove the explanatory comment block at the top of a data file.
- If you're not sure a change is right, use "Create a new branch and
  start a pull request" (step 5 above) instead of committing straight to
  `main` — that way nothing goes live until it's reviewed.
