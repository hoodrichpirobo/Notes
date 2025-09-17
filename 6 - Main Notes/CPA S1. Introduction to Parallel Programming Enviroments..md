2025-09-16 12:24

Status: #child #lectures 

Tags:

# CPA S1. Introduction to Parallel Programming Enviroments.

# Programming in C
In C, **arrays** are a data type to which you first declare but later on you cannot ask about it's size, you must know it yourself.
`double a[N]`
here, the data type it's the same is if it were a double, only that you're telling it that it has N copies.
Also, Strings are arrays of type char just like in `c++.`
## A pointer, on the other hand
Is a variable containing the address of another variable. For example:
`p = &a[2];`
Here, p is pointing to the address of the third element of the array a.
When you declare it, you have to show that it is a pointer with `*`
	For example:     `double *p;`
Although when you use the asterisk on another context, it just means that it is an expression to return the value instead of the address it is pointing to
	For example:     `x = *p;`

## References
[[FSO Concepts]], [[CPA Concepts.]]