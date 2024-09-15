---
layout: post
title: "What's in a name?"
date: 2024-09-13 20:15 -0400
categories: python
published: true
---

Tonight’s entertainment is brought to you by one of the top teams competing in [jailCTF 2024](https://ctf.pyjail.club/).

Arguably the most important bit of prep your team can do ahead of a CTF is to come up with a clever name. This team chose

{% highlight python %}
chr(sum(range(ord(min(str(not()))))))
{% endhighlight %}

Which evaluates to ඞ.

Wait, what?

I’ll admit that this took me way too long to work out because I am not nearly clever enough. Much Googling was done. And also this only works with Python 3+ because unicode.

Working from the inside out:

`not()` is applying [the unary not operator](https://www.w3schools.com/python/python_operators.asp#:~:text=Reverse%20the%20result%2C%20returns%20False%20if%20the%20result%20is%20true) to an empty tuple, which is `not(False)`, which returns `True`. This is something I don’t think that I explicitly realized - but in Python, certain objects are “falsy”, meaning they evaluate to the Boolean `False`, and an empty sequence or collection, such as empty tuple, is one of those falsy objects.

`str()` is [converting that to the actual string of characters](https://www.w3schools.com/python/ref_func_str.asp): “True”

`min()` is [returning the character in “True” with the lowest unicode codepoint](https://www.w3schools.com/python/ref_func_min.asp), which is “T”. So here it’s useful that capital letters come before lowercase and thus have lower codepoint values.

`ord()` is [returning the integer that represents that character](https://www.w3schools.com/python/ref_func_ord.asp), thus “T” becomes 84.

`range()` then [takes that integer and returns the sequence of integers from zero 0 to 84 as a tuple](https://www.w3schools.com/python/ref_func_range.asp). This works because if you only give `range()` a single argument (the integer to stop at), it uses the defaults for start (0) and step (1).

`sum()` is [adding up all of the items in that tuple](https://www.w3schools.com/python/ref_func_sum.asp) (0+1+2+…83), resulting in 3486. In my opinion, `sum(range(84))` is probably the cleverest bit because 3486 is (conveniently) a [triangular number](https://en.wikipedia.org/wiki/Triangular_number) - it is the sum of the natural numbers 1 to 83.

`chr()` is [returning the unicode character represented by that codepoint](https://www.w3schools.com/python/ref_func_chr.asp) (3486), which corresponds to the Sinhalese character ඞ (U+0D9xE)