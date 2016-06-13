---
layout: post
title: GSoC Third Week
---

![Logo](https://summerofcode.withgoogle.com/static/img/summer-of-code-logo.svg)

This week I had been working on the design of the `GaloisField` class and the `GaloisFieldDict` class.<br/><br/>
Firstly, like `UIntDict`, `GaloisFieldDict` was also inheriting `ODictWrapper`, and had the `dict_` as `map<unsigned int, integer_class>` making it a sparse representation.<br/>
Then `GaloisField` was inherting `UPolyBase`, in which the `Container` was a `GaloisFieldDict`.<br/><br/>
The `dict_` being a map, I made some more optimization to the code, mainly with the `insert` function. I gave extra attention to the fact that we can optimize insertion by providing an iterator as hint.<br/>
Apart from it, made a inplace copy of almost all the arithmetic and modular operations/functions. <br/>
Then, as we had already implemented the division operation in Finite field, so I overloaded the `/` operator.<br/><br/>
Down the way, I saw one test constantly failing in Travis CI. The platform it was failing on was OSX. As I don't have access to OSX, the debugging took a long time, But after the debugging, I fixed some good bugs. It highlights the importance of writing good tests including corner cases.<br/><br/>
It was all fine till now. Isuru (my mentor) realized that as we have to do a lot amount of division, and in that we will have to access all the elements of map less than degree of divisor (for calculating remainder). It will take more time with `map` than `vector`. So we decided to shift our `dict_` type to `std::vector<integer_class>`. Now the `GaloisFieldDict` class doesn't inherit from `ODictWrapper` while the `GaloisField` class still have the same structure. Now `GaloisFieldDict`'s `dict_` being a `vector`, I had to implement a function `gf_istrip()`, which strips off the leading zeroes, so that the degree of our polynomial can be accessed directly by `dict_.size()-1` and most importantly the number of computation decreases.<br/>
As this work is in progress, I will post about it in the next week's post.
