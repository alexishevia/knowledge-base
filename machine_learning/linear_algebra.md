# Linear Algebra

Reference: [Coding The Matrix: Linear Algebra Through Computer Science Applications](http://codingthematrix.com/)

## Set terminology and notation
- Set: an unordered collection of objects. Example: `{♥, ♠, ♣, ♦ }`
- `∈:` indicates that an object belongs to a set (equivalently, that the set
  contains the object). For example: `♥ ∈ {♥, ♠, ♣, ♦}`.
- `A ⊆ B`: Read this as "A is a subset of B". This means A and B are sets, and
  every element of A is also an element of B.
- `A = B`: Two sets are equal if they contain exactly the same elements. (There
  is no order among elements of a set.)
- Cardinality: If a set `S` is not infinite, we use `|S|` to denote its
  cardinality, the number of elements it contains.

## Set expressions

In Mathese, we would write "the set of nonnegative numbers" like this:
```
{x ∈ ℝ : x ≥ 0}
```
Read this as "The set of consisting of all elements x of the set of real
numbers such that x is greater than or equal to 0"

There are two parts to this set expression:
1. the part before the colon: This part specifies where the elements of the set
   come from, and introduces a variable or variables that can be used in the
   second part.
2. the part after the colon: This gives a rule that restricts which elements
   specified in the first part actually get to make it into the set.

The analogous Python expression is a set comprehension:
```
S = {-4, 4, -3, 3, -2, 2, -1, 1, 0}
{x for x in S if x >= 0}
```

Instead of `{x ∈ ℝ : x ≥ 0}` you might see just `{x : x ≥ 0}` if it is
considered clear what kind of values x is supposed to take on.

## Cartesian Product
`A × B` is the set of all pairs `(a, b)` where `a∈ A` and `b∈ B`.

Example: for `A = {1, 2}` and `B = {♥, ♠, ♣, ♦}`, `A × B` is
```
{(1, ♥),(2, ♥),(1, ♠),(2, ♠),(1, ♣),(2, ♣),(1, ♦),(2, ♦)}
```

If `A` and `B` are finite sets then `|A × B|` = `|A| × |B|`

## The function
For each input in a set `A`, a function assigns a single output element from
another set `B`.
- `A` is called the domain of the function
- `B` is called the co-domain of the function

Formally, a function is a set of pairs `(a,b)` no two of which have the same
first element.

- domain: set of all inputs over which the function is defined.
- co-domain: set from which the function's output values are chosen. Note that
  one has some leeway in choosing the co-domain since not all of its members
  need be outputs.
- pre-image: input of a function
- image: output of a pre-image under the function.

If `f(q) = r`, we say that "q maps to r under f".
`q` is the pre-image, `r` is the image.
The notation for "q maps to r" is `q -> r`

The notation `f : D -> F` means that `f` is a function whose domain is the set
`D` and whose co-domain is the set `F`. More briefly: "a function from D to F",
or "a function that maps D to F".

The image of a function `f` is the set of all images of all domain elements.
That is, the image of `f` is the set of elements of the co-domain that actually
occurs as outputs.

Note:
- Some people use "range" to mean "co-domain"
- Some people use "range" to mean "image" (seems like this is the most common)

## Functions vs procedures vs computational problems
- procedure: precise description of a computation (what we usually call a
  function in Python is actually a procedure)
- computational problem: input-output specification that a procedure might be
  required to satisfy.

## Composition
For functions `f:A→ B` and `g:B→ C`, the functional composition of `f` and `g`
is the function `(g ◦ f) : A → C` defined by `(g ◦ f)(x) = g(f(x))`

## One-to-one, onto, and invertible functions

By definition, a mathematical function cannot produce different images for the
same pre-image. eg: if `f(-5)` is `-5`, then `f(-5)` cannot be `0` (it must
always produce the same image).

However, a function can produce the same image for two different pre-images.
eg: `f(-5) = 0` && `f(0) = 0`

If the function guarantees that every pre-image will produce a different image,
then it is a "one-to-one" (or injective) function.

A function's co-domain includes every possible image for a function. However,
not all elements in a co-domain are necessarily in the function's image.
eg: For `f : ℝ -> ℝ ` defined as `f(x) = x^2`.
- The domain is all real numbers
- The co-domain is all real numbers
- The image (or range) is only the positive numbers

If a function guarantees that all members of the co-domain are also members of
the image, then it is an "onto" (or surjective) function.

If a function is both one-to-one and surjective, the it is an invertible (or
bijective) function.
