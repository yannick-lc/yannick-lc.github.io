# Blog

Repository for the content of Yannick Le Cacheux's blog.

Available at https://yannick-lc.github.io/ (for now)

Created and hosted using [Jekyll](https://jekyllrb.com/) and [Github Pages](https://docs.github.com/en/pages/quickstart).

## Structure

Jekyll root is in */docs* folder.

For now, hosted on [manifold.fr](https://manifold.fr)

Blog itself is located in manifold.fr/blog (index is at this location)

manifold.fr redirects to manifold.fr/blog for now.

Comments are handled via [Disqus](https://disqus.com/), using
Shortname is set in `_config.yml`.


## Run

To run locally:
```bash
cd docs
bundle exec jekyll serve
```

To install plugins added in `/docs/_config.yml`:
```bash
bundle install
```

To build (supposed so generate `sitemap.xml`):
```bash
bundle exec jekyll build
```

## Ideas

Indicate to how much reading time each article corresponds.
Add author?
Maybe add a collapsible TL;DR section at the beginning, right after introduction?

For collapsible sections in details tag, maybe add emojis like ℹ️ to indicate interesting precisions, off-topic comment and details of computations?

## Todo

Maybe better handle ToC scroll bar on mobile (or disable?)

Add a couple of exercises in matrix notation article

Standalone example of pseudo inverse: 3D hand landmarks

Add a more explicit link to my Twitter profile.

## Check list before go live

- Comments
v Permalinks 
v Blog email address
v Twitter and LinkedIn profiles (+ Twitter handle?)
v SEO and meta tags? + robot.txt (also, ask ChatGPT)
v Domain and /blog

Left to check (live): robots.txt, sitemap.xml and redirection.
