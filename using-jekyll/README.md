
Website for libbitcoin.github.io

This uses [jekyll](https://jekyllrb.com/) with a github pages
compatible theme [Just the
docs](https://pmarsceill.github.io/just-the-docs/).

### The advantages in using jekyll are

1. Author pages in markdown
2. Supported by github, so markdown to html conversion automatically
   happens at github pages.
3. Themes support, if we want to change the look at feel later.
4. In built support for pretty printing code snippets in html.

### Why Just the Docs

The popular Just the Docs theme brings a number of advantages, apart
from the clean professional design.

1. Compatible with github pages.
1. Support for navigation structure on the left.
2. Support for table of contents used in index and examples.
3. Support for search, which might be handy as we document the API more in future.
4. Support for pretty printing code fragments.

# Viewing site locally

1. Checkout branch `using-jekyll`
1. The current generated website is in `using-jekyll/_site`
1. Run any http server to server content from the above directory.

# Making changes on Github pages

The site is generated from markdown content in `using-jekyll`
directory. Once we move `using-jekyll` to root folder and pushed to
master, then markdown to html conversion will be automatically handled
by github pages. So to publish changes, potentially all one has to do
is change markdown and push to master branch.

## Making changes locally

1. Install [rvm](https:rvm.io)
2. Install ruby 2.6.3 `rvm install ruby-2.6.3`
3. Create gemset libbitcoin-website as `rvm gemset create 2.6.3@libbitcoin-website` 
3. Install bundler `gem install bundler`
4. Install required dependencues `bundle install`
5. Run website, `bundle exec jekyll serve` will start an http server
   at localhost:4000. Jekyll will watch for file changes and any
   markdown changes will be available on page refresh.

