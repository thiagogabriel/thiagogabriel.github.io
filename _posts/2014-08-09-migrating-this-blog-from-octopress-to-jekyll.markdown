---
layout: post
title: "Migrating this blog from Octopress to Jekyll"
comments: true
categories: 
    jekyll
    octopress
---

Well, it is been 1 year since my last post. So let's celebrate with a
post about the migration of this blog which I just finished.

The first version of this blog was a Wordpress, probably in 2012. It was easy to create
posts, but I didn't like the way it is built. Wordpress is hard to customize,
I have to login to do something, I need a paid host and I was being attacked
with brute force very often.

On the beginning of 2013 I moved to Octopress hosted on Github. Github
hosts static websites for free, is reliable and allows custom domains. I can submit a
post with `git push` and don't have to care about authentication, since
a sent my SSH key to github. Octopress is a Jekyll
customization with lots of plugins and a fine interface. The bigest
problem is that the workflow I was using with github was worst than when
I was using Wordpress. I had to deal with 2 git branches. One with the
Octopress source code and a second branch with the static page generated.

> GitHub Pages is powered by Jekyll, however all Pages sites are generated using the --safe option to disable custom plugins for security reasons. Unfortunately, this means your plugins won’t work if you’re deploying to GitHub Pages.
>
> You can still use GitHub Pages to publish your site, but you’ll need to convert the site locally and push the generated static files to your GitHub repository instead of the Jekyll source files." [Jekyll Plugins Page](http://jekyllrb.com/docs/plugins/)

The other problem is that the version I was using is a fork from the
[original repo](https://github.com/imathis/octopress) and I don't know
a simple way to update my fork based on original repo without
the risk to mess up my fork.

Today I decided to change my blog to Jekyll to simplify my workflow and
maybe, who knows, blog more often.

I don't have to deal with 2 branches anymore.
The migration was very simple. I created a new jekyll project
from scratch, moved my .markdown files and images to the new project.
This Jekyll version (2.2.0) surprised me with a delightful interface,
responsive layout, with almost no CSS, just as it should be. I still have to do
some improvements but I'm much happier now that I have more control.

The current version of the blog can be found on [my github](https://github.com/thiagogabriel/thiagogabriel.github.io/)

