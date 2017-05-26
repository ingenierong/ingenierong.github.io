---
layout: post
title: Creando webs estaticas con Jekyll
---

Jekyll es una herramienta que nos permite crear paginas web estaticas con un aspecto muy similar a un blog.

![_config.yml]({{ site.baseurl }}/images/avator_frog.png)

Jekyll emplea un entorno Ruby con RubyGems.

Quick reference:

 Install Jekyll and Bundler gems through RubyGems
~ $ gem install jekyll bundler

# Create a new Jekyll site at ./myblog
~ $ jekyll new myblog

# Change into your new directory
~ $ cd myblog

# Build the site on the preview server
~/myblog $ bundle exec jekyll serve

# Now browse to http://localhost:4000

Cuando marcas algo entre comillas simples, las inverasas q estan debajo de  ^, jekyll genera una cajita...

Ejemplo de cajita `soy un markdown` .... un code snippets:


The easiest way to make your first post is to edit this one. Go into /_posts/ and update the Hello World markdown file. For more instructions head over to the [Jekyll Now repository](https://github.com/barryclark/jekyll-now) on GitHub.
