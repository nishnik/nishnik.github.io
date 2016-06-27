---
layout: post
title: GSoC Fifth Week
---

![Logo](https://summerofcode.withgoogle.com/static/img/summer-of-code-logo.svg)

This week, I had been working on [distinct degree factorization](https://en.wikipedia.org/wiki/Factorization_of_polynomials_over_finite_fields#Distinct-degree_factorization) in [this](https://github.com/symengine/symengine/pull/995) PR.<br/>

Distinct degree factorization splits a square-free polynomial into a product of polynomials whose irreducible factors all have the same degree.
<br/>Suppose we have a polynomial: 

```
x**15 - 1
```

When we do distinct degree factorization of it, we get:

```
x**5 + 10
x**10 + x**5 + 1
```

Both the results consist of product of some polynomials with equal degree.

```
x**5 + 10
```

It is product of polynomials of degree 1, while:

```
x**10 + x**5 + 1
```

is product of polynomials of degree 2.

The factorization is achieved by exploiting the fact that:

![Lemma](http://i.imgur.com/N9zZW26.png)

So, for every degree `i` less than half of polynomial's degree, we find the `gcd` of above computed polynomial and the given polynomial. If it's not one, we add it to existing list of factors.

Then we have to find its equal degree factorization, I have implemented it and I am testing it with different cases.
It will run on every input provided from distinct-degree factorization, and break it into polynomials with equal degrees.
<br/>
Currently I am implementing Cantor-Zassenhaus's algorithm.
