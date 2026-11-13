# Redesign brief — Somatic Evolution Research Group website

Repository: `VerenaK90/VerenaK90.github.io` · Branch: `redesign` · Live: https://verenak90.github.io

This file is the specification. Work only on `redesign`. Never push to `main`.

---

## 1. Purpose and audience

Primary audience: appointment committees, grant reviewers, and senior colleagues who already know the field.
Primary job of the site: demonstrate that Verena Körber runs an **independent** research programme, distinct from her PhD (Höfer, DKFZ) and postdoc (Vyas, Oxford) environments.

Secondary: recruitment, and dissemination of the group's software.

The site cannot win an appointment. It can lose one by looking dead, unfinished, or generic. Target state is *flawless and current*, not spectacular.

Four visible proofs of independence must be present and easy to find:
1. Her own funding (named funders, titles, terms).
2. Her own trainees (team page with roles).
3. Her own software (released, versioned, citable).
4. Her own research question, phrased as hers.

## 2. Hard constraints

- **Jekyll on GitHub Pages, native build.** No GitHub Actions, no custom build step.
- **Plugins:** only `jekyll-seo-tag` and `jekyll-redirect-from` (both on the GitHub Pages whitelist). Nothing else. Specifically: no `jekyll-scholar`.
- **No remote theme, no CSS framework.** The existing HTML5-UP "Forty" theme is removed entirely: its layouts, includes, SCSS, and JS go.
- **Self-editability is a requirement, not a nice-to-have.** Every routine content change — a new paper, a new group member, a news item, a job ad — must be possible by editing one `.yml` or `.md` file in the GitHub web editor, with no local tooling and no Git knowledge beyond "commit changes".
- **No external runtime dependencies.** Fonts are self-hosted in the repo. No Google Fonts, no CDN, no analytics, no tracking pixels, no embedded social widgets.
- **Do not invent content.** Where real content is missing, insert an explicit `TODO:` marker in the data file or page. Never fabricate a publication, a funder, a date, a team member, or a figure.

## 3. Design tokens

Define these once as CSS custom properties on `:root` in a single stylesheet. Do not scatter literal colour values through the CSS.

```
--paper        #FFFFFF
--ink          #202020   /* body text */
--ink-muted    #606060   /* metadata, captions */
--rule         #DCDCDC   /* hairlines, table borders */
--accent       #0E5260   /* petrol: links, marks, sketch ink */
--accent-deep  #07323B   /* hover, visited, headings where needed */
```

Petrol is the only accent. Everything else is ink on paper. Oxford blue is deliberately excluded: it is the institute's colour, not the group's, and using it works against the independence signal.

**Typography.** IBM Plex, self-hosted as `woff2` in `assets/fonts/`, Latin subset, `font-display: swap`.

- `IBM Plex Serif` — body text and headings.
- `IBM Plex Sans` — navigation, metadata lines, table headers, footer.
- `IBM Plex Mono` — code, package names, install commands on the Software page.

Type scale, 1.25 ratio on a 17px serif base:

```
0.85rem   metadata, captions          (Sans)
1.0625rem body                        (Serif, line-height 1.65)
1.33rem   h3
1.66rem   h2
2.07rem   h1
2.59rem   home statement
```

Measure: prose columns capped at 68ch. Everything left-aligned; never justified. Container width 1080px for grids (team, software), prose stays in the narrower column even inside a wide container.

**What not to do** (these are the tells of a templated page):
- No all-caps tracked-out eyebrow labels above headings.
- No metadata strings joined with middle dots.
- No arrow glyphs appended to link text.
- No identical rounded cards with soft grey shadows for every content block.
- No fade-up animation on scroll, no hover transition on every element. Motion only where it answers a click (the mobile menu).
- No carousel, no stock photography, no gradient washes.

**Restraint.** The sketches are the one memorable element. Everything around them stays quiet.

## 4. Sketches and images

The group has hand-drawn blackboard-style sketches. They are the visual identity and carry real weight: one per research theme on the Research page, plus small marks where useful.

They will be delivered already processed: background removed, single-colour in `--accent`, consistent line weight, transparent PNG or SVG. **Do not apply CSS filters to them and do not substitute placeholder graphics.** If the processed sketches are not yet in `assets/images/sketches/`, build the pages without them and leave the markup slot in place with a `TODO:` comment.

Portraits: uniform aspect ratio (4:5), uniform treatment, no drop shadows, no circular crops. If the supplied portraits are not uniform, say so rather than compensating with CSS.

## 5. Site structure

Navigation order, which is also the priority order:

```
Research · Publications · Software · Team · News · Join us
```

The current tile-based homepage is removed without replacement. The current navigation order (Open positions first, Research last) is inverted.

