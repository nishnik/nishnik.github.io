---
layout: post
title: GSoC Second Week
---

![Logo](https://summerofcode.withgoogle.com/static/img/summer-of-code-logo.svg)

This week, I implemented some algorithms (`gf_div`, `gf_gcd` etc.) and apart from it I looked into the design consideration also.

# Algorithms Implemented

I implemented 
- `gf_div`

``` C+++
void GaloisFieldDict::gf_div(const GaloisFieldDict &o,
                         const Ptr<GaloisFieldDict> &quo,
                         const Ptr<GaloisFieldDict> &rem) const
```                               
This will change the value of `quo` and `rem`.

- `gf_quo`

This will return the quotient only. It will help when we only need quotient after dividing.
It is better than `gf_div` in terms of time complexity.

- `gf_lshift`

It is efficient way to multiply a polynomial in `GaloisField` by `x**n`

- `gf_rshift`

It is efficient way to divide a polynomial in `GaloisField` by `x**n`

``` C++
void GaloisFieldDict::gf_rshift(const integer_class n,
                            const Ptr<GaloisFieldDict> &quo,
                            const Ptr<GaloisFieldDict> &rem) const
```

Just like gf_div, it also changes the value of `quo` and `rem`.

- `gf_sqr`

This will square the polynomial in `GaloisField`.

- `gf_pow`

It uses binary multiplication to power a polynomial in `GaloisField`.

- `gf_monic`

Changes a polynomial to its monic representation, i.e. `3*x**2 + 4` in `GF(5)` becomes `x**2 + 3`. Here leading coefficient becomes `one`.

- `gf_gcd` and `gf_lcm`

`gf_gcd` by Euclidean Algorithm and `gf_lcm` is product of the two polys divided by their gcd in the finite field.


# Design Change

SymEngine's codebase for `UIntPoly` has changed, it inherits `UPolyBase`, which has two private variables, one is to store the variable and other is container. `UIntPoly` uses `UIntDict` as a container and `UIntDict` is inherited from `ODictWrapper`.
Now as `GaloisField` is just representation of polynomial so I needed something similar, so I made `GaloisField` inherit from `UPolyBase`, and made a container named `GaloisFieldDict`.
This prevented a lot of code duplicacy.
Still there is a lot of conversation going on this topic, I will better post after the final design is fixed.
