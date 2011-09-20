---
layout: post
title: Sliding Window Trick in Python
---

## {{ page.title }}
<time>20.09.2011</time>

The [Sliding Window Trick](http://tjsct.wikidot.com/sliding-window-trick) is a
well-known and widely practiced method in Dynamic Programming that allows you
to shave an order of magnitude off of the memory consumption for certain Dynamic
Programming algorithms by discarding parts of the table that will not be used
in further computation.

### Example

Here is a function that returns the r-th row of
[Pascal's triangle](http://en.wikipedia.org/wiki/Pascal's_triangle) in Python 2.

{% highlight python %}
def comb_row(r):
    C = [(r + 1) * [0] for _ in range(r + 1)]
    C[0][0] = 1
    for i in range(r + 1):
        C[i][0] = C[i][i] = 1
        for j in range(1, i):
            C[i][j] = C[i - 1][j - 1] + C[i - 1][j]
    return C[r]
{% endhighlight %}

A relatively clear implementation, but the memory footprint is quadratic and that
might be too much for certain applications.

### The Sliding Window approach

Note that we only ever operate on the last two rows in the previous example.
Naturally, we can rewrite the function to keep only the last two rows in memory.

{% highlight python %}
def comb_row_sliding(r):
    prev = (r + 1) * [0]
    cur  = (r + 1) * [0]
    prev[0] = 1
    for i in range(r + 1):
        cur[0] = cur[i] = 1
        for j in range(1, i):
            cur[j] = prev[j - 1] + prev[j]
        prev, cur = cur, prev
    return prev
{% endhighlight %}

Much better, but that was a lot of work.

### The trick

Turns out, we only need to change one line of the first implementation to have it
consume only linear memory. It involves a clever use of Python's list repetition syntax.

{% highlight python %}
def comb_row_neat(r):
    C = [(r + 1) * [0], (r + 1) * [0]] * (r / 2 + 1)
    C[0][0] = 1
    for i in range(r + 1):
        C[i][0] = C[i][i] = 1
        for j in range(1, i):
            C[i][j] = C[i - 1][j - 1] + C[i - 1][j]
    return C[r]
{% endhighlight %}

*Homework*: There is a simpler linear-time, linear-memory, in-place algorithm for the
problem that is somewhat harder to spot. I'll leave it as an exercise.
