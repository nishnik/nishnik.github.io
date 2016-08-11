---
layout: post
title: GSoC Eleventh Week
---

![Logo](https://summerofcode.withgoogle.com/static/img/summer-of-code-logo.svg)

This week I worked on little refactoring of `Fields` module. Like moving functions implementations from `.h` file to `.cpp` file in [this](https://github.com/symengine/symengine/pull/1060) PR. I added a `from_uintpoly` method which allows us to create a `GaloisField` object from `UIntPoly` object in [this](https://github.com/symengine/symengine/pull/1059/) PR. After which I worked on the implementation of `diff` method for `GaloisField` in [this](https://github.com/symengine/symengine/pull/1060) PR.
<br>
Then I worked on `Logic` module. It is needed for the implementation of `Intersection` class in `Sets` module. It has the implementation for Logical And, Or and Not operations.
<br>
Both `Or` and `And` class have a private variable named `container_` which is a set of `RCP<const Boolean>`. It stores the `Boolean` objects on which `And` and `Or` operator can't be applied using the known rules.
<br>
`Not` also has one private variable which is an `RCB<const Boolean>` object, which stores the `Boolean` object on which we were not able to apply `not` operator using the current rules.
<br>
Then we have three functions:

```C++
RCP<const Boolean> logical_and(const set_boolean &s);
RCP<const Boolean> logical_or(const set_boolean &s);
RCP<const Boolean> logical_not(const RCP<const Boolean> &s);
```

These are used to do the respective operation on the operands supplied.
<br>
Talking little about implementaion details:

```C++
RCP<const Boolean> logical_and(const set_boolean &s)
{
   return and_or<And>(s, false);
}

RCP<const Boolean> logical_or(const set_boolean &s)
{
   return and_or<Or>(s, true);
}
```

And the function `and_or` do the required operations.
<br>
After [this](https://github.com/symengine/symengine/pull/1061/) PR gets merged, I would start working on `Intersection` class.
