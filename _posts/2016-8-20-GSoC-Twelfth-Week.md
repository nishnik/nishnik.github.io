---
layout: post
title: GSoC Twelfth Week
---

![Logo](https://summerofcode.withgoogle.com/static/img/summer-of-code-logo.svg)

This week I started work on polynomial factorization in `Z`.
I implemented the zassenhaus's algorithm, which factors a primitive square-free polynomial.<br>
The basic idea behind factoring a polynomial in `Z` is first to make it square free using `Yun's` algorithm or something similar and then choosing a prime number `p`, such that the polynomial mod `p` is square free, and `p` doesn't divide its leading coefficient.
After that it is reduced to factoring polynomial in finite field. Which has already been implemented, then we lift all the factors from the finite field to `Z` using hensel lifting.
<br>
The number of time Hensel Lifting has to be done is found using the [Mignotte's bound](http://www.csd.uwo.ca/~moreno//CS424/Lectures/ResultantGcd.html/node5.html).
<br>
This wall required implementation of extended euclidean GCD in the finite fields.
So, after the implementation of factorization of square free algorithms, we were able to perform:

```C++
f = UIntPoly::from_vec(x, {1_z, 0_z, -9_z});
// f = -9x**2 + 1
out = f->zz_zassenhaus();
// out is a set of RCP<const UIntPoly>
// out = {-3x + 1, -3x - 1}
out_f = f->zz_factor_sqf();
// out_f is a pair<integer_class, std::set<RCP<const UIntPoly>>
// out_.f.first = 1
// out_f. second = {3x + 1, 3x - 1}
```

After this I need to implement the algorithm for square free factorization and the trial division for finding the power of factor in the polynomial, this way we will be able to factor the polynomials.
The PR is [here](https://github.com/symengine/symengine/pull/1066).
