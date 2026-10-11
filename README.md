# IntDEx Articles

Articles by Georgia Kali about [IntDEx](https://intdex.org), the AI-native Delivery Experience framework. IntDEx is a research project on AI-native software delivery, and it is seeking IT professionals and organisations to help develop it.

The site is Jekyll, built by GitHub Pages itself (no Actions workflow and no secrets), and published at <https://georgiakali.github.io/intdex/>.

## Publish on GitHub Pages

In the repository settings, open **Pages** and set:

- **Source:** Deploy from a branch
- **Branch:** `main`
- **Folder:** `/ (root)`

`url` and `baseurl` in `_config.yml` must stay aligned with that address: `https://georgiakali.github.io` and `/intdex`.

Plugins are limited to the set GitHub Pages allows natively: `jekyll-feed`, `jekyll-seo-tag`, and `jekyll-sitemap`. Do not add other Jekyll plugins if you want Pages to keep building the site for you.

## Add a post

1. Create `_posts/YYYY-MM-DD-short-title.md`. The date in the filename is the publication date. The home page lists posts newest first.
2. Start the file with this front matter, then write the article in Markdown underneath:

```yaml
---
layout: post
title: "Article title"
date: 2026-10-11
author: Georgia Kali
tags:
  - intdex
description: One or two sentences. This is the home-page summary, the feed text, and the search description.
---
```

3. Give every new tag its own page, or the tag link will 404. Copy `tags/intdex.md` to `tags/your-tag.md` and change `tag`, `permalink`, `title`, and `description`. Keep tags to lowercase letters, numbers, and hyphens, and use the same string in the post and in the tag file.
4. Commit to `main` and push. GitHub Pages rebuilds the site.

The article page shows the author, the date, the tags, and a reading time (about 180 words per minute, rounded up). A post dated in the future stays unpublished until that date.

`Gemfile.lock` is gitignored on purpose. GitHub Pages resolves the `github-pages` gem itself; a lockfile from another machine makes that build warn that dependencies cannot be satisfied.

Set `published: false` in the front matter to keep a file in `_posts/` without listing it. Files in `_drafts/` are also unpublished.

## Remove the sample post

`_posts/2026-10-11-sample-article-delete-this-post.md` is placeholder content, marked **Sample — delete** on the site. Delete it when you add a real article. If nothing else uses the `sample` tag, delete `tags/sample.md` as well.

## Preview locally

Ruby 3 and Bundler are required. From the repository root:

```bash
bundle install
bundle exec jekyll serve
```

Open <http://127.0.0.1:4000/intdex/>. The `/intdex` prefix matches the project-site `baseurl`.

## Feeds and metadata

| File | Produced by |
| --- | --- |
| `/feed.xml` | jekyll-feed |
| `/sitemap.xml` | jekyll-sitemap |
| Title, description, canonical URL, Open Graph and Twitter tags | jekyll-seo-tag |

The header and footer link to the author hub at <https://georgiakali.github.io> and to the project at <https://intdex.org>.
