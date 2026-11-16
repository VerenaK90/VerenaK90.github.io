# Somatic Evolution Research Group — website

Source for https://verenak90.github.io, the group website for Verena
Körber's lab. Built with Jekyll, served by GitHub Pages' native build (no
GitHub Actions, no custom build step).

- Work happens on the `redesign` branch; `main` is what's live.
- To add a paper, a team member, a news item or a job ad, see
  [`EDITING.md`](EDITING.md) — everything routine lives in `_data/*.yml`
  and can be edited from the GitHub web UI.
- To preview locally: `bundle install && bundle exec jekyll serve`.
- [`REDESIGN_BRIEF.md`](REDESIGN_BRIEF.md) is the design specification
  this site was rebuilt from.
