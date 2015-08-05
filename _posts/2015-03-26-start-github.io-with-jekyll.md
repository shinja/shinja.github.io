---
layout: post
title:  "Start github.io with jekyll"
date:   2015-03-27
category: "Web Devilopment"
tags: [jekyll, GitHub, GitHub Pages]
---

## GitHub Pages
It's really cool that [github.com](http://github.com) provides personal pages hosting service.
You could create your personal or organization website following this [instruction](http://pages.github.com), and then you will your own minimal customized blog. :)

####User(organization) Site V.S. Project Site
The user(or organization) site uses the **master** branch as the default branch to generate site, and the project site uses the **hg-pages** branch to publish.


##Jekyll
[GitHub Pages](http://pages.github.com) also support [Jekyll](http://jekyllrb.com/), a simple, blog-aware static site generator. You could easily following [Install Jekyll](https://help.github.com/articles/using-jekyll-with-pages/#installing-jekyll) instruction to install Jekyll and run on your local machine.

####Running Jekyll Locally
I don't want to install bundle packages in the root filesystem, instead of that, I install bundle packages in the GitHub Pages project directory. Here is the installation. Create a **Gemfile** file and add the configuration.

    $sudo apt-get install ruby ruby-dev gcc
    $sudo gem install bundler

    $cat Gemfile
    source 'https://rubygems.org'
    gem 'github-pages'

    $bundle install --path vendor/bundle
    ...
    $bundle exec jekyll serve

#### Exclude Vendor Directory
Add **exclude: [vendor]** (the installing path of bundle packages) in **_config.yml**, or you might get some error message like: *ERROR: YOUR SITE COULD NOT BE BUILT:*


##Jekyll in GitHub Pages

#### Dependency Versions

GitHub Pages only provides the following [jekyll plugins](https://pages.github.com/versions/). Therefore, you want to using some plugins other than GitHub Pages provides,  you may consider run jekyll locally and  generate **_site**   then publish the static pages to github.

Add a list of enabled gems (plugins) to your site's **_config.yml** file, such as:
    gems:
    - jekyll-mentions
    - jemoji
    - jekyll-redirect-from
    - jekyll-sitemap

####References
* [https://help.github.com/articles/using-jekyll-with-pages](https://help.github.com/articles/using-jekyll-with-pages)
* [https://help.github.com/categories/github-pages-basics](https://help.github.com/categories/github-pages-basics/)
