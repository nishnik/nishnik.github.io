---
layout: post
title: GSoC Ninth Week
---

![Logo](https://summerofcode.withgoogle.com/static/img/summer-of-code-logo.svg)

Previous week I had implemented the **Shoup's Algorithm** in [this](https://github.com/symengine/symengine/pull/1045) PR. During the review we came to realise that it is better to use `unsigned int` instead of `integer_class` because we didn't need big numbers. 
<br><br>
Working on the same PR, I found a bug in `negate` and similar function where we were doing:

```C++
for (auto &a : dict_) {
  a *= -1;
  a += modulo_;
```

Here: if the `dict_` is `[0, 0, 10]`, it will negate to `[11, 11, 1]` in `GF(11)`. So, it was needed to add a check when the value is `0`. So, the method was changed to:

```C++
for (auto &a : dict_) {
  a *= -1;
  if (a != 0_z)
    a += modulo_;
}
```
<br>
Along with it I was working on the `gf_factor` [PR](https://github.com/symengine/symengine/pull/1036) and it eventually got merged. It introduced **Zassenhaus's algorithm** and `gf_factor()` function. In coming days, we will have to change `gf_factor` to switch between `gf_zassenhaus` and `gf_shoup` according to the degree of polynomial.
<br><br>
We made one more design change, we changed the factor container from `std::pair<GaloisFieldDict, integer_class>` to `std::pair<GaloisFieldDict, unsigned>` because we didn't need large numbers as power.
<br><br>
Then I started working on change of base class of `GaloisField` class from `UPolyBase` to `UIntPolyBase`, this needed implementation of `eval` and `multi_eval` method, then I implemented the iterator for `GaloisField` class and the `pow` method. The [PR](https://github.com/symengine/symengine/pull/1047/files) is under review.
