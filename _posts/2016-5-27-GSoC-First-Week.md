---
layout: post
title: GSoC First Week
---

Previously, I was working on the [PR](https://github.com/symengine/symengine/pull/942) for `FiniteSet` implementation.
I managed to get it merged this week. So, now we have `UniversalSet`, `EmptySet`, `Interval` and `FiniteSet` implementation in SymEngine.
Where in `FiniteSet` we have a `set_basic` which can contain any `Basic` object. That is apart from `Number` objects we can have `Symbol` objects as well, and even an `Expression`.<br/>

Then I started working on implementing `FiniteField`. I have sent this [PR](https://github.com/symengine/symengine/pull/955). Initially I was using `std::map<unsigned, int>` as the `type` for `dict_` and `int` type for `modulo_`, but I realized that there are already `inverse` function written for `integer_class`/`mpz`, so I changed the `dict_` to `std::map<unsigned, integer_class>` and `modulo_` to `integer_class`.
While implementing this, I thought of writing tests after doing the whole implementation. And when I wrote the tests, I realized how badly I had done the implementation, like missing corner cases and all. It is always a better practice to write tests parallely with your implementation.<br/>

So, As of now I have implemented the following functions:
* `gf_add_ground(const integer_class a)`
* `gf_sub_ground(const integer_class a)`
* `gf_mul_ground(const integer_class a)`
* `gf_quo_ground(const integer_class a)`
* `gf_add(const RCP<const GaloisField> &o)`
* `gf_sub(const RCP<const GaloisField> &o)`
* `gf_mul(const RCP<const GaloisField> &o)`

Where `gf_*_ground` does the operation represented by `*` by the integer `a` to the polynomaial in the given field.
And `gf_add`, `gf_sub`, `gf_mul` do their respective operation with another polynomial in the finite field.
<br/>
I will be implementing `gf_div` this weekend.
