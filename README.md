# chris.topher.li

My personal homepage. One page, one column, no navigation. Static, no
JavaScript, no webfonts, no trackers — about 20 KB in total.

Built with [Jekyll](https://jekyllrb.com/) and served by GitHub Pages.

---

## Where the content lives

Content is deliberately kept out of the templates. To change what the site
*says*, you should never have to touch HTML.

| Path | What's in it |
| --- | --- |
| `content/index.md` | All of the prose. This is the page. |
| `_data/profile.yml` | Name, the line under it, and the contact links. |
| `_data/projects.yml` | The year-gutter list under "Work". |
| `_config.yml` | Site title, tagline, URL, "last updated" date. |

Everything else — `_layouts/`, `_includes/`, `assets/` — is presentation.

> **Some content is still placeholder text marked `TODO`** (the contact address
> in `_data/profile.yml`, one project description). Search the repo for `TODO`.

### Structure of the page

`content/index.md` is a single Markdown document. Each `##` heading becomes a
section label, and Kramdown gives it an id automatically, so `## Work` is
linkable as `/#work`. Each `###` becomes a numbered belief; the leading
`<span class="num">` is what greys out the numeral.

The one piece of generated markup is `{% include timeline.html %}`, which
renders `_data/projects.yml` newest-first.

To add a section, write another `##` heading. There is no nav to update.

---

## Design

- A single measure of ~36rem; the layout is one column at every width.
- A system serif stack (Charter → Iowan Old Style → Sitka → Noto Serif →
  Georgia), so there is no webfont request and no flash of unstyled text.
- Light and dark palettes, switched on `prefers-color-scheme`.
- Print styles live at the bottom of `assets/style.css`.

All of it is in `assets/style.css`, which is the only stylesheet.

---

## Building it

GitHub Pages builds this repo itself on every push to `master` — no CI workflow
and no build step on your machine are required to deploy. Just commit and push.

To preview locally you need Ruby and Jekyll:

```sh
bundle install          # first time only
bundle exec jekyll serve
```

Then open <http://localhost:4000>.

### If `bundle install` fights you

macOS ships Ruby 2.6, which most current gems have dropped. Either install a
modern Ruby (`brew install ruby`, then reopen your shell), or install Jekyll 3.9
against the system Ruby with the versions pinned below:

```sh
export GEM_HOME="$HOME/.gem/ruby/2.6.0"
export PATH="$GEM_HOME/bin:$PATH"
gem install --user-install ffi -v 1.15.5
gem install --user-install i18n -v 1.14.1
gem install --user-install public_suffix -v 4.0.7
gem install --user-install jekyll -v 3.9.5 kramdown-parser-gfm
JEKYLL_NO_BUNDLER_REQUIRE=true jekyll serve
```

(`JEKYLL_NO_BUNDLER_REQUIRE` tells Jekyll to ignore the `Gemfile`, which is
otherwise resolved against a Ruby it can't satisfy.)

---

## Deploying

Push to `master`. In the repo's **Settings → Pages**, source should be
**Deploy from a branch → `master` / `(root)`**.

`CNAME` points the site at `chris.topher.li`; leave it in place.

`_site/` is the build output and is git-ignored — never commit it.
