---
layout: post
title: GSoC Fourth Week
---

![Logo](https://summerofcode.withgoogle.com/static/img/summer-of-code-logo.svg)

This week [Initial Implementation of Finitefield](https://github.com/symengine/symengine/pull/955) got merged. It will allow us to represent polynomial with integral coefficients in finite field.
Talking about the design, we are sticking to the dense representation, i.e. the `dict_` is a vector. 

This week there was an error in [Appveyor](https://ci.appveyor.com/) build, I had no idea how to fix this. I tried to print with every passed test case and use `-VV` option for verbose mode, but it was of no use.
Isuru, then told me that I have to log into the Appveyor's VM and debug it. He helped with `remmina` and we found that there was problem in the `gf_istrip()` function, where I was erasing elements using iterators, but after any insertion or deletion iterators become invalid. So, it is better to use indices, or do re-assignment of iterators there.

After that I started working on square free algorithms. In mathematics, a square-free polynomial is a polynomial defined over a field that is not a multiple of the square of a non unit factor. In general terms, they can be thought as a polynomial with no repeated roots.
And square free factorization is the first step towards factorization of polynomials in finite field.
So, I have implemented:

```C++
GaloisFieldDict gf_diff() const;
bool gf_is_sqf() const;
std::vector<std::pair<GaloisFieldDict, integer_class>> gf_sqf_list() const;
GaloisFieldDict gf_sqf_part() const;
```

- `gf_diff` differentiates the polynomial in the given field.
- `gf_is_sqf` returns whether polynomial is squarefield in the given field.
- `gf_sqf_part` returns the square free part of the polynomaial in the given field.
- `gf_sqf_list` returns the square free decomposition of polynomial's monic representation in the given field.

This PR has also been merged. Currently I am working on Distinct Degree factorization.
