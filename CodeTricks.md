Code Tricks
===========

Assembled & mantained by UC Davis Theoretical Population Biology group,
a.k.a. Teary.


Question: How can I get my scripts to run more efficiently?

Matlab
-----

 * Vectorize everything as matrix algebra
 * Use the matlab profiler

R
-
 * R profiler: Rprof (functionalize your code first)
 * sapply instead of for loops



Did you know, in R:

```R
a/(b+c)
````

is slower than

```R
a/{b+c}
```

and  `a^2 ` is slower than `a*a`.  

Radford Neal [pointed this out](http://radfordneal.wordpress.com/2010/08/19/speeding-up-parentheses-and-lots-more-in-r/) in  R-2.11.1, try testing in R 2.14.1 first.  

Also, although many matrix operations can be performed on `data.frame`, they are _much_ faster when performed on `matrix` data types[^dfmat].

[^dfmat]: need a small example of this


## Compiling code

As of `R` 2.13, the `compiler` package lets you compile code into byte for faster processing.  The basic syntax is:

`compiled.function <- cmpfun(orig.function)`

A demonstration [here](http://dirk.eddelbuettel.com/blog/2011/04/12/) shows that it speeds some basic functions up about 4X.
