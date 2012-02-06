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
-----

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

## Names and speed

Although many matrix operations can be performed on `data.frame`, they are _much_ faster when performed on `matrix` data types[^dfmat].

[^dfmat]: need a small example of this

Accesssing arrays via index is faster than by name, but using names can make for more readable code. 
To achieve fast access and still use names, one can construct an environment that uses a hash table for lookup

```R
e <- new.env(hash=TRUE,size=2)
assign(x="first", value=1, envir=e)
assign(x="second", value=2, envir=e)
e

## Access via
e[["first"]]
get("second", env=e)
```

This tip is from [Joseph Adler](http://broadcast.oreilly.com/2010/03/lookup-performance-in-r.html), who goes throught the speed improvements of this method verus named arrays.


## Compiling code

As of `R` 2.13, the `compiler` package lets you compile code into byte for faster processing.  The basic syntax is:

`compiled.function <- cmpfun(orig.function)`

A demonstration [here](http://dirk.eddelbuettel.com/blog/2011/04/12/) shows that it speeds some basic functions up about 4X.

## Memory 

* preallocate memory 

###  manage memory

* free up space and display stats with `gc()`
* check memory use by `x` using `object.size(x)`
* use `memory.profile()`
* use `mem.limits()` to get/set memory limits
