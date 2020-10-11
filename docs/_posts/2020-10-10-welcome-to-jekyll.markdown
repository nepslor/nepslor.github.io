---
layout: post
title:  "How to build this site - walkthrough"
date:   2020-10-10 14:54:14 +0200
categories: jekyll update
---

This site is build using the github-pages & jekyll framework. This put togheter modern static site generation and versioning control + automatic git workflows. Basically, the site is automatically generated at every git push event. 


* clone from github
`git clonegit@github.com:YOUR_REPO/YOUR_REPO.github.io.git`

* put everything in the new dir docs
`mkdir docs`
`cd docs`
sda

* initialize the bundle and add jekll (this is missing in the official github guide!)
{% highlight bash %}
    bundle init
    bundle add jekyll
{% endhighlight %}

* do not specify version, force 
`bundle exec jekyll new . --force`


* make the following changes in the Gemfile in the docs directory:
{% highlight ruby %}
    # This will help ensure the proper Jekyll version is running.
    # Happy Jekylling!
    #gem "jekyll", "~> 4.1.1"
    # This is the default theme for new Jekyll sites. You may change this to anything you like.
    gem "minima", "~> 2.5"
    # If you want to use GitHub Pages, remove the "gem "jekyll"" above and
    # uncomment the line below. To upgrade, run `bundle update github-pages`.
    gem "github-pages", group: :jekyll_plugins
{% endhighlight %}

* install minima dependencies 
`bundle install`

* test site locally (the default port 4000 is usually used by nomachine, if you don't have installed you can keep it). The `--livereload`option makes your editing dynamic.
`bundle exec jekyll  serve --port 4001 --livereload`

* access the site locally
from a browser: http://localhost:4001/

# Add sections to the main page 
In the docs/ dir:
{% highlight bash %}
mkdir _sections
mkdir _inclusdes
cd _includes
mkdir sections
{% endhighlight %}



create a default.html file with the following content:

{% highlight ruby %}
    {% capture bg-image-style %}
    style="background:{% if section.bg-opaque-overlay != nil %} linear-gradient(
        {{ section.bg-opaque-overlay }},
        {{ section.bg-opaque-overlay }}
    ),{% endif %} {% if section.bg_image != nil %}url('{{ section.bg_image }}') center center fixed; background-size: cover;{% endif %}"
    {% endcapture %}
    <section id="{{ section.title | slugify }}" class="content-section"{{ bg-image-style }}>
    <div class="row">
        <div class="col-md-12">
        <h1>{{ section.title }}</h1>
        {{ section.content }}
        </div>
    </div>
    </section> 
{% endhighlight %}

Create _layouts dir in docs/, copy there all the default theme _layouts from ~/gems/gems/minima-2.5.1/_layouts/ file. Then modify the home.html adding the following section:


this will cycle through the markdown sections that you'll place in the docs/_section folder
