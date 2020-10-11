---
layout: post
title:  "How to build this site - walkthrough"
date:   2020-10-10 14:54:14 +0200
categories: jekyll update
---

This site is built using the GitHub-pages & jekyll framework. This put togheter modern static site generation and versioning control + automatic git workflows. Basically, the site is automatically generated at every git push event. 

In the following you can find a step by step guide to help you replicate this site.

* install Ruby and Jekyll's depenences:
{% highlight bash %}
sudo apt-get install ruby-full build-essential zlib1g-dev
{% endhighlight %}
update bashrc with the required environment variables:
{% highlight bash %}
echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
{% endhighlight %}
Finally, install Jekyll and Bundler
{% highlight bash %}
gem install jekyll bundler
{% endhighlight %}

* Set up a personal or project-specific github repo. You can follow the first part of [this guide ](https://docs.github.com/en/free-pro-team@latest/github/working-with-github-pages/creating-a-github-pages-site-with-jekyll#creating-a-repository-for-your-site) if you have troubles with this. Note that the repo must be set to "Public" for actually deploying it. However, you can start initializing it as private, locally build it to preview it, and change the repo setting to "Public" once you're satisfied with the result.
Once you have set the repo, clone it locally from github. From a directory of your choice, run in the terminal:
{% highlight bash %}
git clonegit@github.com:YOUR_REPO/YOUR_REPO.github.io.git
{% endhighlight %}


* create a docs dir inside the master directory of the locally cloned repo, we'll build the site therein
{% highlight bash %}
mkdir docs
cd docs
{% endhighlight %}

* initialize the bundle and add jekll (this is missing in the official GitHub pages guide)
{% highlight bash %}
    bundle init
    bundle add jekyll
{% endhighlight %}

* without specifying a version, force a new jekyll instance executing in the terminal the folowing:
`bundle exec jekyll new . --force`


* make the following changes in the Gemfile in the docs directory to be able to work with GitHub pages:
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

* install the minima theme dependencies, executing the following in the terminal:
`bundle install`

* test the site locally (the default port 4000 is usually used by nomachine, if you don't have installed you can keep it). The `--livereload`option makes your editing dynamic.
`bundle exec jekyll  serve --port 4001 --livereload`

* access the site locally
from a browser: http://localhost:4001/

# Add sections to the main page 
To add a static initial section to the site (and make the site more landing page look-alike), create the following folders in the docs/ dir:
{% highlight bash %}
mkdir _sections
mkdir _inclusdes
cd _includes
mkdir sections
{% endhighlight %}

in _includes/sections/ create a default.html file with the following content:

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

Now create a _layouts dir in docs/, copy there all the default theme _layouts from ~/gems/gems/minima-2.5.1/_layouts/ file. Directly modifying the layouts in that dir will only affect our local preview at localhost. Copying the layouts file in our repo will allow us to modify them while allowing GitHub to automatically deploy them for us in the hosted version of our site. Then modify the home.html in docs/_layouts/ adding the following section under `{%raw%}{{ content }}{%endraw%}`:
{% highlight ruby %}
{%raw%}
        {% assign sections = site.sections | sort: 'order' %}
        {% for section in sections %}
            {% if section.include != null %}
                {% include {{ section.include }} %}
            {% else %}
                {% include sections/default.html %}
            {% endif %}
        {% endfor %}
{%endraw%}
{% endhighlight %}
this will cycle through the markdown sections that you'll place in the docs/_section folder

# Additional tip
The {%raw%}{%...%}{%endraw%} syntax used by Jekyll is part of the Liquid templating engine. Basically, everything in {%raw%}{%...%}{%endraw%} will be parsed and interpreted. For example, quoting the above code directly would result in rendering the _section content directly in the current page. To escape these tags, and so show them literally, you should use the [raw tag](https://stackoverflow.com/questions/22044488/jekyll-code-in-jekyll). 

