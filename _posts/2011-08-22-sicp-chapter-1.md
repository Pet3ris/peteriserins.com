---
layout: post
title: "SICP in Haskell: Chapter 1"
---

## {{ page.title }}
<time>22.08.2011</time>

I recently (see:
[Starting SICP in Haskell](http://peteriserins.com/2011/08/12/starting-sicp-in-haskell.html))
started doing the SICP exercises in Haskell. After a more-or-less idle week I've managed to
finish Section 1.3 and hence Chapter 1. My solutions are at
[GitHub](https://github.com/Pet3ris/sicp).

Chapter 1 is called Building Abstractions with Procedures and introduces the basics of
programming with a focus on functions including anonymous function and higher-order
functions. It was mostly a recap for me, but there were some new things too, e.g.,
the Miller-Rabin primality test and Simpson's Rule for integration.

Haskell has been entirely adequate so far. It was probably instructive to have to think about
reasonable type signatures for the functions. One mistake I made was trying to use monads for IO
initially. Don't get me wrong, I think monads are great in the long run, but for these kinds of
pet problems, solutions with the `trace` function end up being cleaner and more similar to the
respective lisp versions. Also, for similar reasons, I will try to stop generalizing my types so
much. It's tempting and occasionally instructive to make the functions at least as general as
the respective lisp versions, but I was overdoing it for this Chapter. Wildcard feature that
turned out to be really useful was automatic currying.

Looking forward to the following chapters and hoping it gets a little more challenging. We'll
see how Haskell holds up.
