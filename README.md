# Blog

Repository for the content of Yannick Le Cacheux's blog.

Created and hosted using [Jekyll](https://jekyllrb.com/) and [Github Pages](https://docs.github.com/en/pages/quickstart).

## Structure

Jekyll root is in */docs* folder.

For now, hosted on [manifold.fr](https://manifold.fr)

Blog itself is located in manifold.fr/blog (index is at this location)

manifold.fr redirects to manifold.fr/blog for now.

Comments are handled via [Disqus](https://disqus.com/).
Shortname is set in `_config.yml`.

## Install

To install all packages on new machine:

Install Ruby (may require make etc if not already installed):
```bash
sudo apt install ruby-full build-essential zlib1g-dev
```

Install Jekyll:
```bash
gem install bundler jekyll
```

then `cd docs`, then `bundle install`

If error stating that no permission to write in /var/lib/gems/3.3.0 or something, specify to install gems locally:
bundle config set path vendor/bundle

Then `bundle exec jekyll serve` should hopefully work to start local server.

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

Standalone example of pseudo inverse: 3D hand landmarks

Add a more explicit link to my Twitter profile.

Add copyright/license on blog?

Edit "last modified at" dates

Double check that robots.txt is OK.

Add icon.


## Check list before go live

- Comments
v Permalinks 
v Blog email address
v Twitter and LinkedIn profiles (+ Twitter handle?)
v SEO and meta tags? + robot.txt (also, ask ChatGPT)
v Domain and /blog

Left to check (live): robots.txt, sitemap.xml and redirection.