### Home
No hero image. In order:
1. A three-to-four sentence positioning statement, newly written, **not** the paragraph currently shared verbatim with her IMM profile page.
2. Three highlighted publications, pulled from `_data/publications.yml` where `highlight: true`.
3. A single quiet row of funder names.

### Research
Three to five themes. Each: a heading phrased as a question, two to three sentences of prose, one sketch, and links to the relevant publications and software. This page carries the independence argument and its copy comes from Verena.

### Publications
Reverse-chronological, grouped by year, rendered from `_data/publications.yml`.
Typographic conventions, with a legend at the top of the list:
- Verena's name in bold in every author string.
- `*` shared first authorship.
- `†` corresponding authorship.
- DOI link on the title; separate links for code and data where present.

### Software
One block per package: name in Mono, one-sentence description, install line, links to repository, documentation, Bioconductor/CRAN, and the paper that cites it.

### Team
Grid of portraits, name, role, two to three sentences, email. Alumni in a plain list below, with current position where known.

### News
Reverse-chronological, dated entries, short. Rendered from `_data/news.yml`, not Jekyll posts — a `_posts` collection is more machinery than this needs and the filename date convention is a trap for a non-Git editor.

### Join us
Current openings, plus a paragraph on how to approach her speculatively, plus what the group offers a trainee.

### PI page
Linked from the footer and from the Team page, not in the main navigation: full biography, career path, funding with funder/title/term, teaching and supervision, ORCID (`0009-0005-3888-2648`), Google Scholar, CV as a PDF download.

Rationale for including teaching and funding in full: German appointment procedures treat them as explicit criteria. In UK and US searches they do no harm.

## 6. Data files

Create `_data/` with the schemas below. Each file starts with a comment block explaining, in plain English, how to add an entry — this is what Verena will read in the web editor.

```yaml
# _data/publications.yml
- title:
  authors:          # plain string; mark Verena as **Körber V**
  journal:
  year:
  volume:
  pages:
  doi:
  pmid:
  code:             # optional URL
  data:             # optional URL
  preprint:         # optional URL
  shared_first:     # true | false
  corresponding:    # true | false
  highlight:        # true | false — shows on the home page
```

```yaml
# _data/team.yml
- name:
  role:
  bio:
  email:
  photo:            # filename in assets/images/team/
  scholar:          # optional
  github:           # optional
  alumnus:          # true | false
  now:              # current position, alumni only
```

```yaml
# _data/software.yml
- name:
  description:
  install:          # e.g. BiocManager::install("LACHESIS")
  repo:
  docs:
  paper_doi:
```

```yaml
# _data/funding.yml
- funder:
  title:
  role:             # PI | Co-I
  term:             # e.g. 2023–2027
```

```yaml
# _data/news.yml
- date:             # YYYY-MM-DD
  text:             # one or two sentences, plain text
  link:             # optional
```

Known starting content, to be verified before publication rather than trusted:
- Software: `LACHESIS` (Bioconductor, R), `SCIFER`, `Clonal_hematopoiesis` — all under github.com/VerenaK90.
- Funding: DFG project 526169089 (MDS→AML evolution), plus MRC and CRUK support evidenced by current job adverts. Exact titles and terms are `TODO:` until confirmed.

## 7. Layouts

Keep it to five layouts in `_layouts/`: `default`, `page`, `home`, `pi`, and one list layout shared by Publications/Software/News. Includes for header, navigation, footer, and the publication entry. No JavaScript except a small mobile navigation toggle, written inline, no library.

## 8. Migration and hygiene

- Preserve the existing URLs with `jekyll-redirect-from`: `/OpenPositions.html`, `/Software.html`, `/people.html`, `/publications.html`, `/research.html`. New paths are lowercase and extensionless where Jekyll allows.
- Delete the Forty assets rather than leaving them orphaned in the repo.
- `_config.yml`: set title, description, `url`, `baseurl: ""`, and the `jekyll-seo-tag` fields. Add a `favicon`.
- Accessibility floor: semantic landmarks, visible keyboard focus, colour contrast ≥ 4.5:1 for body text (check `--ink-muted` against white), alt text on every image, `prefers-reduced-motion` respected.
- Responsive down to 360px. Test the publication list and the team grid at that width specifically.
- Write `EDITING.md` at the repository root: a one-page guide for Verena covering how to add a paper, a person, and a news item through the GitHub web editor, with a screenshot-free, copy-paste-ready example for each.

## 9. Working method

1. Before writing code, produce the design plan — palette, type roles, layout concept with ASCII wireframes for Home, Research, and Publications — and check it against this brief.
2. Build the structure and the stylesheet first, with placeholder data, so the layout can be reviewed before content lands.
3. Preview with `bundle exec jekyll serve` and iterate.
4. Commit in small, labelled steps on `redesign`. Open a pull request for Verena to review before anything reaches `main`.
