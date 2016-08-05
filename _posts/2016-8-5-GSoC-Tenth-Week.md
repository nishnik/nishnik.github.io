---
layout: post
title: GSoC Tenth Week
---

![Logo](https://summerofcode.withgoogle.com/static/img/summer-of-code-logo.svg)

This week, I had been working on implementaion of `Union` and `Contains` in [this](https://github.com/symengine/symengine/pull/1053) PR. <br>
Our `Set::contains` function has been changed from :
```
virtual bool contains(const RCP<const Basic> &a) const = 0;
```
to
```
virtual RCP<const Boolean> contains(const RCP<const Basic> &a) const = 0;
```
And these functions:
```
virtual bool is_subset(const RCP<const Set> &o) const = 0;
virtual bool is_proper_subset(const RCP<const Set> &o) const = 0;
virtual bool is_superset(const RCP<const Set> &o) const = 0;
virtual bool is_proper_superset(const RCP<const Set> &o) const = 0;
```
have been changed to:
```
bool is_subset(const RCP<const Set> &o) const
{
    return eq(*this->set_intersection(o), *this);
}
bool is_proper_subset(const RCP<const Set> &o) const
{
    return not eq(*this, *o) and this->is_subset(o);
}
bool is_superset(const RCP<const Set> &o) const
{
    return o->is_subset(rcp_from_this_cast<const Set>());
}
bool is_proper_superset(const RCP<const Set> &o) const
{
    return not eq(*this, *o) and this->is_superset(o);
}
```
depending solely on `set_intersection`.

Then the `SymEngine::set_union(const set_set &in, bool solve = true)` has been defined which will create a `Union` object with `in` if it is not solvable, or will do union operation on all of them.
<br>
Our `Union` class has `std::set` of `Set` to store the different Set containers which can't be unified into one single container.
<br>
Apart from it, the `set_intersection` ans `set_union` virtual functions have been restructured to handle other `Set` types case by case.
