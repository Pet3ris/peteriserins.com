---
layout: post
title: "How To: Compile every language from Vim"
---

## {{ page.title }}
<time>21.06.2011</time>

*Warning*: This post is for users of the Vim text editor. It might not be
relevant to you unless you have been using it already or want a compelling
argument to start doing so.

One of the many reasons I like [Vim](http://www.vim.org/) is how easy it is
to set up a workable environment for any programming language. For most
popular languages, filetype recognition and syntax highlighting are already
in there.  What I like to do further, is to set up easy compilation and running
from within Vim with the click of a button. This post will show how.

We are concerned with single source files, useful for when you are starting out
in a new language, doing programming competitions or merely experimenting with
language features, and want a little more control than you can get with a REPL.

### Setting up C compilation

We are going to start with gcc and C compilation (a sufficiently non-trivial
example), but we will look at a few others in the end. To compile a file test.c
with gcc into test.out, we write

{% highlight bash %}
$ gcc -o test.out test.c
{% endhighlight %}

When editing a file in Vim, you can run a command for the native terminal
by preceding it with :!. For example, in Unix, try writing

    :!ls

So, if we know that our filename is test.c, we can now compile and run
without resorting to an external terminal window

    :!gcc -o test.out test.c && ./test.out

Note we were assuming that the current directory is the directory of the file
we are editing, which is not always the case. This will not be a problem as
we generalize.

Now, this is already quite convenient, but what if we had longer filenames?
Turns out, there is a shortcut for getting the filename, it's "%". Back to Vim:

    :!gcc -o ?? "%" && ??

"%" will expand into "test.c", but how can we get test.out? We need Vim's
filename modifiers. :p gives us the full path and :r removes the extension.
So what we need is 

    :!gcc -o "%:p:r.out" "%:p" && "%:p:r.out"

This would work for every file, all that's left now is to put it in .vimrc.
I like to map it to F9 like so:

{% highlight vim %}
autocmd FileType c map <F9> :!gcc --o "%:p:r.out" "%:p" && "%:p:r.out"<CR>
{% endhighlight %}

And we're good to go! Restart Vim and hit F9 while editing a C file to see it
happen.

### Other languages

Java classes present us with new kinds of issues, but they still fall to
Vim's file modifiers. We use :h to get the classpath and :t helps us get
the class name by stripping the path away.

{% highlight vim %}
autocmd FileType java map <F9> :!javac "%:p" && java -cp "%:p:h" "%:t:r"<CR>
{% endhighlight %}

Interpreted languages are even easier, here's ruby:

{% highlight ruby %}
autocmd FileType ruby map <F9> :!ruby "%:p"<CR>
{% endhighlight %}

### Further tips

If you want to separate compilation and execution, that's easy too.
I've also added a "| more" to make sure the first error does not leave the
screen.

{% highlight vim %}
autocmd FileType c map <F6> :!gcc --o "%:p:r.out" "%:p" <bar> more<CR>
autocmd FileType c map <F7> :!"%:p:r.out"<CR>
{% endhighlight %}

### Documentation

Although :p, :r, :h and :t should be sufficient for most cases, there is much more
you can do with file modifiers. Hit up

    :!help filename-modifiers

To find out more.
