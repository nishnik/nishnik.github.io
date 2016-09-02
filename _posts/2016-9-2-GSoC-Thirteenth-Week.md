---
layout: post
title: GSoC Thirteenth Week
---

![Logo](https://summerofcode.withgoogle.com/static/img/summer-of-code-logo.svg)

This week I worked on the [PR](https://github.com/symengine/symengine/pull/1066) of factoring square free polynomials.
Adding many changes for size in base. Like changing this:

```C++
auto l = std::ceil(std::log(2 * B + 1) / std::log(mp_get_ui(fsqf.first)));
```

to

```C++
if (mp_fits_slong_p(B)) {
    temp = 2 * B + 1;
    l = std::ceil(std::log(mp_get_d(temp))
                  / std::log(mp_get_ui(fsqf.first)));
} else {
    auto b_d = mp_get_d(mp_abs(b));
    l = std::ceil(
        (1 + std::log2(n + 1) / 2.0 + n + log2_d_A + std::log2(b_d))
        / (std::log2(mp_get_ui(fsqf.first))));
}
```
This prevented over-flow.
And a lot of implementation changes were incorporated in `gf_gcdex` also.

I also wrote documentation on `Fields` module [here](https://github.com/symengine/symengine/wiki/Fields-in-SymEngine).
