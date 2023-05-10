---
title: 'Snippet to compile this blog'
date: 2023-04-09
permalink: /posts/2023/04/compile-blog
tags:
  - cs
  - notes
excerpt: 'Snippet to compile this blog'
---

Setup necessary packages on a Chromebook
```
sudo apt update
sudo apt install -y build-essential ruby ruby-dev
sudo gem install bundler
bundle config set --global path $HOME/.gem
```

Install bundle
```
bundle install
```

Build the blog
```
bundle exec jekyll build
```

Serve the blog locally
```
bundle exec jekyll serve
```
