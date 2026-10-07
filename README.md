# mauk9086.github.io

Source for the academic homepage of Mohammad Ahmadullah Khan: https://mauk9086.github.io

Built with the [Academic Pages](https://github.com/academicpages/academicpages.github.io) Jekyll template (MIT licence; see `LICENSE`). The unmodified template is tagged `template-baseline`.

## Where content lives

| What | File(s) |
|---|---|
| Sidebar, site title, links, email | `_config.yml` (`author:` block) |
| Header menu | `_data/navigation.yml` |
| Home page (bio, interests, news) | `_pages/about.md` |
| CV page | `_pages/cv.md`; PDF in `files/` |
| Open-source contributions | `_pages/open-source.md` |
| Publications / manuscripts / thesis | `_publications/*.md` (`category:` = `manuscripts`, `conferences`, `theses`) |
| Research & projects | `_portfolio/*.md` (sorted by the `order:` field) |
| Talks | `_talks/*.md` |
| Teaching and outreach | `_teaching/*.md` |
| Figures | `images/` |

Outstanding inputs are tracked in `MISSING_ITEMS.md` (not published).

## Local preview

With Ruby and Bundler: `bundle install && bundle exec jekyll serve -l -H localhost`, then open http://localhost:4000.
With Docker Desktop running: `docker compose up`.
