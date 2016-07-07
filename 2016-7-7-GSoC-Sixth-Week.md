---
layout: post
title: GSoC Sixth Week
---

![Logo](https://summerofcode.withgoogle.com/static/img/summer-of-code-logo.svg)

After Distinct degree factorization being merged in this [PR](https://github.com/symengine/symengine/pull/995), I started working on Equal degree factorization.
<br>
Following up from previous example, we had:

```
x**5 + 10
```

and

```
x**10 + x**5 + 1
```

as distinct degree factors.
<br>

Now we run Equal degree factorization on both of the above given polynomial, from
```
x**10 + x**5 + 1
```

We get:

```
x**2 + x + 1
x**2 + 3x + 9
x**2 + 4x + 5
x**2 + 5x + 3
x**2 + 9x + 4
```

And for:

```
x**5 + 10
```

We get:

```
x + 2
x + 6
x + 7
x + 8
x + 10
```

See that the first one gave degree two factors and the second one gave degree one factors.

I have implemented the algorithm in [this](https://github.com/symengine/symengine/pull/1026) PR.
<br>
Combining the distinct degree and equal degree factorization, we get the factors of a polynomial in finite field.
For factorizing a polynomial in integral fielf we need to convert it to some finite field polynomial, factor it and then lift it back to integral field. This is [Hensel's Lifting](https://en.wikipedia.org/wiki/Hensel%27s_lemma), I will write about it in the coming blog posts.
<br><br>
I am sorry that I couldn't work this week as I was at *[Robo Cup](http://www.robocup2016.org/en/)*. Looking forward to a good week ahead.
