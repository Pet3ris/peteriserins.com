---
layout: post
title: How this site was built
---

## {{ page.title }}
<time>06.18.2011</time>

Let me begin by elaborating on the construction of this website. Instead of
spraying a cloud of creepy sounding buzzwords, I'll try and start from the
requirements and show why these choices were a good fit in my scenario.
It might be helpful to look at the
[source code](https://www.github.com/Pet3ris/peteriserins.com) as you're
reading this. I am not planning to go through the meaning of every file,
there are [many](http://blog.envylabs.com/2009/08/publishing-a-blog-with-github-pages-and-jekyll/)
[good](http://paulstamatiou.com/how-to-wordpress-to-jekyll)
[tutorials](http://mashable.com/2010/09/02/html5-boilerplate-guide/) on all
technologies involved, so please check them out if you're interested in the
details.

### What does one want in a blog?

There are a couple of little things that matter. A good blog environment would

1. allow me to focus on creating content (posts).  It would take care of
interface and style issues and render my site for viewing on all popular
platforms.
2. It would support simple but important dynamic tasks, such as listing
a certain number of recent posts, extracting dates and titles, allowing
users to comment on the website, etc.
3. It should be easy to debug.

### HTML5 boilerplate

This was a natural starting point for a project using HTML and CSS. It has all
the standard practices baked in. 
[HTML5 boilerplate](http://www.html5boilerplate.com) provides you with

* an appropriate directory structure;
* basic .html, .css and .js files filled out with cross-platform compatibility
boilerplate, resets and libraries;
* build script for minification and other useful automated tasks;
* most importantly, many other things I am not and do not have to be aware
of thanks to the boilerplate team.

### Jekyll

Quite a few people already have advertised
[Jekyll](https://github.com/mojombo/jekyll/) to a more than adequate
extent. It is essentially a preprocessor that has built-in support for
blog posts. I feed in content written in plain-text (more precisely,
markdown), some layout files serving as templates for, e.g.,  posts, and
it spits out a blog in HTML. Yes, no databases, server-side scripting or
admin panels. Best part: you get a working idea of what's going on without
having to dive into the source code.

### Putting it all together

To combine the two, I wanted something that spits out a blog that would have
all the best practices, minified code and whatnot.

To the credit of these technologies, joining them is easy if you are
familiar with both. I run Jekyll first to generate the html for posts and the
main page, putting the end-product in the \_sites folder. Then, the build script
is run on the assembled website. It is cleaned up for publishing and is ready
for deployment at \_sites/publish.

The only non-trivial part was making the build script aware of all the posts
so that it can work on their HTML. The solution is to have the build config
(called project.properties) as a Jekyll template file and write the following
line:

    file.pages =
    {{ "{% for post in site.posts "}} %}
      {{ "{{ post.url | replace_first: '/', '' "}} }},
    {{ "{% endfor "}}%}index.html, 404.html,

It merely loops over all the posts and inserts their URLs into the build
script, comma-separated.

### The result

Writing blog posts becomes as easy and rewarding as drinking
[liquid](http://www.liquidmarkup.org/).
