---
layout: post
title: Set Up Jekyll For GitHub Pages on macOS
date:   2017-07-10 15:00:01 -0600
excerpt: I've always wanted to set up Jekyll for my website. The powerful liquid templating makes building and maintaining a static website so much easier. In addition, the ability to easily customize page and post URL's for SEO (Search Engine Optimization), and to use plain markdown files as page content are very nice.
---

# Set Up Jekyll For GitHub Pages on macOS

{{ page.date | date: "%B %-d, %Y"}}

I've always wanted to set up Jekyll for my website. The powerful liquid templating makes building and maintaining
a static website so much easier. In addition, the ability to easily customize page and post URL's for SEO (Search Engine Optimization), and to use plain markdown files as page content are very nice.

Anyways, the following is the steps I followed to set up Jekyll for this website.

## Requirement

Using a package manager will make your life so much easier. As I am on MacOS, I use [homebrew](https://brew.sh/).

## Ruby

First, install/update `Ruby` with

```bash
$ brew install ruby
```

## RubyGems

RubyGems installed by `brew` is not the latest version though. Therefore, according to [`rubygems` download page](https://rubygems.org/pages/download), run

```bash
$ gem update --system
```

and get the latest version installed.

## Bundler

After rubygems is installed, run

```bash
$ gem install bundler
```

to get [bundler](bundler.io).

## Install all the other dependencies

Follow [GitHub's guide](https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/#step-2-install-jekyll-using-bundler) and create a `Gemfile` under root directory that contains:

```
source 'https://rubygems.org'
gem 'github-pages', group: :jekyll_plugins
```

Then run

```bash
$ bundle install
```

It should take some time to install all the dependencies.

## Prepare Config File

Jekyll needs a `_config.yml` file, let's set it up. Create a file named `_config.yml` under root directory with

```
url: "http://localhost:4000"
```

in it, so that later if you use `{{ site.url }}`, it will be recognized as http://localhost:4000.

## Develop Locally!

Now it's all set! Run

```bash
$ bundle exec jekyll serve
```

and it will be served at `http://localhost:4000` by default.

Enjoy!

## Bonus: test and develop with a custom domain

If you have a custom domain, then you probably don't want to push the above config file to `master` of your GH-pages repository, as it will break your site by using http://localhost:4000 instead of your custom domain url. In this case, the best solution is to create two config files, `_config.yml` and `_development_config.yml` (you can name the second one anything really).

In `_config.yml`, put

```
url: "http://your.custom.domain"
```

and in `_development_config.yml`, put

```
url: "http://localhost:4000"
```

Now, use a different command to serve:

```bash
$ bundle exec jekyll serve _config.yml,_development_config.yml
```

and you are all set! No need to create another branch and go through the trouble.

## References

- [(Jelyll) Installation guide](http://jekyllrb.com/docs/installation/)
- [(RubyGems) Download](https://rubygems.org/pages/download)
- [(GitHub) Setting up your github pages site locally](https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/#step-2-install-jekyll-using-bundler)
- [(StackOverflow) How can I easily manage different base URL of Jekyll webpage on localhost and remote server?](https://stackoverflow.com/questions/37049753/how-can-i-easily-manage-different-base-url-of-jekyll-webpage-on-localhost-and-re)
- [Jekyll Local Preview with Absolute Links](https://www.jaredwolff.com/blog/jekyll-local-preview/)
