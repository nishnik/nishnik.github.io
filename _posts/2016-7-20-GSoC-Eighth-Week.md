---
layout: post
title: GSoC Eighth Week
---

![Logo](https://summerofcode.withgoogle.com/static/img/summer-of-code-logo.svg)

After completing the work on `gf_factor`, I moved on to implement Gathen-Shoup's factorization algorithm. Like Zassenhaus's agorithm, it is also a probabilistic algorithm.
<br>
The paper is available [here](http://www.shoup.net/papers/frobenius.pdf).
<br>
<br>
**First question: Why this algorithm ?**
<br>
> Because, it is kind of faster than zassenhaus's algorithm.

<br>
**Second question: What is "kind of" here ?**
<br>
> Well, it is faster when a specific condition satisfies.

<br>
Its asymptotic runtime is `O(n**2 + n log q).(log n)**2.loglog n`, where `n` is degree of polynomial and `q` is the field characteristics.
<br>
In ["Soft O" notation](https://en.wikipedia.org/wiki/Õ#Mathematical_use), it is `O~(n**2 + n log q)`. While the cantor zassenhaus's algorithm has `O~(n**2 log q)` asymptotic runtime.
<br>
So when `log q` approaches `n`, the difference is remarkable.
<br>

| Algorithm  | Asymptotic Runtime |
| ---|:---:|
Shoup      | `O~(n**2)`
Zassenhaus | `O~(n**3)`

It also works in three parts, firstly square free factorization, then distinct degree and finally equal degree factorization.
<br>
I have completed the implementation of this algorithm on [shoup_factorization](https://github.com/nishnik/symengine/tree/shoup_factorization) branch.
And also, I changed the container (which stores factors) type to `set`.<br>
Will send a PR soon.
