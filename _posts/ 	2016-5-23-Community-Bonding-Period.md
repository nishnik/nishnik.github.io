![Logo](https://summerofcode.withgoogle.com/static/img/summer-of-code-logo.svg)

I have been selected for GSoC'16 to work with [Sympy](http://www.sympy.org/) on **Implementing Finite Fields and Set module in SymEngine".

> [SymEngine](https://github.com/sympy/symengine) is a standalone fast C++ symbolic manipulation library.

# About the Proposal

We all know that Polynomial factorization is one of the fundamental tools of the computer algebra systems. And in symbolic mathematics, it is one of the basic requirement over which other algorithms can be implemented.<br/>
Currently, SymEngine has the implementation of Univariate Polynomial class, which provides us the basic functionality to add, multiply and subtract two polynomials.<br/>
Now, comes the problem of factoring the polynomials.<br/>
We have explicit solution formulas only till polynomials of degree four(the Quadtratic formula for degree 2, [the Cardano formulas](http://en.wikipedia.org/wiki/Cardano_formula#Cardano.27s_method) for third-degree equations, and [the Ferrari formula](http://en.wikipedia.org/wiki/Quartic_function#The_general_case.2C_along_Ferrari.27s_lines) for degree 4).<br/>
For sure, we need a different way out for higher degree polynomials.
We see that there are algorithms for factorization in finite fields:
- [Cantor–Zassenhaus algorithm](https://en.wikipedia.org/wiki/Cantor%E2%80%93Zassenhaus_algorithm)
- [Berlekamp's algorithm](https://en.wikipedia.org/wiki/Berlekamp's_algorithm)

So, this summers I will be working on converting a polynomial in integer field to finite field, then factorizing them. After which we have to do [Hensel Lifting](https://en.wikipedia.org/wiki/Hensel's_lemma) to bring back the factored polynomial to integer field.

Furthermore, I will be working on implementing Sets module. These two together will help us to create a basic infrastructure over which we can develop a solvers module in SymEngine.<br/>

My proposal can be found [here](https://github.com/sympy/sympy/wiki/GSoC-2016-Application-Nishant-Nikhil:-Implementing-Finite-Fields-and-Set-module-in-SymEngine).

# Community Bonding Period

I have been alloted [Isuru Fernando](https://github.com/isuruf), [Thilina Rathnayake](https://github.com/thilinarmtb), [Sumith](https://github.com/Sumith1896) and [Ondřej Čertík](https://github.com/certik) as mentors.<br/>
The SymEngine community is very fast in reachability.
We had a discussion on [gitter channel of SymEngine](https://gitter.im/symengine/symengine), about the proceedings of our Proposal. As SymEngine has an implementaion of sparse polynomials, I will be working on changing them to Finite Fields. Like:
```
GaloisField::GaloisField(std::map<unsigned, int> &dict, unsigned modulo) : modulo_(modulo)
{
	unsigned temp;
	for (auto iter : dict) {
		temp = iter.second % modulo;
		if (temp != 0)
			dict_[iter.first] = temp;
	}
}
```
where `dict` is the dictionary of Univariate Polynomial representation and, `dict_` stores its finite field representation modulo `modulo_`.
I will be implementing this in the first week of GSoC period.

# Work already Done

During the Community Bonding Period, I worked on implementing [`UniversalSet`](https://github.com/symengine/symengine/pull/934) and [`FiniteSet`](https://github.com/symengine/symengine/pull/942).<br/>
`UniversalSet` is a [singleton class](https://en.wikipedia.org/wiki/Singleton_pattern) like `EmptySet`, and while implementing this I learned a lot about Singleton classes.<br/>
`FiniteSet` is a class with a set of `RCP<const Basic>` as member variable. It can contain any object of `Basic` type. While implemeting this, we came on a fix over what to do when we have a interval like [1, 1], i.e. both end points equal. This led to a little change in `Interval`'s code, and now it returns a `FiniteSet`. Though this PR is not merged till now. I hope to get it merged in the next few days and along with it keep working on Finite Field implementation.

