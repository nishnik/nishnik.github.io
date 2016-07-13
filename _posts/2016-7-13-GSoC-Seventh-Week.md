---
layout: post
title: GSoC Seventh Week
---

![Logo](https://summerofcode.withgoogle.com/static/img/summer-of-code-logo.svg)

Previous week, I had started the work on Equal degree factorization [here](https://github.com/symengine/symengine/pull/1026). Here I was storing the factors in a vector and then sorting the factors. Certik pointed out that its better to use some other data structure instead of `vector`. So I have changed the container type to `set`.
<br>Then after both Distinct degree factorization and Equal degree factorization being implemented, I started to work on factoring a polynomial in finite field, this needed integrating square free factorization with these two. I worked on `gf_factor()` method. In this method we take a polynomial in a given field as input, and return all the factors and their respective powers, and polynomial's leading coefficient as output.
<br>

```C++
GaloisFieldDict::gf_factor() const
{
  integer_class lc;
  GaloisFieldDict monic;
  gf_monic(lc, outArg(monic));
  if (monic.degree() < 1)
      return std::make_pair(lc, factors);
  std::vector<std::pair<GaloisFieldDict, integer_class>> sqf_list
      = monic.gf_sqf_list();
  for (auto a : sqf_list) {
      auto temp = (a.first).gf_zassenhaus();
      for (auto f : temp)
          factors.insert({f, a.second});
  }
  return factors;
}
```

For a given polynomial firstly we get its monic representation and it leading coefficient. Then we find the Square free factors of the monic representation. And on each of the square free factor we run the `zassenhaus`'s algorithm.
<br>
I have been working on [this](https://github.com/nishnik/symengine/tree/gf_factor) branch, will create a PR after the Equal degree factorization PR gets merged.
<br>
Then I have started working on Shoup's algorithm for polynomial factorization, will post about it in the coming weeks.
